---
title: Een web-app die is gekoppeld aan een GitHub-opslagplaats implementeren | Microsoft Docs
description: Gebruik een Azure Resource Manager-sjabloon voor het implementeren van een web-app met een project van een GitHub-opslagplaats.
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="b2c20-103">Een web-app die is gekoppeld aan een GitHub-opslagplaats implementeren</span><span class="sxs-lookup"><span data-stu-id="b2c20-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="b2c20-104">In dit onderwerp leert u het maken van een Azure Resource Manager-sjabloon die u implementeert een web-app die is gekoppeld aan een project in een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b2c20-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="b2c20-105">U leert hoe om te definiëren welke bronnen worden geïmplementeerd en het definiëren van de parameters die zijn opgegeven wanneer de implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b2c20-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="b2c20-106">U kunt deze sjabloon gebruiken voor uw eigen implementaties of de sjabloon aanpassen aan uw eisen.</span><span class="sxs-lookup"><span data-stu-id="b2c20-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="b2c20-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b2c20-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b2c20-108">Zie voor de volledige sjabloon [Web App gekoppeld aan de sjabloon GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b2c20-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="b2c20-109">Wat u wilt implementeren</span><span class="sxs-lookup"><span data-stu-id="b2c20-109">What you will deploy</span></span>
<span data-ttu-id="b2c20-110">Met deze sjabloon implementeert u een web-app met de code van een project in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2c20-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="b2c20-111">Klik op de volgende knop om de implementatie automatisch uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="b2c20-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="b2c20-112">[![Implementeren in Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b2c20-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b2c20-113">Parameters</span><span class="sxs-lookup"><span data-stu-id="b2c20-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="b2c20-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="b2c20-114">repoURL</span></span>
<span data-ttu-id="b2c20-115">De URL van de GitHub-opslagplaats met het project te implementeren.</span><span class="sxs-lookup"><span data-stu-id="b2c20-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="b2c20-116">Deze parameter bevat een standaardwaarde, maar deze waarde is alleen bedoeld voor hoe u de URL opgeven voor de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b2c20-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="b2c20-117">U kunt deze waarde gebruiken bij het testen van de sjabloon, maar u wilt en geef de URL van uw eigen opslagplaats bij het werken met de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b2c20-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="b2c20-118">Filialen</span><span class="sxs-lookup"><span data-stu-id="b2c20-118">branch</span></span>
<span data-ttu-id="b2c20-119">De branche van de opslagplaats gebruiken bij het implementeren van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b2c20-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="b2c20-120">De standaardwaarde is master, maar u kunt opgeven dat de naam van elke vertakking in de opslagplaats die u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="b2c20-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="b2c20-121">Resources om te implementeren</span><span class="sxs-lookup"><span data-stu-id="b2c20-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="b2c20-122">Web-app</span><span class="sxs-lookup"><span data-stu-id="b2c20-122">Web app</span></span>
<span data-ttu-id="b2c20-123">Maakt de web-app die is gekoppeld aan het project in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2c20-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="b2c20-124">U de naam van de web-app via de **siteName** parameter en de locatie van de web-app via de **siteLocation** parameter.</span><span class="sxs-lookup"><span data-stu-id="b2c20-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="b2c20-125">In de **dependsOn** element, de sjabloon definieert de web-app als afhankelijk van de service die als host fungeert voor plan.</span><span class="sxs-lookup"><span data-stu-id="b2c20-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="b2c20-126">Omdat dit afhankelijk van het hosting plan is, wordt de web-app niet gemaakt totdat het hosting plan is voltooid, wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b2c20-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="b2c20-127">De **dependsOn** element wordt alleen gebruikt om op te geven van de implementatievolgorde.</span><span class="sxs-lookup"><span data-stu-id="b2c20-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="b2c20-128">Als u de web-app als afhankelijk van de hosting-planning niet inschakelt, Azure Resource Doorberekeningsfuncties zal proberen te maken van beide resources op hetzelfde moment en u kunt een fout kan optreden als de web-app is gemaakt voordat het hosting plan.</span><span class="sxs-lookup"><span data-stu-id="b2c20-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="b2c20-129">De web-app heeft ook een onderliggende resource die is gedefinieerd in **resources** hieronder.</span><span class="sxs-lookup"><span data-stu-id="b2c20-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="b2c20-130">Deze onderliggende resource definieert bron voor het project met de web-app wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b2c20-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="b2c20-131">In deze sjabloon is broncodebeheer gekoppeld aan een bepaalde GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b2c20-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="b2c20-132">De GitHub-opslagplaats is gedefinieerd met de code **'RepoUrl': 'https://github.com/davidebbo-test/Mvc52Application.git'** u mogelijk harde code de URL van de opslagplaats wanneer u maken van een sjabloon die herhaaldelijk een project implementeert wilt terwijl slechts het minimum aantal parameters.</span><span class="sxs-lookup"><span data-stu-id="b2c20-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="b2c20-133">In plaats van hard-coding van de URL van de opslagplaats, kunt u een parameter voor de URL van de opslagplaats toevoegen en gebruiken van die waarde voor de **RepoUrl** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="b2c20-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="b2c20-134">Opdrachten om implementatie uit te voeren</span><span class="sxs-lookup"><span data-stu-id="b2c20-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b2c20-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2c20-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="b2c20-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b2c20-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="b2c20-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b2c20-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="b2c20-138">Zie voor de inhoud van de parameters-JSON-bestand, [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="b2c20-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

