---
title: een virtuele Azure-netwerk peering - aaaCreate Resource Manager - hetzelfde abonnement | Microsoft Docs
description: Meer informatie over hoe toocreate via de Resource-Manager die aanwezig zijn in Hallo dezelfde een virtueel netwerk peering tussen virtuele netwerken gemaakt Azure-abonnement.
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
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Maak een virtueel netwerk peering - Resource Manager, hetzelfde abonnement

In deze zelfstudie leert u toocreate een virtueel netwerk tussen virtuele netwerken die zijn gemaakt via Resource Manager-peering. Beide virtuele netwerken bestaan in Hallo hetzelfde abonnement. Peering twee virtuele netwerken kunnen resources in verschillende virtuele netwerken toocommunicate met elkaar met dezelfde bandbreedte en latentie Hallo alsof Hallo resources in Hallo hetzelfde virtuele netwerk. Meer informatie over [virtuele netwerk peering](virtual-network-peering-overview.md). 

Hallo stappen toocreate een virtueel netwerk peering zijn verschillend, afhankelijk van of Hallo virtuele netwerken in Hallo dezelfde of verschillende, abonnementen en die zijn [Azure implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Hallo virtuele netwerken worden gemaakt via. Meer informatie over hoe toocreate een virtueel netwerk door te klikken op Hallo scenario uit de volgende tabel Hallo-peering in andere scenario's:

|Azure-implementatiemodel  | Azure-abonnement  |
|--------- |---------|
|[Beide Resource Manager](create-peering-different-subscriptions.md) |Andere|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models.md) |Dezelfde|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models-subscriptions.md) |Andere|

Een virtueel netwerk peering kan niet worden gemaakt tussen twee virtuele netwerken die zijn geïmplementeerd via Hallo klassieke implementatiemodel. Een virtueel netwerk peering kan alleen worden gemaakt tussen twee virtuele netwerken die bestaan in Hallo dezelfde Azure-regio. Als u tooconnect virtuele netwerken die zijn beide gemaakt via de klassieke implementatiemodel hello, of die zijn opgenomen in verschillende Azure-regio's nodig hebt, kunt u een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hallo virtuele netwerken. 

U kunt Hallo [Azure-portal](#portal), hello Azure [opdrachtregelinterface](#cli) (CLI) Azure [PowerShell](#powershell), of een [Azure Resource Manager-sjabloon](#template) toocreate peering van een virtueel netwerk. Klik op Hallo vorige hulpprogramma koppelingen toogo direct toohello stappen voor het maken van een virtueel netwerk peering met behulp van het hulpprogramma naar keuze.

## <a name="portal"></a>Maken van de peering - Azure-portal

1. Meld u bij toohello [Azure-portal](https://portal.azure.com). Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
2. Klik op **+ nieuw**, klikt u op **Networking**, klikt u vervolgens op **virtueel netwerk**.
3. In Hallo **virtueel netwerk maken** blade invoert, of Selecteer waarden voor Hallo na instellingen en klik vervolgens op **maken**:
    - **Naam**: *myVnet1*
    - **Adresruimte**: *10.0.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.0.0.0/24*
    - **Abonnement**: uw abonnement te selecteren
    - **Resourcegroep**: Selecteer **nieuw** en voer *myResourceGroup*
    - **Locatie**: *VS-Oost*
4. Voer de stappen 2-3 opnieuw geven Hallo volgende waarden in stap 3:
    - **Naam**: *myVnet2*
    - **Adresruimte**: *10.1.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.1.0.0/24*
    - **Abonnement**: uw abonnement te selecteren
    - **Resourcegroep**: Selecteer **gebruik bestaande** en selecteer *myResourceGroup*
    - **Locatie**: *VS-Oost*
5. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myResourceGroup*. Klik op **myResourceGroup** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myresourcegroup** resourcegroep. Hallo resourcegroep bevat Hallo twee virtuele netwerken in de vorige stappen hebt gemaakt.
6. Klik op **myVNet1**.
7. In Hallo **myVnet1** blade die wordt weergegeven, klikt u op **Peerings** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo.
8. In Hallo **myVnet1 - Peerings** blade die werden weergegeven, klikt u op **+ toevoegen**
9. In Hallo **toevoegen peering** blade die wordt weergegeven, invoeren, of selecteer Hallo volgend opties en klik vervolgens op **OK**:
     - **Naam**: *myVnet1ToMyVnet2*
     - **Virtueel netwerk implementatiemodel**: Selecteer **Resource Manager**. 
     - **Abonnement**: uw abonnement te selecteren
     - **Virtueel netwerk**: klik op **Kies een virtueel netwerk**, klikt u vervolgens op **myVnet2**.
     - **Toestaan van toegang tot het virtuele netwerk:** ervoor te zorgen dat **ingeschakeld** is geselecteerd.
    Er zijn geen andere instellingen worden gebruikt in deze zelfstudie. toolearn over alle peering instellingen lezen [beheren van virtueel netwerk peerings](virtual-network-manage-peering.md#create-a-peering).
10. Wanneer u op **OK** in de vorige stap Hallo Hallo **toevoegen peering** blade wordt gesloten en u ziet Hallo **myVnet1 - Peerings** blade opnieuw. Na enkele seconden verschijnt Hallo peering u hebt gemaakt in Hallo-blade. **Geïnitieerd** wordt vermeld in Hallo **PEERING STATUS** kolom voor Hallo **myVnet1ToMyVnet2** peering u gemaakt. U hebt ingesteld als peer Vnet1 tooVnet2, maar u moet nu myVnet2 toomyVnet1 peer. Hallo peering moet worden gemaakt in beide richtingen tooenable bronnen in Hallo virtuele netwerken toocommunicate met elkaar.
11. Herhaal stap 5-10 nogmaals voor myVnet2.  Naam Hallo peering *myVnet2ToMyVnet1*.
12. Een paar seconden na het klikken op **OK** toocreate Hallo-peering voor MyVnet2, hello **myVnet2ToMyVnet1** peering u zojuist hebt gemaakt wordt vermeld met **verbonden** in Hallo  **STATUS van de PEERING** kolom.
13. Stap 5-7 opnieuw uitvoeren voor MyVnet1. Hallo **PEERING STATUS** voor Hallo **myVnet1ToVNet2** peering is nu er ook **verbonden**. Hallo-peering is tot stand gebracht nadat er **verbonden** in Hallo **PEERING STATUS** kolom voor beide virtuele netwerken in het Hallo-peering.
14. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
15. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, stappen voor voltooid Hallo Hallo [resources verwijderen](#delete-portal) sectie van dit artikel.

Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Peering - maken Azure CLI

Hallo script volgen:

- Hello Azure CLI versie 2.0.4 vereist of hoger. toofind hello versie, Voer Hallo `az --version` opdracht. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Werkt in een Bash-shell. Zie voor opties op Azure CLI-scripts die worden uitgevoerd op Windows-client [hello Azure CLI uitvoeren in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

U kunt in plaats van installatie Hallo CLI en de bijbehorende afhankelijkheden, hello Azure Cloud Shell gebruiken. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. Klik op Hallo **Try it** knop in Hallo-script dat volgt, waardoor een Cloud-Shell waarmee u zich aanmeldt tooyour kunnen aanmelden met Azure-account. tooexecute Hallo script, klikt u op Hallo **kopie** knop en plak Hallo inhoud in uw Cloud-Shell.

1. Een resourcegroep en twee virtuele netwerken maken.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
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

2. Maak een virtueel netwerk tussen de twee virtuele netwerken Hallo-peering.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Na het Hallo-script wordt uitgevoerd, controleert u Hallo peerings voor elke virtuele netwerk. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Voer de vorige opdracht Hallo opnieuw, vervangen *myVnet1* met *myVnet2*. Hallo-uitvoer van beide opdrachten toont **verbonden** in Hallo **PeeringState** kolom.

     Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
5. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-cli) in dit artikel.


## <a name="powershell"></a>Maken van de peering - PowerShell

1. Installeer de meest recente versie Hallo Hallo PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. toostart een PowerShell-sessie te gaan**Start**, voer **powershell**, en klik vervolgens op **PowerShell**.
3. In PowerShell aanmelden tooAzure hiertoe Hallo `login-azurermaccount` opdracht. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
4. Een resourcegroep en twee virtuele netwerken maken. tooexecute hello script kopiëren Hallo volgende script, plakt u deze in PowerShell en druk vervolgens op `Enter` nadat de laatste regel hello wordt weergegeven op het welkomstscherm:

    ```powershell
    # Variables for common values used throughout hello script.
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

5. Maak een virtueel netwerk tussen de twee virtuele netwerken Hallo-peering. Kopiëren Hallo volgende script, plak in tooPowerShell en druk vervolgens op `Enter` nadat de laatste regel hello wordt weergegeven op het welkomstscherm:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview hello subnetten voor het virtuele netwerk hello, kopie Hallo volgende opdracht, plak in tooPowerShell en druk vervolgens op `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Voer de vorige opdracht Hallo opnieuw, vervangen *myVnet1* met *myVnet2*. Hallo-uitvoer van beide opdrachten toont **verbonden** in Hallo **PeeringState** kolom.
7. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
8. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-powershell) in dit artikel.

Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Maken van de peering - Resource Manager-sjabloon

1. Verwijzing [peering van een virtueel netwerk maken](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager-sjabloon. Instructies zijn opgegeven door Hallo-sjabloon voor het Hallo-sjabloon implementeren met behulp van hello Azure-portal, PowerShell of hello Azure CLI. Aanmelden toowhichever hulpprogramma u toodeploy Hallo sjabloon met het gebruik van een account met kiest Hallo noodzakelijke machtigingen toocreate peering van een virtueel netwerk. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
2. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
3. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, stappen voor voltooid Hallo Hallo [resources verwijderen](#delete) sectie van dit artikel, met een Azure-portal, PowerShell of Azure CLI Hallo Hallo.

## <a name="permissions"></a>Machtigingen

Hallo-accounts gebruiken van een virtueel netwerk peering toocreate beschikken Hallo benodigde rol of machtigingen. Bijvoorbeeld, als u twee virtuele netwerken met de naam VNet1 en VNet2 zijn peering, moet uw account worden toegewezen Hallo minimale rol of machtiging voor elke virtuele netwerk te volgen:
    
|Virtueel netwerk|Rol|Machtigingen|
|---|---|---|
|VNet1|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen te[aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).

## <a name="delete"></a>Resources verwijderen
Wanneer u deze zelfstudie hebt voltooid, kunt u toodelete Hallo resources die u hebt gemaakt in de zelfstudie hello, zodat u geen gebruik kosten. Verwijderen van een resourcegroep, worden ook alle resources die in de resourcegroep Hallo verwijderd.

### <a name="delete-portal"></a>Azure-portal

1. Voer in de portal zoekvak Hallo **myResourceGroup**. Klik in de zoekresultaten Hallo **myResourceGroup**.
2. Op Hallo **myResourceGroup** blade, klikt u op Hallo **verwijderen** pictogram.
3. tooconfirm hello wordt verwijderd, Hallo **TYPE Hallo RESOURCEGROEPNAAM** Voer **myResourceGroup**, en klik vervolgens op **verwijderen**.

### <a name="delete-cli"></a>Azure CLI

Voer Hallo volgende opdracht:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Voer Hallo volgende opdracht:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Volgende stappen

- Grondig raken met belangrijke [peering beperkingen virtueel netwerk en het gedrag](virtual-network-manage-peering.md#requirements-and-constraints) voordat het maken van een virtueel netwerk voor productie-peering gebruikt.
- Meer informatie over alle [peering virtuele netwerkinstellingen](virtual-network-manage-peering.md#create-a-peering).
- Meer informatie over hoe te[maken van een hub en spaak netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) met het virtuele netwerk peering.
