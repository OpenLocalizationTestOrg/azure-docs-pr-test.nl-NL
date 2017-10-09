---
title: aaaAzure Mobile Engagement Web SDK-integratie | Microsoft Docs
description: meest recente updates en procedures voor het Azure Mobile Engagement Web SDK Hallo Hallo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="3d0b3-103">Azure Mobile Engagement integreren in een webtoepassing</span><span class="sxs-lookup"><span data-stu-id="3d0b3-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d0b3-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="3d0b3-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="3d0b3-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3d0b3-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="3d0b3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="3d0b3-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="3d0b3-107">Android</span><span class="sxs-lookup"><span data-stu-id="3d0b3-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="3d0b3-108">Hallo procedures in dit artikel wordt beschreven Hallo eenvoudigste manier tooactivate Hallo analytics en bewaking van functies in Azure Mobile Engagement in uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="3d0b3-109">Ga als volgt Hallo stappen tooactivate Hallo logboek rapporten die vereist toocompute zijn alle statistische gegevens over gebruikers, sessies, activiteiten, crashes en technicals.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="3d0b3-110">Voor statistieken van afhankelijk zijn van toepassing, zoals gebeurtenissen, fouten en taken, moet u handmatig log-rapporten activeren met behulp van hello Azure Mobile Engagement-API.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="3d0b3-111">Informatie voor meer informatie over [hoe toouse Hallo Mobile Engagement API tags in een webtoepassing geavanceerde](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="3d0b3-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="3d0b3-112">Inleiding</span><span class="sxs-lookup"><span data-stu-id="3d0b3-112">Introduction</span></span>
<span data-ttu-id="3d0b3-113">[Hello Azure Mobile Engagement Web SDK downloaden](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="3d0b3-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="3d0b3-114">Hallo Mobile Engagement Web SDK wordt geleverd als een enkel JavaScript-bestand, azure-engagement.js, die u hebt tooinclude op elke pagina van de toepassing van uw site of webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d0b3-115">Voordat u dit script uitvoert, moet u een script uitvoeren of code codefragment tooconfigure Mobile Engagement te schrijven voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="3d0b3-116">Browsercompatibiliteit</span><span class="sxs-lookup"><span data-stu-id="3d0b3-116">Browser compatibility</span></span>
<span data-ttu-id="3d0b3-117">Hallo Mobile Engagement Web SDK maakt gebruik van systeemeigen JSON coderen en decoderen bovendien toocross domein AJAX-aanvragen (relying op Hallo W3C CORS-specificatie).</span><span class="sxs-lookup"><span data-stu-id="3d0b3-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="3d0b3-118">Is compatibel met de volgende browsers Hallo:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="3d0b3-119">Microsoft Edge 12 +</span><span class="sxs-lookup"><span data-stu-id="3d0b3-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="3d0b3-120">Internet Explorer 10 +</span><span class="sxs-lookup"><span data-stu-id="3d0b3-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="3d0b3-121">Firefox 3.5 +</span><span class="sxs-lookup"><span data-stu-id="3d0b3-121">Firefox 3.5+</span></span>
* <span data-ttu-id="3d0b3-122">Chrome 4 +</span><span class="sxs-lookup"><span data-stu-id="3d0b3-122">Chrome 4+</span></span>
* <span data-ttu-id="3d0b3-123">Safari 6 +</span><span class="sxs-lookup"><span data-stu-id="3d0b3-123">Safari 6+</span></span>
* <span data-ttu-id="3d0b3-124">Opera 12 +</span><span class="sxs-lookup"><span data-stu-id="3d0b3-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="3d0b3-125">Configureren van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3d0b3-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="3d0b3-126">Een script schrijven dat wordt gemaakt van een globale `azureEngagement` JavaScript-object, zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="3d0b3-127">Omdat de site meerdere pagina's hebben mogelijk, in dit voorbeeld wordt ervan uitgegaan dat dit script wordt opgenomen in elke pagina.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="3d0b3-128">In dit voorbeeld Hallo JavaScript-object met de naam `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="3d0b3-129">Hallo `connectionString` waarde wordt weergegeven in uw toepassing hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3d0b3-130">`appVersionName`en `appVersionCode` zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="3d0b3-131">We raden echter aan dat u ze configureren zodat analytics versie-informatie kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="3d0b3-132">Mobile Engagement scripts opnemen in uw pagina 's</span><span class="sxs-lookup"><span data-stu-id="3d0b3-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="3d0b3-133">Mobile Engagement scripts tooyour pagina's op een van de volgende manieren Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="3d0b3-134">Of dit:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="3d0b3-135">Alias</span><span class="sxs-lookup"><span data-stu-id="3d0b3-135">Alias</span></span>
<span data-ttu-id="3d0b3-136">Nadat Hallo Mobile Engagement Web SDK-script is geladen, het maken van Hallo **engagement** alias tooaccess Hallo SDK-API's.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="3d0b3-137">U kunt deze alias toodefine Hallo SDK-configuratie niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="3d0b3-138">Deze alias wordt gebruikt als een verwijzing in deze documentatie.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="3d0b3-139">Houd er rekening mee dat als Hallo standaardalias met een andere globale variabele van uw pagina conflicteert, u het in Hallo configuratie als volgt desgewenst kunt voordat u Hallo Mobile Engagement Web SDK laden:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="3d0b3-140">Basic-rapportage</span><span class="sxs-lookup"><span data-stu-id="3d0b3-140">Basic reporting</span></span>
<span data-ttu-id="3d0b3-141">Basic rapportage in Mobile Engagement bevat informatie over de statistieken van de sessie-niveau, zoals statistieken over gebruikers, sessies, activiteiten en crashes.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="3d0b3-142">Sessie bijhouden</span><span class="sxs-lookup"><span data-stu-id="3d0b3-142">Session tracking</span></span>
<span data-ttu-id="3d0b3-143">Een sessie Mobile Engagement is onderverdeeld in een volgorde van activiteiten, elk aangeduid met een naam.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="3d0b3-144">In een klassieke website raden wij u aan een andere activiteit te declareren op elke pagina van uw site.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="3d0b3-145">Voor een website of webtoepassing toepassing in welke Hallo huidige pagina nooit verandert, kunt u tootrack Hallo activiteiten op kleinere schaal, zoals binnen Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="3d0b3-146">Ofwel manier, toostart of wijzig Hallo huidige gebruikersactiviteit aanroep Hallo `engagement.agent.startActivity` functie.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="3d0b3-147">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="3d0b3-148">Hallo Mobile Engagement-server beëindigd automatisch een geopende sessie binnen drie minuten nadat de pagina van de toepassing hello is gesloten.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="3d0b3-149">U kunt ook u kunt een sessie beëindigen handmatig door het aanroepen van `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="3d0b3-150">Hiermee stelt u Hallo huidige gebruiker activiteit too'Idle.'</span><span class="sxs-lookup"><span data-stu-id="3d0b3-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="3d0b3-151">Hallo-sessie 10 seconden later worden beëindigd tenzij een nieuwe aanroep te`engagement.agent.startActivity` Hallo sessie hervatten.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="3d0b3-152">U kunt Hallo 10 seconden vertraging in Hallo globale engagement-object als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="3d0b3-153">U kunt geen gebruiken `engagement.agent.endActivity` in Hallo `onunload` retouraanroep omdat u niet AJAX-aanroepen in deze fase.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="3d0b3-154">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="3d0b3-154">Advanced reporting</span></span>
<span data-ttu-id="3d0b3-155">Als u wilt dat tooreport toepassingsspecifieke gebeurtenissen, fouten en taken, moet u eventueel toouse Hallo Mobile Engagement-API.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="3d0b3-156">U toegang tot Mobile Engagement API Hallo via Hallo `engagement.agent` object.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="3d0b3-157">U kunt toegang tot alle Hallo geavanceerde mogelijkheden in Mobile Engagement in Hallo Mobile Engagement-API.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="3d0b3-158">Hallo API wordt beschreven in artikel Hallo [hoe toouse Hallo Mobile Engagement API tags in een webtoepassing geavanceerde](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="3d0b3-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="3d0b3-159">Hallo-URL's gebruikt voor AJAX-aanroepen aanpassen</span><span class="sxs-lookup"><span data-stu-id="3d0b3-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="3d0b3-160">U kunt URL's aanpassen die gebruikmaakt van Mobile Engagement Web SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="3d0b3-161">Bijvoorbeeld: tooredefine Hallo logboek URL (Hallo SDK eindpunt voor logboekregistratie), kunt u Hallo configuratie overschrijven als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="3d0b3-162">Als de functies van uw URL als een tekenreeks die begint resultaat met `/`, `//`, `http://`, of `https://`, Hallo standaardschema wordt niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="3d0b3-163">Standaard Hallo `https://` schema wordt gebruikt voor deze URL's.</span><span class="sxs-lookup"><span data-stu-id="3d0b3-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="3d0b3-164">Als u toocustomize Hallo standaardschema wilt, overschrijven Hallo-configuratie, als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0b3-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
