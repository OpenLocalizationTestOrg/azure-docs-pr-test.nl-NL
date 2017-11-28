---
title: aaaCreate netwerkbeveiligingsgroepen - Azure Resource Manager-sjabloon | Microsoft Docs
description: Meer informatie over hoe toocreate en netwerkbeveiligingsgroepen met een Azure Resource Manager-sjabloon implementeren.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="244ff-103">Netwerk beveiligingsgroepen met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="244ff-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="244ff-104">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="244ff-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="244ff-105">U kunt ook [nsg's maken in het klassieke implementatiemodel Hallo](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="244ff-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="244ff-106">NSG-resources in een sjabloonbestand</span><span class="sxs-lookup"><span data-stu-id="244ff-106">NSG resources in a template file</span></span>
<span data-ttu-id="244ff-107">U kunt weergeven en downloaden Hallo [voorbeeldsjabloon](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="244ff-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="244ff-108">Hallo volgende sectie wordt uitgelegd Hallo definitie van Hallo front-NSG, op basis van Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="244ff-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="244ff-109">tooassociate hello NSG toohello front-end-subnet, hebt u toochange Hallo subnetdefinitie in Hallo sjabloon en gebruik Hallo Verwijzings-id voor Hallo NSG.</span><span class="sxs-lookup"><span data-stu-id="244ff-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="244ff-110">U ziet Hallo dezelfde voor Hallo back-end NSG- en Hallo back-end in de sjabloon Hallo werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="244ff-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="244ff-111">Hallo ARM-sjabloon implementeren met behulp van toodeploy klikt u op</span><span class="sxs-lookup"><span data-stu-id="244ff-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="244ff-112">Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="244ff-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="244ff-113">toodeploy toodeploy, het gebruik van deze sjabloon Klik Volg [deze koppeling](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), klikt u op **tooAzure implementeren**, vervang Hallo standaardparameterwaarden indien nodig en volg de instructies Hallo in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="244ff-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="244ff-114">Hallo ARM-sjabloon implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="244ff-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="244ff-115">toodeploy hello ARM-sjabloon die u hebt gedownload met behulp van PowerShell, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="244ff-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="244ff-116">Als u Azure PowerShell nog nooit hebt gebruikt, volgt u de instructies Hallo in Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) tooinstall en configureer deze.</span><span class="sxs-lookup"><span data-stu-id="244ff-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="244ff-117">Voer Hallo  **`New-AzureRmResourceGroup`**  cmdlet toocreate een resource-groep met Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="244ff-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="244ff-118">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="244ff-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="244ff-119">Hallo ARM-sjabloon implementeren met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="244ff-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="244ff-120">toodeploy hello ARM-sjabloon met behulp van Azure CLI Hallo Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="244ff-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="244ff-121">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="244ff-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="244ff-122">Voer Hallo  **`azure config mode`**  opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="244ff-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="244ff-123">Hallo volgt Hallo verwachte uitvoer voor Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="244ff-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="244ff-124">Voer Hallo  **`azure group deployment create`**  cmdlet toodeploy Hallo nieuwe VNet met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="244ff-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="244ff-125">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="244ff-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="244ff-126">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="244ff-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="244ff-127">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="244ff-127">**-n (or --name)**.</span></span> <span data-ttu-id="244ff-128">Naam van Hallo resource groep toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="244ff-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="244ff-129">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="244ff-129">**-l (or --location)**.</span></span> <span data-ttu-id="244ff-130">Azure-regio waar Hallo resourcegroep wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="244ff-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="244ff-131">**-f (of--sjabloonbestand)**.</span><span class="sxs-lookup"><span data-stu-id="244ff-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="244ff-132">Pad tooyour ARM-sjabloonbestand.</span><span class="sxs-lookup"><span data-stu-id="244ff-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="244ff-133">**-e (of--parametersbestand)**.</span><span class="sxs-lookup"><span data-stu-id="244ff-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="244ff-134">Pad tooyour parametersbestand.</span><span class="sxs-lookup"><span data-stu-id="244ff-134">Path tooyour ARM parameters file.</span></span>

