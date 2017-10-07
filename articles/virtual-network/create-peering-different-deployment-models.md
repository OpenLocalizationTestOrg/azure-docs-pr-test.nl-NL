---
title: aaaCreate een virtuele Azure-peering - andere implementatiemodellen - netwerk hetzelfde abonnement | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk peering tussen virtuele netwerken gemaakt via andere Azure-implementatiemodellen die aanwezig zijn in Hallo dezelfde Azure-abonnement.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Maak een virtueel netwerk peering - verschillend implementatiemodellen, hetzelfde abonnement 

In deze zelfstudie leert u toocreate een virtueel netwerk peering tussen virtuele netwerken die zijn gemaakt via verschillende implementatiemodellen. Beide virtuele netwerken bestaan in Hallo hetzelfde abonnement. Peering twee virtuele netwerken kunnen resources in verschillende virtuele netwerken toocommunicate met elkaar met dezelfde bandbreedte en latentie Hallo alsof Hallo resources in Hallo hetzelfde virtuele netwerk. Meer informatie over [virtuele netwerk peering](virtual-network-peering-overview.md). 

Hallo stappen toocreate een virtueel netwerk peering zijn verschillend, afhankelijk van of Hallo virtuele netwerken in Hallo dezelfde of verschillende, abonnementen en die zijn [Azure implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Hallo virtuele netwerken worden gemaakt via. Meer informatie over hoe toocreate een virtueel netwerk door te klikken op Hallo scenario uit de volgende tabel Hallo-peering in andere scenario's:

|Azure-implementatiemodel  | Azure-abonnement  |
|--------- |---------|
|[Beide Resource Manager](virtual-network-create-peering.md) |Dezelfde|
|[Beide Resource Manager](create-peering-different-subscriptions.md) |Andere|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models-subscriptions.md) |Andere|

Een virtueel netwerk peering kan niet worden gemaakt tussen twee virtuele netwerken die zijn geïmplementeerd via Hallo klassieke implementatiemodel. Een virtueel netwerk peering kan alleen worden gemaakt tussen twee virtuele netwerken die bestaan in Hallo dezelfde Azure-regio. Als u tooconnect virtuele netwerken die zijn beide gemaakt via de klassieke implementatiemodel hello, of die zijn opgenomen in verschillende Azure-regio's nodig hebt, kunt u een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hallo virtuele netwerken. 

Kunt u Hallo [Azure-portal](#portal), hello Azure [opdrachtregelinterface](#cli) (CLI) of Azure [PowerShell](#powershell) toocreate peering van een virtueel netwerk. Klik op Hallo vorige hulpprogramma koppelingen toogo direct toohello stappen voor het maken van een virtueel netwerk peering met behulp van het hulpprogramma naar keuze.

## <a name="cli"></a>Maken van de peering - Portal

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
4. Klik op **+ nieuw**. In Hallo **zoeken Hallo Marketplace** in het vak *virtueel netwerk*. Klik op **virtueel netwerk** wanneer deze wordt weergegeven in zoekresultaten Hallo. 
5. In Hallo **virtueel netwerk** blade Selecteer **klassieke** in Hallo **een implementatiemodel selecteren** vak en klik vervolgens op **maken**.
6. In Hallo **virtueel netwerk maken** blade invoert, of Selecteer waarden voor Hallo na instellingen en klik vervolgens op **maken**:
    - **Naam**: *myVnet2*
    - **Adresruimte**: *10.1.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.1.0.0/24*
    - **Abonnement**: uw abonnement te selecteren
    - **Resourcegroep**: Selecteer **gebruik bestaande** en selecteer *myResourceGroup*
    - **Locatie**: *VS-Oost*
7. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myResourceGroup*. Klik op **myResourceGroup** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myresourcegroup** resourcegroep. Hallo resourcegroep bevat Hallo twee virtuele netwerken in de vorige stappen hebt gemaakt.
8. Klik op **myVNet1**.
9. In Hallo **myVnet1** blade die wordt weergegeven, klikt u op **Peerings** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo.
10. In Hallo **myVnet1 - Peerings** blade die werden weergegeven, klikt u op **+ toevoegen**
11. In Hallo **toevoegen peering** blade die wordt weergegeven, invoeren, of selecteer Hallo volgend opties en klik vervolgens op **OK**:
     - **Naam**: *myVnet1ToMyVnet2*
     - **Virtueel netwerk implementatiemodel**: Selecteer **klassieke**. 
     - **Abonnement**: uw abonnement te selecteren
     - **Virtueel netwerk**: klik op **Kies een virtueel netwerk**, klikt u vervolgens op **myVnet2**.
     - **Toestaan van toegang tot het virtuele netwerk:** ervoor te zorgen dat **ingeschakeld** is geselecteerd.
    Er zijn geen andere instellingen worden gebruikt in deze zelfstudie. toolearn over alle peering instellingen lezen [beheren van virtueel netwerk peerings](virtual-network-manage-peering.md#create-a-peering).
12. Wanneer u op **OK** in de vorige stap Hallo Hallo **toevoegen peering** blade wordt gesloten en u ziet Hallo **myVnet1 - Peerings** blade opnieuw. Na enkele seconden verschijnt Hallo peering u hebt gemaakt in Hallo-blade. **Verbonden** wordt vermeld in Hallo **PEERING STATUS** kolom voor Hallo **myVnet1ToMyVnet2** peering u gemaakt.

    Hallo peer wordt nu ingesteld. Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
14. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, stappen voor voltooid Hallo Hallo [resources verwijderen](#delete-portal) sectie van dit artikel.

## <a name="cli"></a>Peering - maken Azure CLI

1. [Installeer](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate Hallo virtueel netwerk (klassiek).
2. Open een opdrachtsessie en aanmelden met behulp van Hallo tooAzure `azure login` opdracht.
3. Hallo CLI in Service Management-modus uitgevoerd door te voeren Hallo `azure config mode asm` opdracht.
4. Voer Hallo opdracht toocreate Hallo virtueel netwerk (klassiek) te volgen:
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Maak een resourcegroep en een virtueel netwerk (Resource Manager). U kunt Hallo CLI 1.0 of 2.0 gebruiken ([installeren](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). In deze zelfstudie is Hallo CLI 2.0 gebruikte toocreate Hallo virtueel netwerk (Resource Manager), aangezien 2.0 gebruikte toocreate hello peering moet. Uitvoeren Hallo volgende CLI-script vanaf uw lokale machine Hello CLI 2.0.4 bash of hoger is geïnstalleerd. Zie voor opties op die wordt uitgevoerd, bash-scripts CLI op Windows-client, [hello Azure CLI uitvoeren in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). U kunt ook hello Azure Cloud-Shell met Hallo-script uitvoeren. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. Klik op Hallo **Try it** knop in Hallo-script dat volgt, waardoor een Cloud-Shell waarmee u zich aanmeldt tooyour kunnen aanmelden met Azure-account. tooexecute Hallo script, klikt u op Hallo **kopie** knop en plakken, Hallo inhoud in uw Cloud-Shell, drukt u vervolgens op `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Maak een virtueel netwerk peering tussen Hallo twee virtuele netwerken via Hallo verschillende implementatiemodellen is gemaakt. Kopieer Hallo script tooa teksteditor op uw PC te volgen. Vervang `<subscription id>` met uw abonnements-id. Als u uw abonnements-Id niet weet, voert u Hallo `az account show` opdracht. waarde voor Hallo **id** in Hallo uitvoer is de abonnement-id. Hallo gewijzigd script plakken in tooyour CLI-sessie en druk vervolgens op `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Nadat het Hallo-script wordt uitgevoerd, moet u controleren Hallo-peering voor Hallo virtueel netwerk (Resource Manager). Kopiëren Hallo volgende opdracht, plak deze in de CLI-sessie en druk vervolgens op `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hallo uitvoer toont **verbonden** in Hallo **PeeringState** kolom. 

    Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
9. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-cli) in dit artikel.

## <a name="powershell"></a>Maken van de peering - PowerShell

1. Installeer de meest recente versie Hallo Hallo PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) en [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Een PowerShell-sessie starten.
3. In PowerShell aanmelden tooAzure hiertoe Hallo `Add-AzureAccount` opdracht.
4. toocreate een virtueel netwerk (klassiek) met PowerShell, moet u maken een nieuwe, of wijzig een bestaande netwerk configuratiebestand. Meer informatie over hoe te[exporteren, bijwerken en importeren van configuratie van netwerkbestanden](virtual-networks-using-network-configuration-file.md). Hallo bestand moet bevatten de volgende Hallo **VirtualNetworkSite** element voor Hallo virtueel netwerk in deze zelfstudie gebruikt:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Een configuratiebestand gewijzigde netwerk importeren kan leiden tot wijzigingen tooexisting virtuele netwerken (klassiek) in uw abonnement. Zorg ervoor dat u alleen Hallo vorige virtueel netwerk toevoegen en u niet wijzigen of verwijderen van een bestaande virtuele netwerken uit uw abonnement. 
5. Meld u bij tooAzure toocreate Hallo virtueel netwerk (Resource Manager) door te voeren Hallo `login-azurermaccount` opdracht. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
6. Maak een resourcegroep en een virtueel netwerk (Resource Manager). Hallo script kopiëren, plak deze in PowerShell en druk vervolgens op `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Maak een virtueel netwerk peering tussen Hallo twee virtuele netwerken via Hallo verschillende implementatiemodellen is gemaakt. Kopieer Hallo script tooa teksteditor op uw PC te volgen. Vervang `<subscription id>` met uw abonnements-id. Als u uw abonnements-Id niet weet, voert u Hallo `Get-AzureRmSubscription` opdracht tooview deze. waarde voor Hallo **Id** in Hallo geretourneerd uitvoer is uw abonnements-ID. tooexecute hello script kopiëren Hallo gewijzigd script vanaf een teksteditor, klik met de rechtermuisknop in de PowerShell-sessie en druk vervolgens op `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Nadat het Hallo-script wordt uitgevoerd, moet u controleren Hallo-peering voor Hallo virtueel netwerk (Resource Manager). Kopiëren Hallo volgende opdracht, plak deze in uw PowerShell-sessie en druk vervolgens op `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hallo uitvoer toont **verbonden** in Hallo **PeeringState** kolom.

    Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
10. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-powershell) in dit artikel.
 
## <a name="permissions"></a>Machtigingen

Hallo-accounts gebruiken van een virtueel netwerk peering toocreate beschikken Hallo benodigde rol of machtigingen. Bijvoorbeeld, als u twee virtuele netwerken met de naam myVnet1 en myVnet2 zijn peering, moet uw account worden toegewezen Hallo minimale rol of machtiging voor elke virtuele netwerk te volgen:
    
|Virtueel netwerk|Implementatiemodel|Rol|Machtigingen|
|---|---|---|---|
|myVnet1|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N.v.t.|
|myVnet2|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen te[aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).

## <a name="delete"></a>Resources verwijderen
Wanneer u deze zelfstudie hebt voltooid, kunt u toodelete Hallo resources die u hebt gemaakt in de zelfstudie hello, zodat u geen gebruik kosten. Verwijderen van een resourcegroep, worden ook alle resources die in de resourcegroep Hallo verwijderd.

### <a name="delete-portal"></a>Azure-portal

1. Voer in de portal zoekvak Hallo **myResourceGroup**. Klik in de zoekresultaten Hallo **myResourceGroup**.
2. Op Hallo **myResourceGroup** blade, klikt u op Hallo **verwijderen** pictogram.
3. tooconfirm hello wordt verwijderd, Hallo **TYPE Hallo RESOURCEGROEPNAAM** Voer **myResourceGroup**, en klik vervolgens op **verwijderen**.

### <a name="delete-cli"></a>Azure CLI

1. Hello Azure CLI 2.0 toodelete Hallo virtueel netwerk (Resource Manager) met Hallo volgende opdracht gebruiken:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Hello Azure CLI 1.0 toodelete Hallo virtueel netwerk (klassiek) Hallo volgende opdrachten gebruiken:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Voer Hallo opdracht toodelete Hallo virtueel netwerk (Resource Manager) te volgen:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete hello virtueel netwerk (klassiek) met PowerShell, moet u een bestaand bestand van de netwerk-configuratie wijzigen. Meer informatie over hoe te[exporteren, bijwerken en importeren van configuratie van netwerkbestanden](virtual-networks-using-network-configuration-file.md). Verwijder Hallo VirtualNetworkSite element voor Hallo virtuele netwerk dat wordt gebruikt in deze zelfstudie te volgen:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Een configuratiebestand gewijzigde netwerk importeren kan leiden tot wijzigingen tooexisting virtuele netwerken (klassiek) in uw abonnement. Zorg ervoor dat u alleen Hallo vorige virtuele netwerk verwijderen en u niet wijzigen of andere bestaande virtuele netwerken uit uw abonnement verwijderen. 

## <a name="next-steps"></a>Volgende stappen

- Grondig raken met belangrijke [peering beperkingen virtueel netwerk en het gedrag](virtual-network-manage-peering.md#requirements-and-constraints) voordat het maken van een virtueel netwerk voor productie-peering gebruikt.
- Meer informatie over alle [peering virtuele netwerkinstellingen](virtual-network-manage-peering.md#create-a-peering).
- Meer informatie over hoe te[maken van een hub en spaak netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) met het virtuele netwerk peering.
