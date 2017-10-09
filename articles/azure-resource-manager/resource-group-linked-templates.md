---
title: sjablonen voor Azure-implementatie aaaLink | Microsoft Docs
description: Hierin wordt beschreven hoe toouse gekoppeld sjablonen in een Azure Resource Manager-sjabloon toocreate een sjabloonoplossing modulaire. Ziet u hoe de waarden van de parameters toopass, geeft een parameterbestand en URL's dynamisch gemaakt.
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
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="e13c7-104">Gekoppelde sjablonen gebruiken bij het implementeren van Azure-resources</span><span class="sxs-lookup"><span data-stu-id="e13c7-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="e13c7-105">Uit binnen een Azure Resource Manager-sjabloon kunt u koppelen tooanother sjabloon waarmee u toodecompose uw implementatie in een set van gerichte, doel-specifieke sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="e13c7-106">Net als bij een toepassing in verschillende codeklassen ontleedt, biedt afbreken voordelen wat betreft testen, hergebruiken en leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="e13c7-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="e13c7-107">U kunt parameters doorgeven van een sjabloon belangrijkste tooa gekoppelde sjabloon en deze parameters kunnen rechtstreeks toewijzen tooparameters of variabelen die worden weergegeven door Hallo aanroepen van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e13c7-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="e13c7-108">Hallo gekoppelde sjabloon kunt ook de bronsjabloon voor een uitvoer variabele back toohello, waardoor een wederzijdse gegevensuitwisseling tussen sjablonen doorgeven.</span><span class="sxs-lookup"><span data-stu-id="e13c7-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="e13c7-109">Sjabloon tooa koppelen</span><span class="sxs-lookup"><span data-stu-id="e13c7-109">Linking tooa template</span></span>
<span data-ttu-id="e13c7-110">U maakt een koppeling tussen twee sjablonen door toe te voegen een implementatie-bron in de belangrijkste sjabloon Hallo die punten toohello gekoppelde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e13c7-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="e13c7-111">Instellen van Hallo **templateLink** eigenschap toohello URI van de gekoppelde Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e13c7-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="e13c7-112">U kunt parameterwaarden kan opgeven voor de gekoppelde sjabloon Hallo rechtstreeks in uw sjabloon of in een parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="e13c7-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="e13c7-113">Hallo volgende voorbeeld wordt Hallo **parameters** eigenschap toospecify rechtstreeks een parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="e13c7-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

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

<span data-ttu-id="e13c7-114">Net als andere brontypen, kunt u de afhankelijkheden tussen de gekoppelde sjabloon Hallo en andere resources instellen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="e13c7-115">Daarom als voor andere bronnen vereist een waarde voor de uitvoer van de gekoppelde sjabloon hello, kunt u zorgen Hallo gekoppelde sjabloon voordat deze wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e13c7-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="e13c7-116">Of als de gekoppelde sjabloon Hallo is afhankelijk van andere bronnen, kunt u ervoor zorgen dat andere resources worden geïmplementeerd voordat Hallo gekoppelde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e13c7-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="e13c7-117">U kunt een waarde ophalen uit een gekoppelde sjabloon Hello de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="e13c7-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="e13c7-118">Hallo Resource Manager-service moet kunnen tooaccess Hallo gekoppelde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e13c7-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="e13c7-119">U kunt een lokaal bestand of een bestand dat is alleen beschikbaar op uw lokale netwerk voor de gekoppelde sjabloon Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="e13c7-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="e13c7-120">U kunt alleen een URI-waarde die een bevat opgeven **http** of **https**.</span><span class="sxs-lookup"><span data-stu-id="e13c7-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="e13c7-121">Een mogelijkheid is de gekoppelde sjabloon in een opslagaccount en gebruik URI voor het item, zoals weergegeven in het volgende voorbeeld Hallo Hallo tooplace:</span><span class="sxs-lookup"><span data-stu-id="e13c7-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="e13c7-122">Hoewel Hallo gekoppelde sjabloon moet extern beschikbaar zijn, hoeft deze niet toobe algemeen beschikbaar toohello openbaar.</span><span class="sxs-lookup"><span data-stu-id="e13c7-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="e13c7-123">U kunt uw sjabloon tooa persoonlijke storage-account dat is eigenaar van het opslagaccount Hallo toegankelijk tooonly toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="e13c7-124">Vervolgens maakt u een shared access signature (SAS)-token tooenable toegang tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e13c7-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="e13c7-125">U toevoegen deze SAS-token toohello URI voor de gekoppelde sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="e13c7-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="e13c7-126">Zie voor stappen over het instellen van een sjabloon in een opslagaccount en een SAS-token te genereren, [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md) of [resources met Resource Manager-sjablonen te implementeren en Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e13c7-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="e13c7-127">Hallo volgende voorbeeld ziet u een sjabloon voor bovenliggend die koppelingen tooanother sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e13c7-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="e13c7-128">Hallo gekoppelde sjabloon wordt geopend met een SAS-token dat is doorgegeven als parameter.</span><span class="sxs-lookup"><span data-stu-id="e13c7-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="e13c7-129">Hoewel Hallo-token is doorgegeven als een beveiligde tekenreeks, wordt hello URI van Hallo gekoppelde sjabloon, Hallo SAS-token, inclusief vastgelegd op Hallo implementatiebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="e13c7-130">toolimit blootstelling, instellen dat een verlopen voor Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="e13c7-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="e13c7-131">Resource Manager verwerkt elke gekoppelde sjabloon als een afzonderlijke implementatie.</span><span class="sxs-lookup"><span data-stu-id="e13c7-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="e13c7-132">In de geschiedenis van Hallo implementatie voor de resourcegroep hello ziet u afzonderlijke implementaties voor de bovenliggende Hallo en geneste sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![implementatiegeschiedenis](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="e13c7-134">Het parameterbestand tooa koppelen</span><span class="sxs-lookup"><span data-stu-id="e13c7-134">Linking tooa parameter file</span></span>
<span data-ttu-id="e13c7-135">Hallo volgende voorbeeld wordt met Hallo **parametersLink** eigenschap toolink tooa parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="e13c7-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

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

<span data-ttu-id="e13c7-136">Hallo URI waarde Hallo gekoppelde parameterbestand mag geen een lokaal bestand, en vergezeld gaan van een **http** of **https**.</span><span class="sxs-lookup"><span data-stu-id="e13c7-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="e13c7-137">Hallo parameterbestand kan ook worden beperkt tooaccess via een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="e13c7-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="e13c7-138">Met behulp van variabelen toolink sjablonen</span><span class="sxs-lookup"><span data-stu-id="e13c7-138">Using variables toolink templates</span></span>
<span data-ttu-id="e13c7-139">Hallo voorgaande voorbeelden toonden vastgelegde URL waarden voor Hallo sjabloon koppelingen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="e13c7-140">Deze methode werkt mogelijk voor een eenvoudige sjabloon, maar werkt niet goed bij het werken met een groot aantal modulaire sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="e13c7-141">U kunt in plaats daarvan maken van een statische variabele die een basis-URL voor de belangrijkste sjabloon Hallo opslaat en URL's dynamisch voor Hallo gekoppelde sjablonen van deze basis-URL te maken.</span><span class="sxs-lookup"><span data-stu-id="e13c7-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="e13c7-142">Hallo voordeel van deze benadering is kunt u gemakkelijk verplaatsen of fork Hallo-sjabloon, omdat u alleen toochange Hallo statische variabele in de belangrijkste sjabloon Hallo nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="e13c7-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="e13c7-143">de belangrijkste sjabloon Hallo Hallo juiste dat URI 's in de gehele Hallo ontleed sjabloon is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="e13c7-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="e13c7-144">Hallo volgende voorbeeld laat zien hoe een base URL toocreate toouse twee URL's voor gekoppeld sjablonen (**sharedTemplateUrl** en **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="e13c7-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="e13c7-145">U kunt ook [deployment()](resource-group-template-functions-deployment.md#deployment) tooget basis-URL voor de huidige sjabloon Hallo Hallo en die tooget Hallo-URL gebruiken voor andere sjablonen in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="e13c7-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="e13c7-146">Deze methode is handig als uw sjabloonlocatie wijzigt (mogelijk vanwege tooversioning) of het gewenste tooavoid harde-URL's in het sjabloonbestand Hallo coderen.</span><span class="sxs-lookup"><span data-stu-id="e13c7-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="e13c7-147">Compleet voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e13c7-147">Complete example</span></span>
<span data-ttu-id="e13c7-148">Hallo voorbeeld sjablonen na weergeven een vereenvoudigde rangschikking van gekoppelde sjablonen tooillustrate diverse Hallo concepten in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="e13c7-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="e13c7-149">Er wordt vanuit gegaan Hallo sjablonen toohello dezelfde container in een opslagaccount met openbare toegang uitgeschakeld zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e13c7-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="e13c7-150">Hallo gekoppelde sjabloon wordt een waarde back toohello belangrijkste sjabloon doorgegeven in Hallo **levert** sectie.</span><span class="sxs-lookup"><span data-stu-id="e13c7-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="e13c7-151">Hallo **parent.json** bestand bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="e13c7-151">hello **parent.json** file consists of:</span></span>

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

<span data-ttu-id="e13c7-152">Hallo **helloworld.json** bestand bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="e13c7-152">hello **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="e13c7-153">In PowerShell moet u een token voor de container Hallo ophalen en implementeren van Hallo sjablonen met:</span><span class="sxs-lookup"><span data-stu-id="e13c7-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="e13c7-154">In Azure CLI 2.0 ophalen van een token voor Hallo-container en Hallo sjablonen met Hallo na de code implementeren:</span><span class="sxs-lookup"><span data-stu-id="e13c7-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e13c7-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e13c7-155">Next steps</span></span>
* <span data-ttu-id="e13c7-156">Zie toolearn over Hallo Hallo implementatievolgorde voor uw resources definiëren [afhankelijkheden definiëren in Azure Resource Manager-sjablonen](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="e13c7-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="e13c7-157">toolearn hoe toodefine één resource maken maar veel exemplaren ervan raadpleegt [meerdere exemplaren van resources in Azure Resource Manager maken](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="e13c7-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

