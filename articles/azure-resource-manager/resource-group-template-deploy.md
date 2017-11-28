---
title: Resources met PowerShell en de sjabloon implementeren | Microsoft Docs
description: Azure Resource Manager en Azure PowerShell gebruiken voor het implementeren van een bronnen in Azure. De resources zijn gedefinieerd in een Resource Manager-sjabloon.
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
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="67eb3-104">Resources implementeren met Resource Manager-sjablonen en Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="67eb3-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="67eb3-105">In dit onderwerp wordt uitgelegd hoe u Azure PowerShell gebruiken met Resource Manager-sjablonen voor het implementeren van uw resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="67eb3-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="67eb3-106">Als u niet bekend met concepten voor het implementeren bent en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="67eb3-107">De Resource Manager-sjabloon die u implementeert, kan een lokaal bestand op uw computer of een extern bestand dat zich bevindt in een zoals GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="67eb3-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="67eb3-108">De sjabloon die u in dit artikel implementeert vindt u in de [voorbeeldsjabloon](#sample-template) sectie, of als [storage accountsjabloon in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="67eb3-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="67eb3-109">Een sjabloon implementeren vanuit uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="67eb3-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="67eb3-110">Bij het implementeren van resources in Azure, u:</span><span class="sxs-lookup"><span data-stu-id="67eb3-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="67eb3-111">Aanmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="67eb3-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="67eb3-112">Maak een resourcegroep die als de container voor de geïmplementeerde resources fungeert.</span><span class="sxs-lookup"><span data-stu-id="67eb3-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="67eb3-113">De naam van de resourcegroep kan alleen alfanumerieke tekens, punten, onderstrepingstekens, afbreekstreepjes en haakjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="67eb3-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="67eb3-114">Het kan maximaal 90 tekens zijn.</span><span class="sxs-lookup"><span data-stu-id="67eb3-114">It can be up to 90 characters.</span></span> <span data-ttu-id="67eb3-115">Het mag niet eindigen op een punt.</span><span class="sxs-lookup"><span data-stu-id="67eb3-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="67eb3-116">De sjabloon waarin de bronnen te maken aan de resourcegroep implementeren</span><span class="sxs-lookup"><span data-stu-id="67eb3-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="67eb3-117">Een sjabloon kunt opnemen parameters waarmee u de implementatie aanpassen.</span><span class="sxs-lookup"><span data-stu-id="67eb3-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="67eb3-118">U kunt bijvoorbeeld waarden die zijn toegesneden opgeven voor een bepaalde omgeving (zoals ontwikkelen, testen en productie).</span><span class="sxs-lookup"><span data-stu-id="67eb3-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="67eb3-119">De voorbeeldsjabloon definieert een parameter voor de SKU van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="67eb3-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="67eb3-120">Het volgende voorbeeld maakt u een resourcegroep en implementeert een sjabloon op basis van uw lokale computer:</span><span class="sxs-lookup"><span data-stu-id="67eb3-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="67eb3-121">De implementatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="67eb3-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="67eb3-122">Wanneer deze is voltooid, ziet u een bericht die het resultaat bevat:</span><span class="sxs-lookup"><span data-stu-id="67eb3-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="67eb3-123">Een sjabloon implementeren vanuit een externe bron</span><span class="sxs-lookup"><span data-stu-id="67eb3-123">Deploy a template from an external source</span></span>

<span data-ttu-id="67eb3-124">In plaats van Resource Manager-sjablonen worden opgeslagen op uw lokale computer, kunt u ook deze opslaan op een externe locatie.</span><span class="sxs-lookup"><span data-stu-id="67eb3-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="67eb3-125">U kunt sjablonen opslaan in een resourcebeheerbibliotheek (zoals GitHub).</span><span class="sxs-lookup"><span data-stu-id="67eb3-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="67eb3-126">Of u kunt ze opslaan in Azure storage-account voor gedeelde toegang in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="67eb3-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="67eb3-127">Een externe als sjabloon wilt implementeren, gebruiken de **TemplateUri** parameter.</span><span class="sxs-lookup"><span data-stu-id="67eb3-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="67eb3-128">Gebruik de URI in het voorbeeld voor het voorbeeldsjabloon implementeren vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="67eb3-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="67eb3-129">Het vorige voorbeeld vereist een openbaar toegankelijke URI voor de sjabloon die voor de meeste scenario werkt, omdat de sjabloon mag geen gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="67eb3-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="67eb3-130">Als u nodig hebt om op te geven gevoelige gegevens (zoals een beheerderswachtwoord), wordt die waarde als beveiligde parameter doorgeven.</span><span class="sxs-lookup"><span data-stu-id="67eb3-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="67eb3-131">Echter, als u niet wilt dat uw sjabloon openbaar toegankelijk is, kunt u deze beschermen door op te slaan deze in een persoonlijke opslagcontainer.</span><span class="sxs-lookup"><span data-stu-id="67eb3-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="67eb3-132">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een shared access signature (SAS)-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="67eb3-133">De parameterbestanden</span><span class="sxs-lookup"><span data-stu-id="67eb3-133">Parameter files</span></span>

<span data-ttu-id="67eb3-134">In plaats van met parameters wordt doorgegeven als inline-waarden in het script, wellicht u eenvoudiger te gebruiken van een JSON-bestand met de parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="67eb3-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="67eb3-135">De parameterbestand moet in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="67eb3-135">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="67eb3-136">U ziet dat de parameters-sectie bevat een parameternaam die overeenkomt met de parameter die is gedefinieerd in de sjabloon (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="67eb3-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="67eb3-137">De parameter-bestand bevat een waarde voor de parameter.</span><span class="sxs-lookup"><span data-stu-id="67eb3-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="67eb3-138">Deze waarde wordt automatisch doorgegeven aan de sjabloon tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="67eb3-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="67eb3-139">U kunt meerdere parameterbestanden voor verschillende scenario's maken en geeft u het juiste parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="67eb3-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="67eb3-140">Het vorige voorbeeld kopiëren en opslaan als een bestand met de naam `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="67eb3-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="67eb3-141">Als u wilt doorgeven in een lokale parameterbestand, gebruiken de **TemplateParameterFile** parameter:</span><span class="sxs-lookup"><span data-stu-id="67eb3-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="67eb3-142">Voor het doorgeven van een externe parameterbestand, gebruiken de **TemplateParameterUri** parameter:</span><span class="sxs-lookup"><span data-stu-id="67eb3-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="67eb3-143">U kunt de parameters inline en een parameter local-bestand in dezelfde implementatiebewerking gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67eb3-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="67eb3-144">U kunt bijvoorbeeld waarden opgeven in het lokale parameterbestand en toevoegen van andere waarden inline tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="67eb3-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="67eb3-145">Als u waarden voor een parameter in de lokale parameterbestand- en inline opgeeft, wordt de waarde inline voorrang.</span><span class="sxs-lookup"><span data-stu-id="67eb3-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="67eb3-146">Echter, wanneer u een parameterbestand externe gebruikt, u kunt niet doorgeven andere waarden beide inline of vanuit een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="67eb3-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="67eb3-147">Wanneer u een parameterbestand in de **TemplateParameterUri** parameter, alle inline parameters worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="67eb3-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="67eb3-148">Alle parameterwaarden in het externe bestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="67eb3-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="67eb3-149">Als uw sjabloon een gevoelige waarde waarmee u niet opnemen in het parameterbestand bevat, die waarde toevoegen aan een sleutelkluis of dynamisch bieden alle parameter waarden inline.</span><span class="sxs-lookup"><span data-stu-id="67eb3-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="67eb3-150">Als de sjabloon een parameter met dezelfde naam als een van de parameters in de PowerShell-opdracht is bevat PowerShell biedt de parameter van de sjabloon voor de postfix **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="67eb3-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="67eb3-151">Bijvoorbeeld, een parameter genaamd **ResourceGroupName** in uw sjabloon veroorzaakt een conflict met de **ResourceGroupName** parameter in de [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="67eb3-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="67eb3-152">U wordt gevraagd om een waarde voor **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="67eb3-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="67eb3-153">In het algemeen moet u deze verwarring niet door de naam geen parameters met dezelfde naam als parameters die worden gebruikt voor implementatiebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="67eb3-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="67eb3-154">Een sjabloonimplementatie testen</span><span class="sxs-lookup"><span data-stu-id="67eb3-154">Test a template deployment</span></span>

<span data-ttu-id="67eb3-155">U kunt uw sjabloon en de parameterbestanden waarden testen zonder het distribueren van alle resources met [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="67eb3-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="67eb3-156">Als er geen fouten worden aangetroffen, wordt de opdracht is voltooid zonder reactie.</span><span class="sxs-lookup"><span data-stu-id="67eb3-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="67eb3-157">Als er een fout wordt gedetecteerd, wordt een foutbericht geretourneerd door de opdracht.</span><span class="sxs-lookup"><span data-stu-id="67eb3-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="67eb3-158">Poging om door te geven van een onjuiste waarde voor het opslagaccount SKU, resulteert bijvoorbeeld de volgende fout:</span><span class="sxs-lookup"><span data-stu-id="67eb3-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="67eb3-159">Als uw sjabloon een syntaxisfout heeft, foutmelding de opdracht een die wijzen op dat de sjabloon kan niet worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="67eb3-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="67eb3-160">Het bericht geeft de regelnummer en positie van de fout bij het parseren.</span><span class="sxs-lookup"><span data-stu-id="67eb3-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="67eb3-161">Volledige modus, gebruikt de `Mode` parameter:</span><span class="sxs-lookup"><span data-stu-id="67eb3-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="67eb3-162">Voorbeeldsjabloon</span><span class="sxs-lookup"><span data-stu-id="67eb3-162">Sample template</span></span>

<span data-ttu-id="67eb3-163">De volgende sjabloon wordt gebruikt voor de voorbeelden in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="67eb3-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="67eb3-164">Kopiëren en opslaan als een bestand met de naam storage.json.</span><span class="sxs-lookup"><span data-stu-id="67eb3-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="67eb3-165">Om te begrijpen hoe u deze sjabloon maakt, Zie [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="67eb3-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67eb3-166">Next steps</span></span>
* <span data-ttu-id="67eb3-167">De voorbeelden in dit artikel implementeren resources naar een resourcegroep in uw standaardabonnement.</span><span class="sxs-lookup"><span data-stu-id="67eb3-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="67eb3-168">Zie voor het gebruik van een ander abonnement [meerdere Azure-abonnementen beheren](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="67eb3-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="67eb3-169">Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [script voor implementatie van Resource Manager-sjabloon](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="67eb3-170">Om te begrijpen hoe parameters in de sjabloon definieert, Zie [inzicht in de structuur en de syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="67eb3-171">Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="67eb3-172">Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="67eb3-173">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="67eb3-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

