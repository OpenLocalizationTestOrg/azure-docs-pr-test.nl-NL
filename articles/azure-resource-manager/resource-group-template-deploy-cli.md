---
title: resources met Azure CLI en sjabloon aaaDeploy | Microsoft Docs
description: Azure Resource Manager en Azure CLI toodeploy een tooAzure resources gebruiken. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="28489-104">Resources implementeren met Resource Manager-sjablonen en Azure CLI</span><span class="sxs-lookup"><span data-stu-id="28489-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="28489-105">Dit onderwerp wordt uitgelegd hoe toouse Azure CLI 2.0 met Resource Manager-sjablonen toodeploy uw tooAzure resources.</span><span class="sxs-lookup"><span data-stu-id="28489-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="28489-106">Als u niet bekend met het Hallo-concepten voor het implementeren bent en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28489-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="28489-107">Hallo Resource Manager-sjabloon die u implementeert, kan een lokaal bestand op uw computer of een extern bestand dat zich bevindt in een zoals GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="28489-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="28489-108">Hallo-sjabloon die u in dit artikel implementeert is beschikbaar in Hallo [voorbeeldsjabloon](#sample-template) sectie, of als een [storage accountsjabloon in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="28489-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="28489-109">Als u geen Azure CLI is geïnstalleerd, kunt u Hallo [Cloud Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="28489-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="28489-110">Lokale sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="28489-110">Deploy local template</span></span>

<span data-ttu-id="28489-111">Bij het implementeren van resources tooAzure, u:</span><span class="sxs-lookup"><span data-stu-id="28489-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="28489-112">Meld u bij tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="28489-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="28489-113">Maak een resourcegroep die als Hallo-container voor resources Hallo geïmplementeerd fungeert.</span><span class="sxs-lookup"><span data-stu-id="28489-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="28489-114">Hallo-naam van de resourcegroep Hallo kan alleen alfanumerieke tekens, punten, onderstrepingstekens, afbreekstreepjes en haakjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="28489-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="28489-115">Het kan zijn van too90 tekens.</span><span class="sxs-lookup"><span data-stu-id="28489-115">It can be up too90 characters.</span></span> <span data-ttu-id="28489-116">Het mag niet eindigen op een punt.</span><span class="sxs-lookup"><span data-stu-id="28489-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="28489-117">Toohello resource groep Hallo-sjabloon die Hallo resources toocreate definieert implementeren</span><span class="sxs-lookup"><span data-stu-id="28489-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="28489-118">Een sjabloon kan parameters die u in staat toocustomize Hallo implementatie stellen bevatten.</span><span class="sxs-lookup"><span data-stu-id="28489-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="28489-119">U kunt bijvoorbeeld waarden die zijn toegesneden opgeven voor een bepaalde omgeving (zoals ontwikkelen, testen en productie).</span><span class="sxs-lookup"><span data-stu-id="28489-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="28489-120">Hallo-voorbeeldsjabloon definieert een parameter voor het opslagaccount Hallo SKU.</span><span class="sxs-lookup"><span data-stu-id="28489-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="28489-121">Hallo volgende voorbeeld maakt een resourcegroep en implementeert een sjabloon op basis van uw lokale computer:</span><span class="sxs-lookup"><span data-stu-id="28489-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="28489-122">Hallo-implementatie kan toocomplete van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="28489-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="28489-123">Wanneer deze is voltooid, ziet u een bericht met Hallo resultaat:</span><span class="sxs-lookup"><span data-stu-id="28489-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="28489-124">Externe sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="28489-124">Deploy external template</span></span>

<span data-ttu-id="28489-125">In plaats van Resource Manager-sjablonen worden opgeslagen op uw lokale computer, kunt u desgewenst toostore ze in een externe locatie.</span><span class="sxs-lookup"><span data-stu-id="28489-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="28489-126">U kunt sjablonen opslaan in een resourcebeheerbibliotheek (zoals GitHub).</span><span class="sxs-lookup"><span data-stu-id="28489-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="28489-127">Of u kunt ze opslaan in Azure storage-account voor gedeelde toegang in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="28489-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="28489-128">toodeploy een externe-sjabloon gebruiken Hallo **sjabloon uri** parameter.</span><span class="sxs-lookup"><span data-stu-id="28489-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="28489-129">Gebruik hello URI in Hallo voorbeeld toodeploy Hallo voorbeeldsjabloon vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="28489-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="28489-130">Hallo voorgaande voorbeeld vereist een openbaar toegankelijke URI voor Hallo-sjabloon voor de meeste scenario werkt, omdat de sjabloon mag geen gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="28489-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="28489-131">Als u moet toospecify gevoelige gegevens (zoals een beheerderswachtwoord), wordt die waarde als beveiligde parameter doorgeven.</span><span class="sxs-lookup"><span data-stu-id="28489-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="28489-132">Echter, als u niet wilt dat uw sjabloon toobe openbaar toegankelijk is, kunt u deze beschermen door op te slaan deze in een container particuliere opslag.</span><span class="sxs-lookup"><span data-stu-id="28489-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="28489-133">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een shared access signature (SAS)-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="28489-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="28489-134">Sjabloon implementeren vanuit Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="28489-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="28489-135">U kunt [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI-opdrachten voor het implementeren van uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="28489-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="28489-136">Echter, moet u eerst uw sjabloon in laden Hallo bestandsshare voor uw Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="28489-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="28489-137">Als u Cloud Shell niet hebt gebruikt, raadpleegt u [Overzicht van Azure Cloud Shell](../cloud-shell/overview.md) voor informatie over het instellen.</span><span class="sxs-lookup"><span data-stu-id="28489-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="28489-138">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="28489-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="28489-139">Selecteer de Cloud Shell-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="28489-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="28489-140">Hallo naampatroon is `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="28489-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Resourcegroep selecteren](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="28489-142">Hallo storage-account selecteren voor uw Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="28489-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Opslagaccount selecteren](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="28489-144">Selecteer **Bestanden**.</span><span class="sxs-lookup"><span data-stu-id="28489-144">Select **Files**.</span></span>

   ![Bestanden selecteren](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="28489-146">Selecteer Hallo bestandsshare voor Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="28489-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="28489-147">Hallo naampatroon is `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="28489-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Bestandsshare selecteren](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="28489-149">Selecteer **Map toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="28489-149">Select **Add directory**.</span></span>

   ![Map toevoegen](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="28489-151">Geef deze de naam **Sjablonen** en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="28489-151">Name it **templates**, and select **Okay**.</span></span>

   ![Map een naam geven](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="28489-153">Selecteer een nieuwe map.</span><span class="sxs-lookup"><span data-stu-id="28489-153">Select your new directory.</span></span>

   ![Map selecteren](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="28489-155">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="28489-155">Select **Upload**.</span></span>

   ![Uploaden selecteren](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="28489-157">Zoek de sjabloon en upload deze.</span><span class="sxs-lookup"><span data-stu-id="28489-157">Find and upload your template.</span></span>

   ![Bestand uploaden](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="28489-159">Open Hallo-prompt.</span><span class="sxs-lookup"><span data-stu-id="28489-159">Open hello prompt.</span></span>

   ![Cloud Shell openen](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="28489-161">Voer de volgende opdrachten in de Cloud Shell Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="28489-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="28489-162">De parameterbestanden</span><span class="sxs-lookup"><span data-stu-id="28489-162">Parameter files</span></span>

<span data-ttu-id="28489-163">In plaats van met parameters wordt doorgegeven als inline-waarden in het script, soms is het eenvoudiger toouse een JSON-bestand met de Hallo parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="28489-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="28489-164">Hallo parameterbestand moet Hallo na indeling zijn:</span><span class="sxs-lookup"><span data-stu-id="28489-164">hello parameter file must be in hello following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="28489-165">U ziet dat de sectie parameters Hallo een parameternaam die overeenkomt met de Hallo parameter die is gedefinieerd in de sjabloon (storageAccountType) bevat.</span><span class="sxs-lookup"><span data-stu-id="28489-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="28489-166">Hallo parameterbestand bevat een waarde voor parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="28489-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="28489-167">Deze waarde wordt automatisch toohello sjabloon doorgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="28489-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="28489-168">U kunt meerdere parameterbestanden voor verschillende scenario's maken en geeft u de juiste parameterbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="28489-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="28489-169">Hallo voorgaande voorbeeld kopiëren en opslaan als een bestand met de naam `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="28489-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="28489-170">gebruik van een lokale parameterbestand toopass `@` toospecify een lokaal bestand met de naam storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="28489-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="28489-171">Een sjabloonimplementatie testen</span><span class="sxs-lookup"><span data-stu-id="28489-171">Test a template deployment</span></span>

<span data-ttu-id="28489-172">tootest uw sjabloon en de parameterbestanden waarden zonder het distribueren van alle resources gebruiken [az implementatie valideren](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="28489-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="28489-173">Als er geen fouten worden aangetroffen, retourneert Hallo opdracht informatie over de testimplementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="28489-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="28489-174">In het bijzonder, zoals u ziet dat Hallo **fout** waarde null is.</span><span class="sxs-lookup"><span data-stu-id="28489-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="28489-175">Als er een fout wordt gedetecteerd, retourneert Hallo opdracht een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="28489-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="28489-176">Poging een onjuiste waarde voor het opslagaccount Hallo SKU, toopass retourneert bijvoorbeeld Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="28489-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="28489-177">Als uw sjabloon een syntaxisfout heeft, foutmelding Hallo opdracht een die aangeeft dat Hallo sjabloon kan niet worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="28489-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="28489-178">Hallo-bericht geeft aan Hallo regelnummer en positie van Hallo parseerfout.</span><span class="sxs-lookup"><span data-stu-id="28489-178">hello message indicates hello line number and position of hello parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="28489-179">toouse voltooid modus gebruik Hallo `mode` parameter:</span><span class="sxs-lookup"><span data-stu-id="28489-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="28489-180">Voorbeeldsjabloon</span><span class="sxs-lookup"><span data-stu-id="28489-180">Sample template</span></span>

<span data-ttu-id="28489-181">Hallo wordt volgende sjabloon gebruikt voor het Hallo-voorbeelden in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="28489-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="28489-182">Kopiëren en opslaan als een bestand met de naam storage.json.</span><span class="sxs-lookup"><span data-stu-id="28489-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="28489-183">toounderstand hoe toocreate deze sjabloon Zie [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="28489-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="28489-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="28489-184">Next steps</span></span>
* <span data-ttu-id="28489-185">Hallo-voorbeelden in dit artikel implementeren resources tooa-resourcegroep in uw standaardabonnement.</span><span class="sxs-lookup"><span data-stu-id="28489-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="28489-186">Zie voor een ander abonnement toouse [meerdere Azure-abonnementen beheren](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="28489-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="28489-187">Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [script voor implementatie van Resource Manager-sjabloon](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="28489-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="28489-188">hoe toodefine-parameters in de sjabloon zien toounderstand [begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="28489-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="28489-189">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="28489-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="28489-190">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="28489-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="28489-191">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="28489-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
