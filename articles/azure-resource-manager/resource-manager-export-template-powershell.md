---
title: Resource Manager-sjabloon aaaExport met Azure PowerShell | Microsoft Docs
description: Gebruik Azure Resource Manager en Azure PowerShell tooexport een sjabloon van een resourcegroep.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="69e1c-103">Exporteren van Azure Resource Manager-sjablonen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="69e1c-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="69e1c-104">Resource Manager kunt u tooexport Resource Manager-sjabloon uit bestaande resources in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="69e1c-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="69e1c-105">U kunt deze gegenereerde sjabloon toolearn over Hallo sjabloon syntaxis of tooautomate Hallo hergebruik van uw oplossing naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="69e1c-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="69e1c-106">Het is belangrijk toonote dat er twee verschillende manieren tooexport een sjabloon zijn:</span><span class="sxs-lookup"><span data-stu-id="69e1c-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="69e1c-107">Hallo werkelijke sjabloon die u voor een implementatie gebruikt, kunt u exporteren.</span><span class="sxs-lookup"><span data-stu-id="69e1c-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="69e1c-108">Hallo geëxporteerde sjabloon bevat alle Hallo parameters en variabelen exact zo worden weergegeven in de oorspronkelijke sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="69e1c-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="69e1c-109">Deze methode is handig wanneer u een sjabloon tooretrieve nodig.</span><span class="sxs-lookup"><span data-stu-id="69e1c-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="69e1c-110">U kunt een sjabloon met de huidige status van de resourcegroep Hallo Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="69e1c-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="69e1c-111">Hallo geëxporteerde sjabloon is niet op basis van een sjabloon die u voor implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="69e1c-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="69e1c-112">In plaats daarvan wordt een sjabloon die een momentopname van de resourcegroep Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="69e1c-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="69e1c-113">geëxporteerde sjabloon Hallo heeft veel vastgelegde waarden en waarschijnlijk niet zoveel parameters zoals u normaal gesproken zou definiëren.</span><span class="sxs-lookup"><span data-stu-id="69e1c-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="69e1c-114">Deze methode is handig als u de resourcegroep Hallo hebt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="69e1c-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="69e1c-115">Nu moet u toocapture Hallo resourcegroep als sjabloon.</span><span class="sxs-lookup"><span data-stu-id="69e1c-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="69e1c-116">Dit onderwerp bevat beide methoden.</span><span class="sxs-lookup"><span data-stu-id="69e1c-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="69e1c-117">Een oplossing implementeren</span><span class="sxs-lookup"><span data-stu-id="69e1c-117">Deploy a solution</span></span>

<span data-ttu-id="69e1c-118">tooillustrate, zowel voor het exporteren van een sjabloon nadert, u begint met het implementeren van een oplossing tooyour-abonnement.</span><span class="sxs-lookup"><span data-stu-id="69e1c-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="69e1c-119">Als u al een resourcegroep in uw abonnement dat u wilt dat tooexport, hoeft u geen toodeploy deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="69e1c-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="69e1c-120">Hallo rest van dit artikel verwijst echter toohello sjabloon voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="69e1c-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="69e1c-121">Hallo-voorbeeldscript implementeert een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="69e1c-121">hello example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="69e1c-122">Sjabloon opslaan in de implementatiegeschiedenis</span><span class="sxs-lookup"><span data-stu-id="69e1c-122">Save template from deployment history</span></span>

<span data-ttu-id="69e1c-123">U kunt een sjabloon ophalen uit de implementatiegeschiedenis van een met behulp van Hallo [opslaan AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) opdracht.</span><span class="sxs-lookup"><span data-stu-id="69e1c-123">You can retrieve a template from your deployment history by using hello [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="69e1c-124">Hallo bespaart Hallo voorbeeldsjabloon die u eerder implementeert te volgen:</span><span class="sxs-lookup"><span data-stu-id="69e1c-124">hello following example saves hello template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="69e1c-125">Deze retourneert locatie op Hallo van Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="69e1c-125">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="69e1c-126">Hallo-bestand geopend en ziet dat het Hallo exacte sjabloon die u voor implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="69e1c-126">Open hello file, and notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="69e1c-127">Hallo-parameters en variabelen overeen met de Hallo sjabloon vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="69e1c-127">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="69e1c-128">U kunt deze sjabloon opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="69e1c-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="69e1c-129">Resourcegroep exporteren als sjabloon</span><span class="sxs-lookup"><span data-stu-id="69e1c-129">Export resource group as template</span></span>

<span data-ttu-id="69e1c-130">In plaats van een sjabloon worden opgehaald uit de implementatiegeschiedenis hello, kunt u een sjabloon die Hallo huidige status van een resourcegroep vertegenwoordigt met behulp van Hallo ophalen [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) opdracht.</span><span class="sxs-lookup"><span data-stu-id="69e1c-130">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="69e1c-131">U kunt deze opdracht gebruiken wanneer u veel wijzigingen tooyour-resourcegroep hebt aangebracht en er geen bestaande sjabloon alle Hallo wijzigingen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="69e1c-131">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="69e1c-132">Deze retourneert locatie op Hallo van Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="69e1c-132">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="69e1c-133">Hallo-bestand openen en u ziet dat deze anders dan Hallo-sjabloon in GitHub is.</span><span class="sxs-lookup"><span data-stu-id="69e1c-133">Open hello file, and notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="69e1c-134">Bestaat uit verschillende parameters en geen variabelen.</span><span class="sxs-lookup"><span data-stu-id="69e1c-134">It has different parameters and no variables.</span></span> <span data-ttu-id="69e1c-135">zijn de vastgelegde toovalues Hallo opslag SKU en locatie.</span><span class="sxs-lookup"><span data-stu-id="69e1c-135">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="69e1c-136">Hallo volgende voorbeeld ziet u de geëxporteerde sjabloon hello, maar uw sjabloon is een iets andere parameternaam:</span><span class="sxs-lookup"><span data-stu-id="69e1c-136">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="69e1c-137">U kunt deze sjabloon kunt implementeren, maar het vereist raden een unieke naam voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="69e1c-137">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="69e1c-138">Hallo-naam van de parameter is enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="69e1c-138">hello name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="69e1c-139">Geëxporteerde sjabloon aanpassen</span><span class="sxs-lookup"><span data-stu-id="69e1c-139">Customize exported template</span></span>

<span data-ttu-id="69e1c-140">U kunt deze sjabloon toomake wijzigen het toouse gemakkelijker en flexibeler.</span><span class="sxs-lookup"><span data-stu-id="69e1c-140">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="69e1c-141">tooallow voor meer locaties, wijziging Hallo locatie-eigenschap toouse Hallo dezelfde locatie als Hallo resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="69e1c-141">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="69e1c-142">tooavoid met tooguess uniques naam voor het opslagaccount, verwijderen Hallo-parameter voor de opslagaccountnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="69e1c-142">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="69e1c-143">Een parameter voor een achtervoegsel voor opslag en een opslag SKU toevoegen:</span><span class="sxs-lookup"><span data-stu-id="69e1c-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="69e1c-144">Een variabele die wordt gemaakt van de opslagaccountnaam Hallo met Hallo uniqueString functie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="69e1c-144">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="69e1c-145">Hallo-naam van Hallo storage account toohello variabele instellen:</span><span class="sxs-lookup"><span data-stu-id="69e1c-145">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="69e1c-146">Hallo SKU toohello parameter ingesteld:</span><span class="sxs-lookup"><span data-stu-id="69e1c-146">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="69e1c-147">De sjabloon ziet er nu als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="69e1c-147">Your template now looks like:</span></span>

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

<span data-ttu-id="69e1c-148">Implementeer Hallo gewijzigde sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="69e1c-148">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69e1c-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69e1c-149">Next steps</span></span>
* <span data-ttu-id="69e1c-150">Zie voor meer informatie over het gebruik van Hallo portal tooexport een sjabloon [een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="69e1c-150">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="69e1c-151">toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="69e1c-151">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="69e1c-152">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="69e1c-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
