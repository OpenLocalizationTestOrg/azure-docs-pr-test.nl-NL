---
title: aaaDeploy een web-app die is gekoppeld tooa GitHub-opslagplaats | Microsoft Docs
description: Gebruik een Azure Resource Manager-sjabloon toodeploy een web-app met een project van een GitHub-opslagplaats.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="463d9-103">Een web-app gekoppelde tooa GitHub-opslagplaats implementeren</span><span class="sxs-lookup"><span data-stu-id="463d9-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="463d9-104">In dit onderwerp leert u hoe toocreate een Azure Resource Manager-sjabloon die u implementeert een web-app die is gekoppeld tooa-project in een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="463d9-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="463d9-105">U leert hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="463d9-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="463d9-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="463d9-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="463d9-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="463d9-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="463d9-108">Zie voor de volledige sjabloon hello, [Web App gekoppelde tooGitHub sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="463d9-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="463d9-109">Wat u wilt implementeren</span><span class="sxs-lookup"><span data-stu-id="463d9-109">What you will deploy</span></span>
<span data-ttu-id="463d9-110">Met deze sjabloon implementeert u een web-app met Hallo-code van een project in GitHub.</span><span class="sxs-lookup"><span data-stu-id="463d9-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="463d9-111">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="463d9-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="463d9-112">[![TooAzure implementeren](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="463d9-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="463d9-113">Parameters</span><span class="sxs-lookup"><span data-stu-id="463d9-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="463d9-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="463d9-114">repoURL</span></span>
<span data-ttu-id="463d9-115">Hallo-URL voor de GitHub-opslagplaats die Hallo project toodeploy bevat.</span><span class="sxs-lookup"><span data-stu-id="463d9-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="463d9-116">Deze parameter bevat een standaardwaarde, maar deze waarde is alleen bedoeld tooshow u hoe tooprovide URL Hallo voor opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="463d9-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="463d9-117">U kunt deze waarde gebruiken bij het testen Hallo-sjabloon, maar u zult tooprovide Hallo URL uw eigen opslagplaats bij het werken met Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="463d9-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="463d9-118">Filialen</span><span class="sxs-lookup"><span data-stu-id="463d9-118">branch</span></span>
<span data-ttu-id="463d9-119">Hallo-vertakking van Hallo opslagplaats toouse bij het implementeren van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="463d9-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="463d9-120">de standaardwaarde Hallo master is, maar u Hallo-naam van elke vertakking in Hallo opslagplaats kunt opgeven dat u wenst dat toodeploy.</span><span class="sxs-lookup"><span data-stu-id="463d9-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="463d9-121">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="463d9-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="463d9-122">Web-app</span><span class="sxs-lookup"><span data-stu-id="463d9-122">Web app</span></span>
<span data-ttu-id="463d9-123">Hiermee maakt u Hallo web-app die is gekoppeld toohello-project in GitHub.</span><span class="sxs-lookup"><span data-stu-id="463d9-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="463d9-124">U Hallo-naam van de web-app via Hallo Hallo **siteName** parameter en locatie van web-app via Hallo HALLO hallo **siteLocation** parameter.</span><span class="sxs-lookup"><span data-stu-id="463d9-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="463d9-125">In Hallo **dependsOn** element Hallo sjabloon definieert Hallo web-app als afhankelijk van Hallo-service die als host fungeert voor plan.</span><span class="sxs-lookup"><span data-stu-id="463d9-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="463d9-126">Omdat dit afhankelijk van Hallo plan hosten is, is niet Hallo web-app gemaakt tot Hallo die als host fungeert voor plan is voltooid, wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="463d9-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="463d9-127">Hallo **dependsOn** element wordt alleen gebruikt toospecify implementatievolgorde.</span><span class="sxs-lookup"><span data-stu-id="463d9-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="463d9-128">Als u web-app als afhankelijk hosting plan Hallo Hallo niet inschakelt, probeert Azure Resource Doorberekeningsfuncties toocreate beide resources op Hallo dezelfde tijd en u een foutbericht ontvangen als Hallo web-app is gemaakt voordat Hallo hosting-plan.</span><span class="sxs-lookup"><span data-stu-id="463d9-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="463d9-129">Hallo-web-app heeft ook een onderliggende resource die is gedefinieerd in **resources** hieronder.</span><span class="sxs-lookup"><span data-stu-id="463d9-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="463d9-130">Deze onderliggende resource definieert broncodebeheer voor Hallo-project met Hallo web-app wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="463d9-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="463d9-131">In deze sjabloon is Hallo broncodebeheer gekoppelde tooa bepaalde GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="463d9-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="463d9-132">Hallo GitHub-opslagplaats is gedefinieerd door code Hallo **'RepoUrl': 'https://github.com/davidebbo-test/Mvc52Application.git'** u URL van de opslagplaats vastleggen Hallo mogelijk als u wilt dat toocreate een sjabloon die herhaaldelijk implementeert een één project tijdens het minimum aantal parameters Hallo vereisen.</span><span class="sxs-lookup"><span data-stu-id="463d9-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="463d9-133">In plaats van hard-coding van Hallo URL opslagplaats, kunt u een parameter voor de URL van de opslagplaats Hallo toevoegen en gebruiken van die waarde voor Hallo **RepoUrl** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="463d9-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="463d9-134">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="463d9-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="463d9-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="463d9-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="463d9-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="463d9-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="463d9-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="463d9-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="463d9-138">Zie voor de inhoud van Hallo parameters JSON-bestand, [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="463d9-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

