---
title: Maak een virtueel netwerk van Azure-peering - Resource Manager - hetzelfde abonnement | Microsoft Docs
description: Informatie over het maken van een virtueel netwerk peering tussen virtuele netwerken via Resource Manager gemaakt en die aanwezig zijn in dezelfde Azure-abonnement.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: a32a6b33e04c603325ab3612f61e5852682eac7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Maak een virtueel netwerk peering - Resource Manager, hetzelfde abonnement

In deze zelfstudie leert u een virtueel netwerk tussen virtuele netwerken die zijn gemaakt via Resource Manager-peering maken. Beide virtuele netwerken zich in hetzelfde abonnement. Peering twee virtuele netwerken kunnen resources in verschillende virtuele netwerken met elkaar communiceren met de bandbreedte en de latentie, alsof de resources in hetzelfde virtuele netwerk. Meer informatie over [virtuele netwerk peering](virtual-network-peering-overview.md). 

De stappen voor het maken van een virtueel netwerk peering verschillen, afhankelijk van of de virtuele netwerken zijn in dezelfde of verschillende abonnementen en die zijn [Azure implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) via de virtuele netwerken worden gemaakt. Meer informatie over het maken van een virtueel netwerk peering in andere scenario's door te klikken op het scenario uit de volgende tabel:

|Azure-implementatiemodel  | Azure-abonnement  |
|--------- |---------|
|[Beide Resource Manager](create-peering-different-subscriptions.md) |Andere|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models.md) |Dezelfde|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models-subscriptions.md) |Andere|

Een virtueel netwerk peering kan niet worden gemaakt tussen twee virtuele netwerken die zijn geïmplementeerd via het klassieke implementatiemodel. Een virtueel netwerk peering kan alleen worden gemaakt tussen twee virtuele netwerken die zijn opgenomen in dezelfde Azure-regio. Als u virtuele netwerken die zijn beide gemaakt via het klassieke implementatiemodel wilt, of die zijn opgenomen in verschillende Azure-regio's verbinden, kunt u een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) verbinding van de virtuele netwerken. 

U kunt de [Azure-portal](#portal), de Azure [opdrachtregelinterface](#cli) (CLI) Azure [PowerShell](#powershell), of een [Azure Resource Manager-sjabloon](#template)peering van een virtueel netwerk maken. Klik op een van de vorige hulpprogramma koppelingen om rechtstreeks naar de stappen voor het maken van een virtueel netwerk peering met behulp van het hulpprogramma naar keuze te gaan.

## <a name="portal"></a>Maken van de peering - Azure-portal

1. Meld u aan bij [Azure Portal](https://portal.azure.com). Het account dat u zich met aanmeldt moet hebben de vereiste machtigingen om de peering van een virtueel netwerk maken. Zie de [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
2. Klik op **+ nieuw**, klikt u op **Networking**, klikt u vervolgens op **virtueel netwerk**.
3. In de **virtueel netwerk maken** blade invoert, of Selecteer waarden voor de volgende instellingen en klik vervolgens op **maken**:
    - **Naam**: *myVnet1*
    - **Adresruimte**: *10.0.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.0.0.0/24*
    - **Abonnement**: uw abonnement te selecteren
    - **Resourcegroep**: Selecteer **nieuw** en voer *myResourceGroup*
    - **Locatie**: *VS-Oost*
4. Volg de stappen 2-3 opnieuw opgeven van de volgende waarden in stap 3:
    - **Naam**: *myVnet2*
    - **Adresruimte**: *10.1.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.1.0.0/24*
    - **Abonnement**: uw abonnement te selecteren
    - **Resourcegroep**: Selecteer **gebruik bestaande** en selecteer *myResourceGroup*
    - **Locatie**: *VS-Oost*
5. In de **zoeken bronnen** vak aan de bovenkant van de portal type *myResourceGroup*. Klik op **myResourceGroup** wanneer deze wordt weergegeven in de zoekresultaten. Een blade wordt weergegeven voor de **myresourcegroup** resourcegroep. De resourcegroep bevat de twee virtuele netwerken in de vorige stappen hebt gemaakt.
6. Klik op **myVNet1**.
7. In de **myVnet1** blade die wordt weergegeven, klikt u op **Peerings** uit de verticale lijst met opties aan de linkerkant van de blade.
8. In de **myVnet1 - Peerings** blade die werden weergegeven, klikt u op **+ toevoegen**
9. In de **toevoegen peering** blade die wordt weergegeven, invoeren, of de volgende opties selecteren en klik vervolgens op **OK**:
     - **Naam**: *myVnet1ToMyVnet2*
     - **Virtueel netwerk implementatiemodel**: Selecteer **Resource Manager**. 
     - **Abonnement**: uw abonnement te selecteren
     - **Virtueel netwerk**: klik op **Kies een virtueel netwerk**, klikt u vervolgens op **myVnet2**.
     - **Toestaan van toegang tot het virtuele netwerk:** ervoor te zorgen dat **ingeschakeld** is geselecteerd.
    Er zijn geen andere instellingen worden gebruikt in deze zelfstudie. Lees voor meer informatie over instellingen voor alle peering [beheren van virtueel netwerk peerings](virtual-network-manage-peering.md#create-a-peering).
10. Wanneer u op **OK** in de vorige stap, de **toevoegen peering** blade wordt gesloten en u ziet de **myVnet1 - Peerings** blade opnieuw. Na een paar seconden weergegeven de peering die u hebt gemaakt in de blade. **Geïnitieerd** wordt vermeld in de **PEERING STATUS** kolom voor de **myVnet1ToMyVnet2** peering u gemaakt. U hebt ingesteld als peer Vnet1 naar Vnet2, maar u moet nu myVnet2 naar myVnet1 peer. De peering moet worden gemaakt in beide richtingen waarmee bronnen in de virtuele netwerken met elkaar communiceren.
11. Herhaal stap 5-10 nogmaals voor myVnet2.  Naam van de peering *myVnet2ToMyVnet1*.
12. Een paar seconden na het klikken op **OK** peering voor MyVnet2, maken de **myVnet2ToMyVnet1** peering u zojuist hebt gemaakt wordt vermeld met **verbonden** in de  **STATUS van de PEERING** kolom.
13. Stap 5-7 opnieuw uitvoeren voor MyVnet1. De **PEERING STATUS** voor de **myVnet1ToVNet2** peering is nu er ook **verbonden**. De peering is tot stand gebracht nadat er **verbonden** in de **PEERING STATUS** kolom voor beide virtuele netwerken in de peering.
14. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.
15. **Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in de [resources verwijderen](#delete-portal) sectie van dit artikel.

Alle Azure-resources die in een virtueel netwerk hebt u zich nu met elkaar communiceren via hun IP-adressen. Als u van standaard Azure-naamomzetting voor de virtuele netwerken gebruikmaakt, zich de resources in de virtuele netwerken niet voor de naamomzetting tussen de virtuele netwerken. Als u wilt voor het omzetten van namen over virtuele netwerken in een peering, moet u uw eigen DNS-server maken. Meer informatie over het instellen van [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Peering - maken Azure CLI

Het volgende script:

- De Azure CLI versie 2.0.4 vereist of hoger. Uitvoeren als u wilt zoeken naar de versie, de `az --version` opdracht. Als u Azure CLI 2.0 wilt upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Werkt in een Bash-shell. Zie voor opties op Azure CLI-scripts die worden uitgevoerd op Windows-client [uitvoeren van de Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

In plaats van installatie van de CLI en de bijbehorende afhankelijkheden, kunt u de Azure-Cloud-Shell. De Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks in Azure Portal kunt uitvoeren. In deze shell is de Azure CLI vooraf geïnstalleerd en geconfigureerd voor gebruik met uw account. Klik op de **Try it** knop in het script dat volgt, waardoor een Cloud-Shell waarmee u zich aanmeldt bij uw Azure-account met aanmelden kunnen. Voor het uitvoeren van het script, klikt u op de **kopie** knop en plak de inhoud in uw Cloud-Shell.

1. Een resourcegroep en twee virtuele netwerken maken.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Een virtueel netwerk peering tussen de twee virtuele netwerken maken.
 
    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get the id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 to VNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Nadat het script wordt uitgevoerd, Controleer de peerings voor elke virtuele netwerk. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Voer de vorige opdracht opnieuw, vervangen *myVnet1* met *myVnet2*. De uitvoer van beide opdrachten toont **verbonden** in de **PeeringState** kolom.

     Alle Azure-resources die in een virtueel netwerk hebt u zich nu met elkaar communiceren via hun IP-adressen. Als u van standaard Azure-naamomzetting voor de virtuele netwerken gebruikmaakt, zich de resources in de virtuele netwerken niet voor de naamomzetting tussen de virtuele netwerken. Als u wilt voor het omzetten van namen over virtuele netwerken in een peering, moet u uw eigen DNS-server maken. Meer informatie over het instellen van [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.
5. **Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in [resources verwijderen](#delete-cli) in dit artikel.


## <a name="powershell"></a>Maken van de peering - PowerShell

1. Installeer de meest recente versie van de PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/)-module. Zie [Overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) als u nog geen ervaring hebt met Azure PowerShell.
2. Als u een PowerShell-sessie wilt starten, gaat u naar **Start**, voert u **powershell** in en klikt u vervolgens op **PowerShell**.
3. Meld u in PowerShell aan bij Azure door het commando `login-azurermaccount` in te voeren. Het account dat u zich met aanmeldt moet hebben de vereiste machtigingen om de peering van een virtueel netwerk maken. Zie de [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
4. Een resourcegroep en twee virtuele netwerken maken. Kopieer het volgende script voor het uitvoeren van het script, plak deze in PowerShell en druk vervolgens op `Enter` nadat de laatste regel wordt weergegeven op het scherm:

    ```powershell
    # Variables for common values used throughout the script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Een virtueel netwerk peering tussen de twee virtuele netwerken maken. Het volgende script kopiëren, plakken PowerShell en druk vervolgens op `Enter` nadat de laatste regel wordt weergegeven op het scherm:
    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 to VNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. Als u wilt controleren van de subnetten voor het virtuele netwerk, Kopieer de volgende opdracht, plakken PowerShell en druk vervolgens op `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Voer de vorige opdracht opnieuw, vervangen *myVnet1* met *myVnet2*. De uitvoer van beide opdrachten toont **verbonden** in de **PeeringState** kolom.
7. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.
8. **Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in [resources verwijderen](#delete-powershell) in dit artikel.

Alle Azure-resources die in een virtueel netwerk hebt u zich nu met elkaar communiceren via hun IP-adressen. Als u van standaard Azure-naamomzetting voor de virtuele netwerken gebruikmaakt, zich de resources in de virtuele netwerken niet voor de naamomzetting tussen de virtuele netwerken. Als u wilt voor het omzetten van namen over virtuele netwerken in een peering, moet u uw eigen DNS-server maken. Meer informatie over het instellen van [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Maken van de peering - Resource Manager-sjabloon

1. Verwijzing [peering van een virtueel netwerk maken](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager-sjabloon. Bij de sjabloon worden instructies geleverd voor de implementatie van de sjabloon via Azure Portal, PowerShell of Azure CLI. Meld u aan op afhankelijk van wat u hulpprogramma kiezen voor het implementeren van de sjabloon met met een account dat de vereiste machtigingen heeft voor de peering van een virtueel netwerk maken. Zie de [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
2. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.
3. **Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in de [resources verwijderen](#delete) sectie van dit artikel, met behulp van de Azure-portal, PowerShell of Azure CLI.

## <a name="permissions"></a>Machtigingen

De accounts die u gebruikt voor het maken van een virtueel netwerk peering moeten de benodigde rol of machtiging hebben. Bijvoorbeeld, als u twee virtuele netwerken met de naam VNet1 en VNet2 zijn peering, uw account moet worden toegewezen aan de volgende minimale rol of machtiging voor elke virtuele netwerk:
    
|Virtueel netwerk|Rol|Machtigingen|
|---|---|---|
|VNet1|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen voor [aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).

## <a name="delete"></a>Resources verwijderen
Wanneer u deze zelfstudie hebt voltooid, kunt u mogelijk wilt verwijderen van de resources die u hebt gemaakt in de zelfstudie, zodat u geen gebruik kosten. Verwijderen van een resourcegroep, verwijdert tevens alle bronnen die zich in de resourcegroep.

### <a name="delete-portal"></a>Azure-portal

1. Voer in het zoekvak portal **myResourceGroup**. Klik in de zoekresultaten op **myResourceGroup**.
2. Op de **myResourceGroup** blade, klikt u op de **verwijderen** pictogram.
3. Het verwijderen te bevestigen, in de **TYPE de naam van een RESOURCEGROEP** Voer **myResourceGroup**, en klik vervolgens op **verwijderen**.

### <a name="delete-cli"></a>Azure CLI

Voer de volgende opdracht in:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Voer de volgende opdracht in:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Volgende stappen

- Grondig raken met belangrijke [peering beperkingen virtueel netwerk en het gedrag](virtual-network-manage-peering.md#requirements-and-constraints) voordat het maken van een virtueel netwerk voor productie-peering gebruikt.
- Meer informatie over alle [peering virtuele netwerkinstellingen](virtual-network-manage-peering.md#create-a-peering).
- Meer informatie over hoe [maken van een hub en spaak netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) met het virtuele netwerk peering.
