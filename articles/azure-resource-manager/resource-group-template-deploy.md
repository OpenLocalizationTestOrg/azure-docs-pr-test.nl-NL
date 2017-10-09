---
title: resources met PowerShell en de sjabloon aaaDeploy | Microsoft Docs
description: Azure Resource Manager en Azure PowerShell toodeploy een tooAzure resources gebruiken. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="e32f2-104">Resources implementeren met Resource Manager-sjablonen en Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e32f2-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="e32f2-105">Dit onderwerp wordt uitgelegd hoe toouse Azure PowerShell met Resource Manager-sjablonen toodeploy uw tooAzure resources.</span><span class="sxs-lookup"><span data-stu-id="e32f2-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="e32f2-106">Als u niet bekend met het Hallo-concepten voor het implementeren bent en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="e32f2-107">Hallo Resource Manager-sjabloon die u implementeert, kan een lokaal bestand op uw computer of een extern bestand dat zich bevindt in een zoals GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e32f2-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="e32f2-108">Hallo-sjabloon die u in dit artikel implementeert is beschikbaar in Hallo [voorbeeldsjabloon](#sample-template) sectie, of als [storage accountsjabloon in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e32f2-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="e32f2-109">Een sjabloon implementeren vanuit uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="e32f2-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="e32f2-110">Bij het implementeren van resources tooAzure, u:</span><span class="sxs-lookup"><span data-stu-id="e32f2-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="e32f2-111">Meld u bij tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="e32f2-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="e32f2-112">Maak een resourcegroep die als Hallo-container voor resources Hallo geïmplementeerd fungeert.</span><span class="sxs-lookup"><span data-stu-id="e32f2-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="e32f2-113">Hallo-naam van de resourcegroep Hallo kan alleen alfanumerieke tekens, punten, onderstrepingstekens, afbreekstreepjes en haakjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="e32f2-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="e32f2-114">Het kan zijn van too90 tekens.</span><span class="sxs-lookup"><span data-stu-id="e32f2-114">It can be up too90 characters.</span></span> <span data-ttu-id="e32f2-115">Het mag niet eindigen op een punt.</span><span class="sxs-lookup"><span data-stu-id="e32f2-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="e32f2-116">Toohello resource groep Hallo-sjabloon die Hallo resources toocreate definieert implementeren</span><span class="sxs-lookup"><span data-stu-id="e32f2-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="e32f2-117">Een sjabloon kan parameters die u in staat toocustomize Hallo implementatie stellen bevatten.</span><span class="sxs-lookup"><span data-stu-id="e32f2-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="e32f2-118">U kunt bijvoorbeeld waarden die zijn toegesneden opgeven voor een bepaalde omgeving (zoals ontwikkelen, testen en productie).</span><span class="sxs-lookup"><span data-stu-id="e32f2-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="e32f2-119">Hallo-voorbeeldsjabloon definieert een parameter voor het opslagaccount Hallo SKU.</span><span class="sxs-lookup"><span data-stu-id="e32f2-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="e32f2-120">Hallo volgende voorbeeld maakt een resourcegroep en implementeert een sjabloon op basis van uw lokale computer:</span><span class="sxs-lookup"><span data-stu-id="e32f2-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="e32f2-121">Hallo-implementatie kan toocomplete van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="e32f2-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="e32f2-122">Wanneer deze is voltooid, ziet u een bericht met Hallo resultaat:</span><span class="sxs-lookup"><span data-stu-id="e32f2-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="e32f2-123">Een sjabloon implementeren vanuit een externe bron</span><span class="sxs-lookup"><span data-stu-id="e32f2-123">Deploy a template from an external source</span></span>

<span data-ttu-id="e32f2-124">In plaats van Resource Manager-sjablonen worden opgeslagen op uw lokale computer, kunt u desgewenst toostore ze in een externe locatie.</span><span class="sxs-lookup"><span data-stu-id="e32f2-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="e32f2-125">U kunt sjablonen opslaan in een resourcebeheerbibliotheek (zoals GitHub).</span><span class="sxs-lookup"><span data-stu-id="e32f2-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="e32f2-126">Of u kunt ze opslaan in Azure storage-account voor gedeelde toegang in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="e32f2-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="e32f2-127">toodeploy een externe-sjabloon gebruiken Hallo **TemplateUri** parameter.</span><span class="sxs-lookup"><span data-stu-id="e32f2-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="e32f2-128">Gebruik hello URI in Hallo voorbeeld toodeploy Hallo voorbeeldsjabloon vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="e32f2-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="e32f2-129">Hallo voorgaande voorbeeld vereist een openbaar toegankelijke URI voor Hallo-sjabloon voor de meeste scenario werkt, omdat de sjabloon mag geen gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="e32f2-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="e32f2-130">Als u moet toospecify gevoelige gegevens (zoals een beheerderswachtwoord), wordt die waarde als beveiligde parameter doorgeven.</span><span class="sxs-lookup"><span data-stu-id="e32f2-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="e32f2-131">Echter, als u niet wilt dat uw sjabloon toobe openbaar toegankelijk is, kunt u deze beschermen door op te slaan deze in een container particuliere opslag.</span><span class="sxs-lookup"><span data-stu-id="e32f2-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="e32f2-132">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een shared access signature (SAS)-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="e32f2-133">De parameterbestanden</span><span class="sxs-lookup"><span data-stu-id="e32f2-133">Parameter files</span></span>

<span data-ttu-id="e32f2-134">In plaats van met parameters wordt doorgegeven als inline-waarden in het script, soms is het eenvoudiger toouse een JSON-bestand met de Hallo parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="e32f2-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="e32f2-135">Hallo parameterbestand moet Hallo na indeling zijn:</span><span class="sxs-lookup"><span data-stu-id="e32f2-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="e32f2-136">U ziet dat de sectie parameters Hallo een parameternaam die overeenkomt met de Hallo parameter die is gedefinieerd in de sjabloon (storageAccountType) bevat.</span><span class="sxs-lookup"><span data-stu-id="e32f2-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="e32f2-137">Hallo parameterbestand bevat een waarde voor parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="e32f2-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="e32f2-138">Deze waarde wordt automatisch toohello sjabloon doorgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e32f2-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="e32f2-139">U kunt meerdere parameterbestanden voor verschillende scenario's maken en geeft u de juiste parameterbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="e32f2-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="e32f2-140">Hallo voorgaande voorbeeld kopiëren en opslaan als een bestand met de naam `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="e32f2-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="e32f2-141">een lokale parameterbestand toopass gebruiken Hallo **TemplateParameterFile** parameter:</span><span class="sxs-lookup"><span data-stu-id="e32f2-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="e32f2-142">een externe parameterbestand toopass gebruiken Hallo **TemplateParameterUri** parameter:</span><span class="sxs-lookup"><span data-stu-id="e32f2-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="e32f2-143">U kunt de parameters inline gebruiken en een lokale parameter bestand Hallo dezelfde bewerking voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="e32f2-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="e32f2-144">U kunt bijvoorbeeld waarden opgeven in de lokale parameterbestand Hallo en andere waarden inline toevoegen tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e32f2-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="e32f2-145">Als u waarden voor een parameter in zowel de lokale parameterbestand Hallo als inline opgeven, voorrang Hallo inline.</span><span class="sxs-lookup"><span data-stu-id="e32f2-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="e32f2-146">Echter, wanneer u een parameterbestand externe gebruikt, u kunt niet doorgeven andere waarden beide inline of vanuit een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="e32f2-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="e32f2-147">Wanneer u een parameterbestand opgeeft in Hallo **TemplateParameterUri** parameter, alle inline parameters worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="e32f2-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="e32f2-148">Alle parameterwaarden in het externe bestand Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="e32f2-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="e32f2-149">Als de sjabloon een gevoelige waarde die u niet opnemen in het parameterbestand hello bevat, voeg die waarde tooa-sleutelkluis of dynamisch bieden alle parameter waarden inline.</span><span class="sxs-lookup"><span data-stu-id="e32f2-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="e32f2-150">Als de sjabloon een parameter met dezelfde naam als een van de parameters in de PowerShell-opdracht Hallo Hallo hello bevat, PowerShell biedt Hallo-parameter van uw sjabloon Hallo postfix **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="e32f2-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="e32f2-151">Bijvoorbeeld, een parameter genaamd **ResourceGroupName** in uw sjabloon is in strijd met Hallo **ResourceGroupName** parameter in Hallo [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e32f2-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="e32f2-152">U bent na vragen aan gebruiker tooprovide een waarde voor **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="e32f2-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="e32f2-153">In het algemeen voorkomt u deze verwarring door te geven geen parameters met Hallo dezelfde naam als parameters die worden gebruikt voor implementatiebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e32f2-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="e32f2-154">Een sjabloonimplementatie testen</span><span class="sxs-lookup"><span data-stu-id="e32f2-154">Test a template deployment</span></span>

<span data-ttu-id="e32f2-155">tootest uw sjabloon en de parameterbestanden waarden zonder het distribueren van alle resources gebruiken [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="e32f2-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="e32f2-156">Als er geen fouten worden aangetroffen, wordt Hallo-opdracht is voltooid zonder reactie.</span><span class="sxs-lookup"><span data-stu-id="e32f2-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="e32f2-157">Als er een fout wordt gedetecteerd, retourneert Hallo opdracht een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e32f2-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="e32f2-158">Poging een onjuiste waarde voor het opslagaccount Hallo SKU, toopass retourneert bijvoorbeeld Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="e32f2-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="e32f2-159">Als uw sjabloon een syntaxisfout heeft, foutmelding Hallo opdracht een die aangeeft dat Hallo sjabloon kan niet worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="e32f2-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="e32f2-160">Hallo-bericht geeft aan Hallo regelnummer en positie van Hallo parseerfout.</span><span class="sxs-lookup"><span data-stu-id="e32f2-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="e32f2-161">toouse voltooid modus gebruik Hallo `Mode` parameter:</span><span class="sxs-lookup"><span data-stu-id="e32f2-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="e32f2-162">Voorbeeldsjabloon</span><span class="sxs-lookup"><span data-stu-id="e32f2-162">Sample template</span></span>

<span data-ttu-id="e32f2-163">Hallo wordt volgende sjabloon gebruikt voor het Hallo-voorbeelden in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e32f2-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="e32f2-164">Kopiëren en opslaan als een bestand met de naam storage.json.</span><span class="sxs-lookup"><span data-stu-id="e32f2-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="e32f2-165">toounderstand hoe toocreate deze sjabloon Zie [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="e32f2-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e32f2-166">Next steps</span></span>
* <span data-ttu-id="e32f2-167">Hallo-voorbeelden in dit artikel implementeren resources tooa-resourcegroep in uw standaardabonnement.</span><span class="sxs-lookup"><span data-stu-id="e32f2-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="e32f2-168">Zie voor een ander abonnement toouse [meerdere Azure-abonnementen beheren](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="e32f2-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="e32f2-169">Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [script voor implementatie van Resource Manager-sjabloon](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="e32f2-170">hoe toodefine-parameters in de sjabloon zien toounderstand [begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e32f2-171">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e32f2-172">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="e32f2-173">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e32f2-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

