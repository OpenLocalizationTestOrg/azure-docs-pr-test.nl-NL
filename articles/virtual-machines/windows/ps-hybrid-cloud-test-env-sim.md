---
title: aaaSimulated hybride cloud-testomgeving | Microsoft Docs
description: Maakt een gesimuleerde hybride cloud-omgeving voor IT pro of ontwikkeling testen met behulp van twee virtuele Azure-netwerken en een VNet-naar-VNet-verbinding.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Een gesimuleerde hybride cloudomgeving instellen voor testen
In dit artikel begeleidt u bij het maken van een omgeving met gesimuleerde hybride cloud met Microsoft Azure met behulp van twee virtuele Azure-netwerken. Hier wordt de resulterende configuratie Hallo.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Dit simuleert een hybride cloud-productieomgeving en bestaat uit:

* Een gesimuleerde en vereenvoudigd on-premises netwerk wordt gehost in een Azure-netwerk (Hallo TestLab virtueel netwerk).
* Een gesimuleerde cross-premises virtueel netwerk gehost in Azure (TestVNET).
* Een VNet-naar-VNet-verbinding tussen Hallo twee virtuele netwerken.
* Een secundaire domeincontroller in het Hallo TestVNET virtuele netwerk.

Dit biedt dat een basis- en algemene starten van het rapportageservicepunt vanuit die u kunt:

* Toepassingen ontwikkelen en testen in een gesimuleerde hybride cloud-omgeving.
* Test-configuraties van computers, sommige vanuit Hallo TestLab virtueel netwerk en sommige binnen Hallo TestVNET virtueel netwerk, toosimulate hybride cloud-gebaseerde IT werkbelastingen maken.

Er zijn vier belangrijke fasen toosetting u deze testomgeving van hybride cloud:

1. Hallo TestLab virtueel netwerk configureren.
2. Hallo cross-premises virtueel netwerk maken.
3. Hallo VNet-naar-VNet-VPN-verbinding maken.
4. DC2 configureren. 

Deze configuratie is vereist voor een Azure-abonnement. Als u een MSDN- of Visual Studio-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Virtuele machines en virtuele netwerkgateways in Azure kosten in rekening gebracht een lopende financieel wanneer ze worden uitgevoerd. Deze kosten in rekening gebracht op basis van uw MSDN of betaald abonnement. Een Azure VPN-gateway wordt geïmplementeerd als een set van twee virtuele machines in Azure. toominimize hello kosten, Hallo testomgeving maken en het benodigde testen en demonstratie zo snel mogelijk uitvoeren.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>Fase 1: Hallo TestLab virtueel netwerk configureren
Hallo-instructies gebruiken in Hallo [basisconfiguratie testomgeving](https://technet.microsoft.com/library/mt771177.aspx) onderwerp tooconfigure Hallo DC1, APP1 en CLIENT1-computers in hello Azure-netwerk de naam van TestLab. 

Vervolgens start u een Azure PowerShell-prompt.

> [!NOTE]
> Hallo volgende opdracht stelt u Azure PowerShell 1.0 en hoger gebruiken.
> 
> 

Meld u aan tooyour-account.

    Login-AzureRMAccount

De abonnementsnaam van uw met behulp van de volgende opdracht Hallo ophalen.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Stel uw Azure-abonnement. Gebruik Hallo hetzelfde abonnement dat u toobuild de basisconfiguratie in fase 1 gebruikt. Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste naam Hallo vervangen.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Vervolgens voegt u een gateway subnet toohello TestLab virtueel netwerk van uw basisconfiguratie, de gebruikte toohost hello Azure-gateway worden.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Vervolgens vraagt u een openbaar IP-adres tooassign toohello gateway voor Hallo TestLab virtuele netwerk.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Maak vervolgens uw gateway.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Houd er rekening mee dat nieuwe gateways 20 minuten of meer toocreate kunnen hebben.

Verbinding van hello Azure-portal op uw lokale computer, tooDC1 met Hallo corp\gebruiker1-referenties. tooconfigure hello CORP-domein dat computers en gebruikers hun lokale domeincontroller voor verificatie, gebruiken deze opdrachten uitvoeren vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Dit is de huidige configuratie.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>Fase 2: Hallo TestVNET virtueel netwerk maken
Eerst Hallo TestVNET virtueel netwerk maken en beveiligen met een netwerkbeveiligingsgroep.

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

Vervolgens aanvraag een openbare IP-adres toobe toohello gateway toegewezen voor Hallo TestVNET virtuele netwerk en maak uw gateway.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Dit is de huidige configuratie.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>Fase 3: Maak Hallo VNet-naar-VNet-verbinding
Eerst moet u een willekeurige, cryptografisch sterke, 32-teken vooraf gedeelde sleutel van uw netwerk- of -beheerder. U kunt ook gebruik Hallo informatie op [maken van een willekeurige tekenreeks op voor een vooraf gedeelde sleutel IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain een vooraf gedeelde sleutel.

Gebruik vervolgens deze opdrachten toocreate hello VNet-naar-VNet-VPN-verbinding, waarvan sommige toocomplete tijd kan duren.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Na een paar minuten moet Hallo verbinding maken.

Dit is de huidige configuratie.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Fase 4: DC2 configureren
Maak eerst een virtuele machine voor DC2. Deze opdrachten uitvoeren bij hello Azure PowerShell-opdrachtprompt op de lokale computer.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Vervolgens maakt u verbinding toohello nieuwe DC2 virtuele machine uit hello Azure-portal.

Configureer vervolgens een Windows Firewall tooallow verkeer van de regel voor het testen van verbinding. Voer deze opdrachten uit vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op DC2.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

Hallo ping-opdracht moet resulteren in vier geslaagde antwoorden van IP-adres 10.0.0.4. Dit is een test van het verkeer tussen Hallo VNet-naar-VNet-verbinding.

Vervolgens voegt u Hallo extra gegevensschijf op DC2 als een nieuw volume met de stationsletter Hallo F:.

1. In Hallo linkerdeelvenster van Serverbeheer, klikt u op **File and Storage Services**, en klik vervolgens op **schijven**.
2. In het Hallo inhoudsdeelvenster Hallo **schijven** groep, klikt u op **schijf 2** (Hello **partitie** instellen te**onbekende**).
3. Klik op **taken**, en klik vervolgens op **NieuwVolume**.
4. Hallo voordat u een pagina van Wizard Nieuw Volume hello, klik op **volgende**.
5. Klik op Hallo Selecteer Hallo-server en schijfpagina op **schijf 2**, en klik vervolgens op **volgende**. Wanneer u wordt gevraagd, klikt u op **OK**.
6. Klik op Hallo Hallo grootte opgeven van Hallo volume pagina, **volgende**.
7. Klik op Hallo toewijzen tooa station stationsletter of map pagina op **volgende**.
8. Klik op Hallo bestand selecteren pagina systeeminstellingen, **volgende**.
9. Klik op de pagina van het Hallo bevestigen selecties **maken**.
10. Wanneer voltooid, klikt u op **sluiten**.

Configureer vervolgens de DC2 als een replicadomeincontroller voor Hallo corp.contoso.com domein. Deze opdrachten uitvoeren met Windows PowerShell-opdrachtprompt Hallo op DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Er rekening mee dat u na vragen aan gebruiker toosupply beide Hallo corp\gebruiker1 wachtwoord en een wachtwoord van Directory Services Restore Mode (DSRM) en toorestart DC2.

Nu dat hello TestVNET virtueel netwerk heeft zijn eigen DNS-server (DC2), moet u Hallo TestVNET virtueel netwerk toouse deze DNS-server configureren.

1. Klik op Hallo virtuele netwerken pictogram in het linkerdeelvenster Hallo Hallo Azure-portal en klik vervolgens op **TestVNET**.
2. Op Hallo **instellingen** tabblad **DNS-servers**.
3. In **primaire DNS-server**, type **192.168.0.4** tooreplace 10.0.0.4.
4. Klik op **Opslaan**.

Dit is de huidige configuratie. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Uw gesimuleerde hybride cloudomgeving is nu gereed voor het testen.

## <a name="next-step"></a>Volgende stap
* Instellen van een [webgebaseerde line-of-business-toepassing](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in deze omgeving.

