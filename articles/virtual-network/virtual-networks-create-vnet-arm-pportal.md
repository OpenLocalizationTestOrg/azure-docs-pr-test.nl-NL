---
title: een Azure-netwerk met meerdere subnetten aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk met meerdere subnetten in Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Een virtueel netwerk maken met meerdere subnetten

Informatie over hoe toocreate een eenvoudige Azure-netwerk dat is gescheiden openbare en particuliere subnetten in deze zelfstudie. U kunt Azure-resources, zoals virtuele machines, App Service-omgevingen, virtuele-machineschaalsets, Azure HDInsight en cloudservices in een subnet maken. Resources in virtuele netwerken kunnen communiceren met elkaar en met resources in andere netwerken verbonden tooa virtueel netwerk.

Hallo volgende secties vindt u stappen die u toocreate een virtueel netwerk ondernemen kunt met behulp van Hallo [Azure-portal](#portal), hello Azure-opdrachtregelinterface ([Azure CLI](#azure-cli)), [Azure PowerShell ](#powershell), en een [Azure Resource Manager-sjabloon](#resource-manager-template). Hallo-resultaat is Hallo hetzelfde, ongeacht van hulpprogramma dat u toocreate Hallo virtueel netwerk gebruiken. Klik op een hulpprogramma koppeling toogo toothat gedeelte van de zelfstudie Hallo. Meer informatie over alle [virtueel netwerk](virtual-network-manage-network.md) en [subnet](virtual-network-manage-subnet.md) instellingen.

Dit artikel bevat stappen toocreate een virtueel netwerk via Hallo Resource Manager deployment model, wordt u aangeraden bij het maken van nieuwe virtuele netwerken Hallo-implementatiemodel. Als u een virtueel netwerk (klassiek) toocreate moet, Zie [een virtueel netwerk (klassiek) maken](create-virtual-network-classic.md). Als u niet bekend met Azure implementatiemodellen bent, Zie [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Azure-portal

1. Ga in een internetbrowser toohello [Azure-portal](https://portal.azure.com). Meld u aan met uw [Azure-account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u geen Azure-account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Klik in de portal Hallo op **+ nieuw** > **Networking** > **virtueel netwerk**.
3. Op Hallo **virtueel netwerk maken** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:

    |Instelling|Waarde|
    |---|---|
    |Naam|myVnet|
    |Adresruimte|10.0.0.0/16|
    |Subnetnaam|Openbaar|
    |Subnetadresbereik|10.0.0.0/24|
    |Resourcegroep|Laat **nieuw** geselecteerd en voer vervolgens **myResourceGroup**.|
    |Abonnement en de locatie|Selecteer uw abonnement en locatie.

    Als u nieuwe tooAzure, meer informatie over [resourcegroepen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnementen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), en [locaties](https://azure.microsoft.com/regions) (ook wel aangeduid tooas *regio's*).
4. U kunt in Hallo-portal slechts één subnet maken wanneer u een virtueel netwerk maken. In deze zelfstudie maakt u een tweede subnet nadat u Hallo virtueel netwerk maken. U kunt later Internet toegankelijke resources maken in Hallo **openbare** subnet. U bronnen die niet toegankelijk is vanaf Internet Hallo in Hallo ook mogelijk maken **persoonlijke** subnet. toocreate hello tweede subnet in Hallo **zoeken bronnen** vak bovenaan Hallo Hallo pagina **myVnet**. Klik in de zoekresultaten Hallo **myVnet**. Als u meerdere virtuele netwerken met dezelfde naam in uw abonnement hello, controleert u Hallo-resourcegroepen die worden vermeld in elk virtueel netwerk hebt. Zorg ervoor dat u klikt u op Hallo **myVnet** zoekresultaat met Hallo resourcegroep **myResourceGroup**.
5. Op Hallo **myVnet** blade onder **instellingen**, klikt u op **subnetten**.
6. Op Hallo **myVnet - subnetten** blade, klikt u op **+ Subnet**.
7. Op Hallo **subnet toevoegen** blade voor **naam**, voer **persoonlijke**. Voor **-adresbereik**, voer **10.0.1.0/24**.  Klik op **OK**.
8. Op Hallo **myVnet - subnetten** blade, bekijk Hallo subnetten. U kunt zien Hallo **openbare** en **persoonlijke** subnetten die u hebt gemaakt.
9. **Optioneel:** toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-portal) in dit artikel.

## <a name="azure-cli"></a>Azure CLI

Azure CLI-opdrachten zijn Hallo hetzelfde, ongeacht of u Hallo opdrachten vanaf Windows, Linux of Mac OS uitvoeren. Er zijn echter scripting verschillen tussen de houders van het besturingssysteem. Hallo-script in de volgende stappen uit Hallo wordt uitgevoerd in een Bash-shell. 

1. [Installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure CLI is geïnstalleerd. tooget help voor CLI-opdrachten, typ `az <command> --help`. In plaats van installatie Hallo CLI en de vereisten, kunt u hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hallo Cloud Shell heeft hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell (**> _**) knop bovenaan Hallo Hallo [portal](https://portal.azure.com) of klik op Hallo *Try it* knop in Hallo stappen volgen. 
2. Als Hallo CLI die lokaal wordt uitgevoerd, meldt u zich in tooAzure Hello `az login` opdracht. Als Hallo Cloud Shell wordt gebruikt, bent u al aangemeld.
3. Bekijk Hallo script en opmerkingen te volgen. In uw browser Hallo script kopieert en plakt u deze in de CLI-sessie:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Wanneer het Hallo-script is voltooid Hallo subnetten voor Hallo virtueel netwerk wordt uitgevoerd, controleren. Na de opdracht Hallo Kopieer en plak deze in de CLI-sessie:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-cli) in dit artikel.

## <a name="powershell"></a>PowerShell

1. Installeer de meest recente versie Hallo Hallo PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Aanmelden in een PowerShell-sessie tooAzure met uw [Azure-account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) met Hallo `login-azurermaccount` opdracht.

3. Bekijk Hallo script en opmerkingen te volgen. Hallo script kopieert en plakt u deze in uw PowerShell-sessie in uw browser:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. tooreview hello subnetten voor virtueel netwerk hello, Hallo na de opdracht Kopieer en plak deze in uw PowerShell-sessie:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-powershell) in dit artikel.

## <a name="resource-manager-template"></a>Resource Manager-sjabloon

U kunt een virtueel netwerk implementeren met behulp van een Azure Resource Manager-sjabloon. toolearn meer informatie over sjablonen, Zie [wat is er Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). Zie Hallo tooaccess Hallo sjabloon en toolearn over de parameters [een virtueel netwerk maken met twee subnetten](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) sjabloon. U kunt Hallo sjabloon implementeren met behulp van Hallo [portal](#template-portal), [Azure CLI](#template-cli), of [PowerShell](#template-powershell).

**Optioneel:** toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in een subsecties van [resources verwijderen](#delete) in dit artikel.

### <a name="template-portal"></a>Azure-portal

1. Open in uw browser Hallo [sjabloonpagina](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Klik op Hallo **tooAzure implementeren** knop. Als u niet al bent aangemeld in tooAzure, moet u zich aanmelden op het welkomstscherm van Azure portal-aanmelding die wordt weergegeven.
3. Toohello portal aanmelden met uw [Azure-account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u geen Azure-account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Voer Hallo waarden voor Hallo parameters te volgen:

    |Parameter|Waarde|
    |---|---|
    |Abonnement|Selecteer uw abonnement|
    |Resourcegroep|myResourceGroup|
    |Locatie|Een locatie selecteren|
    |Vnet-naam|myVnet|
    |Vnet-adresvoorvoegsel|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Openbaar|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Privé|

5. Ik ga hiermee akkoord toohello bepalingen en voorwaarden en klik vervolgens op **aankoop** toodeploy Hallo virtueel netwerk.

### <a name="template-cli"></a>Azure CLI

1. [Installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure CLI is geïnstalleerd. tooget help voor CLI-opdrachten, typ `az <command> --help`. In plaats van installatie Hallo CLI en de vereisten, kunt u hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hallo Cloud Shell heeft hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell **> _** knop bovenaan Hallo Hallo [portal](https://portal.azure.com), of klik op Hallo **Try it** knop in Hallo stappen volgen. 
2. Als Hallo CLI die lokaal wordt uitgevoerd, meldt u zich in tooAzure Hello `az login` opdracht. Als Hallo Cloud Shell wordt gebruikt, bent u al aangemeld.
3. een resourcegroep voor het virtuele netwerk Hallo toocreate, kopie Hallo volgende opdracht en plak deze in uw sessie CLI:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. U kunt Hallo sjabloon implementeren met behulp van een Hallo parameters opties te volgen:
    - **Standaard parameterwaarden**. Voer Hallo volgende opdracht:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Aangepaste parameterwaarden**. Download en Hallo sjabloon wijzigen voordat u Hallo sjabloon implementeert. Ook kunt Hallo sjabloon implementeren met behulp van de parameters op opdrachtregel Hallo of Hallo sjabloon implementeren met een afzonderlijke parameterbestand. toodownload hello sjabloon en parameters, klikt u op Hallo **bladeren op GitHub** knop op Hallo [een virtueel netwerk maken met twee subnetten](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) sjabloonpagina. Klik in GitHub op Hallo **azuredeploy.parameters.json** of **azuredeploy.json** bestand. Klik vervolgens op Hallo **Raw** knop toodisplay Hallo-bestand. Kopieer Hallo-inhoud van Hallo-bestand in uw browser. Hallo inhoud tooa bestand op uw computer opgeslagen. U kunt Hallo parameterwaarden in Hallo sjabloon wijzigt of Hallo sjabloon implementeren met een afzonderlijke parameterbestand.  

    toolearn informatie over hoe toodeploy sjablonen met behulp van deze methoden, typ `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Installeer de meest recente versie Hallo Hallo PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. In een PowerShell-sessie toosign aan met uw [Azure-account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), voer `login-azurermaccount`.
3. toocreate een resourcegroep voor Hallo virtueel netwerk, Voer Hallo volgende opdracht:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. U kunt Hallo sjabloon implementeren met behulp van een Hallo parameters opties te volgen:
    - **Standaard parameterwaarden**. Voer Hallo volgende opdracht:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Aangepaste parameterwaarden**. Download en Hallo sjabloon wijzigen voordat u deze implementeert. Ook kunt Hallo sjabloon implementeren met behulp van de parameters op opdrachtregel Hallo of Hallo sjabloon implementeren met een afzonderlijke parameterbestand. toodownload hello sjabloon en parameters, klikt u op Hallo **bladeren op GitHub** knop op Hallo [een virtueel netwerk maken met twee subnetten](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) sjabloonpagina. Klik in GitHub op Hallo **azuredeploy.parameters.json** of **azuredeploy.json** bestand. Klik vervolgens op Hallo **Raw** knop toodisplay Hallo-bestand. Kopieer Hallo-inhoud van Hallo-bestand in uw browser. Hallo inhoud tooa bestand op uw computer opgeslagen. U kunt Hallo parameterwaarden in Hallo sjabloon wijzigt of Hallo sjabloon implementeren met een afzonderlijke parameterbestand.  

    toolearn informatie over hoe toodeploy sjablonen met behulp van deze methoden, typ `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Resources verwijderen

Wanneer u deze zelfstudie hebt voltooid, wilt u mogelijk toodelete Hallo resources die u hebt gemaakt, zodat u geen gebruik kosten. Verwijderen van een resourcegroep, worden ook alle resources die in de resourcegroep Hallo verwijderd.

### <a name="delete-portal"></a>Azure-portal

1. Voer in de portal zoekvak Hallo **myResourceGroup**. Klik in de zoekresultaten Hallo **myResourceGroup**.
2. Op Hallo **myResourceGroup** blade, klikt u op Hallo **verwijderen** pictogram.
3. tooconfirm hello wordt verwijderd, Hallo **TYPE Hallo RESOURCEGROEPNAAM** Voer **myResourceGroup**, en klik vervolgens op **verwijderen**.

### <a name="delete-cli"></a>Azure CLI

Voer in een sessie CLI Hallo volgende opdracht:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Voer in een PowerShell-sessie Hallo volgende opdracht:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Volgende stappen

- toolearn over alle virtueel netwerk en subnetinstellingen, Zie [virtuele netwerken beheren](virtual-network-manage-network.md#view-vnet) en [beheren van virtueel netwerksubnetten](virtual-network-manage-subnet.md#create-subnet). U beschikt over verschillende opties voor het gebruik van virtuele netwerken en subnetten in een productie-omgeving toomeet verschillende vereisten.
- toofilter binnenkomend en uitgaand verkeer van de subnetten, maken en toepassen van [netwerkbeveiligingsgroepen](virtual-networks-nsg.md) toosubnets.
- Maak een [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of een [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtuele machine en sluit vervolgens tooan bestaand virtueel netwerk.
- tooconnect twee virtuele netwerken in dezelfde Azure-locatie hello, maakt u een [virtueel netwerk peering](virtual-network-peering-overview.md) tussen Hallo virtuele netwerken.
- Hallo virtueel netwerk tooan on-premises netwerk verbinding via een [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.
