---
title: aaaAdvanced configuratie voor Windows universele Apps Engagement SDK
description: Geavanceerde configuratieopties voor Azure Mobile Engagement met universele Windows-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="a596f-103">Geavanceerde configuratie voor Windows universele Apps Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="a596f-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a596f-104">Universeel Windows</span><span class="sxs-lookup"><span data-stu-id="a596f-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="a596f-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a596f-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="a596f-106">iOS</span><span class="sxs-lookup"><span data-stu-id="a596f-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="a596f-107">Android</span><span class="sxs-lookup"><span data-stu-id="a596f-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="a596f-108">Deze procedure wordt beschreven hoe tooconfigure verschillende configuratieopties voor Azure Mobile Engagement Android-apps.</span><span class="sxs-lookup"><span data-stu-id="a596f-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a596f-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a596f-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="a596f-110">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="a596f-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="a596f-111">Automatische crashrapporten uitschakelen</span><span class="sxs-lookup"><span data-stu-id="a596f-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="a596f-112">U kunt automatische Hallo-crash rapportagefunctie van Engagement uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="a596f-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="a596f-113">Klik, wanneer er een niet-verwerkte uitzondering optreedt, Engagement, gebeurt er niets.</span><span class="sxs-lookup"><span data-stu-id="a596f-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="a596f-114">Als u deze functie uitschakelen en vervolgens als een niet-verwerkte-crash in uw app plaatsvindt, Engagement geen Hallo crash verzendt **en** Hallo-sessie en taken niet gesloten.</span><span class="sxs-lookup"><span data-stu-id="a596f-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="a596f-115">de automatische crash toodisable rapportage, uw configuratie, afhankelijk van Hallo manier waarop u het gedeclareerd aanpassen:</span><span class="sxs-lookup"><span data-stu-id="a596f-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="a596f-116">Van `EngagementConfiguration.xml` bestand</span><span class="sxs-lookup"><span data-stu-id="a596f-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="a596f-117">Rapport vastlopen te ingesteld`false` tussen `<reportCrash>` en `</reportCrash>` labels.</span><span class="sxs-lookup"><span data-stu-id="a596f-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="a596f-118">Van `EngagementConfiguration` object tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="a596f-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="a596f-119">Rapport crash toofalse met behulp van het object EngagementConfiguration ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a596f-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="a596f-120">Uitschakelen van realtime rapportage</span><span class="sxs-lookup"><span data-stu-id="a596f-120">Disable real time reporting</span></span>
<span data-ttu-id="a596f-121">Standaard Hallo Engagement servicerapporten Logboeken in realtime.</span><span class="sxs-lookup"><span data-stu-id="a596f-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="a596f-122">Als uw toepassing wordt vaak logboeken rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze in één keer op regelmatige basis.</span><span class="sxs-lookup"><span data-stu-id="a596f-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="a596f-123">Dit heet 'burst modus'.</span><span class="sxs-lookup"><span data-stu-id="a596f-123">This is called “burst mode”.</span></span>

<span data-ttu-id="a596f-124">toodo worden dus Hallo-methode aanroept:</span><span class="sxs-lookup"><span data-stu-id="a596f-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="a596f-125">Hallo-argument is een waarde in **milliseconden**.</span><span class="sxs-lookup"><span data-stu-id="a596f-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="a596f-126">Aanroepen Hallo methode geen parameters of met de waarde 0 Hallo gewenst tooreactivate Hallo realtime logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="a596f-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="a596f-127">Burst-modus enigszins verhoogt de batterij Hallo maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken).</span><span class="sxs-lookup"><span data-stu-id="a596f-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="a596f-128">U kunt het beste een ' burst ' drempelwaarde niet langer dan 30000 (30s) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a596f-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="a596f-129">Opgeslagen logboeken zijn beperkt too300 items.</span><span class="sxs-lookup"><span data-stu-id="a596f-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="a596f-130">Als het verzenden te lang is, kunt u sommige logboeken gaan verloren.</span><span class="sxs-lookup"><span data-stu-id="a596f-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="a596f-131">Hallo burst drempelwaarde mag niet geconfigureerde tooa periode kleiner is dan een seconde.</span><span class="sxs-lookup"><span data-stu-id="a596f-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="a596f-132">Als u doet dit, ziet u een tracering met Hallo fout hello SDK- en automatisch teruggezet op toohello standaardwaarde nul seconden.</span><span class="sxs-lookup"><span data-stu-id="a596f-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="a596f-133">Deze triggers Hallo SDK tooreport Hallo logboeken realtime.</span><span class="sxs-lookup"><span data-stu-id="a596f-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
