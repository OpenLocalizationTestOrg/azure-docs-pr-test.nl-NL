---
title: aaaMultiple IP-adressen voor virtuele machines in Azure - PowerShell | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met behulp van PowerShell | Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>Meerdere IP-adressen toewijzen toovirtual machines met behulp van PowerShell

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Dit artikel wordt uitgelegd hoe toocreate een virtuele machine (VM) via hello Azure Resource Manager deployment model met behulp van PowerShell. Meerdere IP-adressen kunnen niet worden toegewezen als tooresources via de klassieke implementatiemodel Hallo is gemaakt. meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen

Hallo in de volgende procedure wordt uitgelegd hoe toocreate een voorbeeld van de virtuele machine met meerdere IP-adressen, zoals beschreven in Hallo scenario. Variabele waarden zoals vereist voor uw implementatie te wijzigen.

1. Open een PowerShell-opdrachtprompt en volledige Hallo resterende stappen in deze sectie binnen één PowerShell-sessie. Als u nog niet PowerShell geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.
2. Tooyour aanmeldingsaccount Hello `login-azurermaccount` opdracht.
3. Vervang *myResourceGroup* en *westus* met een naam en locatie van uw keuze. Maak een resourcegroep. Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Maken van een virtueel netwerk (VNet) en het subnet in Hallo dezelfde locatie als Hallo resourcegroep:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. Een netwerkbeveiligingsgroep (NSG) en een regel maken. Hallo NSG Hallo VM beveiligt met regels voor binnenkomend en uitgaand. In dit geval is er een binnenkomende regel gemaakt voor poort 3389, waarmee binnenkomende verbindingen met een extern bureaublad worden toegestaan.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Definieer Hallo primaire IP-configuratie voor Hallo NIC. Wijziging 10.0.0.4 tooa geldig adres in Hallo subnet die u hebt gemaakt, als u hebt eerder gedefinieerde Hallo-waarde gebruikt. Voordat u een statisch IP-adres toewijst, wordt het aanbevolen dat u eerst bevestigen dat dit nog niet in gebruik. Voer de opdracht Hallo `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Als het Hallo-adres beschikbaar is, Hallo retourneert uitvoer *True*. Als niet beschikbaar is, retourneert-uitvoervenster het Hallo *False* en een lijst met adressen die beschikbaar zijn. 

    In het Hallo-opdrachten, na **< vervangen-met-uw unieke-naam > vervangt door Hallo unieke DNS-naam toouse.** Hallo-naam moet uniek zijn in alle openbare IP-adressen binnen een Azure-regio. Dit is een optionele parameter. Het kan worden verwijderd als u wilt dat alleen tooconnect toohello VM via Hallo openbaar IP-adres.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    Wanneer u meerdere IP-configuraties tooa NIC toewijst, één configuratie moet worden toegewezen als Hallo *-primaire*.

    > [!NOTE]
    > Openbare IP-adressen hebben een nominaal kosten. meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.

7. Hallo secundaire IP-configuraties definiëren voor Hallo NIC. U kunt toevoegen of verwijderen van configuraties indien nodig. Elk IP-adresconfiguratie moet een particulier IP-adres toegewezen. Elke configuratie kan desgewenst een openbaar IP-adres toegewezen hebben.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Hallo NIC maken en koppelen van Hallo drie IP-configuraties tooit:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Hoewel alle configuraties zijn tooone NIC in dit artikel worden toegewezen, kunt u meerdere IP-configuraties tooevery NIC die is gekoppeld toohello VM kunt toewijzen. hoe een virtuele machine met meerdere NIC's, toocreate Lees toolearn hello [een virtuele machine maken met meerdere NIC's](virtual-network-deploy-multinic-arm-ps.md) artikel.

9. Hallo VM maken door te voeren van Hallo volgende opdrachten:

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. Toevoegen Hallo privé-IP-adressen toohello VM besturingssysteem via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.

## <a name="add"></a>IP-adressen tooa VM toevoegen

U kunt persoonlijke en openbare IP-adressen tooa NIC toevoegen via Hallo stappen volgen. Hallo voorbeelden in de volgende secties Hallo wordt ervan uitgegaan dat er al een virtuele machine met Hallo drie IP-configuraties beschreven in Hallo [scenario](#Scenario) in dit artikel, maar het is niet vereist dat u doen.

1. Open een PowerShell-opdrachtprompt en volledige Hallo resterende stappen in deze sectie binnen één PowerShell-sessie. Als u nog niet PowerShell geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.
2. Hallo "waarden" Hallo achter $Variables toohello naam Hallo NIC u tooadd IP-adres tooand Hallo resource groep en locatie Hallo die NIC bestaat in wilt wijzigen:

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Als u niet Hallo-naam van de NIC die u wilt dat toochange hello weet, Voer Hallo opdrachten te volgen en Hallo waarden van de vorige variabelen Hallo wijzigen:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Maak een variabele en stel deze toohello NIC bestaande door Hallo volgende opdracht te typen:

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. Wijzig in Hallo opdrachten te volgen, *MyVNet* en *MySubnet* toohello namen van Hallo VNet en subnet Hallo NIC is verbonden met. Voer Hallo opdrachten tooretrieve hello VNet en subnet objecten Hallo die NIC is verbonden met:

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Als u Hallo VNet of subnet naam Hallo die NIC is verbonden met niet weet, voert u Hallo volgende opdracht:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    Zoeken in de uitvoer van Hallo tekst vergelijkbare toohello voorbeelduitvoer te volgen:
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    In deze uitvoer *MyVnet* hello VNet is en *MySubnet* Hallo subnet Hallo NIC is verbonden met is.

5. Voer Hallo stappen in een Hallo uit te voeren, op basis van uw vereisten:

    **Een persoonlijke IP-adres toevoegen**

    een persoonlijke IP-adres tooa NIC tooadd, moet u een IP-configuratie maken. Hallo volgende opdracht maakt u een configuratie met een statisch IP-adres 10.0.0.7. Wanneer u een statisch IP-adres opgeeft, moet dit een ongebruikt adres voor het Hallo-subnet. Het raadzaam dat u eerst testen Hallo adres tooensure deze beschikbaar is door te voeren Hallo `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` opdracht. Als Hallo IP-adres beschikbaar is, Hallo retourneert uitvoer *True*. Als niet beschikbaar is, retourneert-uitvoervenster het Hallo *False*, en een lijst met adressen die beschikbaar zijn.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.

    Hallo persoonlijke IP-adres toohello VM besturingssysteem toevoegen via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.

    **Een openbaar IP-adres toevoegen**

    Een openbaar IP-adres wordt toegevoegd door een openbare IP-adres resource tooeither koppelen van een nieuwe IP-configuratie of een bestaande IP-configuratie. Stappen Hallo in een van Hallo secties die volgen, die u nodig hebt.

    > [!NOTE]
    > Openbare IP-adressen hebben een nominaal kosten. meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.
    >

    - **Hallo openbare IP-resource tooa nieuwe IP-adresconfiguratie koppelen**
    
        Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben. U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken. toocreate een nieuw wachtwoord invoeren Hallo volgende opdracht:
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        toocreate een nieuwe IP-configuratie met een statisch privé IP-adres en het Hallo gekoppeld *myPublicIp3* openbare IP-adres adres resource, Voer Hallo volgende opdracht:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Hallo openbare IP-resource tooan bestaande IP-adresconfiguratie koppelen**

        Een openbare IP-adres resource kan alleen worden gekoppeld tooan IP-configuratie die nog geen die zijn gekoppeld. U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft door te voeren Hallo volgende opdracht:

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        U ziet het vergelijkbare toohello volgende uitvoer:

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Sinds Hallo **PublicIpAddress** kolom voor *IpConfig 3* is leeg, geen openbare IP-adres-resource is momenteel gekoppeld tooit. U kunt een bestaand openbaar IP-adres resource tooIpConfig-3 toevoegen, of Voer Hallo opdracht toocreate een volgende:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Voer Hallo opdracht resource toohello bestaande IP-configuratie met de naam van tooassociate Hallo openbare IP-adressen te volgen *IpConfig 3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Hallo NIC met het nieuwe IP-configuratie Hallo instellen door te voeren van Hallo volgende opdracht:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Hallo privé IP-adressen weergeven en Hallo openbare IP-adres resources toegewezen toohello NIC door te voeren Hallo de volgende opdracht:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Hallo persoonlijke IP-adres toohello VM besturingssysteem toevoegen via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adres toohello besturingssysteem.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
