---
title: aaaSpecifying een Node.js-versie
description: Meer informatie over hoe toospecify Hallo versie van Node.js gebruikt door Azure websites en Cloudservices
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="bd415-103">Een Node.js-versie opgeven in een Azure-toepassing</span><span class="sxs-lookup"><span data-stu-id="bd415-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="bd415-104">Bij het hosten van een Node.js-toepassing, kunt u tooensure dat uw toepassing gebruikmaakt van een specifieke versie van Node.js.</span><span class="sxs-lookup"><span data-stu-id="bd415-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="bd415-105">Er zijn verschillende manieren tooaccomplish dit voor toepassingen die worden gehost op Azure.</span><span class="sxs-lookup"><span data-stu-id="bd415-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="bd415-106">Standaardversies</span><span class="sxs-lookup"><span data-stu-id="bd415-106">Default versions</span></span>
<span data-ttu-id="bd415-107">Hallo Node.js versies is verstrekt door Azure worden voortdurend bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="bd415-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="bd415-108">Tenzij anders vermeld, standaard-versie die is opgegeven in Hallo Hallo `WEBSITE_NODE_DEFAULT_VERSION` omgevingsvariabele wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bd415-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="bd415-109">toooverride deze standaardwaarde, Hallo Volg de stappen in de volgende secties van dit artikel</span><span class="sxs-lookup"><span data-stu-id="bd415-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="bd415-110">Als u uw toepassing in een Azure Cloud Service (web- of worker-rol) host, en deze Hallo eerste keer dat u de toepassing hello hebt geïmplementeerd, Azure toouse wordt geprobeerd dezelfde versie van Node.js Hallo als u op uw ontwikkelingsomgeving hebt geïnstalleerd als deze komt overeen met een van Hallo standaardversies beschikbaar zijn op Azure.</span><span class="sxs-lookup"><span data-stu-id="bd415-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="bd415-111">Versiebeheer voor onderdelen met package.json</span><span class="sxs-lookup"><span data-stu-id="bd415-111">Versioning with package.json</span></span>
<span data-ttu-id="bd415-112">Kunt u Hallo-versie van Node.js toobe gebruikt door toe te voegen Hallo na tooyour **package.json** bestand:</span><span class="sxs-lookup"><span data-stu-id="bd415-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="bd415-113">Waar *versie* Hallo specifieke versie nummer toouse is.</span><span class="sxs-lookup"><span data-stu-id="bd415-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="bd415-114">Kunt u complexere voorwaarden voor de versie, zoals:</span><span class="sxs-lookup"><span data-stu-id="bd415-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="bd415-115">Aangezien 0.6.22 niet een van de Hallo versies beschikbaar zijn in de hostomgeving hello is, hello hoogste versie van Hallo 0,8 reeks die beschikbaar worden gebruikt in plaats daarvan - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="bd415-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="bd415-116">Versiebeheer Websites met App-instellingen</span><span class="sxs-lookup"><span data-stu-id="bd415-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="bd415-117">Als u de toepassing hello in een Website host, kunt u instellen Hallo omgevingsvariabele **WEBSITE_NODE_DEFAULT_VERSION** toohello gewenste versie.</span><span class="sxs-lookup"><span data-stu-id="bd415-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="bd415-118">Versiebeheer Cloudservices met PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd415-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="bd415-119">Als u als host voor Hallo-toepassing in een Cloudservice optreden en Hallo-toepassing met Azure PowerShell implementeert, kunt u de standaardversie van Node.js Hallo overschrijven met behulp van Hallo **Set AzureServiceProjectRole** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd415-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="bd415-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="bd415-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="bd415-121">Opmerking Hallo parameters in Hallo hierboven instructie zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="bd415-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="bd415-122">U kunt controleren of de juiste versie Hallo van Node.js is geselecteerd door te controleren Hallo **engines** eigenschap in uw rol **package.json**.</span><span class="sxs-lookup"><span data-stu-id="bd415-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="bd415-123">U kunt ook Hallo **Get-AzureServiceProjectRoleRuntime** tooretrieve een lijst met Node.js versies beschikbaar voor toepassingen die als Cloudservice wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="bd415-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="bd415-124">Controleer altijd of Hallo-versie van Node.js afhankelijk van uw project zich in deze lijst.</span><span class="sxs-lookup"><span data-stu-id="bd415-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="bd415-125">Met behulp van een aangepaste versie met Azure Websites</span><span class="sxs-lookup"><span data-stu-id="bd415-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="bd415-126">Hoewel Azure verschillende standaardversies zijn van Node.js biedt, kunt u toouse een versie die wordt standaard niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bd415-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="bd415-127">Als uw toepassing als een Azure-Website wordt gehost, u kunt dit doen met behulp van Hallo **iisnode.yml** bestand.</span><span class="sxs-lookup"><span data-stu-id="bd415-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="bd415-128">Hallo doorlopen volgende stappen Hallo proces van het gebruik van een aangepaste versie van Node.Js met een Azure-Website:</span><span class="sxs-lookup"><span data-stu-id="bd415-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="bd415-129">Een nieuwe map maken en maak vervolgens een **server.js** bestand binnen Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="bd415-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="bd415-130">Hallo **server.js** -bestand moet Hallo volgende bevatten:</span><span class="sxs-lookup"><span data-stu-id="bd415-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="bd415-131">Hallo Node.js-versie wordt gebruikt wanneer u Hallo website bladert wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bd415-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="bd415-132">Maak een nieuwe Website en de opmerking Hallo-naam van Hallo-site.</span><span class="sxs-lookup"><span data-stu-id="bd415-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="bd415-133">Hallo volgende wordt bijvoorbeeld Hallo [Azure-opdrachtregelprogramma's] toocreate een nieuwe Azure-Website met de naam **MijnWebsite**, en schakel vervolgens een Git-opslagplaats voor Hallo-website.</span><span class="sxs-lookup"><span data-stu-id="bd415-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="bd415-134">Maak een nieuwe map met de naam **bin** als een onderliggend element van Hallo map waarin zich Hallo **server.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="bd415-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="bd415-135">Downloaden van de specifieke versie van Hallo **node.exe** (versie van Windows hello) dat u wenst dat toouse met uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bd415-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="bd415-136">Bijvoorbeeld, Hallo na gebruikt **curl** toodownload versie 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="bd415-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="bd415-137">Hallo opslaan **node.exe** -bestand in Hallo **bin** map die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bd415-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="bd415-138">Maakt een **iisnode.yml** bestanden per Hallo dezelfde map als Hallo **server.js** bestand en voeg vervolgens Hallo inhoud toohello na **iisnode.yml** bestand:</span><span class="sxs-lookup"><span data-stu-id="bd415-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="bd415-139">Dit pad is waar hello **node.exe** bestand in uw project worden geplaatst wanneer u uw toepassing toohello Azure-Website hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="bd415-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="bd415-140">Uw toepassing publiceren.</span><span class="sxs-lookup"><span data-stu-id="bd415-140">Publish your application.</span></span> <span data-ttu-id="bd415-141">Bijvoorbeeld: nadat ik een nieuwe website eerder met de Hallo--git parameter gemaakt, hello volgende opdrachten wordt toevoegen Hallo toepassing bestanden toomy lokale Git-opslagplaats en push ze toohello website opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="bd415-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="bd415-142">Nadat de toepassing hello is gepubliceerd, opent u Hallo-website in een browser.</span><span class="sxs-lookup"><span data-stu-id="bd415-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="bd415-143">U ziet een bericht weergegeven ' Hallo van Azure actief knooppunt versie: v0.8.1 '.</span><span class="sxs-lookup"><span data-stu-id="bd415-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd415-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd415-144">Next Steps</span></span>
<span data-ttu-id="bd415-145">Nu u weet hoe toospecify Hallo versie van Node.js wordt gebruikt door uw toepassing, kunt u nagaan hoe te[werken met modules], [bouwen en implementeren van een Node.js-website](app-service-web/app-service-web-get-started-nodejs.md), en [hoe toouse hello Azure Opdrachtregelprogramma's voor Mac en Linux].</span><span class="sxs-lookup"><span data-stu-id="bd415-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="bd415-146">Zie voor meer informatie, Hallo [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="bd415-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[hoe toouse hello Azure Opdrachtregelprogramma's voor Mac en Linux]:cli-install-nodejs.md
[Azure-opdrachtregelprogramma's]:cli-install-nodejs.md
[werken met modules]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
