---
title: Azure Mobile Engagement Web SDK-integratie | Microsoft Docs
description: De nieuwste updates en procedures voor het Azure Mobile Engagement Web SDK
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
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="ef373-103">Azure Mobile Engagement integreren in een webtoepassing</span><span class="sxs-lookup"><span data-stu-id="ef373-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef373-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="ef373-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="ef373-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ef373-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="ef373-106">iOS</span><span class="sxs-lookup"><span data-stu-id="ef373-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="ef373-107">Android</span><span class="sxs-lookup"><span data-stu-id="ef373-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="ef373-108">De procedures in dit artikel beschrijven de eenvoudigste manier om het activeren van de analyses en bewaking functies in Azure Mobile Engagement in uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="ef373-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="ef373-109">Volg de stappen voor het activeren van de logboek-rapporten die nodig zijn voor alle statistische gegevens over gebruikers, sessies, activiteiten, crashes en technicals berekenen.</span><span class="sxs-lookup"><span data-stu-id="ef373-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="ef373-110">Voor statistieken van afhankelijk zijn van toepassing, zoals gebeurtenissen, fouten en taken, moet u handmatig log-rapporten activeren met behulp van de API van Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ef373-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="ef373-111">Informatie voor meer informatie over [hoe u de geavanceerde Mobile Engagement API tags in een webtoepassing](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="ef373-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="ef373-112">Inleiding</span><span class="sxs-lookup"><span data-stu-id="ef373-112">Introduction</span></span>
<span data-ttu-id="ef373-113">[Download het Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="ef373-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="ef373-114">De Mobile Engagement Web SDK wordt geleverd als een JavaScript-bestand van één azure-engagement.js, die u wilt opnemen in elke pagina van de toepassing van uw site of webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="ef373-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef373-115">Voordat u dit script uitvoert, moet u een script of codefragment die u schrijft voor het configureren van Mobile Engagement voor uw toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef373-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="ef373-116">Browsercompatibiliteit</span><span class="sxs-lookup"><span data-stu-id="ef373-116">Browser compatibility</span></span>
<span data-ttu-id="ef373-117">De Mobile Engagement Web SDK maakt gebruik van systeemeigen JSON coderen en decoderen, naast de AJAX-aanvragen tussen domeinen (afhankelijk van de specificatie W3C CORS).</span><span class="sxs-lookup"><span data-stu-id="ef373-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="ef373-118">Is compatibel met de volgende browsers:</span><span class="sxs-lookup"><span data-stu-id="ef373-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="ef373-119">Microsoft Edge 12 +</span><span class="sxs-lookup"><span data-stu-id="ef373-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="ef373-120">Internet Explorer 10 +</span><span class="sxs-lookup"><span data-stu-id="ef373-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="ef373-121">Firefox 3.5 +</span><span class="sxs-lookup"><span data-stu-id="ef373-121">Firefox 3.5+</span></span>
* <span data-ttu-id="ef373-122">Chrome 4 +</span><span class="sxs-lookup"><span data-stu-id="ef373-122">Chrome 4+</span></span>
* <span data-ttu-id="ef373-123">Safari 6 +</span><span class="sxs-lookup"><span data-stu-id="ef373-123">Safari 6+</span></span>
* <span data-ttu-id="ef373-124">Opera 12 +</span><span class="sxs-lookup"><span data-stu-id="ef373-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="ef373-125">Configureren van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ef373-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="ef373-126">Een script schrijven dat wordt gemaakt van een globale `azureEngagement` JavaScript-object, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ef373-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="ef373-127">Omdat de site meerdere pagina's hebben mogelijk, in dit voorbeeld wordt ervan uitgegaan dat dit script wordt opgenomen in elke pagina.</span><span class="sxs-lookup"><span data-stu-id="ef373-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="ef373-128">In dit voorbeeld wordt de JavaScript-object met de naam `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="ef373-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="ef373-129">De `connectionString` waarde voor uw toepassing wordt weergegeven in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ef373-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ef373-130">`appVersionName`en `appVersionCode` zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="ef373-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="ef373-131">We raden echter aan dat u ze configureren zodat analytics versie-informatie kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="ef373-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="ef373-132">Mobile Engagement scripts opnemen in uw pagina 's</span><span class="sxs-lookup"><span data-stu-id="ef373-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="ef373-133">Mobile Engagement-scripts toevoegen aan uw pagina's in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="ef373-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="ef373-134">Of dit:</span><span class="sxs-lookup"><span data-stu-id="ef373-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="ef373-135">Alias</span><span class="sxs-lookup"><span data-stu-id="ef373-135">Alias</span></span>
<span data-ttu-id="ef373-136">Nadat het script Mobile Engagement Web SDK is geladen, maakt de **engagement** alias voor toegang tot de SDK-API's.</span><span class="sxs-lookup"><span data-stu-id="ef373-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="ef373-137">U kunt deze alias niet gebruiken voor het definiëren van de configuratie van de SDK.</span><span class="sxs-lookup"><span data-stu-id="ef373-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="ef373-138">Deze alias wordt gebruikt als een verwijzing in deze documentatie.</span><span class="sxs-lookup"><span data-stu-id="ef373-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="ef373-139">Houd er rekening mee dat als de standaardalias met een andere globale variabele van uw pagina conflicteert, u het in de configuratie als volgt desgewenst kunt voordat het laden van de Mobile Engagement Web SDK:</span><span class="sxs-lookup"><span data-stu-id="ef373-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="ef373-140">Basic-rapportage</span><span class="sxs-lookup"><span data-stu-id="ef373-140">Basic reporting</span></span>
<span data-ttu-id="ef373-141">Basic rapportage in Mobile Engagement bevat informatie over de statistieken van de sessie-niveau, zoals statistieken over gebruikers, sessies, activiteiten en crashes.</span><span class="sxs-lookup"><span data-stu-id="ef373-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="ef373-142">Sessie bijhouden</span><span class="sxs-lookup"><span data-stu-id="ef373-142">Session tracking</span></span>
<span data-ttu-id="ef373-143">Een sessie Mobile Engagement is onderverdeeld in een volgorde van activiteiten, elk aangeduid met een naam.</span><span class="sxs-lookup"><span data-stu-id="ef373-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="ef373-144">In een klassieke website raden wij u aan een andere activiteit te declareren op elke pagina van uw site.</span><span class="sxs-lookup"><span data-stu-id="ef373-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="ef373-145">Voor een website of webtoepassing toepassing waarin de huidige pagina nooit verandert, kunt u de activiteiten bijhouden op kleinere schaal, zoals op de pagina.</span><span class="sxs-lookup"><span data-stu-id="ef373-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="ef373-146">In beide gevallen aanroepen om te starten of het wijzigen van de huidige gebruikersactiviteit, de `engagement.agent.startActivity` functie.</span><span class="sxs-lookup"><span data-stu-id="ef373-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="ef373-147">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ef373-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="ef373-148">De Mobile Engagement-server wordt automatisch een geopende sessie binnen drie minuten nadat de pagina van de toepassing wordt gesloten beëindigd.</span><span class="sxs-lookup"><span data-stu-id="ef373-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="ef373-149">U kunt ook u kunt een sessie beëindigen handmatig door het aanroepen van `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="ef373-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="ef373-150">Hiermee stelt u de huidige gebruikersactiviteit 'Inactief'.</span><span class="sxs-lookup"><span data-stu-id="ef373-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="ef373-151">De sessie beëindigd 10 seconden later tenzij een nieuwe aanroep `engagement.agent.startActivity` hervatten van de sessie.</span><span class="sxs-lookup"><span data-stu-id="ef373-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="ef373-152">U kunt de vertraging van 10 seconden in het object globale engagement als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="ef373-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="ef373-153">U kunt geen gebruiken `engagement.agent.endActivity` in de `onunload` retouraanroep omdat u niet AJAX-aanroepen in deze fase.</span><span class="sxs-lookup"><span data-stu-id="ef373-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="ef373-154">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="ef373-154">Advanced reporting</span></span>
<span data-ttu-id="ef373-155">Als u rapporteren van specifieke gebeurtenissen, fouten en taken wilt, moet u eventueel de Mobile Engagement-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef373-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="ef373-156">U toegang tot de API van de Mobile Engagement via de `engagement.agent` object.</span><span class="sxs-lookup"><span data-stu-id="ef373-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="ef373-157">U kunt toegang tot alle van de geavanceerde functies in Mobile Engagement in de Mobile Engagement-API.</span><span class="sxs-lookup"><span data-stu-id="ef373-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="ef373-158">De API wordt beschreven in het artikel [hoe u de geavanceerde Mobile Engagement API tags in een webtoepassing](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="ef373-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="ef373-159">De URL's gebruikt voor AJAX-aanroepen aanpassen</span><span class="sxs-lookup"><span data-stu-id="ef373-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="ef373-160">U kunt URL's die gebruikmaakt van de Mobile Engagement Web SDK aanpassen.</span><span class="sxs-lookup"><span data-stu-id="ef373-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="ef373-161">Bijvoorbeeld, als u wilt definiëren de logboek-URL (het SDK-eindpunt voor logboekregistratie), kunt u de configuratie als volgt vervangen:</span><span class="sxs-lookup"><span data-stu-id="ef373-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="ef373-162">Als de functies van uw URL als een tekenreeks die begint resultaat met `/`, `//`, `http://`, of `https://`, het standaardschema wordt niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ef373-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="ef373-163">Standaard de `https://` schema wordt gebruikt voor deze URL's.</span><span class="sxs-lookup"><span data-stu-id="ef373-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="ef373-164">Als u aanpassen van het standaardschema wilt, overschrijven de configuratie, als volgt:</span><span class="sxs-lookup"><span data-stu-id="ef373-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
