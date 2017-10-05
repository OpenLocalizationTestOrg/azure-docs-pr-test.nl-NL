---
title: Sjablonen voor Azure-implementatie koppelen | Microsoft Docs
description: Beschrijft hoe gekoppelde sjablonen in een Azure Resource Manager-sjabloon gebruiken om een sjabloonoplossing modulaire te maken. Laat zien hoe parameterwaarden doorgeven, geeft u een parameterbestand en dynamisch gemaakte URL's.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="2c528-104">Gekoppelde sjablonen gebruiken bij het implementeren van Azure-resources</span><span class="sxs-lookup"><span data-stu-id="2c528-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="2c528-105">Uit binnen een Azure Resource Manager-sjabloon, kunt u koppelen aan een andere sjabloon waarmee u uw implementatie in een set afbreken gericht, doel-specifieke sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2c528-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="2c528-106">Net als bij een toepassing in verschillende codeklassen ontleedt, biedt afbreken voordelen wat betreft testen, hergebruiken en leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2c528-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="2c528-107">U kunt de parameters van een sjabloon van de belangrijkste doorgeven aan een gekoppelde sjabloon en deze parameters rechtstreeks kunnen toewijzen aan parameters of variabelen die worden weergegeven door de aanroepende sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c528-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="2c528-108">De gekoppelde sjabloon kunt ook een uitvoervariabele doorgeven terug naar de bronsjabloon inschakelen van een wederzijdse gegevensuitwisseling tussen de sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2c528-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="2c528-109">Koppelen aan een sjabloon</span><span class="sxs-lookup"><span data-stu-id="2c528-109">Linking to a template</span></span>
<span data-ttu-id="2c528-110">U maakt een koppeling tussen twee sjablonen door een implementatie-bron in de belangrijkste sjabloon die naar de gekoppelde sjabloon verwijst toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="2c528-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="2c528-111">U stelt de **templateLink** eigenschap met de URI van de gekoppelde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c528-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="2c528-112">U kunt parameterwaarden kan opgeven voor de gekoppelde sjabloon rechtstreeks in uw sjabloon of in een parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="2c528-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="2c528-113">Het volgende voorbeeld wordt de **parameters** eigenschap rechtstreeks een parameterwaarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="2c528-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="2c528-114">Net als andere brontypen, kunt u de afhankelijkheden tussen de gekoppelde sjabloon en andere resources instellen.</span><span class="sxs-lookup"><span data-stu-id="2c528-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="2c528-115">Daarom als voor andere bronnen vereist een waarde voor de uitvoer van de gekoppelde sjabloon, kunt u ervoor dat de gekoppelde sjabloon voordat deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2c528-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="2c528-116">Of als de gekoppelde sjabloon is afhankelijk van andere bronnen, kunt u ervoor zorgen dat andere resources worden geïmplementeerd voordat u de gekoppelde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c528-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="2c528-117">U kunt een waarde wordt opgehaald uit een gekoppelde sjabloon met de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="2c528-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="2c528-118">De Resource Manager-service moet toegang kunnen krijgen tot de gekoppelde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c528-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="2c528-119">U kunt een lokaal bestand of een bestand dat is alleen beschikbaar op uw lokale netwerk voor de gekoppelde sjabloon opgeven.</span><span class="sxs-lookup"><span data-stu-id="2c528-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="2c528-120">U kunt alleen een URI-waarde die een bevat opgeven **http** of **https**.</span><span class="sxs-lookup"><span data-stu-id="2c528-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="2c528-121">Een mogelijkheid is het plaatsen van de gekoppelde sjabloon in een opslagaccount en de URI gebruiken voor het item, zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2c528-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="2c528-122">Hoewel de gekoppelde sjabloon moet extern beschikbaar zijn, hoeft deze niet algemeen beschikbaar is voor het publiek.</span><span class="sxs-lookup"><span data-stu-id="2c528-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="2c528-123">U kunt uw sjabloon toevoegen aan een persoonlijke opslagaccount die toegankelijk is voor alleen de eigenaar van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2c528-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="2c528-124">Vervolgens maakt u een shared access signature (SAS)-token om toegang te maken tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="2c528-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="2c528-125">U toevoegen deze SAS-token aan de URI voor de gekoppelde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c528-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="2c528-126">Zie voor stappen over het instellen van een sjabloon in een opslagaccount en een SAS-token te genereren, [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md) of [resources met Resource Manager-sjablonen te implementeren en Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2c528-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="2c528-127">Het volgende voorbeeld ziet een bovenliggende-sjabloon die is gekoppeld aan een andere sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c528-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="2c528-128">De gekoppelde sjabloon wordt geopend met een SAS-token dat is doorgegeven als parameter.</span><span class="sxs-lookup"><span data-stu-id="2c528-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="2c528-129">Hoewel het token is doorgegeven als een beveiligde tekenreeks, wordt de URI van de gekoppelde sjabloon, met inbegrip van de SAS-token in de implementatiebewerkingen vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="2c528-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="2c528-130">Om te beperken van blootstelling, instellen dat een verlopen voor de token.</span><span class="sxs-lookup"><span data-stu-id="2c528-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="2c528-131">Resource Manager verwerkt elke gekoppelde sjabloon als een afzonderlijke implementatie.</span><span class="sxs-lookup"><span data-stu-id="2c528-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="2c528-132">In de geschiedenis van de implementatie voor de resourcegroep ziet u afzonderlijke implementaties voor de bovenliggende en geneste sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2c528-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![implementatiegeschiedenis](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="2c528-134">Koppelen aan een parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="2c528-134">Linking to a parameter file</span></span>
<span data-ttu-id="2c528-135">Het volgende voorbeeld wordt de **parametersLink** eigenschap in op de koppeling naar een parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="2c528-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="2c528-136">De URI-waarde voor het gekoppelde parameterbestand mag geen een lokaal bestand, en vergezeld gaan van een **http** of **https**.</span><span class="sxs-lookup"><span data-stu-id="2c528-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="2c528-137">De parameter-bestand kan ook worden beperkt tot toegang via een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="2c528-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="2c528-138">Gebruik van variabelen sjablonen koppelen</span><span class="sxs-lookup"><span data-stu-id="2c528-138">Using variables to link templates</span></span>
<span data-ttu-id="2c528-139">De voorgaande voorbeelden toonden vastgelegde URL waarden voor de sjabloon-koppelingen.</span><span class="sxs-lookup"><span data-stu-id="2c528-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="2c528-140">Deze methode werkt mogelijk voor een eenvoudige sjabloon, maar werkt niet goed bij het werken met een groot aantal modulaire sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2c528-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="2c528-141">U kunt in plaats daarvan een statische variabele waarin een basis-URL voor de belangrijkste sjabloon maken en vervolgens de URL's voor de gekoppelde sjablonen van deze basis-URL dynamisch maken.</span><span class="sxs-lookup"><span data-stu-id="2c528-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="2c528-142">Het voordeel van deze benadering is kunt u gemakkelijk verplaatsen of de sjabloon vertakken omdat u alleen hoeft te wijzigen van de statische variabele in de belangrijkste sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c528-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="2c528-143">De belangrijkste sjabloon het juiste URI's in de sjabloon opgesplitste is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="2c528-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="2c528-144">Het volgende voorbeeld laat zien hoe u een basis-URL om te maken van twee URL's voor de gekoppelde sjablonen (**sharedTemplateUrl** en **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="2c528-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="2c528-145">U kunt ook [deployment()](resource-group-template-functions-deployment.md#deployment) ophalen van de basis-URL voor de huidige sjabloon en gebruik die voor de URL voor andere sjablonen op dezelfde locatie bevinden.</span><span class="sxs-lookup"><span data-stu-id="2c528-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="2c528-146">Deze methode is handig als de locatie van uw sjabloon (mogelijk vanwege versioning wijzigt) of u wilt voorkomen dat URL's in het sjabloonbestand hard coderen.</span><span class="sxs-lookup"><span data-stu-id="2c528-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="2c528-147">Compleet voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2c528-147">Complete example</span></span>
<span data-ttu-id="2c528-148">Het volgende voorbeeld sjablonen weergeven een vereenvoudigde rangschikking van gekoppelde sjablonen ter illustratie van enkele concepten uitgelegd die in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2c528-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="2c528-149">Wordt ervan uitgegaan dat de sjablonen zijn toegevoegd aan de container in een opslagaccount met openbare toegang uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2c528-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="2c528-150">De gekoppelde sjabloon retourneert een waarde naar de belangrijkste sjabloon in de **levert** sectie.</span><span class="sxs-lookup"><span data-stu-id="2c528-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="2c528-151">De **parent.json** bestand bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="2c528-151">The **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="2c528-152">De **helloworld.json** bestand bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="2c528-152">The **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="2c528-153">In PowerShell kunt u een token verkrijgen voor de container en implementeren van de sjablonen met:</span><span class="sxs-lookup"><span data-stu-id="2c528-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="2c528-154">In Azure CLI 2.0, moet u een token verkrijgen voor de container en implementeren van de sjablonen met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="2c528-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="2c528-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c528-155">Next steps</span></span>
* <span data-ttu-id="2c528-156">Zie voor meer informatie over het definiëren van de implementatievolgorde voor uw resources, [afhankelijkheden definiëren in Azure Resource Manager-sjablonen](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="2c528-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="2c528-157">Zie voor informatie over het definiëren van één resource maar veel exemplaren van het maken, [meerdere exemplaren van resources in Azure Resource Manager maken](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="2c528-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

