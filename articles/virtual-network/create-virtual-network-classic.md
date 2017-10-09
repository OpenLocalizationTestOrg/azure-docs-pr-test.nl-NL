---
title: een Azure-netwerk (klassiek) met meerdere subnetten aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk (klassiek) met meerdere subnetten in Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Een virtueel netwerk (klassiek) maken met meerdere subnetten

> [!IMPORTANT]
> Azure heeft twee [verschillende implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) voor het maken en werken met resources: Resource Manager en classic. In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt u aan het maken van de meeste nieuwe virtuele netwerken via Hallo [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) implementatiemodel.

Informatie over hoe toocreate een eenvoudige Azure-netwerk (klassiek) dat is gescheiden openbare en particuliere subnetten in deze zelfstudie. U kunt Azure-resources, zoals virtuele machines en cloudservices in een subnet maken. Resources die zijn gemaakt in virtuele netwerken (klassiek) kunnen communiceren met elkaar en met resources in andere netwerken verbonden tooa virtueel netwerk.

Meer informatie over alle [virtueel netwerk](virtual-network-manage-network.md) en [subnet](virtual-network-manage-subnet.md) instellingen.

> [!WARNING]
> Virtuele netwerken (klassiek), worden onmiddellijk verwijderd door Azure wanneer een [abonnement is uitgeschakeld](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Virtuele netwerken (klassiek) verwijderd, ongeacht of de bronnen in het virtuele netwerk Hallo bestaan. Als u later Hallo abonnement opnieuw inschakelt, resources die beschikbaar in het virtuele netwerk Hallo waren moeten opnieuw worden gemaakt.

U kunt een virtueel netwerk (klassiek) maken met behulp van Hallo [Azure-portal](#portal), Hallo [Azure-opdrachtregelinterface (CLI) 1.0](#azure-cli), of [PowerShell](#powershell).

## <a name="portal"></a>Portal

1. Ga in een internetbrowser toohello [Azure-portal](https://portal.azure.com). Meld u aan met uw [Azure-account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u geen Azure-account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Klik op **+ nieuw** in Hallo-portal.
3. Voer *virtueel netwerk* in Hallo **zoeken Hallo Marketplace** vak bovenaan Hallo Hallo **nieuw** blade die wordt weergegeven.  Klik op **virtueel netwerk** wanneer deze wordt weergegeven in zoekresultaten Hallo.
4. Selecteer **klassieke** in Hallo **een implementatiemodel selecteren** vak Hallo **virtueel netwerk** blade die wordt weergegeven, klikt u vervolgens op **maken**. 
5. Voer de volgende waarden op Hallo Hallo **virtueel netwerk maken (klassiek)** blade en klik vervolgens op **maken**:

    |Instelling|Waarde|
    |---|---|
    |Naam|myVnet|
    |Adresruimte|10.0.0.0/16|
    |Subnetnaam|Openbaar|
    |Subnetadresbereik|10.0.0.0/24|
    |Resourcegroep|Laat **nieuw** geselecteerd en voer vervolgens **myResourceGroup**.|
    |Abonnement en de locatie|Selecteer uw abonnement en locatie.

    Als u nieuwe tooAzure, meer informatie over [resourcegroepen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnementen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), en [locaties](https://azure.microsoft.com/regions) (ook wel aangeduid tooas *regio's*).
4. U kunt in Hallo-portal slechts één subnet maken wanneer u een virtueel netwerk maken. In deze zelfstudie maakt u een tweede subnet nadat u Hallo virtueel netwerk maken. U kunt later Internet toegankelijke resources maken in Hallo **openbare** subnet. U bronnen die niet toegankelijk is vanaf Internet Hallo in Hallo ook mogelijk maken **persoonlijke** subnet. toocreate Hallo tweede subnet, voer **myVnet** in Hallo **zoeken bronnen** vak bovenaan Hallo Hallo pagina. Klik op **myVnet** wanneer deze wordt weergegeven in zoekresultaten Hallo.
5. Klik op **subnetten** (in Hallo **instellingen** sectie) op Hallo **virtueel netwerk maken (klassiek)** blade die wordt weergegeven.
6. Klik op **+ toevoegen** op Hallo **myVnet - subnetten** blade die wordt weergegeven.
7. Voer **persoonlijke** voor **naam** op Hallo **subnet toevoegen** blade. Voer **10.0.1.0/24** voor **-adresbereik**.  Klik op **OK**.
8. Op Hallo **myVnet - subnetten** blade ziet u Hallo **openbare** en **persoonlijke** subnetten die u hebt gemaakt.
9. **Optionele**: als u deze zelfstudie hebt voltooid, kunt u toodelete Hallo resources die u hebt gemaakt, zodat u geen gebruik kosten:
    - Klik op **overzicht** op Hallo **myVnet** blade.
    - Klik op Hallo **verwijderen** pictogram op Hallo **myVnet** blade.
    - tooconfirm hello verwijdering, klikt u op **Ja** in Hallo **virtuele netwerk verwijderen** vak.

## <a name="azure-cli"></a>Azure CLI

1. U kunt ofwel [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), of gebruik Hallo CLI binnen hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. tooget help voor CLI-opdrachten, typ `azure <command> --help`. 
2. Aanmelden tooAzure met Hallo-opdracht die volgt op in een sessie CLI. Als u op **Try it** in Hallo vak hieronder een Cloud-Shell wordt geopend. U kunt tooyour Azure-abonnement, aanmelden zonder in te voeren Hallo volgende opdracht:

    ```azurecli-interactive
    azure login
    ```

3. tooensure hello CLI is in Service Management-modus, Voer Hallo volgende opdracht:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Een virtueel netwerk maken met een particulier subnet:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Maak een openbare subnet binnen het virtuele netwerk Hallo:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Hallo virtueel netwerk en subnetten bekijken:

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Optionele**: U kunt toodelete Hallo resources die u hebt gemaakt wanneer u klaar bent met deze zelfstudie, zodat u geen gebruik kosten:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Hoewel u niet een resource groep toocreate een virtueel netwerk (klassiek) opgeven in met behulp van Hallo CLI, Azure Hallo virtueel netwerk maakt in een resourcegroep met de naam *standaard netwerken*.

## <a name="powershell"></a>PowerShell

1. Installeer de meest recente versie Hallo Hallo PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Een PowerShell-sessie starten.
3. In PowerShell aanmelden tooAzure hiertoe Hallo `Add-AzureAccount` opdracht.
4. Wijzig de volgende Hallo pad en bestandsnaam naar gelang van toepassing, vervolgens uw bestaande netwerk-configuratiebestand exporteren:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate een virtueel netwerk met openbare en particuliere subnetten, gebruiken alle tekst editor tooadd hello **VirtualNetworkSite** element zijn dat toohello netwerk configuratiebestand volgt.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Bekijk Hallo volledige [network-configuratieschema bestand](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Hallo netwerk-configuratiebestand importeren:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Een configuratiebestand gewijzigde netwerk importeren kan leiden tot wijzigingen tooexisting virtuele netwerken (klassiek) in uw abonnement. Zorg ervoor dat u alleen Hallo vorige virtueel netwerk toevoegen en u niet wijzigen of verwijderen van een bestaande virtuele netwerken uit uw abonnement. 

7. Hallo virtueel netwerk en subnetten bekijken:

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Optionele**: U kunt toodelete Hallo resources die u hebt gemaakt wanneer u klaar bent met deze zelfstudie, zodat u geen gebruik kosten. toodelete hello virtueel netwerk, volledige stap 4-6 opnieuw, deze tijd verwijderen Hallo **VirtualNetworkSite** element dat u in stap 5 hebt toegevoegd.
 
> [!NOTE]
> Hoewel u niet een resource groep toocreate een virtueel netwerk (klassiek) opgeven in met behulp van PowerShell, Azure Hallo virtueel netwerk maakt in een resourcegroep met de naam *standaard netwerken*.

---

## <a name="next-steps"></a>Volgende stappen

- toolearn over alle virtueel netwerk en subnetinstellingen, Zie [virtuele netwerken beheren](virtual-network-manage-network.md) en [beheren van virtueel netwerksubnetten](virtual-network-manage-subnet.md). U beschikt over verschillende opties voor het gebruik van virtuele netwerken en subnetten in een productie-omgeving toomeet verschillende vereisten.
- toofilter binnenkomend en uitgaand verkeer van de subnetten, maken en toepassen van [netwerkbeveiligingsgroepen](virtual-networks-nsg.md) toosubnets.
- Maak een [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of een [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtuele machine en sluit vervolgens tooan bestaand virtueel netwerk.
- tooconnect twee virtuele netwerken in dezelfde Azure-locatie hello, maakt u een [virtueel netwerk peering](create-peering-different-deployment-models.md) tussen Hallo virtuele netwerken. U kunt een virtueel netwerk (Resource Manager) tooa virtueel netwerk (klassiek) peer, maar u een peering tussen twee virtuele netwerken (klassiek) niet maken.
- Hallo virtueel netwerk tooan on-premises netwerk verbinding via een [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.
