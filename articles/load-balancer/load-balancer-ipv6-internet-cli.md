---
title: aaaCreate een internetgerichte load balancer met IPv6 - Azure CLI | Microsoft Docs
description: Meer informatie over hoe een Internet gerichte load balancer met IPv6 in het gebruik van Azure Resource Manager toocreate hello Azure CLI
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: IPv6-, azure load balancer, dual-stack, openbare IP-adres, systeemeigen ipv6, mobiele, iot
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>De load balancer met IPv6 in Azure Resource Manager hello Azure CLI met behulp van een Internetgericht maken

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [Sjabloon](load-balancer-ipv6-internet-template.md)

Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer. Hallo load balancer biedt hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde service-exemplaren in cloudservices of virtuele machines in een load balancer-set. Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.

## <a name="example-deployment-scenario"></a>Voorbeeldscenario voor implementatie

Hallo volgende diagram illustreert Hallo-oplossing voor taakverdeling wordt geïmplementeerd met behulp van Hallo voorbeeld van de sjabloon die in dit artikel wordt beschreven.

![Load balancer-scenario](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

In dit scenario maakt u hello Azure-resources te volgen:

* twee virtuele machines (VM's)
* de virtuele netwerkinterface voor elke virtuele machine met zowel IPv4 als IPv6-adressen die zijn toegewezen
* een internetgerichte Load Balancer met een IPv4 en IPv6-openbare IP-adres
* een Beschikbaarheidsset toothat bevat Hallo twee virtuele machines
* twee laden taakverdeling regels toomap Hallo openbare VIP's toohello persoonlijke eindpunten

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Hallo-oplossing met behulp van Azure CLI Hallo implementeren

Hallo stappen laten zien hoe toocreate een internetverbinding netwerktaakverdeler met Azure Resource Manager met CLI. Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd en vervolgens samengesteld toocreate een resource.

een load balancer toodeploy, u maken en configureren van Hallo objecten te volgen:

* Front-end-IP-configuratie: bevat openbare IP-adressen voor inkomend netwerkverkeer.
* Back-end-adresgroep - bevat netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer.
* Taakverdeling regels - bevat regels voor toewijzing van een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep.
* Binnenkomende NAT-regels: regels voor toewijzing van een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in het back-end-adresgroep Hallo bevat.
* Tests - beschikbaarheid van health-tests gebruikt toocheck van exemplaren van virtuele machines in het back-end-adresgroep Hallo bevat.

Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>Instellen van uw CLI omgeving toouse Azure Resource Manager

In dit voorbeeld wordt Hallo CLI-hulpprogramma's uitgevoerd in een PowerShell-opdrachtvenster. We hello Azure PowerShell-cmdlets niet gebruiken, maar we gebruiken de scripting mogelijkheden tooimprove leesbaarheid en opnieuw gebruiken van PowerShell.

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo **azure config mode** opdracht tooswitch tooResource Manager-modus.

    ```azurecli
    azure config mode arm
    ```

    Verwachte uitvoer:

        info:    New mode is arm

3. Meld u aan tooAzure en een lijst met abonnementen ophalen.

    ```azurecli
    azure login
    ```

    Voer uw Azure-referenties wanneer u wordt gevraagd.

    ```azurecli
    azure account list
    ```

    Kies Hallo abonnement die u wilt dat toouse. Noteer Hallo abonnements-Id voor de volgende stap Hallo.

4. Variabelen voor gebruik met CLI-opdrachten Hallo PowerShell instellen.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Een resourcegroep, een load balancer, een virtueel netwerk en subnetten maken

1. Een resourcegroep maken

    ```azurecli
    azure group create $rgName $location
    ```

2. Een load balancer maken

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Maak een virtueel netwerk (VNet).

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Maak twee subnetten in dit VNet.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Openbare IP-adressen voor Hallo front-pool maken

1. Hallo PowerShell variabelen instellen

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Maak een openbare IP-Hallo front-end-IP-adresgroep.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > Hallo load balancer gebruikmaakt van Hallo domeinlabel van Hallo openbare IP-adres als de FQDN. Deze een wijziging van de klassieke implementatie dat gebruikmaakt van Hallo cloudservicenaam zoals Hallo load balancer FQDN-naam.
    > In dit voorbeeld Hallo FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Front-end en back-end-adresgroepen maken

In dit voorbeeld maakt het front-end-IP-groep hello, die Hallo binnenkomend netwerkverkeer op Hallo load balancer ontvangt en Hallo backend-IP-groep waar front-pool Hallo Hallo taakverdeling netwerkverkeer verzendt.

1. Hallo PowerShell variabelen instellen

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Maak een front-end-IP-adresgroep Hallo openbare IP-adres gemaakt in de vorige stap Hallo en Hallo load balancer koppelen.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Hallo test, NAT-regels en LB regels maken

In dit voorbeeld maakt Hallo volgende items:

* een test regel toocheck voor connectiviteit tooTCP poort 80
* een NAT-regel tootranslate alle binnenkomend verkeer op poort 3389 tooport 3389 voor RDP<sup>1</sup>
* een NAT-regel tootranslate alle binnenkomend verkeer op poort 3391 tooport 3389 voor RDP<sup>1</sup>
* een load balancer-regel toobalance alle binnenkomend verkeer op poort 80 tooport 80 op Hallo adressen in Hallo back-end-pool.

<sup>1</sup> NAT-regels zijn gekoppeld tooa specifieke virtuele machine exemplaar achter Hallo load balancer. Hallo-netwerkverkeer dat binnenkomt op poort 3389 verzonden toohello specifieke virtuele machine en de poort die is gekoppeld aan Hallo NAT-regel. U moet een protocol (UDP of TCP) voor een NAT-regel opgeven. Beide protocollen kunnen niet worden toegewezen toohello dezelfde poort.

1. Hallo PowerShell variabelen instellen

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Hallo-test maken

    Hallo wordt volgende voorbeeld een TCP-test waarmee wordt gecontroleerd of voor connectiviteit tooback-end TCP-poort 80 elke 15 seconden. Het markeert Hallo back-end-bron niet beschikbaar na twee achtereenvolgende mislukte pogingen.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Binnenkomende NAT-regels waarmee de RDP-verbindingen toohello back-end resources maken

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Regels die verkeer toodifferent back-end-poorten, afhankelijk van welke front-end ontvangen Hallo-aanvraag verzenden voor een load balancer maken

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Controleer uw instellingen

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Verwachte uitvoer:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>NIC's maken

NIC's maken en deze koppelt tooNAT regels, load balancer-regels en -tests.

1. Hallo PowerShell variabelen instellen

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Maken van een NIC voor elke back-end en een IPv6-configuratie toevoegen.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Hallo back-end VM resources maken en koppelen van elke NIC

toocreate virtuele machines, moet u een opslagaccount hebben. Load balancing, moeten Hallo VMs toobe leden van een beschikbaarheidsset. Zie voor meer informatie over het maken van virtuele machines [maken van een virtuele machine in Azure met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Hallo PowerShell variabelen instellen

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > Dit voorbeeld wordt Hallo gebruikersnaam en wachtwoord voor virtuele machines Hallo in ongecodeerde tekst. Juiste Wees voorzichtig bij het gebruik van referenties in Hallo wissen. Zie voor een veiligere methode afhandelen van referenties in PowerShell Hallo [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

2. Hallo storage-account en beschikbaarheid set maken

    U mag een bestaand opslagaccount gebruiken bij het maken van Hallo virtuele machines. Hallo volgende opdracht maakt een nieuw opslagaccount.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    Maak vervolgens Hallo beschikbaarheidsset.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. Hallo virtuele machines maken met de Hallo gekoppeld NIC 's

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Volgende stappen

[Aan de slag met het configureren van een interne load balancer](load-balancer-get-started-ilb-arm-cli.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
