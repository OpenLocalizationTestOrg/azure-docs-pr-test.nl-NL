---
title: Universele geavanceerde Reporting met MobileApps Engagement aaaWindows
description: Hoe tooIntegrate Azure Mobile Engagement met universele Windows-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="2db81-103">Geavanceerde rapportage Hello Windows universele Apps Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="2db81-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2db81-104">Universeel Windows</span><span class="sxs-lookup"><span data-stu-id="2db81-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="2db81-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="2db81-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="2db81-106">iOS</span><span class="sxs-lookup"><span data-stu-id="2db81-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="2db81-107">Android</span><span class="sxs-lookup"><span data-stu-id="2db81-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="2db81-108">Dit onderwerp beschrijft aanvullende scenario's voor rapportage in uw universele Windows-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2db81-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="2db81-109">Deze scenario's omvatten opties die u tooapply toohello app gemaakt in Hallo kunt [aan de slag](mobile-engagement-windows-store-dotnet-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2db81-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2db81-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2db81-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="2db81-111">Voordat u deze zelfstudie begint, moet u eerst Hallo voltooien [aan de slag](mobile-engagement-windows-store-dotnet-get-started.md) zelfstudie, namelijk opzettelijk direct en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="2db81-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="2db81-112">Deze zelfstudie bevat informatie over aanvullende opties die u kunt kiezen uit.</span><span class="sxs-lookup"><span data-stu-id="2db81-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="2db81-113">Configuratie van de engagement tijdens runtime opgeven</span><span class="sxs-lookup"><span data-stu-id="2db81-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="2db81-114">Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project, namelijk waarin deze is opgegeven in Hallo [aan de slag](mobile-engagement-windows-store-dotnet-get-started.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="2db81-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="2db81-115">Maar u kunt dit ook opgeven tijdens runtime: u kunt de volgende methode voordat de initialisatie van de agent Engagement Hallo Hallo aanroepen:</span><span class="sxs-lookup"><span data-stu-id="2db81-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="2db81-116">Aanbevolen methode: overbelasting uw `Page` klassen</span><span class="sxs-lookup"><span data-stu-id="2db81-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="2db81-117">alle tooactivate Hallo rapportage van alle Hallo logboeken vereist voor Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken maken uw `Page` onderliggende klassen overnemen van Hallo `EngagementPage` klassen.</span><span class="sxs-lookup"><span data-stu-id="2db81-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="2db81-118">Hier volgt een voorbeeld van een pagina van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2db81-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="2db81-119">U kunt doen Hallo hetzelfde geldt voor alle pagina's van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2db81-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="2db81-120">C#-bronbestand</span><span class="sxs-lookup"><span data-stu-id="2db81-120">C# Source file</span></span>
<span data-ttu-id="2db81-121">Wijzigen van uw pagina `.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="2db81-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="2db81-122">Toevoegen van tooyour `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="2db81-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="2db81-123">Vervang `Page` met `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="2db81-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="2db81-124">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="2db81-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="2db81-125">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="2db81-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="2db81-126">Als uw pagina Hallo overschrijft `OnNavigatedTo` methode ervoor toocall worden `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="2db81-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="2db81-127">Anders Hallo activiteit wordt niet gerapporteerd (Hallo `EngagementPage` aanroepen `StartActivity` binnen de `OnNavigatedTo` methode).</span><span class="sxs-lookup"><span data-stu-id="2db81-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="2db81-128">XAML-bestand</span><span class="sxs-lookup"><span data-stu-id="2db81-128">XAML file</span></span>
<span data-ttu-id="2db81-129">Wijzigen van uw pagina `.xaml` bestand:</span><span class="sxs-lookup"><span data-stu-id="2db81-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="2db81-130">Tooyour naamruimtedeclaraties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2db81-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="2db81-131">Vervang `Page` met `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="2db81-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="2db81-132">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="2db81-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="2db81-133">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="2db81-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="2db81-134">Hallo standaardwerking overschrijven</span><span class="sxs-lookup"><span data-stu-id="2db81-134">Override hello default behaviour</span></span>
<span data-ttu-id="2db81-135">Standaard is als Hallo activiteitsnaam, zonder extra Hallo klassenaam van Hallo pagina gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="2db81-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="2db81-136">Als Hallo klasse Hallo 'Pagina' achtervoegsel gebruikt, Engagement, wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2db81-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="2db81-137">toooverride hello standaardgedrag voor de naam van de hello, voeg deze code:</span><span class="sxs-lookup"><span data-stu-id="2db81-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="2db81-138">tooreport extra informatie aan de activiteit, voeg deze code:</span><span class="sxs-lookup"><span data-stu-id="2db81-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="2db81-139">Deze methoden worden aangeroepen vanuit Hallo `OnNavigatedTo` methode van uw pagina.</span><span class="sxs-lookup"><span data-stu-id="2db81-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="2db81-140">Alternatieve methode: call `StartActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="2db81-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="2db81-141">Als u niet kunt of toooverload niet wilt dat uw `Page` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent` rechtstreeks methoden.</span><span class="sxs-lookup"><span data-stu-id="2db81-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="2db81-142">We raden aan aanroepen `StartActivity` binnen uw `OnNavigatedTo` methode van uw pagina.</span><span class="sxs-lookup"><span data-stu-id="2db81-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="2db81-143">Zorg ervoor dat u uw sessie correct beëindigen.</span><span class="sxs-lookup"><span data-stu-id="2db81-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="2db81-144">Hallo universele Windows SDK roept automatisch Hallo `EndActivity` methode wanneer de toepassing hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="2db81-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="2db81-145">Het is dus **maximaal** toocall Hallo aanbevolen `StartActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te**nooit** aanroep Hallo `EndActivity` methode.</span><span class="sxs-lookup"><span data-stu-id="2db81-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="2db81-146">Deze methode waarschuwt Hallo Engagement server dat Hallo huidige gebruiker heeft verlaten Hallo toepassing; dit is van invloed op alle toepassingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="2db81-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="2db81-147">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="2db81-147">Advanced reporting</span></span>
<span data-ttu-id="2db81-148">Desgewenst kunt u tooreport toepassingsspecifieke gebeurtenissen, fouten en taken, toodo dus, gebruik andere methoden gevonden in Hallo Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="2db81-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="2db81-149">Hallo Engagement API staat het gebruik van geavanceerde mogelijkheden voor alle Engagement.</span><span class="sxs-lookup"><span data-stu-id="2db81-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="2db81-150">Zie voor meer informatie [hoe toouse Hallo Mobile Engagement API in uw universele Windows-app-tagging geavanceerde](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="2db81-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

