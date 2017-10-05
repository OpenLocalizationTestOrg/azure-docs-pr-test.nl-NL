---
title: Met Azure CLI Resource Manager-sjabloon exporteren | Microsoft Docs
description: Gebruik Azure Resource Manager en Azure CLI voor een sjabloon exporteren uit een resourcegroep.
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
ms.openlocfilehash: 617664129a5353e25da1e90c742c4b009db172ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="122a4-103">Azure Resource Manager-sjablonen met Azure CLI exporteren</span><span class="sxs-lookup"><span data-stu-id="122a4-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="122a4-104">Met Resource Manager kunt u een Resource Manager-sjabloon exporteren uit bestaande resources in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="122a4-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="122a4-105">Deze gegenereerde sjabloon kunt u vervolgens gebruiken om meer te weten te komen over de sjabloonsyntaxis of om desgewenst het hergebruik van uw oplossing te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="122a4-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="122a4-106">Het is belangrijk te weten dat er twee verschillende manieren zijn om een sjabloon te exporteren:</span><span class="sxs-lookup"><span data-stu-id="122a4-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="122a4-107">U kunt de daadwerkelijke sjabloon dat u voor een implementatie hebt gebruikt, exporteren.</span><span class="sxs-lookup"><span data-stu-id="122a4-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="122a4-108">De geëxporteerde sjabloon bevat alle parameters en variabelen precies zoals ze worden weergegeven in de oorspronkelijke sjabloon.</span><span class="sxs-lookup"><span data-stu-id="122a4-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="122a4-109">Deze methode is handig als u nodig hebt voor het ophalen van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="122a4-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="122a4-110">U kunt een sjabloon exporteren met de huidige status van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="122a4-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="122a4-111">De geëxporteerde sjabloon is niet gebaseerd op een sjabloon die u voor de implementatie hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="122a4-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="122a4-112">In plaats daarvan wordt er een sjabloon gemaakt die een momentopname is van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="122a4-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="122a4-113">De geëxporteerde sjabloon heeft veel vastgelegde waarden en waarschijnlijk niet zoveel parameters als u doorgaans zou definiëren.</span><span class="sxs-lookup"><span data-stu-id="122a4-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="122a4-114">Deze methode is handig als u de resourcegroep hebt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="122a4-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="122a4-115">U moet nu de resourcegroep vastleggen als sjabloon.</span><span class="sxs-lookup"><span data-stu-id="122a4-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="122a4-116">Dit onderwerp bevat beide methoden.</span><span class="sxs-lookup"><span data-stu-id="122a4-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="122a4-117">Een oplossing implementeren</span><span class="sxs-lookup"><span data-stu-id="122a4-117">Deploy a solution</span></span>

<span data-ttu-id="122a4-118">Ter illustratie van beide benaderingen voor het exporteren van een sjabloon, laten we beginnen met het implementeren van een oplossing voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="122a4-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="122a4-119">Als u al een resourcegroep in uw abonnement die u wilt exporteren, kunt u beschikt niet over deze oplossing implementeren.</span><span class="sxs-lookup"><span data-stu-id="122a4-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="122a4-120">Echter, de rest van dit artikel verwijst naar de sjabloon voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="122a4-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="122a4-121">Het voorbeeldscript implementeert een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="122a4-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="122a4-122">Sjabloon opslaan in de implementatiegeschiedenis</span><span class="sxs-lookup"><span data-stu-id="122a4-122">Save template from deployment history</span></span>

<span data-ttu-id="122a4-123">U kunt een sjabloon ophalen uit de implementatiegeschiedenis van een met behulp van de [az implementatie exporteren](/cli/azure/group/deployment#export) opdracht.</span><span class="sxs-lookup"><span data-stu-id="122a4-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="122a4-124">Het volgende voorbeeld wordt de sjabloon die u eerder implementeert:</span><span class="sxs-lookup"><span data-stu-id="122a4-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="122a4-125">Retourneert de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="122a4-125">It returns the template.</span></span> <span data-ttu-id="122a4-126">De JSON kopiëren en opslaan als een bestand.</span><span class="sxs-lookup"><span data-stu-id="122a4-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="122a4-127">U ziet dat deze de exacte sjabloon die u voor implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="122a4-127">Notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="122a4-128">De parameters en variabelen overeen met de sjabloon vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="122a4-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="122a4-129">U kunt deze sjabloon opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="122a4-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="122a4-130">Resourcegroep exporteren als sjabloon</span><span class="sxs-lookup"><span data-stu-id="122a4-130">Export resource group as template</span></span>

<span data-ttu-id="122a4-131">In plaats van een sjabloon worden opgehaald uit de implementatiegeschiedenis van de, kunt u ophalen van een sjabloon die de huidige status van een resourcegroep met behulp van vertegenwoordigt de [exporteren az](/cli/azure/group#export) opdracht.</span><span class="sxs-lookup"><span data-stu-id="122a4-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="122a4-132">U kunt deze opdracht gebruiken wanneer u veel wijzigingen hebt aangebracht in de resourcegroep en er geen bestaande sjabloon alle wijzigingen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="122a4-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="122a4-133">Retourneert de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="122a4-133">It returns the template.</span></span> <span data-ttu-id="122a4-134">De JSON kopiëren en opslaan als een bestand.</span><span class="sxs-lookup"><span data-stu-id="122a4-134">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="122a4-135">U ziet dat deze anders dan de sjabloon in GitHub is.</span><span class="sxs-lookup"><span data-stu-id="122a4-135">Notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="122a4-136">Bestaat uit verschillende parameters en geen variabelen.</span><span class="sxs-lookup"><span data-stu-id="122a4-136">It has different parameters and no variables.</span></span> <span data-ttu-id="122a4-137">De SKU-opslag en de locatie zijn vastgelegde waarden.</span><span class="sxs-lookup"><span data-stu-id="122a4-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="122a4-138">Het volgende voorbeeld ziet u de geëxporteerde sjabloon, maar uw sjabloon is een iets andere parameternaam:</span><span class="sxs-lookup"><span data-stu-id="122a4-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="122a4-139">U kunt deze sjabloon kunt implementeren, maar het vereist raden een unieke naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="122a4-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="122a4-140">De naam van de parameter is enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="122a4-140">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="122a4-141">Geëxporteerde sjabloon aanpassen</span><span class="sxs-lookup"><span data-stu-id="122a4-141">Customize exported template</span></span>

<span data-ttu-id="122a4-142">U kunt deze sjabloon om deze te gebruiken gemakkelijker en flexibeler wijzigen.</span><span class="sxs-lookup"><span data-stu-id="122a4-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="122a4-143">Als u wilt toestaan voor meer locaties, de locatie-eigenschap voor het gebruik van dezelfde locatie als de resourcegroep te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="122a4-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="122a4-144">Om te voorkomen dat te raden een uniques naam op voor storage-account, verwijdert u de parameter voor de opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="122a4-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="122a4-145">Een parameter voor een achtervoegsel voor opslag en een opslag SKU toevoegen:</span><span class="sxs-lookup"><span data-stu-id="122a4-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="122a4-146">Een variabele die wordt gemaakt van de naam van het opslagaccount met de functie uniqueString toevoegen:</span><span class="sxs-lookup"><span data-stu-id="122a4-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="122a4-147">De naam van het storage-account aan de variabele instellen:</span><span class="sxs-lookup"><span data-stu-id="122a4-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="122a4-148">De SKU op de parameter ingesteld:</span><span class="sxs-lookup"><span data-stu-id="122a4-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="122a4-149">De sjabloon ziet er nu als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="122a4-149">Your template now looks like:</span></span>

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

<span data-ttu-id="122a4-150">De gewijzigde sjabloon opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="122a4-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="122a4-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="122a4-151">Next steps</span></span>
* <span data-ttu-id="122a4-152">Zie voor meer informatie over het exporteren van een sjabloon met de portal [een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="122a4-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="122a4-153">Om parameters te definiëren in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="122a4-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="122a4-154">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="122a4-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>