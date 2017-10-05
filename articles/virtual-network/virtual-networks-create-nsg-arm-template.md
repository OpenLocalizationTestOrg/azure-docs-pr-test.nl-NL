---
title: Maken van netwerkbeveiligingsgroepen - Azure Resource Manager-sjabloon | Microsoft Docs
description: Informatie over het maken en implementeren van netwerkbeveiligingsgroepen met een Azure Resource Manager-sjabloon.
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
ms.openlocfilehash: 88f7e5b2144daee7bf1c8e7312ba98e6fa967899
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="c4c65-103">Netwerk beveiligingsgroepen met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="c4c65-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c4c65-104">Dit artikel is van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c4c65-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="c4c65-105">U kunt ook [nsg's maken in het klassieke implementatiemodel](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c4c65-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="c4c65-106">NSG-resources in een sjabloonbestand</span><span class="sxs-lookup"><span data-stu-id="c4c65-106">NSG resources in a template file</span></span>
<span data-ttu-id="c4c65-107">U kunt bekijken en download de [voorbeeldsjabloon](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="c4c65-107">You can view and download the [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="c4c65-108">De volgende sectie bevat de definitie van de front-NSG, op basis van het scenario.</span><span class="sxs-lookup"><span data-stu-id="c4c65-108">The following section shows the definition of the front-end NSG, based on the scenario.</span></span>

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
<span data-ttu-id="c4c65-109">Als u wilt het NSG aan de front-end-subnet koppelt, die u moet de subnetdefinitie in de sjabloon wijzigen en de Verwijzings-id gebruiken voor het NSG.</span><span class="sxs-lookup"><span data-stu-id="c4c65-109">To associate the NSG to the front-end subnet, you have to change the subnet definition in the template, and use the reference id for the NSG.</span></span>

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

<span data-ttu-id="c4c65-110">U ziet dezelfde wordt uitgevoerd als de back-end-NSG en het subnet van de back-end in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c4c65-110">Notice the same being done for the back-end NSG and the back-end subnet in the template.</span></span>

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="c4c65-111">De ARM-sjabloon implementeren met klik om te implementeren</span><span class="sxs-lookup"><span data-stu-id="c4c65-111">Deploy the ARM template by using click to deploy</span></span>
<span data-ttu-id="c4c65-112">De voorbeeldsjabloon in de openbare opslagplaats maakt gebruik van een parameterbestand dat de standaardwaarden bevat voor het genereren van het hierboven beschreven scenario.</span><span class="sxs-lookup"><span data-stu-id="c4c65-112">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="c4c65-113">Als u deze sjabloon wilt implementeren met behulp van Klik om te implementeren, volgt u [deze koppeling](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG). Klik op **Distribueren naar Azure**, vervang indien nodig de standaardparameterwaarden en volg de instructies in de portal.</span><span class="sxs-lookup"><span data-stu-id="c4c65-113">To deploy this template using click to deploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-arm-template-by-using-powershell"></a><span data-ttu-id="c4c65-114">De ARM-sjabloon implementeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4c65-114">Deploy the ARM template by using PowerShell</span></span>
<span data-ttu-id="c4c65-115">Volg de onderstaande stappen voor het implementeren van de ARM-sjabloon die u hebt gedownload met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4c65-115">To deploy the ARM template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="c4c65-116">Als u Azure PowerShell nog nooit hebt gebruikt, volg de instructies in de [hoe voor het installeren en configureren van Azure PowerShell](/powershell/azure/overview) te installeren en configureren.</span><span class="sxs-lookup"><span data-stu-id="c4c65-116">If you have never used Azure PowerShell, follow the instructions in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) to install and configure it.</span></span>
2. <span data-ttu-id="c4c65-117">Voer de  **`New-AzureRmResourceGroup`**  cmdlet om een resourcegroep met de sjabloon te maken.</span><span class="sxs-lookup"><span data-stu-id="c4c65-117">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="c4c65-118">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c4c65-118">Expected output:</span></span>

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

## <a name="deploy-the-arm-template-by-using-the-azure-cli"></a><span data-ttu-id="c4c65-119">De ARM-sjabloon implementeren met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4c65-119">Deploy the ARM template by using the Azure CLI</span></span>
<span data-ttu-id="c4c65-120">Als u wilt de ARM-sjabloon implementeren met behulp van de Azure CLI, de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c4c65-120">To deploy the ARM template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="c4c65-121">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="c4c65-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c4c65-122">Voer de opdracht **`azure config mode`** uit om over te schakelen naar de modus Resource Manager, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4c65-122">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c4c65-123">Hier volgt de verwachte uitvoer voor de opdracht:</span><span class="sxs-lookup"><span data-stu-id="c4c65-123">The following is the expected output for the command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="c4c65-124">Voer de **`azure group deployment create`** cmdlet uit om de nieuwe VNet te implementeren met behulp van de sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c4c65-124">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="c4c65-125">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="c4c65-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="c4c65-126">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c4c65-126">Expected output:</span></span>
   
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
   
   * <span data-ttu-id="c4c65-127">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="c4c65-127">**-n (or --name)**.</span></span> <span data-ttu-id="c4c65-128">Naam van de resourcegroep worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4c65-128">Name of the resource group to be created.</span></span>
   * <span data-ttu-id="c4c65-129">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="c4c65-129">**-l (or --location)**.</span></span> <span data-ttu-id="c4c65-130">Azure-regio waar de resourcegroep wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4c65-130">Azure region where the resource group will be created.</span></span>
   * <span data-ttu-id="c4c65-131">**-f (of--sjabloonbestand)**.</span><span class="sxs-lookup"><span data-stu-id="c4c65-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="c4c65-132">Pad naar het sjabloonbestand ARM.</span><span class="sxs-lookup"><span data-stu-id="c4c65-132">Path to your ARM template file.</span></span>
   * <span data-ttu-id="c4c65-133">**-e (of--parametersbestand)**.</span><span class="sxs-lookup"><span data-stu-id="c4c65-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="c4c65-134">Pad naar uw parametersbestand ARM.</span><span class="sxs-lookup"><span data-stu-id="c4c65-134">Path to your ARM parameters file.</span></span>

