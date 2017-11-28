---
title: Resource Manager-sjabloon aaaExport met Azure CLI | Microsoft Docs
description: Gebruik Azure Resource Manager en Azure CLI tooexport een sjabloon van een resourcegroep.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="2e461-103">Azure Resource Manager-sjablonen met Azure CLI exporteren</span><span class="sxs-lookup"><span data-stu-id="2e461-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="2e461-104">Resource Manager kunt u tooexport Resource Manager-sjabloon uit bestaande resources in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e461-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="2e461-105">U kunt deze gegenereerde sjabloon toolearn over Hallo sjabloon syntaxis of tooautomate Hallo hergebruik van uw oplossing naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="2e461-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="2e461-106">Het is belangrijk toonote dat er twee verschillende manieren tooexport een sjabloon zijn:</span><span class="sxs-lookup"><span data-stu-id="2e461-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="2e461-107">Hallo werkelijke sjabloon die u voor een implementatie gebruikt, kunt u exporteren.</span><span class="sxs-lookup"><span data-stu-id="2e461-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="2e461-108">Hallo geëxporteerde sjabloon bevat alle Hallo parameters en variabelen exact zo worden weergegeven in de oorspronkelijke sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e461-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="2e461-109">Deze methode is handig wanneer u een sjabloon tooretrieve nodig.</span><span class="sxs-lookup"><span data-stu-id="2e461-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="2e461-110">U kunt een sjabloon met de huidige status van de resourcegroep Hallo Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="2e461-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="2e461-111">Hallo geëxporteerde sjabloon is niet op basis van een sjabloon die u voor implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2e461-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="2e461-112">In plaats daarvan wordt een sjabloon die een momentopname van de resourcegroep Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2e461-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="2e461-113">geëxporteerde sjabloon Hallo heeft veel vastgelegde waarden en waarschijnlijk niet zoveel parameters zoals u normaal gesproken zou definiëren.</span><span class="sxs-lookup"><span data-stu-id="2e461-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="2e461-114">Deze methode is handig als u de resourcegroep Hallo hebt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2e461-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="2e461-115">Nu moet u toocapture Hallo resourcegroep als sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2e461-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="2e461-116">Dit onderwerp bevat beide methoden.</span><span class="sxs-lookup"><span data-stu-id="2e461-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="2e461-117">Een oplossing implementeren</span><span class="sxs-lookup"><span data-stu-id="2e461-117">Deploy a solution</span></span>

<span data-ttu-id="2e461-118">tooillustrate, zowel voor het exporteren van een sjabloon nadert, u begint met het implementeren van een oplossing tooyour-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e461-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="2e461-119">Als u al een resourcegroep in uw abonnement dat u wilt dat tooexport, hoeft u geen toodeploy deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e461-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="2e461-120">Hallo rest van dit artikel verwijst echter toohello sjabloon voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e461-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="2e461-121">Hallo-voorbeeldscript implementeert een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2e461-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="2e461-122">Sjabloon opslaan in de implementatiegeschiedenis</span><span class="sxs-lookup"><span data-stu-id="2e461-122">Save template from deployment history</span></span>

<span data-ttu-id="2e461-123">U kunt een sjabloon ophalen uit de implementatiegeschiedenis van een met behulp van Hallo [az implementatie exporteren](/cli/azure/group/deployment#export) opdracht.</span><span class="sxs-lookup"><span data-stu-id="2e461-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="2e461-124">Hallo bespaart Hallo voorbeeldsjabloon die u eerder implementeert te volgen:</span><span class="sxs-lookup"><span data-stu-id="2e461-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="2e461-125">Het resultaat Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2e461-125">It returns hello template.</span></span> <span data-ttu-id="2e461-126">Hallo JSON kopiëren en opslaan als een bestand.</span><span class="sxs-lookup"><span data-stu-id="2e461-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="2e461-127">U ziet dat het Hallo exacte sjabloon die u voor implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2e461-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="2e461-128">Hallo-parameters en variabelen overeen met de Hallo sjabloon vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="2e461-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="2e461-129">U kunt deze sjabloon opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="2e461-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="2e461-130">Resourcegroep exporteren als sjabloon</span><span class="sxs-lookup"><span data-stu-id="2e461-130">Export resource group as template</span></span>

<span data-ttu-id="2e461-131">In plaats van een sjabloon worden opgehaald uit de implementatiegeschiedenis hello, kunt u een sjabloon die Hallo huidige status van een resourcegroep vertegenwoordigt met behulp van Hallo ophalen [exporteren az](/cli/azure/group#export) opdracht.</span><span class="sxs-lookup"><span data-stu-id="2e461-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="2e461-132">U kunt deze opdracht gebruiken wanneer u veel wijzigingen tooyour-resourcegroep hebt aangebracht en er geen bestaande sjabloon alle Hallo wijzigingen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="2e461-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="2e461-133">Het resultaat Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2e461-133">It returns hello template.</span></span> <span data-ttu-id="2e461-134">Hallo JSON kopiëren en opslaan als een bestand.</span><span class="sxs-lookup"><span data-stu-id="2e461-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="2e461-135">U ziet dat deze anders dan Hallo-sjabloon in GitHub is.</span><span class="sxs-lookup"><span data-stu-id="2e461-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="2e461-136">Bestaat uit verschillende parameters en geen variabelen.</span><span class="sxs-lookup"><span data-stu-id="2e461-136">It has different parameters and no variables.</span></span> <span data-ttu-id="2e461-137">zijn de vastgelegde toovalues Hallo opslag SKU en locatie.</span><span class="sxs-lookup"><span data-stu-id="2e461-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="2e461-138">Hallo volgende voorbeeld ziet u de geëxporteerde sjabloon hello, maar uw sjabloon is een iets andere parameternaam:</span><span class="sxs-lookup"><span data-stu-id="2e461-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="2e461-139">U kunt deze sjabloon kunt implementeren, maar het vereist raden een unieke naam voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2e461-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="2e461-140">Hallo-naam van de parameter is enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="2e461-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="2e461-141">Geëxporteerde sjabloon aanpassen</span><span class="sxs-lookup"><span data-stu-id="2e461-141">Customize exported template</span></span>

<span data-ttu-id="2e461-142">U kunt deze sjabloon toomake wijzigen het toouse gemakkelijker en flexibeler.</span><span class="sxs-lookup"><span data-stu-id="2e461-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="2e461-143">tooallow voor meer locaties, wijziging Hallo locatie-eigenschap toouse Hallo dezelfde locatie als Hallo resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="2e461-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="2e461-144">tooavoid met tooguess uniques naam voor het opslagaccount, verwijderen Hallo-parameter voor de opslagaccountnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e461-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="2e461-145">Een parameter voor een achtervoegsel voor opslag en een opslag SKU toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e461-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="2e461-146">Een variabele die wordt gemaakt van de opslagaccountnaam Hallo met Hallo uniqueString functie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e461-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="2e461-147">Hallo-naam van Hallo storage account toohello variabele instellen:</span><span class="sxs-lookup"><span data-stu-id="2e461-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="2e461-148">Hallo SKU toohello parameter ingesteld:</span><span class="sxs-lookup"><span data-stu-id="2e461-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="2e461-149">De sjabloon ziet er nu als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="2e461-149">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="2e461-150">Implementeer Hallo gewijzigde sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2e461-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e461-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e461-151">Next steps</span></span>
* <span data-ttu-id="2e461-152">Zie voor meer informatie over het gebruik van Hallo portal tooexport een sjabloon [een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="2e461-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="2e461-153">toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="2e461-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="2e461-154">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2e461-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>