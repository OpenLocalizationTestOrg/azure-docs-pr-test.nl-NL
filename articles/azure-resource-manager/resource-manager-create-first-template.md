---
title: de eerste Azure Resource Manager-sjabloon aaaCreate | Microsoft Docs
description: Een stapsgewijze handleiding toocreating uw eerste Azure Resource Manager-sjabloon. Hier ziet u hoe toouse verwijzing naar de sjabloon voor een sjabloon storage account toocreate Hallo Hallo.
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
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="a4274-104">Uw eerste Azure Resource Manager-sjabloon maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="a4274-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="a4274-105">In dit onderwerp leidt u door Hallo stappen voor het maken van uw eerste Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a4274-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="a4274-106">Resource Manager-sjablonen zijn JSON-bestanden die Hallo resources moet u toodeploy voor uw oplossing definiëren.</span><span class="sxs-lookup"><span data-stu-id="a4274-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="a4274-107">toounderstand hello concepten die horen bij het implementeren en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4274-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="a4274-108">Als u bestaande resources hebt en tooget een sjabloon voor deze bronnen wilt, raadpleegt u [een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="a4274-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="a4274-109">toocreate en herzien sjablonen, moet u een JSON-editor.</span><span class="sxs-lookup"><span data-stu-id="a4274-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="a4274-110">[Visual Studio Code](https://code.visualstudio.com/) is een lichte, open-source, platformoverschrijdende code-editor.</span><span class="sxs-lookup"><span data-stu-id="a4274-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="a4274-111">U wordt sterk aangeraden om Visual Studio Code te gebruiken voor het maken van Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a4274-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="a4274-112">In dit onderwerp wordt ervan uitgegaan dat u VS Code gebruikt. Als u een andere JSON-editor (zoals Visual Studio) hebt, kunt u die editor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4274-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4274-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a4274-113">Prerequisites</span></span>

* <span data-ttu-id="a4274-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a4274-114">Visual Studio Code.</span></span> <span data-ttu-id="a4274-115">U kunt VS Code, indien nodig, installeren via [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a4274-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="a4274-116">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a4274-116">An Azure subscription.</span></span> <span data-ttu-id="a4274-117">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="a4274-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="a4274-118">Sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a4274-118">Create template</span></span>

<span data-ttu-id="a4274-119">Laten we beginnen met een eenvoudige sjabloon waarmee een tooyour voor opslagaccountabonnement wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a4274-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="a4274-120">Selecteer **Bestand** > **Nieuw bestand**.</span><span class="sxs-lookup"><span data-stu-id="a4274-120">Select **File** > **New File**.</span></span> 

   ![Nieuw bestand](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="a4274-122">Kopieer en plak de volgende JSON-syntaxis in het bestand Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4274-122">Copy and paste hello following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="a4274-123">Namen van opslagaccounts zijn enkele beperkingen waardoor ze moeilijk tooset.</span><span class="sxs-lookup"><span data-stu-id="a4274-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="a4274-124">Hallo-naam moet tussen 3 en 24 tekens lang, gebruik alleen cijfers en kleine letters en uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="a4274-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="a4274-125">Hallo voorgaande sjabloon worden gebruikt voor Hallo [uniqueString](resource-group-template-functions-string.md#uniquestring) werken toogenerate een hash-waarde.</span><span class="sxs-lookup"><span data-stu-id="a4274-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="a4274-126">toogive deze hash waarde meer betekenis: Hallo voorvoegsel wordt toegevoegd *opslag*.</span><span class="sxs-lookup"><span data-stu-id="a4274-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="a4274-127">Sla dit bestand als **azuredeploy.json** tooa lokale map.</span><span class="sxs-lookup"><span data-stu-id="a4274-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Sjabloon opslaan](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="a4274-129">Sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="a4274-129">Deploy template</span></span>

<span data-ttu-id="a4274-130">U gereed toodeploy deze sjabloon zijn.</span><span class="sxs-lookup"><span data-stu-id="a4274-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="a4274-131">U PowerShell of Azure CLI toocreate een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a4274-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="a4274-132">Vervolgens implementeert u een opslaggroep account toothat resource.</span><span class="sxs-lookup"><span data-stu-id="a4274-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="a4274-133">Gebruik Hallo volgende opdrachten uit Hallo-map met de Hallo-sjabloon voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4274-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="a4274-134">Gebruik voor een lokale installatie van Azure CLI Hallo volgende opdrachten uit Hallo-map met de Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="a4274-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="a4274-135">Wanneer de implementatie is voltooid, wordt uw storage-account bestaat in de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4274-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="a4274-136">Sjabloon implementeren vanuit Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a4274-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="a4274-137">U kunt [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI-opdrachten voor het implementeren van uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a4274-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="a4274-138">Echter, moet u eerst uw sjabloon in laden Hallo bestandsshare voor uw Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="a4274-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="a4274-139">Als u Cloud Shell niet hebt gebruikt, raadpleegt u [Overzicht van Azure Cloud Shell](../cloud-shell/overview.md) voor informatie over het instellen.</span><span class="sxs-lookup"><span data-stu-id="a4274-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="a4274-140">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4274-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="a4274-141">Selecteer de Cloud Shell-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a4274-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="a4274-142">Hallo naampatroon is `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="a4274-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Resourcegroep selecteren](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="a4274-144">Hallo storage-account selecteren voor uw Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="a4274-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Opslagaccount selecteren](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="a4274-146">Selecteer **Bestanden**.</span><span class="sxs-lookup"><span data-stu-id="a4274-146">Select **Files**.</span></span>

   ![Bestanden selecteren](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="a4274-148">Selecteer Hallo bestandsshare voor Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="a4274-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="a4274-149">Hallo naampatroon is `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="a4274-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Bestandsshare selecteren](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="a4274-151">Selecteer **Map toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a4274-151">Select **Add directory**.</span></span>

   ![Map toevoegen](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="a4274-153">Geef deze de naam **Sjablonen** en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4274-153">Name it **templates**, and select **Okay**.</span></span>

   ![Map een naam geven](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="a4274-155">Selecteer een nieuwe map.</span><span class="sxs-lookup"><span data-stu-id="a4274-155">Select your new directory.</span></span>

   ![Map selecteren](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="a4274-157">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="a4274-157">Select **Upload**.</span></span>

   ![Uploaden selecteren](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="a4274-159">Zoek de sjabloon en upload deze.</span><span class="sxs-lookup"><span data-stu-id="a4274-159">Find and upload your template.</span></span>

   ![Bestand uploaden](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="a4274-161">Open Hallo-prompt.</span><span class="sxs-lookup"><span data-stu-id="a4274-161">Open hello prompt.</span></span>

   ![Cloud Shell openen](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="a4274-163">Voer de volgende opdrachten in de Cloud Shell Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4274-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="a4274-164">Wanneer de implementatie is voltooid, wordt uw storage-account bestaat in de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4274-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="a4274-165">Hallo-sjabloon aanpassen</span><span class="sxs-lookup"><span data-stu-id="a4274-165">Customize hello template</span></span>

<span data-ttu-id="a4274-166">Hallo sjabloon werkt goed samen, maar het is niet flexibel.</span><span class="sxs-lookup"><span data-stu-id="a4274-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="a4274-167">Altijd implementeert u een lokaal redundante opslag tooSouth VS-midden.</span><span class="sxs-lookup"><span data-stu-id="a4274-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="a4274-168">de naam van de Hallo is altijd *opslag* gevolgd door een hash-waarde.</span><span class="sxs-lookup"><span data-stu-id="a4274-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="a4274-169">tooenable Hallo-sjabloon voor verschillende scenario's met parameters toohello sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a4274-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="a4274-170">Hallo ziet volgende voorbeeld Hallo parameters sectie met twee parameters.</span><span class="sxs-lookup"><span data-stu-id="a4274-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="a4274-171">de eerste parameter Hallo `storageSKU` kunt u toospecify Hallo type redundantie.</span><span class="sxs-lookup"><span data-stu-id="a4274-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="a4274-172">Deze wordt beperkt door Hallo-waarden die u kunt doorgeven in toovalues die geldig voor een opslagaccount zijn.</span><span class="sxs-lookup"><span data-stu-id="a4274-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="a4274-173">Er wordt ook een standaardwaarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a4274-173">It also specifies a default value.</span></span> <span data-ttu-id="a4274-174">tweede parameter Hallo `storageNamePrefix` set tooallow maximaal 11 tekens is.</span><span class="sxs-lookup"><span data-stu-id="a4274-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="a4274-175">Hiermee wordt een standaardwaarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a4274-175">It specifies a default value.</span></span>

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
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="a4274-176">Voeg een variabele met de naam in gedeelte variabelen Hallo `storageName`.</span><span class="sxs-lookup"><span data-stu-id="a4274-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="a4274-177">Het voorvoegsel op Hallo van Hallo parameters en een hash van Hallo combineert [uniqueString](resource-group-template-functions-string.md#uniquestring) functie.</span><span class="sxs-lookup"><span data-stu-id="a4274-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="a4274-178">Hierbij Hallo [toLower](resource-group-template-functions-string.md#tolower) tooconvert alle tekens toolowercase werken.</span><span class="sxs-lookup"><span data-stu-id="a4274-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="a4274-179">toouse deze nieuwe waarden voor uw opslagaccount, wijzig de resourcedefinitie Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4274-179">toouse these new values for your storage account, change hello resource definition:</span></span>

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

<span data-ttu-id="a4274-180">U ziet dat Hallo naam van het opslagaccount hello toohello variabele die u hebt toegevoegd nu is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a4274-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="a4274-181">Hallo SKU-naam is toohello waarde van parameter Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a4274-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="a4274-182">Hallo vestiging dezelfde locatie als de resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4274-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="a4274-183">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="a4274-183">Save your file.</span></span> 

<span data-ttu-id="a4274-184">Na het voltooien van Hallo stappen in dit artikel is de sjabloon nu ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="a4274-184">After completing hello steps in this article, your template now looks like:</span></span>

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
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
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

## <a name="redeploy-template"></a><span data-ttu-id="a4274-185">Sjabloon opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="a4274-185">Redeploy template</span></span>

<span data-ttu-id="a4274-186">Implementeer opnieuw Hallo sjabloon met verschillende waarden.</span><span class="sxs-lookup"><span data-stu-id="a4274-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="a4274-187">Gebruik voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4274-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="a4274-188">Gebruik voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="a4274-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="a4274-189">Upload de gewijzigde sjabloon toohello file share voor Hallo Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="a4274-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="a4274-190">Hallo bestaand bestand overschrijven.</span><span class="sxs-lookup"><span data-stu-id="a4274-190">Overwrite hello existing file.</span></span> <span data-ttu-id="a4274-191">Gebruik vervolgens Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a4274-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="a4274-192">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="a4274-192">Clean up resources</span></span>

<span data-ttu-id="a4274-193">Wanneer deze niet langer nodig is, Hallo resources die u hebt geïmplementeerd door het verwijderen van resourcegroep Hallo opschonen.</span><span class="sxs-lookup"><span data-stu-id="a4274-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="a4274-194">Gebruik voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4274-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="a4274-195">Gebruik voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="a4274-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="a4274-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4274-196">Next steps</span></span>
* <span data-ttu-id="a4274-197">Zie toolearn meer informatie over het Hallo-structuur van een sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a4274-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a4274-198">Zie toolearn over de eigenschappen voor een opslagaccount hello [opslagaccounts sjabloonverwijzing](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="a4274-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="a4274-199">tooview voltooid sjablonen voor verschillende soorten oplossingen, Zie Hallo [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="a4274-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
