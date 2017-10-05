---
title: Eerste Azure Resource Manager-sjabloon maken | Microsoft Docs
description: Een stapsgewijze handleiding voor het maken van uw eerste Azure Resource Manager-sjabloon. U leert hoe u de sjabloonverwijzing voor een opslagaccount gebruikt om een sjabloon te maken.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 49086b51e2db1aebed45746306ae14b6f1feb631
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="fcf5f-104">Uw eerste Azure Resource Manager-sjabloon maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="fcf5f-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="fcf5f-105">In dit onderwerp worden de stappen beschreven voor het maken van uw eerste Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="fcf5f-106">Resource Manager-sjablonen zijn JSON-bestanden die de resources definiëren die u voor uw oplossing moet implementeren.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="fcf5f-107">Zie [Overzicht van Azure Resource Manager](resource-group-overview.md) voor inzicht in de concepten die gerelateerd zijn aan het implementeren en beheren van uw Azure-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="fcf5f-108">Zie [Een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md) als u een sjabloon voor bestaande resources wilt maken.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="fcf5f-109">U hebt een JSON-editor nodig om sjablonen te maken en reviseren.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="fcf5f-110">[Visual Studio Code](https://code.visualstudio.com/) is een lichte, open-source, platformoverschrijdende code-editor.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="fcf5f-111">U wordt sterk aangeraden om Visual Studio Code te gebruiken voor het maken van Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="fcf5f-112">In dit onderwerp wordt ervan uitgegaan dat u VS Code gebruikt. Als u een andere JSON-editor (zoals Visual Studio) hebt, kunt u die editor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcf5f-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fcf5f-113">Prerequisites</span></span>

* <span data-ttu-id="fcf5f-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-114">Visual Studio Code.</span></span> <span data-ttu-id="fcf5f-115">U kunt VS Code, indien nodig, installeren via [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fcf5f-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="fcf5f-116">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-116">An Azure subscription.</span></span> <span data-ttu-id="fcf5f-117">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="fcf5f-118">Sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="fcf5f-118">Create template</span></span>

<span data-ttu-id="fcf5f-119">Laten we beginnen met een eenvoudige sjabloon waarmee een opslagaccount in uw abonnement wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-119">Let's start with a simple template that deploys a storage account to your subscription.</span></span>

1. <span data-ttu-id="fcf5f-120">Selecteer **Bestand** > **Nieuw bestand**.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-120">Select **File** > **New File**.</span></span> 

   ![Nieuw bestand](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="fcf5f-122">Kopieer en plak de volgende JSON-syntaxis in het bestand:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-122">Copy and paste the following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="fcf5f-123">Er gelden enkele beperkingen voor opslagaccountnamen waardoor ze moeilijk in te stellen zijn.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-123">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="fcf5f-124">De naam moet tussen de 3 en 24 tekens lang zijn, alleen cijfers en kleine letters bevatten en uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-124">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="fcf5f-125">In de voorgaande sjabloon wordt de functie [uniqueString](resource-group-template-functions-string.md#uniquestring) gebruikt om een hashwaarde te genereren.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-125">The preceding template uses the [uniqueString](resource-group-template-functions-string.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="fcf5f-126">Het voorvoegsel *opslag* wordt toegevoegd om deze hashwaarde meer betekenis te geven.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-126">To give this hash value more meaning, it adds the prefix *storage*.</span></span> 

3. <span data-ttu-id="fcf5f-127">Sla dit bestand als **azuredeploy.json** op in een lokale map.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-127">Save this file as **azuredeploy.json** to a local folder.</span></span>

   ![Sjabloon opslaan](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="fcf5f-129">Sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="fcf5f-129">Deploy template</span></span>

<span data-ttu-id="fcf5f-130">U kunt deze sjabloon nu implementeren.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-130">You are ready to deploy this template.</span></span> <span data-ttu-id="fcf5f-131">U kunt PowerShell of Azure CLI gebruiken om een resourcegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-131">You use either PowerShell or Azure CLI to create a resource group.</span></span> <span data-ttu-id="fcf5f-132">Vervolgens implementeert u een opslagaccount in deze resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-132">Then, you deploy a storage account to that resource group.</span></span>

* <span data-ttu-id="fcf5f-133">Gebruik voor PowerShell de volgende opdrachten uit de map met de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-133">For PowerShell, use the following commands from the folder containing the template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="fcf5f-134">Gebruik voor een lokale installatie van Azure CLI de volgende opdrachten uit de map met de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-134">For a local installation of Azure CLI, use the following commands from the folder containing the template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="fcf5f-135">Wanneer de implementatie is voltooid, bevindt het opslagaccount zich in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-135">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="fcf5f-136">Sjabloon implementeren vanuit Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="fcf5f-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="fcf5f-137">U kunt [Cloud Shell](../cloud-shell/overview.md) gebruiken om de Azure CLI-opdrachten voor het implementeren van uw sjabloon uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-137">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="fcf5f-138">U moet de sjabloon echter eerst in de bestandsshare voor Cloud Shell laden.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-138">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="fcf5f-139">Als u Cloud Shell niet hebt gebruikt, raadpleegt u [Overzicht van Azure Cloud Shell](../cloud-shell/overview.md) voor informatie over het instellen.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="fcf5f-140">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fcf5f-140">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="fcf5f-141">Selecteer de Cloud Shell-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="fcf5f-142">Het naampatroon is `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-142">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Resourcegroep selecteren](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="fcf5f-144">Selecteer het opslagaccount voor Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-144">Select the storage account for your Cloud Shell.</span></span>

   ![Opslagaccount selecteren](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="fcf5f-146">Selecteer **Bestanden**.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-146">Select **Files**.</span></span>

   ![Bestanden selecteren](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="fcf5f-148">Selecteer de bestandsshare voor Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-148">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="fcf5f-149">Het naampatroon is `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-149">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Bestandsshare selecteren](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="fcf5f-151">Selecteer **Map toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-151">Select **Add directory**.</span></span>

   ![Map toevoegen](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="fcf5f-153">Geef deze de naam **Sjablonen** en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-153">Name it **templates**, and select **Okay**.</span></span>

   ![Map een naam geven](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="fcf5f-155">Selecteer een nieuwe map.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-155">Select your new directory.</span></span>

   ![Map selecteren](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="fcf5f-157">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-157">Select **Upload**.</span></span>

   ![Uploaden selecteren](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="fcf5f-159">Zoek de sjabloon en upload deze.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-159">Find and upload your template.</span></span>

   ![Bestand uploaden](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="fcf5f-161">Open de prompt.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-161">Open the prompt.</span></span>

   ![Cloud Shell openen](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="fcf5f-163">Voer de volgende opdrachten in Cloud Shell in:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-163">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="fcf5f-164">Wanneer de implementatie is voltooid, bevindt het opslagaccount zich in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-164">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="customize-the-template"></a><span data-ttu-id="fcf5f-165">De sjabloon aanpassen</span><span class="sxs-lookup"><span data-stu-id="fcf5f-165">Customize the template</span></span>

<span data-ttu-id="fcf5f-166">De sjabloon werkt goed, maar is niet flexibel.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-166">The template works fine, but it is not flexible.</span></span> <span data-ttu-id="fcf5f-167">Deze implementeert altijd een lokaal redundante opslag in Zuid-centraal VS.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-167">It always deploys a locally redundant storage to South Central US.</span></span> <span data-ttu-id="fcf5f-168">De naam is altijd *Opslag* gevolgd door een hashwaarde.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-168">The name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="fcf5f-169">Voeg parameters toe aan de sjabloon om ervoor te zorgen dat u deze voor verschillende scenario's kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-169">To enable using the template for different scenarios, add parameters to the template.</span></span>

<span data-ttu-id="fcf5f-170">In het volgende voorbeeld wordt de sectie Parameters weergegeven met twee parameters.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-170">The following example shows the parameters section with two parameters.</span></span> <span data-ttu-id="fcf5f-171">Met de eerste parameter `storageSKU` kunt u het type redundantie opgeven.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-171">The first parameter `storageSKU` enables you to specify the type of redundancy.</span></span> <span data-ttu-id="fcf5f-172">Hiermee beperkt u de waarden die kunnen worden doorgegeven, tot waarden die geldig zijn voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-172">It limits the values you can pass in to values that are valid for a storage account.</span></span> <span data-ttu-id="fcf5f-173">Er wordt ook een standaardwaarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-173">It also specifies a default value.</span></span> <span data-ttu-id="fcf5f-174">De tweede parameter `storageNamePrefix` is ingesteld om een maximum aantal van 11 tekens toe te staan.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-174">The second parameter `storageNamePrefix` is set to allow a maximum of 11 characters.</span></span> <span data-ttu-id="fcf5f-175">Hiermee wordt een standaardwaarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="fcf5f-176">Voeg in de sectie Variabelen een variabele in met de naam `storageName`.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-176">In the variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="fcf5f-177">Deze combineert de voorvoegselwaarde van de parameters met een hashwaarde van de functie [uniqueString](resource-group-template-functions-string.md#uniquestring).</span><span class="sxs-lookup"><span data-stu-id="fcf5f-177">It combines the prefix value from the parameters and a hash value from the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="fcf5f-178">Deze maakt gebruik van de functie [toLower](resource-group-template-functions-string.md#tolower) om alle tekens te converteren naar kleine letters.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-178">It uses the [toLower](resource-group-template-functions-string.md#tolower) function to convert all characters to lowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="fcf5f-179">Als u deze nieuwe waarden wilt gebruiken voor uw opslagaccount, wijzigt u de resourcedefinitie:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-179">To use these new values for your storage account, change the resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="fcf5f-180">U ziet nu dat de naam van het opslagaccount is ingesteld op de variabele die u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-180">Notice that the name of the storage account is now set to the variable that you added.</span></span> <span data-ttu-id="fcf5f-181">De naam van de SKU is ingesteld op de waarde van de parameter.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-181">The SKU name is set to the value of the parameter.</span></span> <span data-ttu-id="fcf5f-182">De locatie is ingesteld op dezelfde locatie als de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-182">The location is set the same location as the resource group.</span></span>

<span data-ttu-id="fcf5f-183">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-183">Save your file.</span></span> 

<span data-ttu-id="fcf5f-184">Na het voltooien van de stappen in dit artikel ziet uw sjabloon er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-184">After completing the steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="fcf5f-185">Sjabloon opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="fcf5f-185">Redeploy template</span></span>

<span data-ttu-id="fcf5f-186">Implementeer de sjabloon opnieuw met verschillende waarden.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-186">Redeploy the template with different values.</span></span>

<span data-ttu-id="fcf5f-187">Gebruik voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="fcf5f-188">Gebruik voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="fcf5f-189">Upload voor Cloud Shell de gewijzigde sjabloon naar de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-189">For the Cloud Shell, upload your changed template to the file share.</span></span> <span data-ttu-id="fcf5f-190">Overschrijf het bestaande bestand.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-190">Overwrite the existing file.</span></span> <span data-ttu-id="fcf5f-191">Gebruik vervolgens deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-191">Then, use the following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="fcf5f-192">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="fcf5f-192">Clean up resources</span></span>

<span data-ttu-id="fcf5f-193">Schoon de geïmplementeerd resources, wanneer u deze niet meer nodig hebt, op door de resourcegroep te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-193">When no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

<span data-ttu-id="fcf5f-194">Gebruik voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="fcf5f-195">Gebruik voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="fcf5f-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="fcf5f-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fcf5f-196">Next steps</span></span>
* <span data-ttu-id="fcf5f-197">Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md) voor meer informatie over de structuur van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-197">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fcf5f-198">Zie [Storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts) (Sjabloonverwijzing voor opslagaccounts) voor meer informatie over de eigenschappen van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-198">To learn about the properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="fcf5f-199">Zie de [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) voor volledige sjablonen voor verschillende soorten oplossingen.</span><span class="sxs-lookup"><span data-stu-id="fcf5f-199">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
