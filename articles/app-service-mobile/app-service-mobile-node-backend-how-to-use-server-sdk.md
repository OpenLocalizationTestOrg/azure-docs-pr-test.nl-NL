---
title: aaaHow toowork met back-endserver voor Hallo Node.js SDK voor Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toowork met back-endserver voor Node.js SDK Hallo voor Azure App Service Mobile Apps.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="d016d-103">Hoe toouse hello Azure Mobile Apps Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="d016d-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="d016d-104">Dit artikel vindt u gedetailleerde informatie over en voorbeelden ziet u hoe toowork met een back-end voor Node.js in Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="d016d-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="d016d-105"><a name="Introduction"></a>Inleiding</span><span class="sxs-lookup"><span data-stu-id="d016d-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="d016d-106">Azure App Service Mobile Apps biedt Hallo mogelijkheid tooadd mobile-geoptimaliseerde gegevenstoegang Web API tooa webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d016d-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="d016d-107">Hello Azure App Service Mobile Apps SDK is beschikbaar voor ASP.NET- en Node.js-webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="d016d-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="d016d-108">Hallo SDK biedt Hallo volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="d016d-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="d016d-109">Tabelbewerkingen (lezen, Insert, Update, Delete) voor toegang tot gegevens</span><span class="sxs-lookup"><span data-stu-id="d016d-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="d016d-110">Aangepaste API-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="d016d-110">Custom API operations</span></span>

<span data-ttu-id="d016d-111">Beide bewerkingen kunnen worden gebruikt voor verificatie binnen alle id-providers toegestaan door Azure App Service, met inbegrip van sociale id-providers zoals Facebook, Twitter, Google en Microsoft, evenals Azure Active Directory voor de identiteit van de onderneming.</span><span class="sxs-lookup"><span data-stu-id="d016d-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="d016d-112">U vindt voorbeelden voor elk gebruiksvoorbeeld in Hallo [directory voorbeelden op GitHub].</span><span class="sxs-lookup"><span data-stu-id="d016d-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d016d-113">Ondersteunde Platforms</span><span class="sxs-lookup"><span data-stu-id="d016d-113">Supported Platforms</span></span>
<span data-ttu-id="d016d-114">Hello Azure Mobile Apps knooppunt SDK biedt ondersteuning voor Hallo die huidige TNS bij de release van knooppunt en later.</span><span class="sxs-lookup"><span data-stu-id="d016d-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="d016d-115">Op moment van schrijven is het meest recente TNS versie Hallo knooppunt v4.5.0.</span><span class="sxs-lookup"><span data-stu-id="d016d-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="d016d-116">Andere versies van knooppunt werkt, maar worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d016d-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="d016d-117">Hello Azure Mobile Apps knooppunt SDK ondersteunt twee databasestuurprogramma - hello knooppunt mssql-stuurprogramma ondersteunt SQL Azure en lokale exemplaren van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d016d-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="d016d-118">Hallo sqlite3 stuurprogramma ondersteunt SQLite-databases in één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d016d-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="d016d-119"><a name="howto-cmdline-basicapp"></a>Procedure: een eenvoudige Node.js back-end met Hallo opdrachtregel maken</span><span class="sxs-lookup"><span data-stu-id="d016d-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="d016d-120">Elke back-end van Azure App Service Mobile App Node.js wordt gestart als een toepassing ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="d016d-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="d016d-121">ExpressJS is Hallo meest populaire web service framework beschikbaar voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="d016d-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="d016d-122">U kunt een eenvoudige maken [Express] toepassing als volgt:</span><span class="sxs-lookup"><span data-stu-id="d016d-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="d016d-123">Maak een map voor uw project in een opdracht of een PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="d016d-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="d016d-124">Pakketstructuur van npm init tooinitialize Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="d016d-125">Hallo npm init-opdracht wordt u gevraagd een reeks vragen tooinitialize Hallo project.</span><span class="sxs-lookup"><span data-stu-id="d016d-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="d016d-126">Zie Hallo voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="d016d-126">See hello example output:</span></span>

    ![Hallo npm init-uitvoer][0]
3. <span data-ttu-id="d016d-128">Hallo snelle en apps van azure mobile bibliotheken van de npm-opslagplaats Hallo installeren.</span><span class="sxs-lookup"><span data-stu-id="d016d-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="d016d-129">Maak een app.js tooimplement Hallo basic mobiele-bestandsserver.</span><span class="sxs-lookup"><span data-stu-id="d016d-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="d016d-130">Deze toepassing maakt een WebAPI mobile geoptimaliseerd met één eindpunt (`/tables/TodoItem`) waarmee niet-geverifieerde toegang tooan onderliggende SQL-gegevensopslag met behulp van een dynamische schema.</span><span class="sxs-lookup"><span data-stu-id="d016d-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="d016d-131">Is geschikt voor een snel starten van de client-bibliotheek te volgen:</span><span class="sxs-lookup"><span data-stu-id="d016d-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="d016d-132">[Android Client Quick Start]</span><span class="sxs-lookup"><span data-stu-id="d016d-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="d016d-133">[Apache Cordova-Client Quick Start]</span><span class="sxs-lookup"><span data-stu-id="d016d-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="d016d-134">[iOS-Client Quick Start]</span><span class="sxs-lookup"><span data-stu-id="d016d-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="d016d-135">[Windows Store-Client Quick Start]</span><span class="sxs-lookup"><span data-stu-id="d016d-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="d016d-136">[Quick Start voor Xamarin.iOS-Client]</span><span class="sxs-lookup"><span data-stu-id="d016d-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="d016d-137">[Snelstartgids voor Xamarin.Android-Client]</span><span class="sxs-lookup"><span data-stu-id="d016d-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="d016d-138">[Quick Start Xamarin.Forms-Client]</span><span class="sxs-lookup"><span data-stu-id="d016d-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="d016d-139">Hallo code vindt u voor deze eenvoudige toepassing in Hallo [basicapp voorbeeld op GitHub].</span><span class="sxs-lookup"><span data-stu-id="d016d-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="d016d-140"><a name="howto-vs2015-basicapp"></a>Procedure: een back-end knooppunt maken met Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d016d-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="d016d-141">Visual Studio 2015 is een uitbreiding toodevelop Node.js-toepassingen binnen Hallo IDE vereist.</span><span class="sxs-lookup"><span data-stu-id="d016d-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="d016d-142">toostart, installatie Hallo [1.1 van Node.js-hulpprogramma's voor Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d016d-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="d016d-143">Zodra Hallo Node.js-Tools voor Visual Studio zijn geïnstalleerd, moet u een snelle 4.x-toepassing maken:</span><span class="sxs-lookup"><span data-stu-id="d016d-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="d016d-144">Open Hallo **nieuw Project** dialoogvenster (van **bestand** > **nieuw** > **Project wordt gemaakt...** ).</span><span class="sxs-lookup"><span data-stu-id="d016d-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="d016d-145">Vouw **sjablonen** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="d016d-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="d016d-146">Selecteer Hallo **Azure Node.js Express 4 basistoepassing**.</span><span class="sxs-lookup"><span data-stu-id="d016d-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="d016d-147">Vul in Hallo projectnaam.</span><span class="sxs-lookup"><span data-stu-id="d016d-147">Fill in hello project name.</span></span>  <span data-ttu-id="d016d-148">Klik op *OK*.</span><span class="sxs-lookup"><span data-stu-id="d016d-148">Click *OK*.</span></span>

    ![Nieuw Project voor Visual Studio 2015][1]
5. <span data-ttu-id="d016d-150">Klik met de rechtermuisknop Hallo **npm** uit en selecteer **installeren nieuwe npm pakketten...** .</span><span class="sxs-lookup"><span data-stu-id="d016d-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="d016d-151">Mogelijk moet u toorefresh hello npm catalogus over het maken van uw eerste Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d016d-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="d016d-152">Klik op **vernieuwen** indien nodig.</span><span class="sxs-lookup"><span data-stu-id="d016d-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="d016d-153">Voer *apps van azure mobile* in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="d016d-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="d016d-154">Klik op Hallo **azure mobile apps 2.0.0** van het pakket en klik vervolgens op **pakket installeren**.</span><span class="sxs-lookup"><span data-stu-id="d016d-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Nieuwe npm pakketten installeren][2]
8. <span data-ttu-id="d016d-156">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="d016d-156">Click **Close**.</span></span>
9. <span data-ttu-id="d016d-157">Open Hallo *app.js* tooadd ondersteuning voor hello Azure Mobile Apps SDK.</span><span class="sxs-lookup"><span data-stu-id="d016d-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="d016d-158">Regel 6 at Hallo onderaan Hallo-bibliotheek in instructies vereisen, Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d016d-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="d016d-159">Andere instructies app.use toevoegen op ongeveer regel 27 na Hallo Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="d016d-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="d016d-160">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="d016d-160">Save hello file.</span></span>
10. <span data-ttu-id="d016d-161">Voer Hallo toepassing lokaal (hello API worden geleverd op http://localhost: 3000) of tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="d016d-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="d016d-162"><a name="create-node-backend-portal"></a>Procedure: een Node.js-backend met hello Azure-portal maken</span><span class="sxs-lookup"><span data-stu-id="d016d-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="d016d-163">U kunt een rechts van de back-end voor mobiele App maken in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d016d-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="d016d-164">Kunt u Hallo volgende stappen of een client en server samen te met de volgende Hallo maken volgen [maken van een mobiele app](app-service-mobile-ios-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d016d-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="d016d-165">Hallo-zelfstudie bevat een vereenvoudigde versie van deze instructies en wordt aanbevolen voor bewijs van concept projecten.</span><span class="sxs-lookup"><span data-stu-id="d016d-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="d016d-166">Terug in Hallo *aan de slag* blade onder **maken van een tabel-API**, kies **Node.js** als uw **back-endtaal**.</span><span class="sxs-lookup"><span data-stu-id="d016d-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="d016d-167">Hallo selectievakje voor '**ik erken dat hiermee alle inhoud van site overschreven wordt.**', klikt u vervolgens op **takentabel maken**.</span><span class="sxs-lookup"><span data-stu-id="d016d-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="d016d-168"><a name="download-quickstart"></a>Hoe: Download Hallo Node.js-back-end Quick Start CodeProject met Git</span><span class="sxs-lookup"><span data-stu-id="d016d-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="d016d-169">Wanneer u een back-end voor Node.js mobiele App maakt met behulp van de portal Hallo **snel starten** blade een Node.js-project is gemaakt voor u en geïmplementeerde tooyour site.</span><span class="sxs-lookup"><span data-stu-id="d016d-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="d016d-170">U kunt de tabellen en API's toevoegen en bewerken van codebestanden voor Hallo Node.js back-end in de portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="d016d-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="d016d-171">U kunt ook verschillende extra toodownload Hallo back-end implementatieproject gebruiken zodat u kunt toevoegen of tabellen en API's wijzigen en vervolgens opnieuw Hallo-project publiceren.</span><span class="sxs-lookup"><span data-stu-id="d016d-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="d016d-172">Zie voor meer informatie de [Implementatiehandleiding voor Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="d016d-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="d016d-173">Hallo wordt volgende procedure een Git-opslagplaats toodownload Hallo Quick Start-projectcode.</span><span class="sxs-lookup"><span data-stu-id="d016d-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="d016d-174">Installeer Git als u dat nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="d016d-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="d016d-175">Hallo stappen vereist tooinstall Git variëren tussen besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="d016d-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="d016d-176">Zie [installeren Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) voor besturingssysteem-specifieke distributies en installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="d016d-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="d016d-177">Hallo stappen in [inschakelen Hallo App Service-app opslagplaats](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable Hallo Git-opslagplaats voor uw back-end-site, waardoor een notitie van Hallo implementatie gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d016d-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="d016d-178">Hallo blade voor uw back-end voor de mobiele App Noteer Hallo **Git-kloon-URL** instelling.</span><span class="sxs-lookup"><span data-stu-id="d016d-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="d016d-179">Hallo uitvoeren `git clone` opdracht Hallo Git-kloon-URL, invoeren van het wachtwoord indien nodig, zoals in het volgende voorbeeld met:</span><span class="sxs-lookup"><span data-stu-id="d016d-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="d016d-180">Bladeren toolocal directory, die in het voorgaande voorbeeld Hallo /todolist, en u ziet dat projectbestanden zijn gedownload.</span><span class="sxs-lookup"><span data-stu-id="d016d-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="d016d-181">Zoek Hallo `todoitem.json` bestand in Hallo `/tables` directory.</span><span class="sxs-lookup"><span data-stu-id="d016d-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="d016d-182">Dit bestand definieert machtigingen voor de tabel.</span><span class="sxs-lookup"><span data-stu-id="d016d-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="d016d-183">Hallo ook zoeken `todoitem.js` bestanden per Hallo dezelfde directory waarmee wordt gedefinieerd dat CRUD-bewerking voor de tabel Hallo scripts.</span><span class="sxs-lookup"><span data-stu-id="d016d-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="d016d-184">Nadat u wijzigingen tooproject bestanden aangebracht hebt, uitvoeren Hallo opdrachten tooadd, doorvoeren en vervolgens de wijzigingen toohello site uploaden te volgen:</span><span class="sxs-lookup"><span data-stu-id="d016d-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="d016d-185">Wanneer u nieuwe bestanden toohello project toevoegt, moet u eerst tooexecute hello `git add .` opdracht.</span><span class="sxs-lookup"><span data-stu-id="d016d-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="d016d-186">Telkens wanneer een nieuwe reeks doorvoeracties wordt doorgeschoven, toohello site opnieuw Hallo site wordt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="d016d-187"><a name="howto-publish-to-azure"></a>Hoe: uw Node.js-back-end-tooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="d016d-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="d016d-188">Microsoft Azure biedt veel mechanismen voor het publiceren van uw Azure App Service Mobile Apps Node.js-back-end voor hello Azure-service.</span><span class="sxs-lookup"><span data-stu-id="d016d-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="d016d-189">Deze omvatten gebruik geïntegreerd in Visual Studio-hulpprogramma's voor, opdrachtregelprogramma's en continue implementatie-opties op basis van broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="d016d-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="d016d-190">Zie voor meer informatie over dit onderwerp de [Implementatiehandleiding voor Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="d016d-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="d016d-191">Azure App Service biedt specifiek advies voor Node.js-toepassing die u vóór de implementatie controleren moet:</span><span class="sxs-lookup"><span data-stu-id="d016d-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="d016d-192">Hoe te[Hallo knooppunt versie opgeven]</span><span class="sxs-lookup"><span data-stu-id="d016d-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="d016d-193">Hoe te[knooppunt-modules gebruiken]</span><span class="sxs-lookup"><span data-stu-id="d016d-193">How too[use Node modules]</span></span>

### <span data-ttu-id="d016d-194"><a name="howto-enable-homepage"></a>Procedure: een startpagina van uw toepassing inschakelen</span><span class="sxs-lookup"><span data-stu-id="d016d-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="d016d-195">Veel toepassingen zijn een combinatie van web- en mobiele apps en Hallo ExpressJS framework, kunt u de twee toocombine facetten.</span><span class="sxs-lookup"><span data-stu-id="d016d-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="d016d-196">Soms echter, kunt u tooonly implementeren een mobiele-interface.</span><span class="sxs-lookup"><span data-stu-id="d016d-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="d016d-197">Het is nuttig tooprovide die een landingspagina pagina tooensure Hallo app-service actief is.</span><span class="sxs-lookup"><span data-stu-id="d016d-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="d016d-198">Geef uw eigen introductiepagina of de startpagina van een tijdelijke inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d016d-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="d016d-199">een tijdelijke introductiepagina tooenable gebruiken Hallo tooinstantiate Azure Mobile Apps te volgen:</span><span class="sxs-lookup"><span data-stu-id="d016d-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="d016d-200">Als u deze optie beschikbaar wilt bij het ontwikkelen van lokaal, kunt u deze instelling tooyour toevoegen `azureMobile.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="d016d-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="d016d-201"><a name="TableOperations"></a>Tabelbewerkingen</span><span class="sxs-lookup"><span data-stu-id="d016d-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="d016d-202">Hallo apps van azure mobile Node.js Server SDK biedt mechanismen tooexpose gegevens opgeslagen in Azure SQL Database als een WebAPI tabellen.</span><span class="sxs-lookup"><span data-stu-id="d016d-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="d016d-203">Er zijn vijf operations beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="d016d-203">Five operations are provided.</span></span>

| <span data-ttu-id="d016d-204">Bewerking</span><span class="sxs-lookup"><span data-stu-id="d016d-204">Operation</span></span> | <span data-ttu-id="d016d-205">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d016d-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d016d-206">GET-/tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="d016d-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="d016d-207">Alle records in de tabel Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="d016d-207">Get all records in hello table</span></span> |
| <span data-ttu-id="d016d-208">GET-/tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="d016d-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="d016d-209">Ophalen van een bepaalde record in de tabel Hallo</span><span class="sxs-lookup"><span data-stu-id="d016d-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="d016d-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="d016d-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="d016d-211">Een record in de tabel Hallo maken</span><span class="sxs-lookup"><span data-stu-id="d016d-211">Create a record in hello table</span></span> |
| <span data-ttu-id="d016d-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="d016d-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="d016d-213">Een record in de tabel Hallo bijwerken</span><span class="sxs-lookup"><span data-stu-id="d016d-213">Update a record in hello table</span></span> |
| <span data-ttu-id="d016d-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="d016d-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="d016d-215">Een record in de tabel Hallo verwijderen</span><span class="sxs-lookup"><span data-stu-id="d016d-215">Delete a record in hello table</span></span> |

<span data-ttu-id="d016d-216">Biedt ondersteuning voor deze WebAPI [OData] en breidt Hallo tabel schema toosupport [offline gegevenssynchronisatie].</span><span class="sxs-lookup"><span data-stu-id="d016d-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="d016d-217"><a name="howto-dynamicschema"></a>Hoe: tabellen met behulp van een dynamische schema definiëren</span><span class="sxs-lookup"><span data-stu-id="d016d-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="d016d-218">Voordat een tabel kan worden gebruikt, moet worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="d016d-219">Tabellen kunnen worden gedefinieerd met een statische schema (Hallo developer definieert waar Hallo kolommen in Hallo schema) of dynamisch (Hallo SDK bepaalt waar Hallo schema op basis van binnenkomende aanvragen).</span><span class="sxs-lookup"><span data-stu-id="d016d-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="d016d-220">Bovendien kunt Hallo ontwikkelaars bepaalde aspecten van Hallo WebAPI beheren door Javascript-code toohello definitie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d016d-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="d016d-221">Als een best practice moet u elke tabel in een Javascript-bestand in Hallo tabellen directory definiëren en vervolgens de tabellen tables.import() methode tooimport hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d016d-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="d016d-222">Basic-app-Hallo uitbreidt, zou Hallo app.js bestand worden aangepast:</span><span class="sxs-lookup"><span data-stu-id="d016d-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="d016d-223">Hallo-tabel in definiëren. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="d016d-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="d016d-224">Tabellen dynamische schema standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d016d-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="d016d-225">tooturn uit dynamische schema instellen globaal Hallo App-instelling **MS_DynamicSchema** toofalse binnen hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d016d-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="d016d-226">U vindt een compleet voorbeeld in Hallo [todo-voorbeeld op GitHub].</span><span class="sxs-lookup"><span data-stu-id="d016d-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="d016d-227"><a name="howto-staticschema"></a>Hoe: tabellen met behulp van een statische schema definiëren</span><span class="sxs-lookup"><span data-stu-id="d016d-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="d016d-228">U kunt expliciet Hallo kolommen tooexpose via Hallo WebAPI definiëren.</span><span class="sxs-lookup"><span data-stu-id="d016d-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="d016d-229">Hello die node.js-SDK voor apps van azure mobile voegt automatisch eventuele extra kolommen die vereist zijn voor offline synchronisatie toohello gegevenslijst die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="d016d-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="d016d-230">De Quick Start-clienttoepassingen vereisen bijvoorbeeld dat een tabel met twee kolommen: tekst (tekenreeks) en (een Booleaanse waarde) te voltooien.</span><span class="sxs-lookup"><span data-stu-id="d016d-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="d016d-231">Hallo tabel kan worden gedefinieerd in Hallo tabel definitie JavaScript-bestand (te vinden in Hallo tabellen directory) als volgt:</span><span class="sxs-lookup"><span data-stu-id="d016d-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="d016d-232">Als u tabellen statisch definieert, moet u ook Hallo tables.initialize() methode toocreate Hallo-databaseschema aanroepen tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="d016d-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="d016d-233">Hallo tables.initialize() methode retourneert een [belofte] zodat de webservice Hallo dienen geen aanvragen voordat Hallo-database wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="d016d-234"><a name="howto-sqlexpress-setup"></a>Hoe: Gebruik SQL Express als gegevensopslag ontwikkeling op uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="d016d-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="d016d-235">Hello Azure Mobile Apps Hallo AzureMobile Apps knooppunt SDK biedt drie opties voor die gegevens out of box Hallo: SDK biedt drie opties voor die gegevens out of box Hallo:</span><span class="sxs-lookup"><span data-stu-id="d016d-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="d016d-236">Gebruik Hallo **geheugen** stuurprogramma-archief voor het voorbeeld van een niet-permanente tooprovide</span><span class="sxs-lookup"><span data-stu-id="d016d-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="d016d-237">Gebruik Hallo **mssql** stuurprogramma tooprovide gegevensopslag SQL Express voor ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="d016d-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="d016d-238">Gebruik Hallo **mssql** stuurprogramma tooprovide een Azure SQL Database-gegevensarchief voor productie</span><span class="sxs-lookup"><span data-stu-id="d016d-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="d016d-239">Hello Azure Mobile Apps Node.js SDK maakt gebruik van Hallo [mssql Node.js pakket] tooestablish en gebruik van een verbinding tooboth SQL Express- en SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="d016d-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="d016d-240">Dit pakket vereist dat u TCP-verbindingen op uw exemplaar van SQL Express inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d016d-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="d016d-241">Hallo geheugen stuurprogramma biedt geen een volledige set van opslagruimten voor het testen.</span><span class="sxs-lookup"><span data-stu-id="d016d-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="d016d-242">Als u uw back-end lokaal tootest wilt, we raden aan Hallo gebruik van een gegevensarchief SQL Express en Hallo mssql-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="d016d-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="d016d-243">Download en installeer [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="d016d-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="d016d-244">Zorg ervoor dat u SQL Server 2014 Express Hallo met extra editie installeren.</span><span class="sxs-lookup"><span data-stu-id="d016d-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="d016d-245">Tenzij u expliciet ondersteuning voor 64-bits vereist, verbruikt Hallo 32-bits versie minder geheugen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="d016d-246">Hallo SQL Server 2014 Configuration Manager worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="d016d-247">Vouw Hallo **SQL Server-netwerkconfiguratie** knooppunt in het menu van Hallo links structuur.</span><span class="sxs-lookup"><span data-stu-id="d016d-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="d016d-248">Klik op **protocollen voor SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="d016d-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="d016d-249">Met de rechtermuisknop op **TCP/IP** en selecteer **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="d016d-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="d016d-250">Klik op **OK** in Hallo pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="d016d-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="d016d-251">Met de rechtermuisknop op **TCP/IP** en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="d016d-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="d016d-252">Klik op Hallo **IP-adressen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d016d-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="d016d-253">Hallo zoeken **IPAll** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d016d-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="d016d-254">In Hallo **TCP-poort** veld **1433**.</span><span class="sxs-lookup"><span data-stu-id="d016d-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="d016d-255">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d016d-255">Click **OK**.</span></span>  <span data-ttu-id="d016d-256">Klik op **OK** in Hallo pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="d016d-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="d016d-257">Klik op **SQL Server-Services** in het menu van Hallo links structuur.</span><span class="sxs-lookup"><span data-stu-id="d016d-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="d016d-258">Met de rechtermuisknop op **SQL Server (SQLEXPRESS)** en selecteer **opnieuw starten**</span><span class="sxs-lookup"><span data-stu-id="d016d-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="d016d-259">Hallo SQL Server 2014 Configuration Manager te sluiten.</span><span class="sxs-lookup"><span data-stu-id="d016d-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="d016d-260">Voer Hallo SQL Server 2014 Management Studio en maak verbinding tooyour lokale exemplaar van SQL Express</span><span class="sxs-lookup"><span data-stu-id="d016d-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="d016d-261">Met de rechtermuisknop op uw exemplaar in Object Explorer Hallo en selecteer **eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="d016d-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="d016d-262">Selecteer Hallo **beveiliging** pagina.</span><span class="sxs-lookup"><span data-stu-id="d016d-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="d016d-263">Zorg ervoor dat Hallo **modus van SQL Server en Windows-verificatie** is geselecteerd</span><span class="sxs-lookup"><span data-stu-id="d016d-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="d016d-264">Klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="d016d-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="d016d-265">Vouw **beveiliging** > **aanmeldingen** in Object Explorer Hallo</span><span class="sxs-lookup"><span data-stu-id="d016d-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="d016d-266">Met de rechtermuisknop op **aanmeldingen** en selecteer **New Login...**</span><span class="sxs-lookup"><span data-stu-id="d016d-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="d016d-267">Typ een aanmeldingsnaam.</span><span class="sxs-lookup"><span data-stu-id="d016d-267">Enter a Login name.</span></span>  <span data-ttu-id="d016d-268">Selecteer **SQL Server-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="d016d-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="d016d-269">Voer een wachtwoord, voert u Hallo hetzelfde wachtwoord in **wachtwoord bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="d016d-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="d016d-270">Hallo-wachtwoord moet voldoen aan de complexiteitsvereisten van Windows.</span><span class="sxs-lookup"><span data-stu-id="d016d-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="d016d-271">Klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="d016d-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="d016d-272">Met de rechtermuisknop op uw nieuwe aanmelding en selecteer **eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="d016d-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="d016d-273">Selecteer Hallo **serverfuncties** pagina</span><span class="sxs-lookup"><span data-stu-id="d016d-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="d016d-274">Controleer Hallo vak volgende toohello **dbcreator** serverfunctie</span><span class="sxs-lookup"><span data-stu-id="d016d-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="d016d-275">Klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="d016d-275">Click **OK**</span></span>
   13. <span data-ttu-id="d016d-276">Hallo SQL Server 2015 Management Studio sluiten</span><span class="sxs-lookup"><span data-stu-id="d016d-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="d016d-277">Zorg ervoor dat u records Hallo-gebruikersnaam en wachtwoord die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="d016d-278">Mogelijk moet u de aanvullende serverfuncties tooassign of machtigingen, afhankelijk van de vereisten van uw specifieke database.</span><span class="sxs-lookup"><span data-stu-id="d016d-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="d016d-279">Hallo Node.js-toepassing hello leest **SQLCONNSTR_MS_TableConnectionString** omgevingsvariabele voor Hallo-verbindingsreeks voor deze database.</span><span class="sxs-lookup"><span data-stu-id="d016d-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="d016d-280">U kunt deze variabele instellen in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="d016d-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="d016d-281">Bijvoorbeeld, kunt u PowerShell tooset deze omgevingsvariabele:</span><span class="sxs-lookup"><span data-stu-id="d016d-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="d016d-282">Toegang tot Hallo-database via een TCP/IP-verbinding en geef een gebruikersnaam en wachtwoord voor Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="d016d-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="d016d-283"><a name="howto-config-localdev"></a>Hoe: uw project voor lokale ontwikkeling configureren</span><span class="sxs-lookup"><span data-stu-id="d016d-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="d016d-284">Azure Mobile Apps leest een JavaScript-bestand aangeroepen *azureMobile.js* van het lokale bestandssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="d016d-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="d016d-285">Niet gebruiken in dit bestand tooconfigure hello Azure Mobile Apps SDK in productie - App-instellingen gebruiken in Hallo [Azure-portal] in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="d016d-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="d016d-286">Hallo *azureMobile.js* bestand moet een configuratieobject exporteren.</span><span class="sxs-lookup"><span data-stu-id="d016d-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="d016d-287">meest voorkomende Hallo-instellingen zijn:</span><span class="sxs-lookup"><span data-stu-id="d016d-287">hello most common settings are:</span></span>

* <span data-ttu-id="d016d-288">Database-instellingen</span><span class="sxs-lookup"><span data-stu-id="d016d-288">Database Settings</span></span>
* <span data-ttu-id="d016d-289">Instellingen voor diagnostische logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="d016d-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="d016d-290">Alternatieve CORS-instellingen</span><span class="sxs-lookup"><span data-stu-id="d016d-290">Alternate CORS Settings</span></span>

<span data-ttu-id="d016d-291">Een voorbeeld *azureMobile.js* bestand Hallo voorafgaand aan de database-instellingen volgt implementeren:</span><span class="sxs-lookup"><span data-stu-id="d016d-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="d016d-292">Het is raadzaam dat u toevoegt, *azureMobile.js* tooyour *.gitignore* bestand (of andere broncodebeheer bestand negeren) tooprevent wachtwoorden worden opgeslagen in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="d016d-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="d016d-293">Altijd productie-instellingen configureren in App-instellingen in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d016d-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="d016d-294"><a name="howto-appsettings"></a>Procedure: App-instellingen voor uw mobiele App configureren</span><span class="sxs-lookup"><span data-stu-id="d016d-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="d016d-295">De meeste instellingen in Hallo *azureMobile.js* bestand hebben een equivalente App-instelling in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d016d-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="d016d-296">Hallo lijst tooconfigure na uw app in App-instellingen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d016d-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="d016d-297">App-instelling</span><span class="sxs-lookup"><span data-stu-id="d016d-297">App Setting</span></span> | <span data-ttu-id="d016d-298">*azureMobile.js* instelling</span><span class="sxs-lookup"><span data-stu-id="d016d-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="d016d-299">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d016d-299">Description</span></span> | <span data-ttu-id="d016d-300">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d016d-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d016d-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="d016d-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="d016d-302">naam</span><span class="sxs-lookup"><span data-stu-id="d016d-302">name</span></span> |<span data-ttu-id="d016d-303">Hallo-naam van Hallo-app</span><span class="sxs-lookup"><span data-stu-id="d016d-303">hello name of hello app</span></span> |<span data-ttu-id="d016d-304">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d016d-304">string</span></span> |
| <span data-ttu-id="d016d-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="d016d-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="d016d-306">Logging.level</span><span class="sxs-lookup"><span data-stu-id="d016d-306">logging.level</span></span> |<span data-ttu-id="d016d-307">Minimale logboekniveau van berichten toolog</span><span class="sxs-lookup"><span data-stu-id="d016d-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="d016d-308">fout, waarschuwing, info, uitgebreid, foutopsporing, stom</span><span class="sxs-lookup"><span data-stu-id="d016d-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="d016d-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="d016d-309">**MS_DebugMode**</span></span> |<span data-ttu-id="d016d-310">Fouten opsporen</span><span class="sxs-lookup"><span data-stu-id="d016d-310">debug</span></span> |<span data-ttu-id="d016d-311">In- of de foutopsporingsmodus uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d016d-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="d016d-312">True, false</span><span class="sxs-lookup"><span data-stu-id="d016d-312">true, false</span></span> |
| <span data-ttu-id="d016d-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="d016d-313">**MS_TableSchema**</span></span> |<span data-ttu-id="d016d-314">Data.schema</span><span class="sxs-lookup"><span data-stu-id="d016d-314">data.schema</span></span> |<span data-ttu-id="d016d-315">Naam van de standaard schema voor de SQL-tabellen</span><span class="sxs-lookup"><span data-stu-id="d016d-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="d016d-316">tekenreeks (standaard: dbo)</span><span class="sxs-lookup"><span data-stu-id="d016d-316">string (default: dbo)</span></span> |
| <span data-ttu-id="d016d-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="d016d-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="d016d-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="d016d-318">data.dynamicSchema</span></span> |<span data-ttu-id="d016d-319">In- of de foutopsporingsmodus uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d016d-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="d016d-320">True, false</span><span class="sxs-lookup"><span data-stu-id="d016d-320">true, false</span></span> |
| <span data-ttu-id="d016d-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="d016d-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="d016d-322">versie (set tooundefined)</span><span class="sxs-lookup"><span data-stu-id="d016d-322">version (set tooundefined)</span></span> |<span data-ttu-id="d016d-323">Hallo X-ZUMO-Server-versie-header wordt uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="d016d-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="d016d-324">True, false</span><span class="sxs-lookup"><span data-stu-id="d016d-324">true, false</span></span> |
| <span data-ttu-id="d016d-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="d016d-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="d016d-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="d016d-326">skipversioncheck</span></span> |<span data-ttu-id="d016d-327">Controle van versie Hallo van client-API wordt uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="d016d-327">Disables hello client API version check</span></span> |<span data-ttu-id="d016d-328">True, false</span><span class="sxs-lookup"><span data-stu-id="d016d-328">true, false</span></span> |

<span data-ttu-id="d016d-329">tooset een App-instelling:</span><span class="sxs-lookup"><span data-stu-id="d016d-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="d016d-330">Meld u bij toohello [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d016d-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="d016d-331">Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="d016d-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="d016d-332">Standaard wordt de blade instellingen Hallo geopend.</span><span class="sxs-lookup"><span data-stu-id="d016d-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="d016d-333">Als dit niet zo is, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d016d-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="d016d-334">Klik op **toepassingsinstellingen** in algemene Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="d016d-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="d016d-335">Schuif toohello sectie App-instellingen.</span><span class="sxs-lookup"><span data-stu-id="d016d-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="d016d-336">Als uw app instelt, al bestaat, klikt u op Hallo van Hallo app tooedit Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="d016d-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="d016d-337">Als uw app-instelling niet bestaat, voert u Hallo App-instelling in het vak Hallo-sleutel en Hallo-waarde in het vak Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="d016d-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="d016d-338">Nadat u voltooid zijn, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d016d-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="d016d-339">Het wijzigen van de meeste appinstellingen voor vereist service opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="d016d-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="d016d-340"><a name="howto-use-sqlazure"></a>Procedure: SQL-Database gebruiken als uw gegevensarchief productie</span><span class="sxs-lookup"><span data-stu-id="d016d-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="d016d-341">Met behulp van Azure SQL Database als gegevensopslag is identiek alle typen voor Azure App Service-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d016d-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="d016d-342">Als u dit nog niet hebt gedaan, volgt u deze stappen toocreate een back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="d016d-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="d016d-343">Meld u bij toohello [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d016d-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="d016d-344">In hello linksboven Hallo-venster, klikt u op Hallo **+ nieuw** knop > **Web en mobiel** > **mobiele App**, Geef een naam op voor uw back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="d016d-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="d016d-345">In Hallo **resourcegroep** Voer Hallo dezelfde naam als uw app.</span><span class="sxs-lookup"><span data-stu-id="d016d-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="d016d-346">Hallo standaard App Service-abonnement is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="d016d-347">Als u toochange uw App Service-abonnement wenst, kunt u doen door te klikken op Hallo App Service Plan > **+ maken van nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="d016d-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="d016d-348">Geef een naam op van de nieuwe App Service-abonnement Hallo en selecteer de juiste locatie.</span><span class="sxs-lookup"><span data-stu-id="d016d-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="d016d-349">Klik op Hallo prijscategorie en selecteer een geschikte prijscategorie voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="d016d-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="d016d-350">Selecteer **weergeven van alle** tooview meer opties, zoals prijzen **vrije** en **gedeelde**.</span><span class="sxs-lookup"><span data-stu-id="d016d-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="d016d-351">Nadat u de prijscategorie hebt geselecteerd, klikt u op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="d016d-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="d016d-352">Terug in Hallo **App Service-abonnement** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d016d-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="d016d-353">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d016d-353">Click **Create**.</span></span> <span data-ttu-id="d016d-354">Inrichting van een back-end voor de mobiele App kan een paar minuten duren.</span><span class="sxs-lookup"><span data-stu-id="d016d-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="d016d-355">Zodra het Hallo-backend voor mobiele Apps is ingericht, Hallo wordt geopend Hallo **instellingen** blade voor back-end van Hallo mobiele App.</span><span class="sxs-lookup"><span data-stu-id="d016d-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="d016d-356">Zodra de back-end van Hallo mobiele App is gemaakt, kunt u tooeither verbinding maken met een bestaande SQL-database tooyour backend voor mobiele Apps of maak een nieuwe SQL-database.</span><span class="sxs-lookup"><span data-stu-id="d016d-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="d016d-357">In deze sectie maken we een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="d016d-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="d016d-358">Als u al een database in Hallo dezelfde locatie als back-end van Hallo mobiele app in plaats daarvan kunt u **gebruik een bestaande database** en selecteer vervolgens die database.</span><span class="sxs-lookup"><span data-stu-id="d016d-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="d016d-359">Hallo-gebruik van een database op een andere locatie wordt niet aanbevolen vanwege de hogere latenties.</span><span class="sxs-lookup"><span data-stu-id="d016d-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="d016d-360">Klik in het Hallo nieuwe backend voor mobiele Apps, op **instellingen** > **mobiele App** > **gegevens** > **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d016d-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="d016d-361">In Hallo **gegevensverbinding toevoegen** blade, klikt u op **SQL Database - vereiste instellingen configureren** > **een nieuwe database maken**.</span><span class="sxs-lookup"><span data-stu-id="d016d-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="d016d-362">Voer de naam van de Hallo van de nieuwe database Hallo in Hallo **naam** veld.</span><span class="sxs-lookup"><span data-stu-id="d016d-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="d016d-363">Klik op **Server**.</span><span class="sxs-lookup"><span data-stu-id="d016d-363">Click **Server**.</span></span>  <span data-ttu-id="d016d-364">In Hallo **nieuwe server** blade, voer een unieke naam in Hallo **servernaam** veld en geef een geschikte **aanmeldgegevens van serverbeheerder** en **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d016d-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="d016d-365">Zorg ervoor dat **toestaan azure-services tooaccess server** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d016d-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="d016d-366">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d016d-366">Click **OK**.</span></span>

    ![Een Azure SQL-Database maken][6]
4. <span data-ttu-id="d016d-368">Op Hallo **nieuwe database** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d016d-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="d016d-369">Terug op Hallo **gegevensverbinding toevoegen** blade Selecteer **verbindingsreeks**, Voer Hallo aanmeldingsnaam en het wachtwoord die u hebt opgegeven bij het maken van Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="d016d-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="d016d-370">Als u een bestaande database gebruikt, geeft u Hallo-aanmeldingsreferenties voor die database.</span><span class="sxs-lookup"><span data-stu-id="d016d-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="d016d-371">Nadat u hebt ingevoerd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d016d-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="d016d-372">Terug op Hallo **gegevensverbinding toevoegen** blade opnieuw in en klikt u op **OK** toocreate Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="d016d-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="d016d-373">Maken van database Hallo kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="d016d-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="d016d-374">Gebruik Hallo **meldingen** gebied toomonitor Hallo voortgang van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="d016d-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="d016d-375">Voortgang niet totdat het Hallo-database is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d016d-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="d016d-376">Zodra met succes is geïmplementeerd, wordt een verbindingsreeks voor Hallo SQL Database-exemplaar in uw mobiele back-end App-instellingen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d016d-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="d016d-377">U kunt deze appinstelling in Hallo zien **instellingen** > **toepassingsinstellingen** > **verbindingsreeksen**.</span><span class="sxs-lookup"><span data-stu-id="d016d-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="d016d-378"><a name="howto-tables-auth"></a>Procedure: verificatie vereisen voor toegang tot tootables</span><span class="sxs-lookup"><span data-stu-id="d016d-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="d016d-379">Als u toouse App Service-verificatie met Hallo tabellen eindpunt wenst, moet u App Service-verificatie configureren in Hallo [Azure-portal] eerste.</span><span class="sxs-lookup"><span data-stu-id="d016d-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="d016d-380">Voor meer informatie over het configureren van verificatie in een Azure App Service, bekijken Hallo configuratiehandleiding voor de identiteitsprovider hello wilt toouse:</span><span class="sxs-lookup"><span data-stu-id="d016d-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="d016d-381">[Hoe tooconfigure Azure Active Directory-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="d016d-382">[Hoe tooconfigure Facebook-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="d016d-383">[Hoe tooconfigure Google-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="d016d-384">[Hoe Microsoft Authentication tooconfigure]</span><span class="sxs-lookup"><span data-stu-id="d016d-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="d016d-385">[Hoe tooconfigure Twitter-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="d016d-386">Elke tabel heeft een access-eigenschap die gebruikt toocontrol access toohello-tabel worden kan.</span><span class="sxs-lookup"><span data-stu-id="d016d-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="d016d-387">Hallo volgende voorbeeld ziet u een statisch gedefinieerde tabel met de verificatie is vereist.</span><span class="sxs-lookup"><span data-stu-id="d016d-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="d016d-388">Hallo access-eigenschap kan duren voordat een van drie waarden</span><span class="sxs-lookup"><span data-stu-id="d016d-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="d016d-389">*anonieme* geeft aan dat de clienttoepassing Hallo tooread gegevens zonder verificatie is toegestaan</span><span class="sxs-lookup"><span data-stu-id="d016d-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="d016d-390">*geverifieerde* geeft aan dat de clienttoepassing Hallo verificatietoken voor een geldig met Hallo-aanvraag moet verzenden</span><span class="sxs-lookup"><span data-stu-id="d016d-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="d016d-391">*uitgeschakeld* geeft aan dat deze tabel is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="d016d-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="d016d-392">Als Hallo access-eigenschap gedefinieerd is, is niet-geverifieerde toegang toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d016d-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="d016d-393"><a name="howto-tables-getidentity"></a>Procedure: verificatie claims gebruiken met uw tabellen</span><span class="sxs-lookup"><span data-stu-id="d016d-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="d016d-394">U kunt instellen wanneer er verschillende claims die worden aangevraagd wanneer verificatie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d016d-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="d016d-395">Deze claims zijn niet normaal gesproken beschikbaar via Hallo `context.user` object.</span><span class="sxs-lookup"><span data-stu-id="d016d-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="d016d-396">Maar ze kunnen worden opgehaald met Hallo `context.user.getIdentity()` methode.</span><span class="sxs-lookup"><span data-stu-id="d016d-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="d016d-397">Hallo `getIdentity()` methode retourneert een voorraad die wordt omgezet tooan-object.</span><span class="sxs-lookup"><span data-stu-id="d016d-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="d016d-398">Hallo-object is ingevoerd met de verificatiemethode (facebook, google, twitter, microsoftaccount of aad).</span><span class="sxs-lookup"><span data-stu-id="d016d-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="d016d-399">Als u verificatie van de Microsoft-Account en aanvraag Hallo e-mailadressen claim hebt ingesteld, kunt u bijvoorbeeld Hallo e-mailadres toohello record toevoegen Hello tabel controller te volgen:</span><span class="sxs-lookup"><span data-stu-id="d016d-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="d016d-400">toosee welke claims beschikbaar zijn, gebruikt u een web browser tooview hello `/.auth/me` eindpunt van uw site.</span><span class="sxs-lookup"><span data-stu-id="d016d-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="d016d-401"><a name="howto-tables-disabled"></a>Hoe: Schakel toegang toospecific tabelbewerkingen</span><span class="sxs-lookup"><span data-stu-id="d016d-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="d016d-402">In de toevoeging tooappearing op Hallo tabel worden Hallo toegang eigenschap gebruikte toocontrol afzonderlijke bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d016d-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="d016d-403">Er zijn vier bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="d016d-403">There are four operations:</span></span>

* <span data-ttu-id="d016d-404">*Lees* RESTful GET Hallo-bewerking op Hallo-tabel is</span><span class="sxs-lookup"><span data-stu-id="d016d-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="d016d-405">*invoegen* hello RESTful POST-bewerking op Hallo-tabel is</span><span class="sxs-lookup"><span data-stu-id="d016d-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="d016d-406">*bijwerken* hello RESTful PATCH bewerking is voor Hallo tabel</span><span class="sxs-lookup"><span data-stu-id="d016d-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="d016d-407">*Verwijder* hello RESTful verwijderbewerking op Hallo-tabel is</span><span class="sxs-lookup"><span data-stu-id="d016d-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="d016d-408">Bijvoorbeeld, kunt u desgewenst tooprovide een alleen-lezen niet-geverifieerde tabel:</span><span class="sxs-lookup"><span data-stu-id="d016d-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="d016d-409"><a name="howto-tables-query"></a>Hoe: Hallo-query die wordt gebruikt met tabelbewerkingen aanpassen</span><span class="sxs-lookup"><span data-stu-id="d016d-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="d016d-410">Een algemene vereiste voor tabelbewerkingen is tooprovide een beperkte weergave van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="d016d-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="d016d-411">Bijvoorbeeld, kunt u desgewenst een tabel die is gecodeerd met Hallo geverifieerde gebruikers-ID dat kunt u alleen lezen of bijwerken van uw eigen records.</span><span class="sxs-lookup"><span data-stu-id="d016d-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="d016d-412">Hallo tabeldefinitie na biedt deze functionaliteit:</span><span class="sxs-lookup"><span data-stu-id="d016d-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="d016d-413">Bewerkingen die normaal gesproken een query uitvoeren hebben een queryeigenschap die u met een waar aanpassen kunt component.</span><span class="sxs-lookup"><span data-stu-id="d016d-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="d016d-414">eigenschap Hallo-query is een [QueryJS] dat object gebruikte tooconvert een OData-query toosomething die gegevens back-end Hallo kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="d016d-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="d016d-415">Eenvoudige gelijkheid gevallen (zoals Hallo voorafgaand aan een), kan een kaart worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d016d-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="d016d-416">U kunt ook specifieke SQL-componenten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d016d-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="d016d-417"><a name="howto-tables-softdelete"></a>Hoe: voorlopig verwijderen configureren in een tabel</span><span class="sxs-lookup"><span data-stu-id="d016d-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="d016d-418">Voorlopige verwijderingen worden records niet daadwerkelijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d016d-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="d016d-419">In plaats daarvan markeren het als verwijderd in de database Hallo door in te stellen Hallo verwijderde kolom tootrue.</span><span class="sxs-lookup"><span data-stu-id="d016d-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="d016d-420">Hello Azure Mobile Apps SDK automatisch voorlopig verwijderde records worden verwijderd uit de resultaten tenzij Hallo Mobile Client SDK IncludeDeleted() gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d016d-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="d016d-421">een tabel voor voorlopig verwijderen, tooconfigure ingesteld Hallo `softDelete` eigenschap in het definitiebestand voor Hallo tabel:</span><span class="sxs-lookup"><span data-stu-id="d016d-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="d016d-422">Een mechanisme voor het opschonen van records - vanuit een clienttoepassing, via een webtaak, Azure-functie of via een aangepaste API gebruiken, moet u instellen.</span><span class="sxs-lookup"><span data-stu-id="d016d-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="d016d-423"><a name="howto-tables-seeding"></a>Procedure: de database met gegevens Seed</span><span class="sxs-lookup"><span data-stu-id="d016d-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="d016d-424">Wanneer u een nieuwe toepassing maakt, kunt u desgewenst tooseed een tabel met gegevens.</span><span class="sxs-lookup"><span data-stu-id="d016d-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="d016d-425">Dit kan worden uitgevoerd binnen Hallo tabel definitie JavaScript-bestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="d016d-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="d016d-426">Seeding van de gegevens wordt alleen uitgevoerd wanneer Hallo tabel door hello Azure Mobile Apps SDK is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d016d-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="d016d-427">Als Hallo tabel al in Hallo-database bestaat, wordt er worden geen gegevens ingevoegd in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="d016d-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="d016d-428">Als u dynamische schema is ingeschakeld, klikt u vervolgens het schema afgeleid van Hallo seeding gegevens.</span><span class="sxs-lookup"><span data-stu-id="d016d-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="d016d-429">Het is raadzaam dat u niet expliciet Hallo aanroepen `tables.initialize()` methode toocreate Hallo tabel Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d016d-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="d016d-430"><a name="Swagger"></a>Hoe: Swagger-ondersteuning inschakelen</span><span class="sxs-lookup"><span data-stu-id="d016d-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="d016d-431">Azure App Service Mobile Apps wordt geleverd met ingebouwde [Swagger] ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="d016d-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="d016d-432">Hallo swagger-ui tooenable Swagger-ondersteuning, eerst installeren als een afhankelijkheid:</span><span class="sxs-lookup"><span data-stu-id="d016d-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="d016d-433">Zodra u hebt geïnstalleerd, kunt u ondersteuning voor Swagger in Azure Mobile Apps-constructor Hallo inschakelen:</span><span class="sxs-lookup"><span data-stu-id="d016d-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="d016d-434">U waarschijnlijk alleen wilt tooenable Swagger worden ondersteund in ontwikkeling edities.</span><span class="sxs-lookup"><span data-stu-id="d016d-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="d016d-435">U kunt dit doen door het gebruik van de `NODE_ENV` app-instelling:</span><span class="sxs-lookup"><span data-stu-id="d016d-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="d016d-436">Hallo swagger-eindpunt bevindt zich op http://*uw site*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="d016d-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="d016d-437">U hebt toegang tot Hallo Swagger-gebruikersinterface via Hallo `/swagger/ui` eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d016d-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="d016d-438">Als u ervoor verificatie toorequire inlezen in uw hele toepassing kiest, Swagger, treedt een fout.</span><span class="sxs-lookup"><span data-stu-id="d016d-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="d016d-439">Kies voor de beste resultaten tooallow niet-geverifieerde aanvragen via in hello Azure App Service-verificatie / autorisatie-instellingen beheren vervolgens verificatie met behulp van Hallo `table.access` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d016d-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="d016d-440">U kunt ook toevoegen Hallo Swagger optie tooyour `azureMobile.js` als u alleen Swagger ondersteuning bij het ontwikkelen van lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="d016d-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="d016d-441"><a name="push">Pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="d016d-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="d016d-442">Mobiele Apps worden geïntegreerd met Azure Notification Hubs tooenable u toosend gericht push notifications toomillions van apparaten voor alle primaire platforms.</span><span class="sxs-lookup"><span data-stu-id="d016d-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="d016d-443">U kunt pushmeldingen verzenden via Notification Hubs meldingen tooiOS, Android en Windows-apparaten.</span><span class="sxs-lookup"><span data-stu-id="d016d-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="d016d-444">meer informatie over alles wat u kunt doen met toolearn Notification Hubs, Zie [overzicht van Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d016d-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="d016d-445"></a><a name="send-push"></a>Hoe: pushmeldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="d016d-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="d016d-446">Hallo volgende code toont hoe toouse Hallo push object toosend een uitzending push-melding tooregistered iOS-apparaten:</span><span class="sxs-lookup"><span data-stu-id="d016d-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="d016d-447">Door een sjabloon push-registratie van Hallo client maakt, kunt u in plaats daarvan een sjabloon push-bericht toodevices op alle ondersteunde platforms verzenden.</span><span class="sxs-lookup"><span data-stu-id="d016d-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="d016d-448">Hallo van de volgende code wordt getoond hoe toosend een melding van de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="d016d-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="d016d-449"><a name="push-user"></a>Hoe: verzenden push notifications tooan geverifieerde gebruiker met tags</span><span class="sxs-lookup"><span data-stu-id="d016d-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="d016d-450">Wanneer een geverifieerde gebruiker geregistreerd voor pushmeldingen, wordt een gebruikers-ID-tag toohello registratie automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d016d-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="d016d-451">Met deze code, kunt u push notifications tooall apparaten zijn geregistreerd door een specifieke gebruiker verzenden.</span><span class="sxs-lookup"><span data-stu-id="d016d-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="d016d-452">Hallo volgende code wordt Hallo SID van gebruiker Hallo-aanvraag en verzendt een sjabloon tooevery apparaatregistratie voor pushberichten voor die gebruiker:</span><span class="sxs-lookup"><span data-stu-id="d016d-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="d016d-453">Wanneer u registreert voor pushmeldingen vanuit een geverifieerde client, moet u ervoor zorgen dat de verificatie is voltooid voordat u de registratie.</span><span class="sxs-lookup"><span data-stu-id="d016d-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="d016d-454"><a name="CustomAPI"></a>Aangepaste API 's</span><span class="sxs-lookup"><span data-stu-id="d016d-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="d016d-455"><a name="howto-customapi-basic"></a>Procedure: een aangepaste API definiëren</span><span class="sxs-lookup"><span data-stu-id="d016d-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="d016d-456">Bovendien toohello data access-API via Hallo /tables eindpunt, Azure Mobile Apps dekking van uw aangepaste API kan bieden.</span><span class="sxs-lookup"><span data-stu-id="d016d-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="d016d-457">Aangepaste API's worden gedefinieerd in een vergelijkbare manier toohello tabeldefinities en toegang tot alle Hallo dezelfde mogelijkheden, zoals verificatie.</span><span class="sxs-lookup"><span data-stu-id="d016d-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="d016d-458">Als u toouse App Service-verificatie met een aangepaste API wenst, moet u App Service-verificatie configureren in Hallo [Azure-portal] eerste.</span><span class="sxs-lookup"><span data-stu-id="d016d-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="d016d-459">Voor meer informatie over het configureren van verificatie in een Azure App Service, bekijken Hallo configuratiehandleiding voor de identiteitsprovider hello wilt toouse:</span><span class="sxs-lookup"><span data-stu-id="d016d-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="d016d-460">[Hoe tooconfigure Azure Active Directory-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="d016d-461">[Hoe tooconfigure Facebook-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="d016d-462">[Hoe tooconfigure Google-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="d016d-463">[Hoe Microsoft Authentication tooconfigure]</span><span class="sxs-lookup"><span data-stu-id="d016d-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="d016d-464">[Hoe tooconfigure Twitter-verificatie]</span><span class="sxs-lookup"><span data-stu-id="d016d-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="d016d-465">Aangepaste API's zijn gedefinieerd op ongeveer dezelfde manier als tabellen API Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d016d-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="d016d-466">Maak een **api** directory</span><span class="sxs-lookup"><span data-stu-id="d016d-466">Create an **api** directory</span></span>
2. <span data-ttu-id="d016d-467">Het JavaScript-bestand van een API-definitie maken in Hallo **api** directory.</span><span class="sxs-lookup"><span data-stu-id="d016d-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="d016d-468">Gebruik Hallo importeren methode tooimport hello **api** directory.</span><span class="sxs-lookup"><span data-stu-id="d016d-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="d016d-469">Hier volgt Hallo prototype api-definitie op basis van Hallo basic-app voorbeeld die hebben we eerder hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d016d-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="d016d-470">Voorbeeld-API die retourneert Hallo server datum Hallo met *Date.now()* methode.</span><span class="sxs-lookup"><span data-stu-id="d016d-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="d016d-471">Hier volgt Hallo api/date.js bestand:</span><span class="sxs-lookup"><span data-stu-id="d016d-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="d016d-472">Elke parameter is een van de Hallo RESTful Standaardwerkwoorden - GET, POST, PATCH of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d016d-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="d016d-473">Hallo-methode is een standaard [ExpressJS Middleware] functie die u output Hallo vereist verzendt.</span><span class="sxs-lookup"><span data-stu-id="d016d-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="d016d-474"><a name="howto-customapi-auth"></a>Procedure: verificatie vereisen voor toegang tot tooa aangepaste API</span><span class="sxs-lookup"><span data-stu-id="d016d-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="d016d-475">Azure Mobile Apps SDK wordt de verificatie geïmplementeerd in Hallo dezelfde manier voor zowel Hallo tabellen eindpunt en aangepaste API's.</span><span class="sxs-lookup"><span data-stu-id="d016d-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="d016d-476">Als u wilt toevoegen verificatie toohello API ontwikkeld in de vorige sectie hello, een **toegang** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="d016d-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="d016d-477">U kunt ook verificatie op specifieke bewerkingen opgeven:</span><span class="sxs-lookup"><span data-stu-id="d016d-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="d016d-478">Hallo moet hetzelfde token die wordt gebruikt voor het Hallo tabellen eindpunt worden gebruikt voor aangepaste API's waarvoor verificatie is vereist.</span><span class="sxs-lookup"><span data-stu-id="d016d-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="d016d-479"><a name="howto-customapi-auth"></a>Hoe: grote bestandsuploads verwerken</span><span class="sxs-lookup"><span data-stu-id="d016d-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="d016d-480">Azure Mobile Apps SDK gebruikt Hallo [hoofdtekst parser middleware](https://github.com/expressjs/body-parser) tooaccept en inhoud van de hoofdtekst van de inzending decoderen.</span><span class="sxs-lookup"><span data-stu-id="d016d-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="d016d-481">U kunt vooraf hoofdtekst parser tooaccept groter bestandsuploads configureren:</span><span class="sxs-lookup"><span data-stu-id="d016d-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="d016d-482">Hallo-bestand is base 64-codering voor verzending.</span><span class="sxs-lookup"><span data-stu-id="d016d-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="d016d-483">Dit verhoogt de Hallo grootte van de werkelijke uploaden Hallo (en daarom moet u rekening houden met de grootte van Hallo).</span><span class="sxs-lookup"><span data-stu-id="d016d-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="d016d-484"><a name="howto-customapi-sql"></a>Hoe: uitvoeren van aangepaste SQL-instructies</span><span class="sxs-lookup"><span data-stu-id="d016d-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="d016d-485">Hello Azure Mobile Apps SDK kunt u access toohello gehele Context via Hallo request-object, zodat u tooexecute geparametriseerde toohello gedefinieerde gegevensprovider voor SQL-instructies eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="d016d-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="d016d-486"><a name="Debugging"></a>Foutopsporing, gemakkelijk tabellen en eenvoudige API 's</span><span class="sxs-lookup"><span data-stu-id="d016d-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="d016d-487"><a name="howto-diagnostic-logs"></a>Procedure: fouten opsporen, diagnoses stellen en problemen met Azure Mobile apps</span><span class="sxs-lookup"><span data-stu-id="d016d-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="d016d-488">Hello Azure App Service biedt verschillende opsporen en oplossen van technieken voor Node.js-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d016d-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="d016d-489">Raadpleeg toohello artikelen tooget gestart bij het oplossen van uw back-end voor Node.js Mobile te volgen:</span><span class="sxs-lookup"><span data-stu-id="d016d-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="d016d-490">[Bewaking van een Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="d016d-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="d016d-491">[Diagnostische logboekregistratie in Azure App Service inschakelen]</span><span class="sxs-lookup"><span data-stu-id="d016d-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="d016d-492">[Een Azure App Service in Visual Studio oplossen]</span><span class="sxs-lookup"><span data-stu-id="d016d-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="d016d-493">Node.js-toepassingen toegang hebben tooa breed scala aan extra diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="d016d-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="d016d-494">Intern Hallo maakt gebruik van Azure Mobile Apps Node.js SDK [Winston] voor diagnostische logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="d016d-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="d016d-495">Logboekregistratie is standaard ingeschakeld door de foutopsporingsmodus inschakelen of Hallo instellen **MS_DebugMode** tootrue van app-instelling in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d016d-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="d016d-496">Gegenereerde logboeken worden weergegeven in Hallo diagnostische logboeken op Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d016d-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="d016d-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Procedure: werken met gemakkelijk tabellen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d016d-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="d016d-498">Eenvoudig tabellen in het Hallo-portal kunnen u maken en werken met tabellen rechts in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d016d-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="d016d-499">U kunt zelfs tabelbewerkingen Hallo App Service-Editor met bewerken.</span><span class="sxs-lookup"><span data-stu-id="d016d-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="d016d-500">Wanneer u klikt op **gemakkelijk tabellen** in uw back-end voor site-instellingen kunt u toevoegen, wijzigen of verwijderen van een tabel.</span><span class="sxs-lookup"><span data-stu-id="d016d-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="d016d-501">U ziet ook de gegevens in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d016d-501">You can also see data in hello table.</span></span>

![Werken met gemakkelijk tabellen](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="d016d-503">Hallo zijn volgende opdrachten beschikbaar op de opdrachtbalk Hallo voor een tabel:</span><span class="sxs-lookup"><span data-stu-id="d016d-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="d016d-504">**Machtigingen wijzigen** - wijzigen Hallo-machtiging voor lezen, invoegen, bijwerken en verwijderen van bewerkingen op Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="d016d-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="d016d-505">Opties zijn tooallow anonieme toegang, toorequire verificatie of toodisable alle toegang tot toohello bewerking.</span><span class="sxs-lookup"><span data-stu-id="d016d-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="d016d-506">**Bewerk script** -Hallo scriptbestand voor de tabel Hallo in Hallo App Service-Editor wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="d016d-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="d016d-507">**Schema beheren** - toevoegen of verwijderen van kolommen of Hallo tabelindex wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d016d-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="d016d-508">**Tabel wissen** -afgekapt van een bestaande tabel verwijderen van alle gegevensrijen maar waarbij Hallo schema ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d016d-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="d016d-509">**Verwijderen van rijen** -afzonderlijke rijen met gegevens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d016d-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="d016d-510">**Weergave streaminglogboeken** -u toohello streaming log-service voor uw site verbindt.</span><span class="sxs-lookup"><span data-stu-id="d016d-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="d016d-511"><a name="work-easy-apis"></a>Procedure: werken met eenvoudige API's in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d016d-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="d016d-512">Eenvoudige API's in Hallo-portal kunt u maken en werken met aangepaste API's rechts in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d016d-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="d016d-513">Hallo App Service-Editor met API-scripts, kunt u bewerken.</span><span class="sxs-lookup"><span data-stu-id="d016d-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="d016d-514">Wanneer u klikt op **eenvoudige API's** in uw back-end voor site-instellingen kunt u toevoegen, wijzigen of verwijderen van een aangepaste API-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d016d-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Werken met eenvoudige API 's](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="d016d-516">In Hallo-portal kunt u wijzigen Hallo toegangsmachtigingen voor een bepaalde HTTP-actie, scriptbestand Hallo-API in App Service Editor bewerken of Hallo streaminglogboeken weergeven.</span><span class="sxs-lookup"><span data-stu-id="d016d-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="d016d-517"><a name="online-editor"></a>Hoe: code bewerken in Hallo App Service-Editor</span><span class="sxs-lookup"><span data-stu-id="d016d-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="d016d-518">Hello Azure-portal kunt u uw Node.js-back-end scriptbestanden in App Service-Editor Hallo bewerken zonder te hoeven Hallo project tooyour lokale computer downloaden.</span><span class="sxs-lookup"><span data-stu-id="d016d-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="d016d-519">tooedit scriptbestanden in Hallo online-editor:</span><span class="sxs-lookup"><span data-stu-id="d016d-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="d016d-520">Klik op de blade van uw mobiele App-back-end **alle instellingen** > beide **gemakkelijk tabellen** of **eenvoudige API's**, klikt u op een tabel of de API en klik vervolgens op **script bewerken**.</span><span class="sxs-lookup"><span data-stu-id="d016d-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="d016d-521">Hallo-scriptbestand wordt geopend in Hallo App Service-Editor.</span><span class="sxs-lookup"><span data-stu-id="d016d-521">hello script file is opened in hello App Service Editor.</span></span>

    ![App Service-Editor](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="d016d-523">Breng uw wijzigingen toohello code-bestand in Hallo online-editor.</span><span class="sxs-lookup"><span data-stu-id="d016d-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="d016d-524">Wijzigingen worden automatisch opgeslagen terwijl u typt.</span><span class="sxs-lookup"><span data-stu-id="d016d-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android Client Quick Start]: app-service-mobile-android-get-started.md
[Apache Cordova-Client Quick Start]: app-service-mobile-cordova-get-started.md
[iOS-Client Quick Start]: app-service-mobile-ios-get-started.md
[Quick Start voor Xamarin.iOS-Client]: app-service-mobile-xamarin-ios-get-started.md
[Snelstartgids voor Xamarin.Android-Client]: app-service-mobile-xamarin-android-get-started.md
[Quick Start Xamarin.Forms-Client]: app-service-mobile-xamarin-forms-get-started.md
[Windows Store-Client Quick Start]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[offline gegevenssynchronisatie]: app-service-mobile-offline-data-sync.md
[Hoe tooconfigure Azure Active Directory-verificatie]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Hoe tooconfigure Facebook-verificatie]: app-service-mobile-how-to-configure-facebook-authentication.md
[Hoe tooconfigure Google-verificatie]: app-service-mobile-how-to-configure-google-authentication.md
[Hoe Microsoft Authentication tooconfigure]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Hoe tooconfigure Twitter-verificatie]: app-service-mobile-how-to-configure-twitter-authentication.md
[Implementatiehandleiding voor Azure App Service]: ../app-service-web/web-sites-deploy.md
[Bewaking van een Azure App Service]: ../app-service-web/web-sites-monitor.md
[Diagnostische logboekregistratie in Azure App Service inschakelen]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Een Azure App Service in Visual Studio oplossen]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[Hallo knooppunt versie opgeven]: ../nodejs-specify-node-version-azure-apps.md
[knooppunt-modules gebruiken]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure-portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[belofte]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp voorbeeld op GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo-voorbeeld op GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[directory voorbeelden op GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[1.1 van Node.js-hulpprogramma's voor Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js pakket]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
