---
title: een ASP.NET MVC 5 aaaDeploy mobiele web-app in Azure App Service
description: Een zelfstudie waarmee u leert u hoe een web-app tooAzure App Service met behulp van mobiele toodeploy functies in ASP.NET MVC 5-webtoepassing.
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="83ef8-103">Een ASP.NET MVC 5 mobiele web-app in Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="83ef8-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="83ef8-104">Deze zelfstudie leert u basisprincipes van hoe een ASP.NET MVC 5 toobuild web-app die mobiele apparaten geschikte Hallo en tooAzure App Service implementeren.</span><span class="sxs-lookup"><span data-stu-id="83ef8-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="83ef8-105">Voor deze zelfstudie, moet u [Visual Studio Express 2013 for Web] [ Visual Studio Express 2013] of Hallo professional edition van Visual Studio als u die hebt.</span><span class="sxs-lookup"><span data-stu-id="83ef8-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="83ef8-106">U kunt [Visual Studio 2015] maar Hallo schermopnamen afwijken en moet u Hallo ASP.NET 4.x-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="83ef8-107">Wat u moet bouwen</span><span class="sxs-lookup"><span data-stu-id="83ef8-107">What You'll Build</span></span>
<span data-ttu-id="83ef8-108">Voor deze zelfstudie, voegt u functies voor mobiele toohello eenvoudige conferentie aanbieding toepassing die opgegeven in Hallo [starter project][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="83ef8-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="83ef8-109">Hallo volgende schermafbeelding ziet u Hallo ASP.NET-sessies in de toepassing hello voltooid, zoals te zien is in de browser-emulator Hallo in Internet Explorer 11 F12-hulpprogramma's voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="83ef8-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="83ef8-110">Kunt u Internet Explorer 11 F12 Hallo-hulpprogramma's voor ontwikkelaars en Hallo [Fiddler hulpprogramma] [ Fiddler] toohelp opsporen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="83ef8-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="83ef8-111">U leert vaardigheden</span><span class="sxs-lookup"><span data-stu-id="83ef8-111">Skills You'll Learn</span></span>
<span data-ttu-id="83ef8-112">Dit is wat u leert:</span><span class="sxs-lookup"><span data-stu-id="83ef8-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="83ef8-113">Hoe toouse Visual Studio 2013 toopublish uw webtoepassing rechtstreeks tooa web-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="83ef8-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="83ef8-114">Hoe sjablonen Hallo ASP.NET MVC 5 Hallo CSS Bootstrap framework gebruiken voor het verbeteren van de weergave op mobiele apparaten</span><span class="sxs-lookup"><span data-stu-id="83ef8-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="83ef8-115">Hoe toocreate mobiele-specifieke tootarget specifieke mobiele browsers, zoals Hallo iPhone- en Android-weergaven</span><span class="sxs-lookup"><span data-stu-id="83ef8-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="83ef8-116">Hoe toocreate responsief weergaven (weergaven die toodifferent browsers op apparaten reageren)</span><span class="sxs-lookup"><span data-stu-id="83ef8-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="83ef8-117">Hallo-ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="83ef8-117">Set up hello development environment</span></span>
<span data-ttu-id="83ef8-118">Uw ontwikkelomgeving instellen door het installeren van hello Azure SDK voor .NET 2.5.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="83ef8-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="83ef8-119">tooinstall hello Azure SDK voor .NET, klik op onderstaande koppeling voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="83ef8-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="83ef8-120">Als u geen Visual Studio 2013 nog is geïnstalleerd, wordt deze door een koppeling Hallo geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="83ef8-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="83ef8-121">Deze zelfstudie vereist de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="83ef8-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="83ef8-122">[Azure SDK voor Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="83ef8-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="83ef8-123">Op het Web Platform Installer venster Hallo **installeren** te gaan met Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="83ef8-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="83ef8-124">U moet ook een browser mobiele emulator.</span><span class="sxs-lookup"><span data-stu-id="83ef8-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="83ef8-125">Geen van de volgende Hallo werkt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-125">Any of hello following will work:</span></span>

* <span data-ttu-id="83ef8-126">Browser-Emulator in [Internet Explorer 11 F12 ontwikkelhulpprogramma's] [ EmulatorIE11] (gebruikt in alle mobiele browser schermafbeeldingen).</span><span class="sxs-lookup"><span data-stu-id="83ef8-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="83ef8-127">Deze heeft gebruiker agent tekenreeks standaardinstellingen voor Windows Phone 8, Windows Phone 7 en Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="83ef8-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="83ef8-128">Browser-Emulator in [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="83ef8-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="83ef8-129">Deze bevat standaardinstellingen voor talloze Android-apparaten, evenals Apple iPhone, iPad Apple en Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="83ef8-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="83ef8-130">Het emuleert touch-gebeurtenissen ook.</span><span class="sxs-lookup"><span data-stu-id="83ef8-130">It also emulates touch events.</span></span>
* <span data-ttu-id="83ef8-131">[Opera mobiele Emulator][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="83ef8-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="83ef8-132">Visual Studio-projecten met C\# broncode tooaccompany beschikbaar zijn in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="83ef8-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="83ef8-133">[Download voor Starter-project][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="83ef8-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="83ef8-134">[Download voor project voltooid][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="83ef8-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="83ef8-135"><a name="bkmk_DeployStarterProject"></a>Hallo starter project tooan Azure-web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="83ef8-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="83ef8-136">Hallo conferentie aanbieding toepassing downloaden [starter project][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="83ef8-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="83ef8-137">Klik in Windows Verkenner met de rechtermuisknop op Hallo gedownloade ZIP-bestand en kies *eigenschappen*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="83ef8-138">In Hallo **eigenschappen** dialoogvenster Kies Hallo **blokkering** knop.</span><span class="sxs-lookup"><span data-stu-id="83ef8-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="83ef8-139">(Deblokkering wordt voorkomen dat een beveiligingswaarschuwing die optreedt wanneer u toouse probeert een *.zip* -bestand dat u hebt gedownload vanuit web Hallo.)</span><span class="sxs-lookup"><span data-stu-id="83ef8-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="83ef8-140">Met de rechtermuisknop op Hallo ZIP-bestand en selecteer **Alles uitpakken** Hallo-bestand uitpakken.</span><span class="sxs-lookup"><span data-stu-id="83ef8-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="83ef8-141">Open in Visual Studio Hallo *C#\Mvc5Mobile.sln* bestand.</span><span class="sxs-lookup"><span data-stu-id="83ef8-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="83ef8-142">Klik in Solution Explorer met de rechtermuisknop op het Hallo-project en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="83ef8-143">Klik in het Web publiceren op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="83ef8-144">Als u nog niet al aangemeld bij Azure, klikt u op **account toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="83ef8-145">Ga als volgt Hallo prompts toolog in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="83ef8-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="83ef8-146">Hallo dialoogvenster App Service wordt nu u weergegeven, zoals aangemeld.</span><span class="sxs-lookup"><span data-stu-id="83ef8-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="83ef8-147">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="83ef8-148">In Hallo **Web-Appnaam** veld, geeft u een unieke app-voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="83ef8-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="83ef8-149">De naam van uw volledige web-app worden  *&lt;voorvoegsel >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="83ef8-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="83ef8-150">Ook selecteren of geef een nieuwe Resourcegroepnaam in **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="83ef8-151">Klik vervolgens op **nieuw** toocreate een nieuw App Service-plan.</span><span class="sxs-lookup"><span data-stu-id="83ef8-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="83ef8-152">Hallo nieuwe App Service-abonnement configureren en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="83ef8-153">Klik op terug in het dialoogvenster Create App Service Hallo, **maken**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="83ef8-154">Nadat hello Azure-resources zijn gemaakt, wordt met instellingen voor uw nieuwe app Hallo Hallo webpublicatie dialoogvenster ingevuld.</span><span class="sxs-lookup"><span data-stu-id="83ef8-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="83ef8-155">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="83ef8-156">Als Visual Studio is voltooid publishing Hallo starter-project toohello Azure-web-app, open Hallo bureaublad browser toodisplay Hallo live web-app.</span><span class="sxs-lookup"><span data-stu-id="83ef8-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="83ef8-157">Start uw browser mobiele emulator, Hallo-URL voor Hallo conferentie toepassing kopiëren (*<prefix>*. azurewebsites.net) in de emulator hello, en klik op de knop rechts bovenaan en selecteer **bladeren door de tag**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="83ef8-158">Als u van Internet Explorer 11 als standaardbrowser hello gebruikmaakt, hoeft u alleen tootype `F12`, klikt u vervolgens `Ctrl+8`, en wijzig vervolgens de browser-profiel op Hallo te**Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="83ef8-159">De onderstaande afbeelding ziet u Hallo *AllTags* weergeven in de modus Staand (wordt gekozen door **bladeren door de tag**).</span><span class="sxs-lookup"><span data-stu-id="83ef8-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="83ef8-160">Terwijl u fouten in uw MVC 5-toepassingen vanuit Visual Studio opsporen kunt, kunt u uw web-app tooAzure publiceren opnieuw tooverify Hallo live web-app rechtstreeks vanuit uw mobiele browser of een browser-emulator.</span><span class="sxs-lookup"><span data-stu-id="83ef8-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="83ef8-161">Hallo-weergave is erg leesbaar op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="83ef8-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="83ef8-162">U ziet ook al enkele Hallo visual effecten toegepast door Hallo Bootstrap CSS-framework.</span><span class="sxs-lookup"><span data-stu-id="83ef8-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="83ef8-163">Klik op Hallo **ASP.NET** koppeling.</span><span class="sxs-lookup"><span data-stu-id="83ef8-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="83ef8-164">Hallo ASP.NET tag weergave is zoomen gemonteerd toohello-scherm Bootstrap automatisch voor u gebeurt.</span><span class="sxs-lookup"><span data-stu-id="83ef8-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="83ef8-165">U kunt echter deze weergave toobetter gesorteerde Hallo mobiele browser verbeteren.</span><span class="sxs-lookup"><span data-stu-id="83ef8-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="83ef8-166">Bijvoorbeeld, Hallo **datum** kolom moeilijk leesbaar is.</span><span class="sxs-lookup"><span data-stu-id="83ef8-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="83ef8-167">Later in de zelfstudie Hallo wijzigt u Hallo *AllTags* toomake weergeven deze mobiele apparaten geschikte.</span><span class="sxs-lookup"><span data-stu-id="83ef8-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="83ef8-168"><a name="bkmk_bootstrap"></a>Bootstrap CSS-Framework</span><span class="sxs-lookup"><span data-stu-id="83ef8-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="83ef8-169">Sjabloon is nieuw in Hallo MVC 5 ingebouwde Bootstrap ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="83ef8-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="83ef8-170">U hebt al gezien hoe deze verschillende weergaven in uw toepassing hello onmiddellijk verbetert.</span><span class="sxs-lookup"><span data-stu-id="83ef8-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="83ef8-171">Hallo-navigatiebalk bovenaan Hallo is automatisch samenvouwbare Hallo browser breedte kleiner is.</span><span class="sxs-lookup"><span data-stu-id="83ef8-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="83ef8-172">Wijzig het formaat van het browservenster Hallo op Hallo bureaublad browser, en zien hoe de navigatiebalk Hallo verandert het uiterlijk.</span><span class="sxs-lookup"><span data-stu-id="83ef8-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="83ef8-173">Dit is Hallo responsief ontwerp die is ingebouwd in de Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="83ef8-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="83ef8-174">toosee hoe Hallo Web-app eruit zonder Bootstrap, open *App\_Start\\BundleConfig.cs* en uitcommentarieer Hallo regels met *bootstrap.js* en *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="83ef8-175">Hallo volgende code toont Hallo laatste twee instructies Hallo `RegisterBundles` methode na Hallo wijziging:</span><span class="sxs-lookup"><span data-stu-id="83ef8-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="83ef8-176">Druk op `Ctrl+F5` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="83ef8-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="83ef8-177">Houd rekening met dat deze Hallo samenvouwbare navigatiebalk is nu alleen een gewone niet-geordende lijst.</span><span class="sxs-lookup"><span data-stu-id="83ef8-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="83ef8-178">Klik op **bladeren door de tag** opnieuw in en klik vervolgens op **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="83ef8-179">In de weergave van de mobiele emulator hello ziet u nu dat het is niet meer toohello zoomen gemonteerd scherm en u horizontaal in volgorde toosee Hallo rechterzijde van Hallo tabel schuiven moet.</span><span class="sxs-lookup"><span data-stu-id="83ef8-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="83ef8-180">De wijzigingen ongedaan maken en vernieuwen Hallo mobiele browser tooverify Hallo mobiele apparaten geschikte weer is hersteld.</span><span class="sxs-lookup"><span data-stu-id="83ef8-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="83ef8-181">Bootstrap is niet specifiek tooASP.NET MVC 5 en kunt u profiteren van deze functies in een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="83ef8-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="83ef8-182">Maar is nu ingebouwd in de ASP.NET MVC 5-projectsjabloon, zodat uw MVC 5-webtoepassing van de Bootstrap standaard profiteren kan.</span><span class="sxs-lookup"><span data-stu-id="83ef8-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="83ef8-183">Ga voor meer informatie over Bootstrap toothe [Bootstrap] [ BootstrapSite] site.</span><span class="sxs-lookup"><span data-stu-id="83ef8-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="83ef8-184">In de volgende sectie Hallo ziet u hoe tooprovide mobile browser specifieke weergaven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="83ef8-185"><a name="bkmk_overrideviews"></a>Hallo weergaven, indelingen en gedeeltelijke weergaven overschrijven</span><span class="sxs-lookup"><span data-stu-id="83ef8-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="83ef8-186">U kunt elke weergave (inclusief indelingen en gedeeltelijke weergaven) voor mobiele browsers in het algemeen voor een afzonderlijke mobiele browser of voor een bepaalde browser overschrijven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="83ef8-187">tooprovide een mobiele-specifieke weergeven, kunt u een weergavebestand kopiëren en toevoegen *. Mobiele* toohello bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="83ef8-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="83ef8-188">Bijvoorbeeld een mobiele telefoon toocreate *Index* weergeven, kunt u *weergaven\\Start\\Index.cshtml* naar *weergaven\\Start\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="83ef8-189">In deze sectie maakt u een indelingsbestand mobile-specifieke.</span><span class="sxs-lookup"><span data-stu-id="83ef8-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="83ef8-190">toostart, kopie *weergaven\\gedeelde\\\_Layout.cshtml* naar *weergaven\\gedeelde\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="83ef8-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="83ef8-191">Open  *\_Layout.Mobile.cshtml* en wijzig Hallo titel van **MVC5 toepassing** te**MVC5 toepassing (mobiel)**.</span><span class="sxs-lookup"><span data-stu-id="83ef8-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="83ef8-192">In elk `Html.ActionLink` -aanroep voor navigatiebalk hello, verwijdert u 'Zoeken op' in elke koppeling *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="83ef8-193">Hallo volgende code toont Hallo voltooid `<ul class="nav navbar-nav">` tag van Hallo mobiele indelingsbestand.</span><span class="sxs-lookup"><span data-stu-id="83ef8-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="83ef8-194">Kopiëren Hallo *weergaven\\Start\\AllTags.cshtml* van het bestand in *weergaven\\Start\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="83ef8-195">Open nieuwe Hallo-bestand en wijzig de `<h2>` -element van de 'Labels' te ' labels (M) ':</span><span class="sxs-lookup"><span data-stu-id="83ef8-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="83ef8-196">Blader toohello labels pagina met een bureaublad browser en browser mobiele emulator.</span><span class="sxs-lookup"><span data-stu-id="83ef8-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="83ef8-197">Hallo mobiele browser emulator Hallo bevat twee wijzigingen (titel van Hallo  *\_Layout.Mobile.cshtml* en de titel van Hallo *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="83ef8-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="83ef8-198">Daarentegen Hallo bureaubladweergave niet is gewijzigd (met de titels van  *\_Layout.cshtml* en *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="83ef8-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="83ef8-199"><a name="bkmk_browserviews"></a>Browser-specifieke weergaven maken</span><span class="sxs-lookup"><span data-stu-id="83ef8-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="83ef8-200">Bovendien toomobile-specifieke en bureaublad-specifieke weergaven, kunt u weergaven voor een afzonderlijke browser.</span><span class="sxs-lookup"><span data-stu-id="83ef8-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="83ef8-201">U kunt bijvoorbeeld weergaven die specifiek voor Hallo iPhone- of Android-browser Hallo zijn maken.</span><span class="sxs-lookup"><span data-stu-id="83ef8-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="83ef8-202">In deze sectie maakt u een indeling voor Hallo iPhone browser en een iPhone-versie van Hallo *AllTags* weergeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="83ef8-203">Open Hallo *Global.asax* bestand en voeg Hallo na code toohello onder aan de `Application_Start` methode.</span><span class="sxs-lookup"><span data-stu-id="83ef8-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="83ef8-204">Deze code definieert een nieuwe weergavemodus met de naam 'iPhone' die wordt vergeleken met elke inkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="83ef8-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="83ef8-205">Als de binnenkomende aanvraag Hallo overeenkomt met de voorwaarde die u gedefinieerd (dat wil zeggen, als de gebruikersagent Hallo bevat Hallo tekenreeks 'iPhone'), zoekt ASP.NET MVC weergaven waarvan de naam het achtervoegsel 'iPhone bevat'.</span><span class="sxs-lookup"><span data-stu-id="83ef8-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="83ef8-206">Wanneer toe te voegen mobiele browserspecifieke weergavemodus, zoals voor iPhone- en Android, of tooset Hallo eerste argument te worden`0` (insert Hallo boven aan het Hallo-lijst) toomake ervoor die Hallo browserspecifieke modus heeft voorrang op Hallo mobile-sjabloon (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="83ef8-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="83ef8-207">Als mobile Hallo-sjabloon in plaats daarvan Hallo boven aan het Hallo-lijst is, wordt het via uw beoogde weergavemodus geselecteerd (eerste overeenkomst wins Hallo en Hallo mobiele sjabloon komt overeen met alle mobiele browsers).</span><span class="sxs-lookup"><span data-stu-id="83ef8-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="83ef8-208">Hallo-code, met de rechtermuisknop op `DefaultDisplayMode`, kies **los**, en kies vervolgens `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="83ef8-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="83ef8-209">Hiermee voegt u een verwijzing toothe `System.Web.WebPages` naamruimte, is de locatie de `DisplayModeProvider` en `DefaultDisplayMode` typen zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="83ef8-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="83ef8-210">U kunt ook kunt u alleen handmatig Hallo regel toothe na toevoegen `using` sectie van het Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="83ef8-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="83ef8-211">Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="83ef8-211">Save hello changes.</span></span> <span data-ttu-id="83ef8-212">Kopieer de *weergaven\\gedeelde\\\_Layout.Mobile.cshtml* van het bestand in *weergaven\\gedeelde\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="83ef8-213">Hallo nieuw bestand open en wijzig de titel van Hallo `MVC5 Application (Mobile)` naar `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="83ef8-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="83ef8-214">Kopiëren Hallo *weergaven\\Start\\AllTags.Mobile.cshtml* van het bestand in *weergaven\\Start\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="83ef8-215">Wijzig in nieuw bestand Hallo Hallo `<h2>` element van ' labels (M) ' te 'Tags (iPhone)'.</span><span class="sxs-lookup"><span data-stu-id="83ef8-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="83ef8-216">Hallo-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="83ef8-216">Run hello application.</span></span> <span data-ttu-id="83ef8-217">Voer een emulator mobiele browser, zorg ervoor dat de gebruikersagent te is ingesteld 'iPhone' en blader toohello *AllTags* weergeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="83ef8-218">Als u de emulator Hallo in Internet Explorer 11 F12 ontwikkelhulpprogramma's gebruikt, configureert u emulatie toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="83ef8-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="83ef8-219">Browser-profiel = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="83ef8-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="83ef8-220">Tekenreeks van de gebruikersagent = **aangepast**</span><span class="sxs-lookup"><span data-stu-id="83ef8-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="83ef8-221">Aangepaste tekenreeks = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="83ef8-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="83ef8-222">Hallo volgende schermafbeelding ziet u Hallo *AllTags* weergave die wordt weergegeven in de emulator in Internet Explorer 11 F12 ontwikkelhulpprogramma's met aangepaste tekenreeks gebruikersagent hello (dit is een tekenreeks van de gebruikersagent iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="83ef8-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="83ef8-223">Selecteer in de mobiele browser Hallo Hallo **luidsprekers** koppeling.</span><span class="sxs-lookup"><span data-stu-id="83ef8-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="83ef8-224">Omdat er geen een mobiele weergave (*AllSpeakers.Mobile.cshtml*), Hallo standaard luidsprekers weergeven (*AllSpeakers.cshtml*) is gegenereerd door middel van Hallo mobiele weergave ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="83ef8-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="83ef8-225">Zoals hieronder aangegeven, Hallo titel **MVC5 toepassing (mobiel)** is gedefinieerd in  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="83ef8-226">U kunt een standaard (niet-mobiele) weergave van rendering binnen een mobiele indeling globaal uitschakelen door in te stellen `RequireConsistentDisplayMode` naar `true` in Hallo *weergaven\\\_ViewStart.cshtml* bestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="83ef8-227">Wanneer `RequireConsistentDisplayMode` te is ingesteld,`true`, mobiele Hallo-indeling (*\_Layout.Mobile.cshtml*) wordt alleen gebruikt voor mobiele weergaven (dat wil zeggen wanneer het weergavebestand is van Hallo formulier  ***weergavenaam** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="83ef8-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="83ef8-228">U kunt tooset `RequireConsistentDisplayMode` te`true` als uw mobiele lay-out niet goed met niet-mobiele weergaven werkt.</span><span class="sxs-lookup"><span data-stu-id="83ef8-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="83ef8-229">Hallo schermafbeelding hieronder toont hoe Hallo *luidsprekers* behalve wanneer `RequireConsistentDisplayMode` te is ingesteld,`true` (zonder Hallo tekenreeks '(mobiel)' in hello navigeerbare balk Hallo boven).</span><span class="sxs-lookup"><span data-stu-id="83ef8-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="83ef8-230">U kunt consistent weergavemodus in een bepaalde weergave uitschakelen door in te stellen `RequireConsistentDisplayMode` te`false` in Hallo-bestand voor weergave.</span><span class="sxs-lookup"><span data-stu-id="83ef8-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="83ef8-231">De volgende tekst in Hallo *weergaven\\Start\\AllSpeakers.cshtml* bestand sets `RequireConsistentDisplayMode` te`false`:</span><span class="sxs-lookup"><span data-stu-id="83ef8-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="83ef8-232">In deze sectie we hebt gezien hoe toocreate mobiele indelingen en weergaven en hoe toocreate indelingen en weergaven voor specifieke apparaten, zoals iPhone Hallo.</span><span class="sxs-lookup"><span data-stu-id="83ef8-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="83ef8-233">Hallo belangrijkste voordeel van het Hallo Bootstrap CSS-framework is echter de responsieve indeling, wat betekent dat een enkele opmaakmodel kan worden toegepast op het bureaublad, telefoon en Tablet PC-browsers toocreate een consistent uiterlijk.</span><span class="sxs-lookup"><span data-stu-id="83ef8-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="83ef8-234">In de volgende sectie Hallo ziet u hoe tooleverage toocreate mobiele apparaten geschikte Bootstrap weergaven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="83ef8-235"><a name="bkmk_Improvespeakerslist"></a>Hallo luidsprekers lijst verbeteren</span><span class="sxs-lookup"><span data-stu-id="83ef8-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="83ef8-236">Zoals u zojuist hebt gezien, Hallo *luidsprekers* weergave kan worden gelezen, maar Hallo koppelingen zijn klein en moeilijk tootap op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="83ef8-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="83ef8-237">In deze sectie maakt u Hallo *AllSpeakers* weergave mobiele apparaten geschikte, die grote, gemakkelijk Tik koppelingen worden weergegeven en bevat een zoekopdracht vak tooquickly luidsprekers vinden.</span><span class="sxs-lookup"><span data-stu-id="83ef8-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="83ef8-238">Kunt u Hallo Bootstrap [gekoppelde lijstgroep] [ linked list group] stijlen voor het verbeteren van Hallo *luidsprekers* weergeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="83ef8-239">In *weergaven\\Start\\AllSpeakers.cshtml*, Hallo inhoud van Hallo Razor bestand vervangen door Hallo-code hieronder.</span><span class="sxs-lookup"><span data-stu-id="83ef8-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="83ef8-240">Hallo `class="list-group"` kenmerk in Hallo `<div>` tag geldt de Bootstrap lijst stijlen en Hallo `class="input-group-item"` kenmerk Bootstrap lijst item stijlen tooeach koppeling wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="83ef8-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="83ef8-241">Hallo mobiele browser vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="83ef8-242">Hallo bijgewerkt weergave ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="83ef8-243">Hallo Bootstrap [gekoppelde lijstgroep] [ linked list group] stijlen maakt Hallo hele vak voor elke koppeling geklikt, dit een veel betere gebruikerservaring is.</span><span class="sxs-lookup"><span data-stu-id="83ef8-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="83ef8-244">Overschakelen van toothe bureaublad en bekijk Hallo consistente look gebruiken.</span><span class="sxs-lookup"><span data-stu-id="83ef8-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="83ef8-245">Hallo mobiele browserweergave is verbeterd, is het moeilijk om te navigeren Hallo lange lijst met luidsprekers.</span><span class="sxs-lookup"><span data-stu-id="83ef8-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="83ef8-246">Bootstrap geen biedt een zoekopdracht filter functionaliteit out-of-the-box, maar u kunt deze toevoegen met een paar regels code.</span><span class="sxs-lookup"><span data-stu-id="83ef8-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="83ef8-247">U wordt eerst een zoekopdracht vak toohello weergave toevoegen en vervolgens met JavaScript-code voor filterfunctie Hallo Hallo aansluiten.</span><span class="sxs-lookup"><span data-stu-id="83ef8-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="83ef8-248">In *weergaven\\Start\\AllSpeakers.cshtml*, Voeg een \<formulier\> code direct na Hallo \<h2\> labels, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="83ef8-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="83ef8-249">U ziet dat Hallo `<form>` en `<input>` labels beide Hallo Bootstrap stijlen toegepast toothem hebben.</span><span class="sxs-lookup"><span data-stu-id="83ef8-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="83ef8-250">Hallo `<span>` element voegt een Bootstrap [glyphicon] [ glyphicon] toothe zoekvak.</span><span class="sxs-lookup"><span data-stu-id="83ef8-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="83ef8-251">In Hallo *Scripts* map, Voeg een JavaScript-bestand aangeroepen *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="83ef8-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="83ef8-252">Hallo-bestand openen en plak Hallo code in het volgende:</span><span class="sxs-lookup"><span data-stu-id="83ef8-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="83ef8-253">U moet ook tooinclude filter.js in uw geregistreerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="83ef8-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="83ef8-254">Open *App\_Start\\BundleConfig.cs* en eerste hello-pakketten te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="83ef8-255">Wijzigen van de eerste `bundles.Add` instructie (voor Hallo **jquery** bundel) tooinclude *Scripts\\filter.js*als volgt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="83ef8-256">Hallo **jquery** bundel wordt al weergegeven Hallo standaard  *\_lay-out* weergeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="83ef8-257">Later kunt u gebruikmaken van Hallo dezelfde JavaScript-code tooapply de lijstweergaven filter functionaliteit tooother.</span><span class="sxs-lookup"><span data-stu-id="83ef8-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="83ef8-258">Vernieuw Hallo mobiele browser en ga toohello *AllSpeakers* weergeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="83ef8-259">In het zoekvak typt u 'sc'.</span><span class="sxs-lookup"><span data-stu-id="83ef8-259">In the search box, type "sc".</span></span> <span data-ttu-id="83ef8-260">Hallo luidsprekers lijst moet nu worden gefilterd op basis van de zoekreeks tooyour.</span><span class="sxs-lookup"><span data-stu-id="83ef8-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="83ef8-261"><a name="bkmk_improvetags"></a>Hallo lijst Tags verbeteren</span><span class="sxs-lookup"><span data-stu-id="83ef8-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="83ef8-262">Zoals Hallo *luidsprekers* weergeven, hello *labels* weergave kan worden gelezen, maar Hallo koppelingen zijn kort en moeilijk tootap op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="83ef8-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="83ef8-263">Kunt u Hallo oplossen *labels* weergave Hallo dezelfde manier oplossen van Hallo *luidsprekers* weergeven, als u codewijzigingen Hallo beschreven eerder, maar met de volgende Hallo `Html.ActionLink` syntaxis van de methode in  *Weergaven\\Start\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="83ef8-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="83ef8-264">Hallo vernieuwd bureaublad browser ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="83ef8-265">En Hallo vernieuwd mobiele browser ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="83ef8-266">Als u dat Hallo oorspronkelijke lijstopmaak merkt is er nog steeds mobiele browser Hallo en zich afvragen wat is er gebeurd tooyour nice Bootstrap stijlen, is dit een artefact van uw eerdere actie toocreate mobiele specifieke weergaven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="83ef8-267">Nu dat u Hallo Bootstrap CSS-framework toocreate een responsief ontwerp gebruikt, gaat u head en verwijderen van deze mobiele-specifieke weergaven en Hallo mobiele-specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="83ef8-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="83ef8-268">Wanneer u dit hebt gedaan, wordt vernieuwd mobiele browser Hallo Hallo Bootstrap stijlen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="83ef8-269"><a name="bkmk_improvedates"></a>Hallo lijst datums verbeteren</span><span class="sxs-lookup"><span data-stu-id="83ef8-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="83ef8-270">U kunt de verbeteren Hallo *datums* weergeven zoals verbeterde van Hallo *luidsprekers* en *labels* bekijkt hello codewijzigingen beschreven eerder, maar met de volgende Hallo Alsu`Html.ActionLink` syntaxis van de methode in *weergaven\\Start\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="83ef8-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="83ef8-271">U ontvangt een weergave vernieuwd mobiele browser als volgt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="83ef8-272">U kunt verder verbeteren Hallo *datums* weergeven door te organiseren Hallo datum / tijd-waarden per datum.</span><span class="sxs-lookup"><span data-stu-id="83ef8-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="83ef8-273">Dit kan worden gedaan met Hallo Bootstrap [panelen] [ panels] opmaak.</span><span class="sxs-lookup"><span data-stu-id="83ef8-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="83ef8-274">Vervang de inhoud Hallo Hallo *weergaven\\Start\\AllDates.cshtml* bestand met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="83ef8-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="83ef8-275">Deze code maakt een afzonderlijke `<div class="panel panel-primary">` label voor elke afzonderlijke datum in de lijst Hallo en maakt gebruik van Hallo [gekoppelde lijstgroep] [ linked list group] voor de respectieve koppelingen als voorheen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="83ef8-276">Hier ziet u welke Hallo mobiele browser lijkt wanneer deze code wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="83ef8-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="83ef8-277">Switch toohello bureaublad browser.</span><span class="sxs-lookup"><span data-stu-id="83ef8-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="83ef8-278">Opnieuw, houd er rekening mee Hallo consistent uiterlijk.</span><span class="sxs-lookup"><span data-stu-id="83ef8-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="83ef8-279"><a name="bkmk_improvesessionstable"></a>Hallo SessionsTable weergave verbeteren</span><span class="sxs-lookup"><span data-stu-id="83ef8-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="83ef8-280">In deze sectie maakt u Hallo *SessionsTable* meer mobiele apparaten geschikte weergeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="83ef8-281">Deze wijziging is uitgebreider Hallo eerdere wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="83ef8-282">Tik op Hallo in Hallo mobiele browser **Tag** knop, voert u `asp` in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="83ef8-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="83ef8-283">Tik op Hallo **ASP.NET** koppeling.</span><span class="sxs-lookup"><span data-stu-id="83ef8-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="83ef8-284">Zoals u ziet, is Hallo weergave opgemaakt als een tabel, momenteel ontworpen toobe in Hallo bureaublad browser weergegeven is.</span><span class="sxs-lookup"><span data-stu-id="83ef8-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="83ef8-285">Het is echter iets moeilijk tooread op een mobiele browser.</span><span class="sxs-lookup"><span data-stu-id="83ef8-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="83ef8-286">toofix deze, open *weergaven\\Start\\SessionsTable.cshtml* en vervang Hallo inhoud van het bestand met de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="83ef8-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="83ef8-287">Hallo code doet 3 dingen:</span><span class="sxs-lookup"><span data-stu-id="83ef8-287">hello code does 3 things:</span></span>

* <span data-ttu-id="83ef8-288">maakt gebruik van Hallo Bootstrap [aangepaste gekoppelde lijstgroep] [ custom linked list group] tooformat Hallo sessiegegevens verticaal, zodat deze informatie kan worden gelezen op een mobiele browser (met behulp van klassen, zoals lijst-groep-item-tekst)</span><span class="sxs-lookup"><span data-stu-id="83ef8-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="83ef8-289">van toepassing hello [raster system] [ grid system] toothe lay-out, dus die sessie Hallo-items stroom horizontaal in Hallo bureaublad browser en verticaal in Hallo mobiele browser (met behulp van Hallo col-md-4-klasse)</span><span class="sxs-lookup"><span data-stu-id="83ef8-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="83ef8-290">maakt gebruik van Hallo [responsief hulpprogramma's] [ responsive utilities] verbergen Hallo sessie labels ziet er in Hallo mobiele browser (met behulp van Hallo verborgen xs klasse)</span><span class="sxs-lookup"><span data-stu-id="83ef8-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="83ef8-291">U kunt ook een titel koppeling toogo toohello respectieve sessie tikken.</span><span class="sxs-lookup"><span data-stu-id="83ef8-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="83ef8-292">Hallo in onderstaande afbeelding weerspiegelt Hallo codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="83ef8-293">Hallo Bootstrap rastersysteem die u automatisch toegepast rangschikt de sessies verticaal in Hallo mobiele browser.</span><span class="sxs-lookup"><span data-stu-id="83ef8-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="83ef8-294">U ziet ook Hallo labels worden niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="83ef8-295">Switch toohello bureaublad browser.</span><span class="sxs-lookup"><span data-stu-id="83ef8-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="83ef8-296">Let op Hallo labels worden nu weergegeven in Hallo bureaublad browser.</span><span class="sxs-lookup"><span data-stu-id="83ef8-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="83ef8-297">Bovendien kunt u zien dat Hallo Bootstrap rastersysteem die u toegepast Hallo-items voor sessie in twee kolommen rangschikt.</span><span class="sxs-lookup"><span data-stu-id="83ef8-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="83ef8-298">Als u de browser vergroot, ziet u dat Hallo regeling toothree kolommen is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="83ef8-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="83ef8-299"><a name="bkmk_improvesessionbycode"></a>Hallo SessionByCode weergave verbeteren</span><span class="sxs-lookup"><span data-stu-id="83ef8-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="83ef8-300">Ten slotte kunt u straks Hallo *SessionByCode* toomake weergeven deze mobiele apparaten geschikte.</span><span class="sxs-lookup"><span data-stu-id="83ef8-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="83ef8-301">Tik op Hallo in Hallo mobiele browser **Tag** knop, voert u `asp` in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="83ef8-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="83ef8-302">Tik op Hallo **ASP.NET** koppeling.</span><span class="sxs-lookup"><span data-stu-id="83ef8-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="83ef8-303">Hallo ASP.NET tag-sessies worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83ef8-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="83ef8-304">Kies Hallo **bouwen van één pagina toepassing met ASP.NET en AngularJS** koppeling.</span><span class="sxs-lookup"><span data-stu-id="83ef8-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="83ef8-305">Hallo standaard bureaubladweergave functioneert, maar u kunt Hallo uiterlijk eenvoudig verbeteren met behulp van een aantal onderdelen Bootstrap GUI.</span><span class="sxs-lookup"><span data-stu-id="83ef8-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="83ef8-306">Open *weergaven\\Start\\SessionByCode.cshtml* en vervang Hallo inhoud door Hallo aantekeningen te volgen:</span><span class="sxs-lookup"><span data-stu-id="83ef8-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="83ef8-307">nieuwe markup Hallo Bootstrap panelen opmaak tooimprove Hallo mobiele weergave gebruikt.</span><span class="sxs-lookup"><span data-stu-id="83ef8-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="83ef8-308">Hallo mobiele browser vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="83ef8-309">Hallo geeft volgende afbeelding Hallo codewijzigingen die u zojuist hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="83ef8-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="83ef8-310">Inpakken en controleren</span><span class="sxs-lookup"><span data-stu-id="83ef8-310">Wrap Up and Review</span></span>
<span data-ttu-id="83ef8-311">Deze zelfstudie leert u hoe ASP.NET MVC 5 toodevelop mobiele apparaten geschikte toouse webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="83ef8-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="83ef8-312">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="83ef8-312">These include:</span></span>

* <span data-ttu-id="83ef8-313">Een ASP.NET MVC 5 toepassing tooan App Service-web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="83ef8-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="83ef8-314">Bootstrap toocreate responsief web-indeling gebruiken in uw toepassing MVC 5</span><span class="sxs-lookup"><span data-stu-id="83ef8-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="83ef8-315">Lay-out, weergaven en gedeeltelijke weergaven vervangen globaal en voor een afzonderlijke weergave</span><span class="sxs-lookup"><span data-stu-id="83ef8-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="83ef8-316">Indeling bepalen en gedeeltelijke overschrijven afdwingen met behulp van de `RequireConsistentDisplayMode` eigenschap</span><span class="sxs-lookup"><span data-stu-id="83ef8-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="83ef8-317">Weergaven die zijn gericht op specifieke browsers, zoals Hallo iPhone browser maken</span><span class="sxs-lookup"><span data-stu-id="83ef8-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="83ef8-318">Bootstrap stijlen in Razor code toepassen</span><span class="sxs-lookup"><span data-stu-id="83ef8-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="83ef8-319">Zie ook</span><span class="sxs-lookup"><span data-stu-id="83ef8-319">See Also</span></span>
* [<span data-ttu-id="83ef8-320">9 basisprincipes van responsief ontwerp</span><span class="sxs-lookup"><span data-stu-id="83ef8-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="83ef8-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="83ef8-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="83ef8-322">[Officiële Blog van het Bootstrap][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="83ef8-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="83ef8-323">[Twitter Bootstrap zelfstudie uit zelfstudie Republiek][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="83ef8-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="83ef8-324">[Hallo Bootstrap Playground][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="83ef8-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="83ef8-325">[W3C aanbeveling mobiele Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="83ef8-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="83ef8-326">[W3C Candidate aanbeveling voor query's voor media][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="83ef8-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="83ef8-327">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="83ef8-327">What's changed</span></span>
* <span data-ttu-id="83ef8-328">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="83ef8-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

