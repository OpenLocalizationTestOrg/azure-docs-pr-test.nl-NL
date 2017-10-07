---
title: aaaCreate en beheren van Windows-virtuele machines in Azure met meerdere NIC's | Microsoft Docs
description: Meer informatie over hoe toocreate en beheren van een Windows-VM met meerdere NIC's aangesloten tooit met behulp van Azure PowerShell of de Resource Manager-sjablonen.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Maken en beheren van een virtuele Windows-machine met meerdere NIC 's
Virtuele machines (VM's) in Azure, kunnen meerdere virtuele netwerk interface cards (NIC's) die zijn aangesloten toothem hebben. Een veelvoorkomend scenario toohave verschillende subnetten voor front-end en back-end-connectiviteit is of een netwerk toegewezen tooa bewaking of back-upoplossing. Dit artikel wordt uitgelegd hoe een virtuele machine met meerdere NIC's toocreate tooit gekoppeld. U leert ook hoe tooadd of verwijder NIC's van een bestaande virtuele machine. Andere [VM-grootten](sizes.md) ondersteunen een verschillend aantal NIC's, dus het formaat van uw virtuele machine dienovereenkomstig.

Voor gedetailleerde informatie, inclusief hoe toocreate meerdere NIC's in uw eigen PowerShell-scripts, Zie [implementeren meerdere NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Vereisten
Zorg ervoor dat u Hallo hebt [meest recente versie van Azure PowerShell geïnstalleerd en geconfigureerd](/powershell/azure/overview).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Een virtuele machine met meerdere NIC's maken
Maak eerst een resourcegroep. Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *EastUs* locatie:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Virtueel netwerk en subnetten maken
Een gebruikelijk scenario is voor een virtueel netwerk toohave twee of meer subnetten. Eén subnet mogelijk voor front-verkeer, Hallo andere voor back-end-verkeer. tooconnect tooboth subnetten wordt vervolgens gebruikt u meerdere NIC's op de virtuele machine.

1. Twee subnetten voor virtueel netwerk met definiëren [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hallo volgende voorbeeld definieert Hallo subnetten voor *mySubnetFrontEnd* en *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Maken van uw virtuele netwerk en de subnetten met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Meerdere NIC's maken
Maak twee NIC's met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Koppel een NIC toohello front-end-subnet en één NIC toohello back-end-subnet. Hallo volgende voorbeeld wordt gemaakt met de naam NIC's *myNic1* en *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

Maakt u gewoonlijk ook een [netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) of [netwerktaakverdeler](../../load-balancer/load-balancer-overview.md) toohelp beheren en distribueren van verkeer tussen uw virtuele machines. Hallo [meer gedetailleerde VM meerdere NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artikel begeleidt u bij het maken van een netwerkbeveiligingsgroep en NIC's toewijzen.

### <a name="create-hello-virtual-machine"></a>Hallo virtuele machine maken
Nu starten toobuild uw VM-configuratie. Elk VM-grootte heeft een limiet voor Hallo kunt u het totale aantal NIC's die u tooa VM kunt toevoegen. Zie voor meer informatie [Windows VM-grootten](sizes.md).

1. Instellen van uw VM referenties toohello `$cred` variabele als volgt:

    ```powershell
    $cred = Get-Credential
    ```

2. Definieer uw virtuele machine met [nieuwe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). Hallo volgende voorbeeld definieert een virtuele machine met de naam *myVM* en maakt gebruik van een VM-grootte die ondersteuning biedt voor meer dan twee NIC's (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Maken van de rest van de VM-configuratie met Hallo [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) en [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Hallo volgende voorbeeld maakt een Windows Server 2016 VM:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Koppel Hallo twee NIC's die u eerder hebt gemaakt met [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Maak ten slotte uw virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Toevoegen van een NIC tooan bestaande VM
toevoegen van een virtuele NIC tooan bestaande VM, dat Hallo VM ongedaan wordt gemaakt tooadd Hallo virtuele NIC en Hallo VM start.

1. Toewijzing ongedaan maken met virtuele machine Hallo [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. De bestaande configuratie Hallo Hallo VM ophalen met [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo *myVM* in *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Hallo volgende voorbeeld wordt een virtuele NIC met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) met de naam *myNic3* die is gekoppeld te*mySubnetBackEnd*. Hallo virtuele NIC is gekoppeld toohello VM met de naam *myVM* in *myResourceGroup* met [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>Primaire virtuele NIC 's
    Moet één van Hallo NIC's op een VM meerdere NIC toobe primaire. Als een van de bestaande virtuele NIC's Hallo Hallo VM is al ingesteld als primaire, kunt u deze stap overslaan. Hallo volgende voorbeeld wordt ervan uitgegaan dat twee virtuele NIC's nu aanwezig is op een virtuele machine zijn en u tooadd Hallo eerste NIC (`[0]`) als primaire Hallo:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Start met virtuele machine Hallo [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Een NIC van een bestaande virtuele machine verwijderen
tooremove een virtuele NIC van een bestaande VM u Hallo VM ongedaan gemaakt, verwijdert u Hallo virtuele NIC en vervolgens start Hallo VM.

1. Toewijzing ongedaan maken met virtuele machine Hallo [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. De bestaande configuratie Hallo Hallo VM ophalen met [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo *myVM* in *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Informatie ophalen over Hallo NIC verwijderen met [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Hallo volgende voorbeeld worden gegevens opgehaald over *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Verwijder Hallo NIC met [verwijderen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) en vervolgens update Hallo VM met [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm). Hallo volgende voorbeeld wordt verwijderd *myNic3* verkregen met `$nicId` in de voorgaande stap Hallo:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Start met virtuele machine Hallo [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Meerdere NIC's met behulp van sjablonen maken
Azure Resource Manager-sjablonen bieden een manier toocreate meerdere exemplaren van een bron tijdens implementatie, zoals meerdere NIC's maken. Resource Manager-sjablonen gebruiken declaratieve JSON-bestanden toodefine uw omgeving. Zie voor meer informatie [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). U kunt *kopie* toospecify Hallo aantal exemplaren toocreate:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Zie voor meer informatie [maken van meerdere exemplaren met *kopie*](../../resource-group-create-multiple.md). 

U kunt ook `copyIndex()` tooappend de naam van een aantal tooa-resource. Vervolgens kunt u maken *myNic1*, *MyNic2* enzovoort. Hallo toont volgende code een voorbeeld van een indexwaarde Hallo toevoegen:

```json
"name": "[concat('myNic', copyIndex())]", 
```

U kunt een compleet voorbeeld van lezen [meerdere NIC's maken met Resource Manager-sjablonen](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Volgende stappen
Bekijk [Windows VM-grootten](sizes.md) wanneer u probeert een virtuele machine met meerdere NIC's toocreate. Betalen aandacht toohello maximum aantal NIC's die ondersteuning biedt voor elke VM-grootte. 


