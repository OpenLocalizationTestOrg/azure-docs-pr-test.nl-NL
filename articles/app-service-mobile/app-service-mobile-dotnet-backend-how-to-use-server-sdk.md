---
title: aaaHow toowork met back-endserver voor Hallo .NET SDK voor Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toowork met .NET back-endserver SDK Hallo voor Azure App Service Mobile Apps.
keywords: App service, azure app service, mobiele app, mobiele service, schaal, schaalbaar, app-implementatie, azure app-implementatie
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="8719c-104">Werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="8719c-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="8719c-105">Dit onderwerp leest u hoe toouse Hallo .NET back-endserver SDK in de belangrijkste scenario's voor Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="8719c-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="8719c-106">Hello Azure Mobile Apps SDK kunt u werken met mobiele clients van uw ASP.NET-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8719c-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="8719c-107">Hallo [server .NET SDK voor Azure Mobile Apps] [ 2] is open-source op GitHub.</span><span class="sxs-lookup"><span data-stu-id="8719c-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="8719c-108">Hallo-opslagplaats bevat alle broncode inclusief Hallo hele server SDK-eenheid test suite en sommige-voorbeeldprojecten.</span><span class="sxs-lookup"><span data-stu-id="8719c-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="8719c-109">Referentiedocumentatie</span><span class="sxs-lookup"><span data-stu-id="8719c-109">Reference documentation</span></span>
<span data-ttu-id="8719c-110">Hallo-naslagdocumentatie voor Hallo server SDK bevindt zich hier: [Azure Mobile Apps .NET Reference][1].</span><span class="sxs-lookup"><span data-stu-id="8719c-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="8719c-111"><a name="create-app"></a>Procedure: een mobiele App voor .NET-back-end maken</span><span class="sxs-lookup"><span data-stu-id="8719c-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="8719c-112">Als u een nieuw project begint, kunt u een App Service-toepassing met behulp van beide Hallo [Azure-portal] of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8719c-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="8719c-113">U kunt Hallo App Service-toepassing lokaal uitvoeren of Hallo project tooyour cloud-gebaseerde App Service mobiele app publiceren.</span><span class="sxs-lookup"><span data-stu-id="8719c-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="8719c-114">Als u mobiele mogelijkheden tooan bestaand project toevoegen wilt, Zie Hallo [downloaden en te initialiseren Hallo SDK](#install-sdk) sectie.</span><span class="sxs-lookup"><span data-stu-id="8719c-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="8719c-115">Maken van een .NET-backend met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8719c-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="8719c-116">een App Service mobiele back-end toocreate, ofwel Volg Hallo [Quick Start-zelfstudie] [ 3] of als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8719c-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="8719c-117">Terug in Hallo *aan de slag* blade onder **maken van een tabel-API**, kies **C#** als uw **back-endtaal**.</span><span class="sxs-lookup"><span data-stu-id="8719c-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="8719c-118">Klik op **downloaden**, pak de gecomprimeerde project bestanden tooyour lokale computer en open Hallo oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8719c-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="8719c-119">Maken van een .NET-backend met behulp van Visual Studio 2013 en Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="8719c-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="8719c-120">Hallo installeren [Azure SDK voor .NET] [ 4] (versie 2.9.0 of hoger) toocreate een Azure Mobile Apps-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8719c-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="8719c-121">Nadat u Hallo SDK hebt geïnstalleerd, maakt u een ASP.NET-toepassing hello stappen te volgen met:</span><span class="sxs-lookup"><span data-stu-id="8719c-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="8719c-122">Open Hallo **nieuw Project** dialoogvenster (van *bestand* > **nieuw** > **Project wordt gemaakt...** ).</span><span class="sxs-lookup"><span data-stu-id="8719c-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="8719c-123">Vouw **sjablonen** > **Visual C#**, en selecteer **Web**.</span><span class="sxs-lookup"><span data-stu-id="8719c-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="8719c-124">Selecteer **ASP.NET-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="8719c-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="8719c-125">Vul in Hallo projectnaam.</span><span class="sxs-lookup"><span data-stu-id="8719c-125">Fill in hello project name.</span></span> <span data-ttu-id="8719c-126">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8719c-126">Then click **OK**.</span></span>
5. <span data-ttu-id="8719c-127">Onder *ASP.NET 4.5.2-sjabloon sjablonen*, selecteer **mobiele Apps van Azure**.</span><span class="sxs-lookup"><span data-stu-id="8719c-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="8719c-128">Controleer **hosten in de cloud Hallo** toocreate een mobiele back-end in Hallo cloud toowhich kunt u dit project publiceren.</span><span class="sxs-lookup"><span data-stu-id="8719c-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="8719c-129">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8719c-129">Click **OK**.</span></span>

## <span data-ttu-id="8719c-130"><a name="install-sdk"></a>Hoe: downloaden en te initialiseren Hallo SDK</span><span class="sxs-lookup"><span data-stu-id="8719c-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="8719c-131">Hallo SDK is beschikbaar via [NuGet.org]. Dit pakket bevat Hallo basisfunctionaliteit vereist tooget gestart met behulp van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="8719c-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="8719c-132">tooinitialize Hallo SDK, moet u tooperform acties op Hallo **HttpConfiguration** object.</span><span class="sxs-lookup"><span data-stu-id="8719c-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="8719c-133">Hallo SDK installeren</span><span class="sxs-lookup"><span data-stu-id="8719c-133">Install hello SDK</span></span>
<span data-ttu-id="8719c-134">tooinstall hello SDK, klik met de rechtermuisknop op Hallo serverproject in Visual Studio, selecteer **NuGet-pakketten beheren**, zoekt u Hallo [Microsoft.Azure.Mobile.Server] van het pakket en klik vervolgens op  **Installeer**.</span><span class="sxs-lookup"><span data-stu-id="8719c-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="8719c-135"><a name="server-project-setup"></a>Hallo serverproject initialiseren</span><span class="sxs-lookup"><span data-stu-id="8719c-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="8719c-136">Een .NET-back-end-serverproject is geïnitialiseerd vergelijkbare tooother ASP.NET projecten, met inbegrip van een OWIN-Opstartklasse.</span><span class="sxs-lookup"><span data-stu-id="8719c-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="8719c-137">Zorg ervoor dat u verwijst naar de NuGet-pakket Hallo `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="8719c-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="8719c-138">tooadd deze klasse in Visual Studio met de rechtermuisknop op uw server-project en selecteer **toevoegen** >
**Nieuw Item**, klikt u vervolgens **Web**  >  ** Algemene** > **OWIN-Opstartklasse**.</span><span class="sxs-lookup"><span data-stu-id="8719c-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="8719c-139">Een klasse wordt gegenereerd met Hallo kenmerk te volgen:</span><span class="sxs-lookup"><span data-stu-id="8719c-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="8719c-140">In Hallo `Configuration()` methode van uw OWIN-Opstartklasse gebruik een **HttpConfiguration** object tooconfigure hello Azure Mobile Apps-omgeving.</span><span class="sxs-lookup"><span data-stu-id="8719c-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="8719c-141">Hallo volgt initialiseert Hallo serverproject met geen extra functies:</span><span class="sxs-lookup"><span data-stu-id="8719c-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="8719c-142">tooenable afzonderlijke functies, moet u uitbreidingsmethoden aanroepen op Hallo **MobileAppConfiguration** object voordat u **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="8719c-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="8719c-143">Hallo volgende code wordt bijvoorbeeld toegevoegd Hallo standaard routeert tooall API-domeincontrollers die het Hallo-kenmerk `[MobileAppController]` tijdens de initialisatie:</span><span class="sxs-lookup"><span data-stu-id="8719c-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="8719c-144">Hallo server Quick Start vanuit Azure portal aanroepen Hallo **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="8719c-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="8719c-145">Deze equivalente toohello na de installatie:</span><span class="sxs-lookup"><span data-stu-id="8719c-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="8719c-146">Hallo uitbreidingsmethoden zijn:</span><span class="sxs-lookup"><span data-stu-id="8719c-146">hello extension methods used are:</span></span>

* <span data-ttu-id="8719c-147">`AddMobileAppHomeController()`biedt Hallo standaard Azure Mobile Apps-startpagina.</span><span class="sxs-lookup"><span data-stu-id="8719c-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="8719c-148">`MapApiControllers()`aangepaste API biedt voor WebAPI-controllers gedecoreerd worden met Hallo `[MobileAppController]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8719c-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="8719c-149">`AddTables()`bevat een toewijzing van Hallo `/tables` eindpunten tootable domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="8719c-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="8719c-150">`AddTablesWithEntityFramework()`is een korte voorhanden voor toewijzing Hallo `/tables` eindpunten met behulp van Entity Framework op basis van domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="8719c-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="8719c-151">`AddPushNotifications()`biedt een eenvoudige methode voor het registreren van apparaten voor Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="8719c-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="8719c-152">`MapLegacyCrossDomainController()`biedt standaard CORS-headers voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="8719c-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="8719c-153">SDK-extensies</span><span class="sxs-lookup"><span data-stu-id="8719c-153">SDK extensions</span></span>
<span data-ttu-id="8719c-154">Hallo-op basis van het NuGet-extensiepakketten te volgen bieden verschillende mobiele functies die kunnen worden gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8719c-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="8719c-155">U uitbreidingen inschakelen tijdens de initialisatie met Hallo **MobileAppConfiguration** object.</span><span class="sxs-lookup"><span data-stu-id="8719c-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="8719c-156">[Microsoft.Azure.Mobile.Server.Quickstart] ondersteunt Hallo basisinstellingen Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="8719c-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="8719c-157">Toegevoegde toohello configuratie door de aanroepende Hallo **UseDefaultConfiguration** extensiemethode tijdens de initialisatie.</span><span class="sxs-lookup"><span data-stu-id="8719c-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="8719c-158">Deze extensie bevat de volgende extensies: meldingen, verificatie, entiteit, tabellen, verschillende domeinen en thuis-pakketten.</span><span class="sxs-lookup"><span data-stu-id="8719c-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="8719c-159">Dit pakket wordt gebruikt door Hallo Mobile Apps Quick Start op Hallo Azure-portal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8719c-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="8719c-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Hallo standaard implementeert *deze mobiele app is actief en werkend pagina* voor Hallo website hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="8719c-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="8719c-161">Toohello configuratie toevoegen door het aanroepen van de **AddMobileAppHomeController** extensiemethode.</span><span class="sxs-lookup"><span data-stu-id="8719c-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="8719c-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) bevat klassen voor het werken met gegevens en sets-up Hallo data pipeline.</span><span class="sxs-lookup"><span data-stu-id="8719c-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="8719c-163">Toohello configuratie toevoegen door de aanroepende Hallo **AddTables** extensiemethode.</span><span class="sxs-lookup"><span data-stu-id="8719c-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="8719c-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) kunnen Hallo Entity Framework tooaccess gegevens in Hallo SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="8719c-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="8719c-165">Toohello configuratie toevoegen door de aanroepende Hallo **AddTablesWithEntityFramework** extensiemethode.</span><span class="sxs-lookup"><span data-stu-id="8719c-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="8719c-166">[Microsoft.Azure.Mobile.Server.Authentication] schakelt verificatie en sets-up Hallo OWIN middleware toovalidate tokens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8719c-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="8719c-167">Toohello configuratie toevoegen door de aanroepende Hallo **AddAppServiceAuthentication** en **IAppBuilder**. **UseAppServiceAuthentication** uitbreidingsmethoden.</span><span class="sxs-lookup"><span data-stu-id="8719c-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="8719c-168">[Microsoft.Azure.Mobile.Server.Notifications] maakt het mogelijk pushmeldingen en definieert een push-eindpunt voor registratie.</span><span class="sxs-lookup"><span data-stu-id="8719c-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="8719c-169">Toohello configuratie toevoegen door de aanroepende Hallo **AddPushNotifications** extensiemethode.</span><span class="sxs-lookup"><span data-stu-id="8719c-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="8719c-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) maakt u een domeincontroller die gegevens toolegacy webbrowsers vanuit uw mobiele App fungeert.</span><span class="sxs-lookup"><span data-stu-id="8719c-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="8719c-171">Toohello configuratie toevoegen door het aanroepen van de **MapLegacyCrossDomainController** extensiemethode.</span><span class="sxs-lookup"><span data-stu-id="8719c-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="8719c-172">[Microsoft.Azure.Mobile.Server.Login] hello AppServiceLoginHandler.CreateToken() methode, die een statische methode die wordt gebruikt tijdens aangepaste verificatie scenario's biedt.</span><span class="sxs-lookup"><span data-stu-id="8719c-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="8719c-173"><a name="publish-server-project"></a>Hoe: Hallo serverproject publiceren</span><span class="sxs-lookup"><span data-stu-id="8719c-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="8719c-174">Deze sectie leest u hoe toopublish uw .NET-back-end project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8719c-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="8719c-175">U kunt ook uw back endproject met Git implementeren of een van de andere methoden behandeld in Hallo Hallo [Implementatiedocumentatie voor Azure App Service](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8719c-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="8719c-176">In Visual Studio opnieuw worden opgebouwd Hallo project toorestore NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="8719c-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="8719c-177">Klik in Solution Explorer met de rechtermuisknop op Hallo-project op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8719c-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="8719c-178">Hallo moet eerste keer dat u publiceert, u een publicatieprofiel toodefine.</span><span class="sxs-lookup"><span data-stu-id="8719c-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="8719c-179">Wanneer u al een profiel dat is gedefinieerd hebt, kunt u selecteren en op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8719c-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="8719c-180">Als u wordt gevraagd tooselect een doel publiceren, klikt u op **Microsoft Azure App Service** > **volgende**, en (indien nodig) aanmelden met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="8719c-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="8719c-181">Visual Studio downloadt en veilig opgeslagen uw publicatie-instellingen rechtstreeks uit Azure.</span><span class="sxs-lookup"><span data-stu-id="8719c-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="8719c-182">Kies uw **abonnement**, selecteer **brontype** van **weergave**, vouw **mobiele App**, en klikt u op back-end van uw mobiele App en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8719c-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="8719c-183">Controleer of Hallo profielgegevens publiceren en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8719c-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="8719c-184">Als uw back-end voor de mobiele App is gepubliceerd, ziet u een startpagina die slagen aangeeft.</span><span class="sxs-lookup"><span data-stu-id="8719c-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="8719c-185"><a name="define-table-controller"></a>Procedure: een tabel controller definiëren</span><span class="sxs-lookup"><span data-stu-id="8719c-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="8719c-186">Een tabel Controller tooexpose een SQL-tabel toomobile clients definiëren.</span><span class="sxs-lookup"><span data-stu-id="8719c-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="8719c-187">Een tabel Controller configureren, moet drie stappen:</span><span class="sxs-lookup"><span data-stu-id="8719c-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="8719c-188">Maak een klasse gegevens overbrengen Object (DTO).</span><span class="sxs-lookup"><span data-stu-id="8719c-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="8719c-189">Configureer een tabelverwijzing in Hallo Mobile DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="8719c-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="8719c-190">Maak een tabel-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="8719c-190">Create a table controller.</span></span>

<span data-ttu-id="8719c-191">Een Data Transfer Object (DTO) is een gewone C#-object dat eigenschappen van overneemt `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="8719c-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="8719c-192">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8719c-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="8719c-193">Hallo DTO is gebruikte toodefine Hallo tabel binnen Hallo SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8719c-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="8719c-194">Hallo toocreate vermelding van de database, het toevoegen van een `DbSet<>` eigenschap op Hallo van DbContext die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8719c-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="8719c-195">In Hallo project standaardsjabloon voor Azure Mobile Apps hello DbContext heet `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="8719c-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="8719c-196">Als u hello die Azure SDK geïnstalleerd hebt, kunt u een sjabloon tabel controller nu als volgt maken:</span><span class="sxs-lookup"><span data-stu-id="8719c-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="8719c-197">Met de rechtermuisknop op de map Hallo-Controllers en selecteer **toevoegen** > **Controller...** .</span><span class="sxs-lookup"><span data-stu-id="8719c-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="8719c-198">Selecteer Hallo **Azure Mobile Apps tabel Controller** optie en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8719c-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="8719c-199">In Hallo **Controller toevoegen** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="8719c-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="8719c-200">In Hallo **Modelklasse** vervolgkeuzelijst, selecteer uw nieuwe DTO.</span><span class="sxs-lookup"><span data-stu-id="8719c-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="8719c-201">In Hallo **DbContext** vervolgkeuzelijst, selecteer Hallo Mobile Service DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="8719c-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="8719c-202">naam van de domeincontroller Hallo is voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8719c-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="8719c-203">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="8719c-203">Click **Add**.</span></span>

<span data-ttu-id="8719c-204">Hallo Quick Start-serverproject bevat een voorbeeld van een eenvoudige **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="8719c-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="8719c-205"><a name="adjust-pagesize"></a>Hoe: Hallo tabel paginering grootte aanpassen</span><span class="sxs-lookup"><span data-stu-id="8719c-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="8719c-206">Azure Mobile Apps retourneert standaard 50 records per aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8719c-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="8719c-207">Paginering zorgt ervoor dat clientcomputers Hallo komt niet bezighouden hun gebruikersinterface-thread noch Hallo server te lang een goede gebruikerservaring gezorgd.</span><span class="sxs-lookup"><span data-stu-id="8719c-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="8719c-208">toochange hello tabel paginering grootte toename Hallo serverzijde 'toegestane grootte van de query' en hello clientzijde pagina grootte Hallo serverzijde 'toegestane grootte van de query' is aangepast met Hallo `EnableQuery` kenmerk:</span><span class="sxs-lookup"><span data-stu-id="8719c-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="8719c-209">Zorg ervoor Hallo PageSize Hallo dezelfde of een groter is dan Hallo door Hallo-client wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="8719c-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="8719c-210">Raadpleeg toohello specifieke client procedure documentatie voor meer informatie over het wijzigen van het paginaformaat Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="8719c-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="8719c-211">Procedure: een aangepaste API-controller definiëren</span><span class="sxs-lookup"><span data-stu-id="8719c-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="8719c-212">Hallo aangepaste API-controller biedt Hallo meest eenvoudige functionaliteit tooyour backend voor mobiele Apps bij het blootstellen van een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8719c-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="8719c-213">U kunt een API-controller van het mobiele-specifieke met kenmerk [MobileAppController] Hallo registreren.</span><span class="sxs-lookup"><span data-stu-id="8719c-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="8719c-214">Hallo `MobileAppController` kenmerk registreert Hallo route, stelt Hallo Mobile Apps JSON serialisatiefunctie en Hiermee schakelt u [controle van de client versie](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8719c-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="8719c-215">Klik in Visual Studio met de rechtermuisknop op Hallo domeincontrollers map **toevoegen** > **Controller**, selecteer **Web API 2-Controller&mdash;leeg** en Klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8719c-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="8719c-216">Geef een **controllernaam**, zoals `CustomController`, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8719c-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="8719c-217">Voeg toe Hallo volgende Hallo nieuwe controller klassebestand met de instructie:</span><span class="sxs-lookup"><span data-stu-id="8719c-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="8719c-218">Toepassing hello **[MobileAppController]** toohello API-controller klassendefinitie, zoals in het volgende voorbeeld Hallo kenmerk:</span><span class="sxs-lookup"><span data-stu-id="8719c-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="8719c-219">Voeg in App_Start/Startup.MobileApp.cs-bestand, een aanroep van toohello **MapApiControllers** uitbreidingsmethode, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="8719c-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="8719c-220">U kunt ook Hallo `UseDefaultConfiguration()` extensiemethode in plaats van `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="8719c-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="8719c-221">Elke domeincontroller die geen **MobileAppControllerAttribute** toegepast nog steeds toegankelijk zijn voor clients, maar deze kan niet worden correct gebruikt door clients met behulp van een client voor mobiele App SDK.</span><span class="sxs-lookup"><span data-stu-id="8719c-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="8719c-222">Procedure: werken met verificatie</span><span class="sxs-lookup"><span data-stu-id="8719c-222">How to: Work with authentication</span></span>
<span data-ttu-id="8719c-223">Mobiele Apps van Azure maakt gebruik van App Service-verificatie / autorisatie toosecure uw mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="8719c-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="8719c-224">Deze sectie leest u hoe tooperform Hallo na verificatie-gerelateerde taken in uw project met .NET back-end-server:</span><span class="sxs-lookup"><span data-stu-id="8719c-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="8719c-225">Procedure: verificatie tooa serverproject toevoegen</span><span class="sxs-lookup"><span data-stu-id="8719c-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="8719c-226">Procedure: aangepaste verificatie voor uw toepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="8719c-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="8719c-227">Hoe: ophalen geverifieerde gebruikersgegevens</span><span class="sxs-lookup"><span data-stu-id="8719c-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="8719c-228">Hoe: beperken van toegang tot gegevens voor gemachtigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="8719c-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="8719c-229"><a name="add-auth"></a>Procedure: verificatie tooa serverproject toevoegen</span><span class="sxs-lookup"><span data-stu-id="8719c-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="8719c-230">U kunt verificatie tooyour serverproject toevoegen door uit te breiden Hallo **MobileAppConfiguration** object en OWIN middleware configureren.</span><span class="sxs-lookup"><span data-stu-id="8719c-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="8719c-231">Wanneer u Hallo installeert [Microsoft.Azure.Mobile.Server.Quickstart] pakket en aanroep Hallo **UseDefaultConfiguration** uitbreidingsmethode, kunt u toostep 3 overslaan.</span><span class="sxs-lookup"><span data-stu-id="8719c-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="8719c-232">In Visual Studio, installeert u Hallo [Microsoft.Azure.Mobile.Server.Authentication] pakket.</span><span class="sxs-lookup"><span data-stu-id="8719c-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="8719c-233">Voeg volgende regel code aan begin Hallo HALLO hallo in Hallo Startup.cs project-bestand **configuratie** methode:</span><span class="sxs-lookup"><span data-stu-id="8719c-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="8719c-234">Dit onderdeel OWIN-middleware valideert tokens die zijn uitgegeven door App Service-gateway Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8719c-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="8719c-235">Hallo toevoegen `[Authorize]` kenmerk tooany controller of methode die verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="8719c-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="8719c-236">toolearn over het tooauthenticate clients tooyour back-end van Mobile Apps Zie [toevoegen verificatie tooyour app](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="8719c-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="8719c-237"><a name="custom-auth"></a>Procedure: aangepaste verificatie voor uw toepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="8719c-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="8719c-238">Als u niet dat toouse een van de App Service-verificatie/autorisatie-providers hello wenst, kunt u uw eigen systeem aanmelding implementeren.</span><span class="sxs-lookup"><span data-stu-id="8719c-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="8719c-239">Hallo installeren [Microsoft.Azure.Mobile.Server.Login] tooassist met verificatie token genereren van het pakket.</span><span class="sxs-lookup"><span data-stu-id="8719c-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="8719c-240">Geef uw eigen code voor het valideren van gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="8719c-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="8719c-241">U kunt bijvoorbeeld controleren tegen gezouten en hash-wachtwoorden in een database.</span><span class="sxs-lookup"><span data-stu-id="8719c-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="8719c-242">Hallo in Hallo onderstaand voorbeeld `isValidAssertion()` methode (elders gedefinieerd) is verantwoordelijk voor deze controles.</span><span class="sxs-lookup"><span data-stu-id="8719c-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="8719c-243">Hallo aangepaste verificatie wordt blootgelegd door een ApiController maken en blootstellen `register` en `login` acties.</span><span class="sxs-lookup"><span data-stu-id="8719c-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="8719c-244">Hallo-client moet een aangepaste UI toocollect Hallo-informatie van Hallo-gebruiker gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8719c-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="8719c-245">Hallo-informatie wordt verzonden toohello API met een standaard HTTP POST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="8719c-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="8719c-246">Zodra het Hallo-server valideert Hallo verklaring, een token is uitgegeven met Hallo `AppServiceLoginHandler.CreateToken()` methode.</span><span class="sxs-lookup"><span data-stu-id="8719c-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="8719c-247">Hallo ApiController **beter niet** hello gebruiken `[MobileAppController]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8719c-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="8719c-248">Een voorbeeld `login` actie:</span><span class="sxs-lookup"><span data-stu-id="8719c-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="8719c-249">In de Hallo voorgaande voorbeeld, zijn LoginResult en LoginResultUser serialiseerbaar objecten blootstellen vereiste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="8719c-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="8719c-250">Hallo client verwacht aanmelding antwoorden toobe geretourneerd als JSON-objecten van het formulier Hallo:</span><span class="sxs-lookup"><span data-stu-id="8719c-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="8719c-251">Hallo `AppServiceLoginHandler.CreateToken()` methode bevat een *doelgroep* en een *verlener* parameter.</span><span class="sxs-lookup"><span data-stu-id="8719c-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="8719c-252">Beide parameters zijn toohello-URL van de hoofdmap van uw toepassing met behulp van HTTPS-schema Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8719c-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="8719c-253">U moet op dezelfde manier instellen *secretKey* toobe Hallo-waarde van uw toepassing de handtekeningsleutel.</span><span class="sxs-lookup"><span data-stu-id="8719c-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="8719c-254">Hallo ondertekening sleutel in een client kan worden gebruikt toomint sleutels en gebruikers te imiteren niet distribueren.</span><span class="sxs-lookup"><span data-stu-id="8719c-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="8719c-255">Kunt u de handtekeningsleutel terwijl die in App Service wordt gehost door te verwijzen naar Hallo Hallo *WEBSITE\_AUTH\_ondertekening\_sleutel* omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="8719c-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="8719c-256">Indien nodig in de context van een lokale foutopsporing, volgt u de instructies Hallo in Hallo [lokale foutopsporing met verificatie](#local-debug) sectie tooretrieve Hallo sleutel en op te slaan als een toepassingsinstelling.</span><span class="sxs-lookup"><span data-stu-id="8719c-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="8719c-257">Hallo uitgegeven token mogelijk ook andere claims en een vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="8719c-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="8719c-258">Minimaal Hallo uitgegeven token vergezeld gaan van een onderwerp (**sub**) claim.</span><span class="sxs-lookup"><span data-stu-id="8719c-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="8719c-259">U kunt standaard client Hallo ondersteunen `loginAsync()` methode door Hallo verificatie route overbelasting.</span><span class="sxs-lookup"><span data-stu-id="8719c-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="8719c-260">Als de client Hallo aanroept `client.loginAsync('custom');` toolog in uw route moet `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="8719c-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="8719c-261">U kunt instellen Hallo route voor het gebruik van Hallo aangepaste verificatie controller `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="8719c-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="8719c-262">Met behulp van Hallo `loginAsync()` aanpak zorgt ervoor dat Hallo-verificatietoken is gekoppeld tooevery volgende aanroep toohello service.</span><span class="sxs-lookup"><span data-stu-id="8719c-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="8719c-263"><a name="user-info"></a>Hoe: ophalen geverifieerde gebruikersgegevens</span><span class="sxs-lookup"><span data-stu-id="8719c-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="8719c-264">Wanneer een gebruiker is geverifieerd door App Service, kunt u toegang tot Hallo toegewezen gebruikers-ID en andere informatie die in uw .NET-back-end-code.</span><span class="sxs-lookup"><span data-stu-id="8719c-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="8719c-265">Hallo gebruikersgegevens kan worden gebruikt voor het nemen van autorisatiebeslissingen in Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="8719c-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="8719c-266">Hallo haalt volgende code Hallo gebruikers-ID die is gekoppeld aan een aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8719c-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="8719c-267">Hallo SID is afgeleid van Hallo provider-specifieke gebruikers-ID en statisch voor een bepaalde gebruiker en de aanmeldingsprovider.</span><span class="sxs-lookup"><span data-stu-id="8719c-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="8719c-268">Hallo SID is null voor ongeldige verificatietokens.</span><span class="sxs-lookup"><span data-stu-id="8719c-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="8719c-269">App Service kunt u bepaalde claims aanvragen bij uw aanmeldingsprovider.</span><span class="sxs-lookup"><span data-stu-id="8719c-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="8719c-270">Elke identiteitsprovider krijgt u meer informatie, met behulp van de identiteitsprovider SDK.</span><span class="sxs-lookup"><span data-stu-id="8719c-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="8719c-271">U kunt bijvoorbeeld Hallo Facebook Graph API gebruiken voor vrienden informatie.</span><span class="sxs-lookup"><span data-stu-id="8719c-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="8719c-272">Hallo provider blade in hello Azure-portal kunt u claims die worden aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="8719c-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="8719c-273">Sommige claims nodig aanvullende configuratie met de id-provider Hallo.</span><span class="sxs-lookup"><span data-stu-id="8719c-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="8719c-274">Hallo volgende code aanroepen Hallo **GetAppServiceIdentityAsync** extensie methode tooget Hallo aanmeldingsreferenties, waaronder Hallo toegangsaanvragen token benodigde toomake tegen Hallo Facebook Graph API:</span><span class="sxs-lookup"><span data-stu-id="8719c-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="8719c-275">Toevoegen van een instructie voor `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extensiemethode.</span><span class="sxs-lookup"><span data-stu-id="8719c-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="8719c-276"><a name="authorize"></a>Hoe: beperken van toegang tot gegevens voor gemachtigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="8719c-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="8719c-277">In de vorige sectie hello bleek we hoe tooretrieve Hallo gebruikers-ID van een geverifieerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8719c-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="8719c-278">U kunt beperken toodata toegang en andere bronnen op basis van deze waarde.</span><span class="sxs-lookup"><span data-stu-id="8719c-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="8719c-279">Een kolom userId tootables toe te voegen en het filteren van Hallo queryresultaten door Hallo gebruikers-ID is bijvoorbeeld een eenvoudige manier toolimit gegevens alleen tooauthorized gebruikers geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8719c-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="8719c-280">Hallo retourneert volgende code rijen met gegevens alleen als Hallo SID overeenkomt met de waarde in Hallo UserId kolom in de takentabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="8719c-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="8719c-281">Hallo `Query()` methode retourneert een `IQueryable` die kan worden bewerkt door LINQ toohandle filteren.</span><span class="sxs-lookup"><span data-stu-id="8719c-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="8719c-282">Hoe: push notifications tooa serverproject toevoegen</span><span class="sxs-lookup"><span data-stu-id="8719c-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="8719c-283">Push notifications tooyour serverproject toevoegen door uit te breiden Hallo **MobileAppConfiguration** object en het maken van een client Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="8719c-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="8719c-284">In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**, zoeken naar `Microsoft.Azure.Mobile.Server.Notifications`, klikt u vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="8719c-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="8719c-285">Herhaal deze stap tooinstall hello `Microsoft.Azure.NotificationHubs` pakket, waaronder Hallo Notification Hubs-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="8719c-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="8719c-286">In App_Start/Startup.MobileApp.cs, en voeg een aanroep van toohello **AddPushNotifications()** extensiemethode tijdens de initialisatie:</span><span class="sxs-lookup"><span data-stu-id="8719c-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="8719c-287">Na de code die wordt gemaakt van een client Notification Hubs Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8719c-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="8719c-288">U kunt nu Hallo Notification Hubs toosend push notifications tooregistered clientapparaten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8719c-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="8719c-289">Zie voor meer informatie [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="8719c-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="8719c-290">Zie toolearn meer informatie over Notification Hubs [overzicht van Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8719c-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="8719c-291"><a name="tags"></a>Hoe: Enable gericht push met Tags</span><span class="sxs-lookup"><span data-stu-id="8719c-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="8719c-292">Notification Hubs kunt u toospecific registraties van gerichte meldingen verzenden met behulp van codes.</span><span class="sxs-lookup"><span data-stu-id="8719c-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="8719c-293">Verschillende labels worden automatisch gemaakt:</span><span class="sxs-lookup"><span data-stu-id="8719c-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="8719c-294">Hallo installatie-ID identificeert een specifiek apparaat.</span><span class="sxs-lookup"><span data-stu-id="8719c-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="8719c-295">Hallo gebruikers-Id op basis van Hallo geverifieerde SID identificeert een specifieke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8719c-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="8719c-296">installatie-ID toegankelijk zijn vanuit Hallo Hallo **omwille van** -eigenschap op Hallo **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="8719c-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="8719c-297">Hallo volgende voorbeeld ziet u hoe u een installatie-ID tooadd een tag tooa specifieke installatie in Notification Hubs:</span><span class="sxs-lookup"><span data-stu-id="8719c-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="8719c-298">Labels verstrekt door Hallo client tijdens de registratie voor pushberichten worden genegeerd door Hallo back-end bij het maken van Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="8719c-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="8719c-299">een client tooadd tooenable tags toohello installatie, moet u een aangepaste API gebruiken waarmee labels Hallo vóór het patroon wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8719c-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="8719c-300">Zie [Client toegevoegd push notification-tags] [ 5] in Hallo App Service Mobile Apps voltooide Quick Start-voorbeeld voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8719c-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="8719c-301"><a name="push-user"></a>Hoe: verzenden push notifications tooan geverifieerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="8719c-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="8719c-302">Wanneer een geverifieerde gebruiker geregistreerd voor pushmeldingen, wordt een gebruikers-ID-tag toohello registratie automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8719c-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="8719c-303">Met deze code, kunt u push notifications tooall apparaat hebt geregistreerd met deze persoon verzenden.</span><span class="sxs-lookup"><span data-stu-id="8719c-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="8719c-304">Hallo volgende code wordt Hallo SID van de gebruiker die de aanvraag en verzendt een sjabloon tooevery apparaatregistratie voor pushberichten voor deze persoon:</span><span class="sxs-lookup"><span data-stu-id="8719c-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="8719c-305">Wanneer u registreert voor pushmeldingen vanuit een geverifieerde client, moet u ervoor zorgen dat de verificatie is voltooid voordat u de registratie.</span><span class="sxs-lookup"><span data-stu-id="8719c-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="8719c-306">Zie voor meer informatie [Push toousers] [ 6] in Hallo App Service Mobile Apps voltooide Quick Start-voorbeeld voor .NET-back-end.</span><span class="sxs-lookup"><span data-stu-id="8719c-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="8719c-307">Procedure: fouten opsporen en oplossen van Hallo SDK voor .NET-Server</span><span class="sxs-lookup"><span data-stu-id="8719c-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="8719c-308">Azure App Service biedt verschillende opsporen en oplossen van technieken voor ASP.NET-toepassingen:</span><span class="sxs-lookup"><span data-stu-id="8719c-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="8719c-309">Bewaking van een Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8719c-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="8719c-310">Diagnostische logboekregistratie in Azure App Service inschakelen</span><span class="sxs-lookup"><span data-stu-id="8719c-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="8719c-311">Een Azure App Service in Visual Studio oplossen</span><span class="sxs-lookup"><span data-stu-id="8719c-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="8719c-312">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="8719c-312">Logging</span></span>
<span data-ttu-id="8719c-313">U kunt tooApp Service diagnostische logboeken schrijven met behulp van Hallo standaard ASP.NET trace schrijven.</span><span class="sxs-lookup"><span data-stu-id="8719c-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="8719c-314">Voordat u toohello logboeken schrijven kan, moet u diagnostische gegevens inschakelen in uw back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="8719c-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="8719c-315">tooenable diagnostische gegevens en schrijven toohello Logboeken:</span><span class="sxs-lookup"><span data-stu-id="8719c-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="8719c-316">Volg de stappen Hallo in [hoe diagnostische gegevens tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="8719c-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="8719c-317">Voeg de volgende Hallo in uw codebestand met de instructie:</span><span class="sxs-lookup"><span data-stu-id="8719c-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="8719c-318">Maakt een tracering writer toowrite Hallo .NET backend toohello diagnostische logboeken, als volgt:</span><span class="sxs-lookup"><span data-stu-id="8719c-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="8719c-319">Publiceren van uw serverproject en toegang tot het Hallo mobiele App back-end tooexecute Hallo codepad met de Hallo logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="8719c-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="8719c-320">Downloaden en te evalueren Hallo Logboeken, zoals beschreven in [hoe: Logboeken downloaden](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="8719c-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="8719c-321"><a name="local-debug"></a>Lokale foutopsporing met verificatie</span><span class="sxs-lookup"><span data-stu-id="8719c-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="8719c-322">U kunt uw toepassing uitvoeren lokaal tootest gewijzigd voordat u ze toohello cloud publiceert.</span><span class="sxs-lookup"><span data-stu-id="8719c-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="8719c-323">Druk op voor de meeste Azure Mobile Apps back-ends, *F5* tijdens het in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8719c-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="8719c-324">Er zijn echter enkele aanvullende overwegingen bij het gebruik van verificatie.</span><span class="sxs-lookup"><span data-stu-id="8719c-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="8719c-325">Er moet een cloud-gebaseerde mobiele app met App Service-verificatie/autorisatie geconfigureerd en uw client hello cloudeindpunt opgegeven als Hallo alternatieve aanmeldings-host moet hebben.</span><span class="sxs-lookup"><span data-stu-id="8719c-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="8719c-326">Zie Hallo-documentatie voor uw clientplatform voor Hallo specifieke stappen vereist.</span><span class="sxs-lookup"><span data-stu-id="8719c-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="8719c-327">Zorg ervoor dat uw mobiele back-end [Microsoft.Azure.Mobile.Server.Authentication] geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8719c-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="8719c-328">Voeg in uw toepassing OWIN-Opstartklasse volgende hello, na `MobileAppConfiguration` is toegepaste tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="8719c-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="8719c-329">In de Hallo voorgaande voorbeeld, moet u configureren Hallo *authAudience* en *authIssuer* toepassingsinstellingen binnen uw Web.config bestand tooeach worden de URL van de hoofdmap van uw toepassing hello HTTPS gebruiken schema.</span><span class="sxs-lookup"><span data-stu-id="8719c-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="8719c-330">U moet op dezelfde manier instellen *authSigningKey* toobe Hallo-waarde van uw toepassing de handtekeningsleutel.</span><span class="sxs-lookup"><span data-stu-id="8719c-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="8719c-331">tooobtain hello ondertekeningssleutel:</span><span class="sxs-lookup"><span data-stu-id="8719c-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="8719c-332">Navigeer tooyour app binnen Hallo [Azure-portal]</span><span class="sxs-lookup"><span data-stu-id="8719c-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="8719c-333">Klik op **extra**, **Kudu**, **gaat**.</span><span class="sxs-lookup"><span data-stu-id="8719c-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="8719c-334">Klik op Hallo Kudu Management site **omgeving**.</span><span class="sxs-lookup"><span data-stu-id="8719c-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="8719c-335">Hallo-waarde voor *WEBSITE\_AUTH\_ondertekening\_sleutel*.</span><span class="sxs-lookup"><span data-stu-id="8719c-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="8719c-336">Gebruik Hallo ondertekeningssleutel voor Hallo *authSigningKey* parameter in de configuratie van uw lokale toepassingen.  Uw mobiele back-end is nu ingericht toovalidate tokens bij lokale uitvoering waarin clientcomputers Hallo Hallo token van een cloud-gebaseerde Hallo-eindpunt verkrijgt.</span><span class="sxs-lookup"><span data-stu-id="8719c-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure-portal]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
