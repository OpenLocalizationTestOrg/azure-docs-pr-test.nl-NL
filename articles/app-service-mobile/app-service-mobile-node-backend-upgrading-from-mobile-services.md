---
title: aaaUpgrade van Mobile Services tooAzure App Service - Node.js
description: Meer informatie over hoe tooeasily upgrade voor uw Mobile Services-toepassing tooan App Service-mobiele App
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a><span data-ttu-id="f5045-103">Upgrade van uw bestaande Node.js Azure Mobile Service-tooApp Service</span><span class="sxs-lookup"><span data-stu-id="f5045-103">Upgrade your existing Node.js Azure Mobile Service tooApp Service</span></span>
<span data-ttu-id="f5045-104">App Service Mobile is een nieuwe manier toobuild mobiele toepassingen met Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f5045-104">App Service Mobile is a new way toobuild mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="f5045-105">toolearn meer, Zie [wat zijn Mobile Apps?].</span><span class="sxs-lookup"><span data-stu-id="f5045-105">toolearn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="f5045-106">Dit onderwerp wordt beschreven hoe een bestaande toepassing van de back-end voor Node.js van Azure Mobile Services tooa tooupgrade nieuwe App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="f5045-106">This topic describes how tooupgrade an existing Node.js backend application from Azure Mobile Services tooa new App Service Mobile Apps.</span></span> <span data-ttu-id="f5045-107">Terwijl u deze upgrade uitvoert, kunt uw bestaande Mobile Services-toepassing toooperate blijven.</span><span class="sxs-lookup"><span data-stu-id="f5045-107">While you perform this upgrade, your existing Mobile Services application can continue toooperate.</span></span>  <span data-ttu-id="f5045-108">Als u een Node.js-toepassing voor back-end tooupgrade nodig hebt, raadpleegt u te[upgraden van uw .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span><span class="sxs-lookup"><span data-stu-id="f5045-108">If you need tooupgrade a Node.js backend application, refer too[Upgrading your .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="f5045-109">Wanneer een mobiele back-end bijgewerkte tooAzure App Service is, heeft toegang tot tooall functies van de App en worden in rekening gebracht volgens te[App Service-prijzen], niet Mobile Services-prijzen.</span><span class="sxs-lookup"><span data-stu-id="f5045-109">When a mobile backend is upgraded tooAzure App Service, it has access tooall App Service features and are billed according too[App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="f5045-110">Migreren upgraden</span><span class="sxs-lookup"><span data-stu-id="f5045-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="f5045-111">Het is raadzaam dat u [uitvoeren van een migratie](app-service-mobile-migrating-from-mobile-services.md) voordat u doorgaat door middel van een upgrade.</span><span class="sxs-lookup"><span data-stu-id="f5045-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="f5045-112">Op deze manier kunt u beide versies van uw toepassing plaatsen op Hallo van dezelfde App Service-Plan en er zijn geen extra kosten in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="f5045-112">This way, you can put both versions of your application on hello same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a><span data-ttu-id="f5045-113">Verbeteringen in Mobile Apps Node.js server SDK</span><span class="sxs-lookup"><span data-stu-id="f5045-113">Improvements in Mobile Apps Node.js server SDK</span></span>
<span data-ttu-id="f5045-114">Upgraden van nieuwe toohello [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) bevat veel verbeteringen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="f5045-114">Upgrading toohello new [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) provides a lot of improvements, including:</span></span>

* <span data-ttu-id="f5045-115">Op basis van Hallo [Express framework](http://expressjs.com/en/index.html), Hallo nieuwe knooppunt SDK is lichte en tookeep up met nieuwe versies van het knooppunt wordt ontworpen dat ze afkomstig zijn uit. U kunt gedrag van de toepassing hello met Express-middleware aanpassen.</span><span class="sxs-lookup"><span data-stu-id="f5045-115">Based on hello [Express framework](http://expressjs.com/en/index.html), hello new Node SDK is light-weight and designed tookeep up with new Node versions as they come out. You can customize hello application behavior with Express middleware.</span></span>
* <span data-ttu-id="f5045-116">Aanzienlijke prestatieverbeteringen vergeleken toohello Mobile Services SDK.</span><span class="sxs-lookup"><span data-stu-id="f5045-116">Significant performance improvements compared toohello Mobile Services SDK.</span></span>
* <span data-ttu-id="f5045-117">U kunt nu een website host samen met uw mobiele back-end; Daarnaast is het eenvoudig tooadd hello Azure Mobile SDK tooany bestaande express.v4 toepassing.</span><span class="sxs-lookup"><span data-stu-id="f5045-117">You can now host a website together with your mobile backend; similarly, it's easy tooadd hello Azure Mobile SDK tooany existing express.v4 application.</span></span>
* <span data-ttu-id="f5045-118">Gebouwd voor verschillende platforms en lokale ontwikkeling, Hallo Mobile Apps SDK kan worden ontwikkeld en lokaal uitvoeren op Windows, Linux en OS x-platforms.</span><span class="sxs-lookup"><span data-stu-id="f5045-118">Built for cross-platform and local development, hello Mobile Apps SDK can be developed and run locally on Windows, Linux, and OSX platforms.</span></span> <span data-ttu-id="f5045-119">Het is nu eenvoudig toouse algemene knooppunt technieken zoals uitgevoerd [Mocha](https://mochajs.org/) eerdere toodeployment wordt getest.</span><span class="sxs-lookup"><span data-stu-id="f5045-119">It's now easy toouse common Node development techniques like running [Mocha](https://mochajs.org/) tests prior toodeployment.</span></span>

## <span data-ttu-id="f5045-120"><a name="overview"></a>Upgrade basisoverzicht</span><span class="sxs-lookup"><span data-stu-id="f5045-120"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="f5045-121">tooaid bij het bijwerken van een Node.js back-end van Azure App Service heeft een pakket compatibiliteit verstrekt.</span><span class="sxs-lookup"><span data-stu-id="f5045-121">tooaid in upgrading a Node.js backend, Azure App Service has provided a compatibility package.</span></span>  <span data-ttu-id="f5045-122">Na de upgrade hebt u een site niew die geïmplementeerd tooa nieuwe App Service-site worden kan.</span><span class="sxs-lookup"><span data-stu-id="f5045-122">After upgrade, you will have a niew site that can be deployed tooa new App Service site.</span></span>

<span data-ttu-id="f5045-123">Hallo Mobile Services-client-SDK's zijn **niet** compatibel is met de Hallo nieuwe Mobile Apps server SDK.</span><span class="sxs-lookup"><span data-stu-id="f5045-123">hello Mobile Services client SDKs are **not** compatible with hello new Mobile Apps server SDK.</span></span> <span data-ttu-id="f5045-124">In de volgorde tooprovide continuïteit van de service voor uw app, moet u wijzigingen tooa site momenteel bedient gepubliceerde clients niet publiceren.</span><span class="sxs-lookup"><span data-stu-id="f5045-124">In order tooprovide continuity of service for your app, you should not publish changes tooa site currently serving published clients.</span></span> <span data-ttu-id="f5045-125">In plaats daarvan moet u een nieuwe mobiele app die als een duplicaat fungeert maken.</span><span class="sxs-lookup"><span data-stu-id="f5045-125">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="f5045-126">U kunt deze toepassing plaatsen op Hallo dezelfde App Service tooavoid steeds extra financiële kosten plannen.</span><span class="sxs-lookup"><span data-stu-id="f5045-126">You can put this application on hello same App Service plan tooavoid incurring additional financial cost.</span></span>

<span data-ttu-id="f5045-127">U moet dan twee versies van de toepassing hello: een blijft dezelfde Hallo en fungeert gepubliceerde apps in Hallo wild en de andere die u kunt vervolgens een upgrade en de doelserver met een nieuwe client release.</span><span class="sxs-lookup"><span data-stu-id="f5045-127">You will then have two versions of hello application: one that stays hello same and serves published apps in hello wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="f5045-128">U kunt verplaatsen en testen van uw code in uw tempo, maar moet u ervoor zorgen dat alle oplossingen voor problemen u toegepaste tooboth krijgen.</span><span class="sxs-lookup"><span data-stu-id="f5045-128">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied tooboth.</span></span> <span data-ttu-id="f5045-129">Als u denkt dat een gewenste aantal client-apps in het wild toohello meest recente versie hebt bijgewerkt, kunt u de oorspronkelijke gemigreerde Apps Hallo verwijderen als u wenst.</span><span class="sxs-lookup"><span data-stu-id="f5045-129">Once you feel that a desired number of client apps in the wild have updated toohello latest version, you can delete hello original migrated app if you desire.</span></span> <span data-ttu-id="f5045-130">Hiervoor niet eventuele extra financieel kosten als gehost in Hallo dezelfde App Service plan als uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="f5045-130">It doesn't incur any additional monetary costs, if hosted in hello same App Service plan as your Mobile App.</span></span>

<span data-ttu-id="f5045-131">Hallo volledige overzicht voor het upgradeproces Hallo is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f5045-131">hello full outline for hello upgrade process is as follows:</span></span>

1. <span data-ttu-id="f5045-132">Download uw bestaande (gemigreerde) Azure Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="f5045-132">Download your existing (migrated) Azure Mobile Service.</span></span>
2. <span data-ttu-id="f5045-133">Hallo project tooan mobiele Apps van Azure converteren met Hallo compatibiliteit-pakket.</span><span class="sxs-lookup"><span data-stu-id="f5045-133">Convert hello project tooan Azure Mobile App using hello compatibility package.</span></span>
3. <span data-ttu-id="f5045-134">Corrigeer eventuele verschillen (zoals de verificatie-instellingen).</span><span class="sxs-lookup"><span data-stu-id="f5045-134">Correct any differences (such as authentication settings).</span></span>
4. <span data-ttu-id="f5045-135">De geconverteerde tooa voor mobiele Apps van Azure-project implementeert nieuwe App Service.</span><span class="sxs-lookup"><span data-stu-id="f5045-135">Deploy your converted Azure Mobile App project tooa new App Service.</span></span>
5. <span data-ttu-id="f5045-136">Een nieuwe versie van de clienttoepassing dat gebruik nieuwe mobiele App Hallo vrijgeven.</span><span class="sxs-lookup"><span data-stu-id="f5045-136">Release a new version of your client application that use hello new Mobile App.</span></span>
6. <span data-ttu-id="f5045-137">(Optioneel) Verwijder uw oorspronkelijke gemigreerde mobile service-app.</span><span class="sxs-lookup"><span data-stu-id="f5045-137">(Optional) Delete your original migrated mobile service app.</span></span>

<span data-ttu-id="f5045-138">Verwijderen kan optreden wanneer verkeer niet wordt weergegeven op uw oorspronkelijke gemigreerde mobiele service.</span><span class="sxs-lookup"><span data-stu-id="f5045-138">Deletion can occur when you don't see any traffic on your original migrated mobile service.</span></span>

## <span data-ttu-id="f5045-139"><a name="install-npm-package"></a>Hallo vereisten installeren</span><span class="sxs-lookup"><span data-stu-id="f5045-139"><a name="install-npm-package"></a> Install hello Pre-requisites</span></span>
<span data-ttu-id="f5045-140">U moet [Node] installeren op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="f5045-140">You should install [Node] on your local machine.</span></span>  <span data-ttu-id="f5045-141">U moet ook Hallo compatibiliteit pakketten installeren.</span><span class="sxs-lookup"><span data-stu-id="f5045-141">You should also install hello compatibility package.</span></span>  <span data-ttu-id="f5045-142">Nadat het knooppunt is geïnstalleerd, kunt u de volgende opdracht uit een nieuwe cmd of PowerShell-prompt Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f5045-142">After Node is installed, you can run hello following command from a new cmd or PowerShell prompt:</span></span>

```npm i -g azure-mobile-apps-compatibility```

## <span data-ttu-id="f5045-143"><a name="obtain-ams-scripts"></a>Verkrijgen van uw Azure Mobile Services-Scripts</span><span class="sxs-lookup"><span data-stu-id="f5045-143"><a name="obtain-ams-scripts"></a> Obtain your Azure Mobile Services Scripts</span></span>
* <span data-ttu-id="f5045-144">Meld u bij toohello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="f5045-144">Log in toohello [Azure Portal].</span></span>
* <span data-ttu-id="f5045-145">Met behulp van **alle Resources** of **App Services**, zoeken naar uw Mobile Services-site.</span><span class="sxs-lookup"><span data-stu-id="f5045-145">Using **All Resources** or **App Services**, find your Mobile Services site.</span></span>
* <span data-ttu-id="f5045-146">Binnen site hello, klikt u op **extra** -> **Kudu** -> **gaat** tooopen hello Kudu site.</span><span class="sxs-lookup"><span data-stu-id="f5045-146">Within hello site, click on **Tools** -> **Kudu** -> **Go** tooopen hello Kudu site.</span></span>
* <span data-ttu-id="f5045-147">Klik op **Console voor foutopsporing** -> **PowerShell** tooopen Hallo-console voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="f5045-147">Click on **Debug Console** -> **PowerShell** tooopen hello Debug console.</span></span>
* <span data-ttu-id="f5045-148">Navigeer te`site/wwwroot/App_Data/config` door te klikken op elke map op zijn beurt</span><span class="sxs-lookup"><span data-stu-id="f5045-148">Navigate too`site/wwwroot/App_Data/config` by clicking on each directory in turn</span></span>
* <span data-ttu-id="f5045-149">Klik op Hallo downloaden pictogram volgende toohello `scripts` directory.</span><span class="sxs-lookup"><span data-stu-id="f5045-149">Click on hello download icon next toohello `scripts` directory.</span></span>

<span data-ttu-id="f5045-150">Dit wordt Hallo-scripts in het ZIP-indeling gedownload.</span><span class="sxs-lookup"><span data-stu-id="f5045-150">This will download hello scripts in ZIP format.</span></span>  <span data-ttu-id="f5045-151">Maak een nieuwe map op uw lokale machine en uitpakken Hallo `scripts.ZIP` bestand binnen Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="f5045-151">Create a new directory on your local machine and unpack hello `scripts.ZIP` file within hello directory.</span></span>  <span data-ttu-id="f5045-152">Hiermee maakt u een `scripts` directory.</span><span class="sxs-lookup"><span data-stu-id="f5045-152">This will create a `scripts` directory.</span></span>

## <span data-ttu-id="f5045-153"><a name="scaffold-app"></a>Scaffold hello nieuwe Azure Mobile Apps back-end</span><span class="sxs-lookup"><span data-stu-id="f5045-153"><a name="scaffold-app"></a> Scaffold hello new Azure Mobile Apps backend</span></span>
<span data-ttu-id="f5045-154">Hallo volgende opdracht uit met de Hallo scripts map Hallo-directory worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f5045-154">Run hello following command from hello directory containing hello scripts directory:</span></span>

```scaffold-mobile-app scripts out```

<span data-ttu-id="f5045-155">Hiermee maakt u een ondersteunde back-end voor Azure Mobile Apps in Hallo `out` directory.</span><span class="sxs-lookup"><span data-stu-id="f5045-155">This will create a scaffolded Azure Mobile Apps backend in hello `out` directory.</span></span>  <span data-ttu-id="f5045-156">Hoewel niet vereist, is het een goed idee toocheck hello `out` map in een bron code opslagplaats van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="f5045-156">Although not required, it's a good idea toocheck hello `out` directory into a source code repository of your choice.</span></span>

## <span data-ttu-id="f5045-157"><a name="deploy-ama-app"></a>Uw back-end van Azure Mobile Apps implementeren</span><span class="sxs-lookup"><span data-stu-id="f5045-157"><a name="deploy-ama-app"></a> Deploy your Azure Mobile Apps backend</span></span>
<span data-ttu-id="f5045-158">Tijdens de implementatie moet u toodo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f5045-158">During deployment, you will need toodo hello following:</span></span>

1. <span data-ttu-id="f5045-159">Een nieuwe mobiele App maken in Hallo [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="f5045-159">Create a new Mobile App in hello [Azure Portal].</span></span>
2. <span data-ttu-id="f5045-160">Voer Hallo `createViews.sql` script op basis van de database verbonden.</span><span class="sxs-lookup"><span data-stu-id="f5045-160">Run hello `createViews.sql` script on your connected database.</span></span>
3. <span data-ttu-id="f5045-161">Koppeling Hallo database die is gekoppeld tooyour Mobile Service tooyour nieuwe App Service.</span><span class="sxs-lookup"><span data-stu-id="f5045-161">Link hello database that is linked tooyour Mobile Service tooyour new App Service.</span></span>
4. <span data-ttu-id="f5045-162">Koppelen van andere bronnen (zoals Notification Hubs)-toohello nieuwe App Service.</span><span class="sxs-lookup"><span data-stu-id="f5045-162">Link any other resources (such as Notification Hubs) toohello new App Service.</span></span>
5. <span data-ttu-id="f5045-163">Hallo gegenereerde code tooyour nieuwe site implementeert.</span><span class="sxs-lookup"><span data-stu-id="f5045-163">Deploy hello generated code tooyour new site.</span></span>

### <a name="create-a-new-mobile-app"></a><span data-ttu-id="f5045-164">Een nieuwe mobiele App maken</span><span class="sxs-lookup"><span data-stu-id="f5045-164">Create a new Mobile App</span></span>
1. <span data-ttu-id="f5045-165">Aanmelden op Hallo [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="f5045-165">Log in at hello [Azure Portal].</span></span>
2. <span data-ttu-id="f5045-166">Klik op **+NIEUW** > **Web en mobiel** > **Mobile App** en geef een naam op voor de nieuwe back-end van Mobile App.</span><span class="sxs-lookup"><span data-stu-id="f5045-166">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="f5045-167">Voor Hallo **resourcegroep**, selecteer een bestaande resourcegroep of maak een nieuwe (Hallo met behulp van dezelfde naam als uw app).</span><span class="sxs-lookup"><span data-stu-id="f5045-167">For hello **Resource Group**, select an existing resource group, or create a new one (using hello same name as your app.)</span></span>

    <span data-ttu-id="f5045-168">U kunt ofwel een ander App Service-abonnement selecteren of een nieuw maken.</span><span class="sxs-lookup"><span data-stu-id="f5045-168">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="f5045-169">Voor meer informatie over het plannen van de App-Services en hoe een nieuw plan in een andere prijscategorie toocreate servicetier en op de gewenste locatie, Zie [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5045-169">For more about App Services plans and how toocreate a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="f5045-170">Voor Hallo **App Service-abonnement**, Hallo standaardabonnement (in Hallo [standaardcategorie](https://azure.microsoft.com/pricing/details/app-service/)) is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f5045-170">For hello **App Service plan**, hello default plan (in hello [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="f5045-171">U kunt ook een ander abonnement selecteren of [een nieuw abonnement maken](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="f5045-171">You can also  select a different plan, or [create a new one](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="f5045-172">Hallo App Service-abonnement instellingen bepalen Hallo [locatie, functies, kosten en rekenresources](https://azure.microsoft.com/pricing/details/app-service/) die zijn gekoppeld aan uw app.</span><span class="sxs-lookup"><span data-stu-id="f5045-172">hello App Service plan's settings determine hello [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span>

    <span data-ttu-id="f5045-173">Nadat u op Hallo plan besluit, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f5045-173">After you decide on hello plan, click **Create**.</span></span> <span data-ttu-id="f5045-174">Hiermee maakt u back-end van Hallo mobiele App.</span><span class="sxs-lookup"><span data-stu-id="f5045-174">This creates hello Mobile App backend.</span></span>

### <a name="run-createviewssql"></a><span data-ttu-id="f5045-175">CreateViews.SQL uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f5045-175">Run CreateViews.SQL</span></span>
<span data-ttu-id="f5045-176">Hallo gegenereerde app bevat een bestand met de naam `createViews.sql`.</span><span class="sxs-lookup"><span data-stu-id="f5045-176">hello scaffolded app contains a file called `createViews.sql`.</span></span>  <span data-ttu-id="f5045-177">Dit script moet worden uitgevoerd met de doeldatabase.</span><span class="sxs-lookup"><span data-stu-id="f5045-177">This script must be executed against the target database.</span></span>  <span data-ttu-id="f5045-178">Hallo-verbindingsreeks voor de doeldatabase Hallo kan worden verkregen van de gemigreerde mobiele service uit Hallo **instellingen** blade onder **verbindingsreeksen**.</span><span class="sxs-lookup"><span data-stu-id="f5045-178">hello connection string for hello target database can be obtained from your migrated mobile service from hello **Settings** blade under **Connection Strings**.</span></span>  <span data-ttu-id="f5045-179">Dit sjabloon heet `MS_TableConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="f5045-179">It is named `MS_TableConnectionString`.</span></span>

<span data-ttu-id="f5045-180">U kunt dit script in SQL Server Management Studio of Visual Studio kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f5045-180">You can run this script from within SQL Server Management Studio or Visual Studio.</span></span>

### <a name="link-hello-database-tooyour-app-service"></a><span data-ttu-id="f5045-181">Koppeling Hallo Database tooyour App Service</span><span class="sxs-lookup"><span data-stu-id="f5045-181">Link hello Database tooyour App Service</span></span>
<span data-ttu-id="f5045-182">Koppeling Hallo bestaande database tooyour App Service:</span><span class="sxs-lookup"><span data-stu-id="f5045-182">Link hello existing database tooyour App Service:</span></span>

* <span data-ttu-id="f5045-183">In Hallo [Azure Portal], opent u uw App Service.</span><span class="sxs-lookup"><span data-stu-id="f5045-183">In hello [Azure Portal], open your App Service.</span></span>
* <span data-ttu-id="f5045-184">Selecteer **alle instellingen** -> **gegevensverbindingen**.</span><span class="sxs-lookup"><span data-stu-id="f5045-184">Select **All Settings** -> **Data Connections**.</span></span>
* <span data-ttu-id="f5045-185">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f5045-185">Click on **+ Add**.</span></span>
* <span data-ttu-id="f5045-186">Selecteer in de vervolgkeuzelijst hello, **SQL-Database**</span><span class="sxs-lookup"><span data-stu-id="f5045-186">In hello drop-down, select **SQL Database**</span></span>
* <span data-ttu-id="f5045-187">Onder **SQL-Database**, selecteer uw bestaande database en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f5045-187">Under **SQL Database**, select your existing database, then click on **Select**.</span></span>
* <span data-ttu-id="f5045-188">Onder **verbindingsreeks**, Hallo gebruikersnaam en wachtwoord invoeren voor Hallo-database en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f5045-188">Under **Connection string**, enter hello username and password for hello database, then click on **OK**.</span></span>
* <span data-ttu-id="f5045-189">In Hallo **gegevensverbindingen toevoegen** blade, klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f5045-189">In hello **Add data connections** blade, click on **OK**.</span></span>

<span data-ttu-id="f5045-190">Hallo-gebruikersnaam en wachtwoord vindt door bekijkt hello verbindingsreeks voor de doeldatabase Hallo in uw gemigreerde Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="f5045-190">hello username and password can be found by viewing hello Connection String for hello target database in your migrated Mobile Service.</span></span>

### <a name="set-up-authentication"></a><span data-ttu-id="f5045-191">Verificatie instellen</span><span class="sxs-lookup"><span data-stu-id="f5045-191">Set up authentication</span></span>
<span data-ttu-id="f5045-192">Mobiele Apps van Azure kunt u de Azure Active Directory, Facebook, Google, Microsoft en Twitter verificatie tooconfigure binnen Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="f5045-192">Azure Mobile Apps allows you tooconfigure Azure Active Directory, Facebook, Google, Microsoft and Twitter authentication within hello service.</span></span>  <span data-ttu-id="f5045-193">Aangepaste verificatie moet toobe afzonderlijk ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="f5045-193">Custom authentication will need toobe developed separately.</span></span>  <span data-ttu-id="f5045-194">Raadpleeg de Hallo [Authenticatieconcepten] documentatie en [verificatie Quick Start] documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f5045-194">Refer to hello [Authentication Concepts] documentation and [Authentication Quickstart] documentation for more information.</span></span>  

## <span data-ttu-id="f5045-195"><a name="updating-clients"></a>Mobiele clients bijwerken</span><span class="sxs-lookup"><span data-stu-id="f5045-195"><a name="updating-clients"></a>Update Mobile clients</span></span>
<span data-ttu-id="f5045-196">Zodra u een operationele back-end voor mobiele apps hebt, kunt u werken op een nieuwe versie van uw clienttoepassing waarin deze worden verbruikt.</span><span class="sxs-lookup"><span data-stu-id="f5045-196">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="f5045-197">Mobile Apps bevat ook een nieuwe versie van Hallo client-SDK's en vergelijkbare toohello serverupgrade hierboven, moet u tooremove alle verwijzingen toohello Mobile Services SDK's voordat de installatie van de Mobile Apps-versies.</span><span class="sxs-lookup"><span data-stu-id="f5045-197">Mobile Apps also includes a new version of hello client SDKs, and similar toohello server upgrade above, you will need tooremove all references toohello Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="f5045-198">Een van de belangrijkste wijzigingen Hallo tussen versies Hallo is dat Hallo constructors niet langer zijn vereist voor de sleutel van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="f5045-198">One of hello main changes between hello versions is that hello constructors no longer require an application key.</span></span>
<span data-ttu-id="f5045-199">U nu doorgeven gewoon Hallo-URL van uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="f5045-199">You now simply pass in hello URL of your Mobile App.</span></span> <span data-ttu-id="f5045-200">Bijvoorbeeld: op Hallo .NET-clients, Hallo `MobileServiceClient` constructor is nu:</span><span class="sxs-lookup"><span data-stu-id="f5045-200">For example, on hello .NET clients, hello `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

<span data-ttu-id="f5045-201">U kunt lezen over het installeren van Hallo nieuwe SDK's en het gebruik van de nieuwe structuur Hallo via de onderstaande koppelingen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="f5045-201">You can read about installing hello new SDKs and using hello new structure via hello links below:</span></span>

* [<span data-ttu-id="f5045-202">Android versie 2.2 of hoger</span><span class="sxs-lookup"><span data-stu-id="f5045-202">Android version 2.2 or later</span></span>](app-service-mobile-android-how-to-use-client-library.md)
* [<span data-ttu-id="f5045-203">iOS-versie 3.0.0 of hoger</span><span class="sxs-lookup"><span data-stu-id="f5045-203">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="f5045-204">.NET (Windows/Xamarin) versie 2.0.0 of hoger</span><span class="sxs-lookup"><span data-stu-id="f5045-204">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)
* [<span data-ttu-id="f5045-205">Apache Cordova-versie 2.0 of hoger</span><span class="sxs-lookup"><span data-stu-id="f5045-205">Apache Cordova version 2.0 or later</span></span>](app-service-mobile-cordova-how-to-use-client-library.md)

<span data-ttu-id="f5045-206">Als uw toepassing maakt gebruik van pushmeldingen, noteer Hallo specifieke registratie-instructies voor elk platform, zijn omdat er er enkele wijzigingen ook.</span><span class="sxs-lookup"><span data-stu-id="f5045-206">If your application makes use of push notifications, make note of hello specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="f5045-207">Wanneer u Hallo nieuwe clientversie gereed hebt, try it out in op basis van uw project bijgewerkte server.</span><span class="sxs-lookup"><span data-stu-id="f5045-207">When you have hello new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="f5045-208">Na de validatie of deze werkt, kunt u een nieuwe versie van uw toepassing toocustomers vrijgeven.</span><span class="sxs-lookup"><span data-stu-id="f5045-208">After validating that it works, you can release a new version of your application toocustomers.</span></span> <span data-ttu-id="f5045-209">Zodra uw klanten hebben al een kans tooreceive deze updates, kunt u uiteindelijk Hallo Mobile Services versie van uw app verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f5045-209">Eventually, once your customers have had a chance tooreceive these updates, you can delete hello Mobile Services version of your app.</span></span> <span data-ttu-id="f5045-210">Op dit moment hebt u volledig tooan App Service-mobiele App bijgewerkt met behulp van Hallo nieuwste Mobile Apps server SDK.</span><span class="sxs-lookup"><span data-stu-id="f5045-210">At this point, you have completely upgraded tooan App Service Mobile App using hello latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

[Azure Portal]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[wat zijn Mobile Apps?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[App Service-prijzen]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Authenticatieconcepten]: ../app-service/app-service-authentication-overview.md
[verificatie Quick Start]: app-service-mobile-auth.md

[Azure Portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
