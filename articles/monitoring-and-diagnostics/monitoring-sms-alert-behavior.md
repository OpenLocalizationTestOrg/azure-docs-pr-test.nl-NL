---
title: Waarschuwing gedrag in Actiegroepen aaaSMS | Microsoft Docs
description: Indeling van de SMS-bericht en reageert tooSMS berichten toounsubscribe, opnieuw abonneren ' of om hulp vragen.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="1bd91-103">SMS gedrag in Actiegroepen waarschuwing</span><span class="sxs-lookup"><span data-stu-id="1bd91-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="1bd91-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1bd91-104">Overview</span></span> ##
<span data-ttu-id="1bd91-105">Actiegroepen kunnen u een lijst met ontvangers tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="1bd91-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="1bd91-106">Deze groepen kunnen vervolgens worden gebruikt bij het definiëren van de activiteit logboek waarschuwingen; ervoor te zorgen dat een bepaalde actie-groep wordt geïnformeerd wanneer Hallo activiteit logboek waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1bd91-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="1bd91-107">Een Hallo waarschuwingen mechanismen ondersteund is SMS; Hallo waarschuwingen ondersteuning voor bidirectionele communicatie.</span><span class="sxs-lookup"><span data-stu-id="1bd91-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="1bd91-108">Er kan een gebruiker reageren tooan waarschuwing naar:</span><span class="sxs-lookup"><span data-stu-id="1bd91-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="1bd91-109">**Afmelden bij meldingen:** een gebruiker kan afmelden bij alle SMS-waarschuwingen voor alle actiegroepen of een actiegroep enkelvoud.</span><span class="sxs-lookup"><span data-stu-id="1bd91-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="1bd91-110">**Opnieuw abonneren ' tooalerts:** een gebruiker kan opnieuw abonneren ' tooall SMS-berichten voor alle actiegroepen of een actiegroep enkelvoud.</span><span class="sxs-lookup"><span data-stu-id="1bd91-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="1bd91-111">**Hulp vragen:** een gebruiker kunt vragen voor meer informatie over Hallo SMS.</span><span class="sxs-lookup"><span data-stu-id="1bd91-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="1bd91-112">Ze worden omgeleid toothis artikel</span><span class="sxs-lookup"><span data-stu-id="1bd91-112">They will be redirected toothis article</span></span>

<span data-ttu-id="1bd91-113">Dit artikel behandelt Hallo gedrag van de SMS-berichten Hallo en hello antwoord acties Hallo gebruiker kunt onderneemt op basis van landinstellingen Hallo van Hallo gebruiker:</span><span class="sxs-lookup"><span data-stu-id="1bd91-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="1bd91-114">Verenigde Staten/Canada SMS-gedrag</span><span class="sxs-lookup"><span data-stu-id="1bd91-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="1bd91-115">Een SMS-bericht ontvangen</span><span class="sxs-lookup"><span data-stu-id="1bd91-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="1bd91-116">Een SMS-ontvanger die is geconfigureerd als onderdeel van een actiegroep, ontvangt een SMS-bericht wanneer een waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1bd91-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="1bd91-117">Hallo SMS voert u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="1bd91-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="1bd91-118">Korte naam van groep van Hallo actie deze waarschuwing is verzonden naar</span><span class="sxs-lookup"><span data-stu-id="1bd91-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="1bd91-119">Titel van de waarschuwing Hallo</span><span class="sxs-lookup"><span data-stu-id="1bd91-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="1bd91-120">Afmelden bij de SMS-berichten voor een actiegroep</span><span class="sxs-lookup"><span data-stu-id="1bd91-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="1bd91-121">Een gebruiker kan zich afmeldt SMS voor waarschuwingen voor de groep één actie door reageert toohello Stuur 20873 met trefwoorden Hallo: "uitschakelen &lt;korte naam van actiegroep&gt;'.</span><span class="sxs-lookup"><span data-stu-id="1bd91-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="1bd91-122">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="1bd91-122">Ex.</span></span> <span data-ttu-id="1bd91-123">Een gebruiker die toounsubscribe van waarschuwingen voor een actiegroep met Hallo korte naam 'Azure', zou een SMS toohello Stuur 20873 met de tekst 'Uitschakelen Azure' verzenden</span><span class="sxs-lookup"><span data-stu-id="1bd91-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="1bd91-124">Afmelden bij de SMS-berichten voor alle actiegroepen</span><span class="sxs-lookup"><span data-stu-id="1bd91-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="1bd91-125">Een gebruiker kan afmelden bij alle SMS-berichten voor alle actiegroepen door reageert toohello Stuur 20873 met een Hallo trefwoorden te volgen:</span><span class="sxs-lookup"><span data-stu-id="1bd91-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="1bd91-126">STOPPEN</span><span class="sxs-lookup"><span data-stu-id="1bd91-126">STOP</span></span>

<span data-ttu-id="1bd91-127">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="1bd91-127">Ex.</span></span> <span data-ttu-id="1bd91-128">Een gebruiker die toounsubscribe van SMS-berichten worden voor alle actiegroepen, zou een SMS toohello Stuur 20873 met de tekst 'STOP' verzenden</span><span class="sxs-lookup"><span data-stu-id="1bd91-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="1bd91-129">Als een gebruiker heeft zich afgemeld SMS gewaarschuwd, maar wordt vervolgens toegevoegd tooa nieuwe actiegroep; ze worden ontvangen van de SMS-berichten voor de nieuwe groep in te grijpen, maar blijven afgemeld alle vorige Actiegroepen.</span><span class="sxs-lookup"><span data-stu-id="1bd91-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="1bd91-130">Waarschuwingen voor één actiegroep tooSMS resubscribing</span><span class="sxs-lookup"><span data-stu-id="1bd91-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="1bd91-131">Een gebruiker kan opnieuw abonneren ' tooSMS voor waarschuwingen voor de groep één actie door reageert toohello Stuur 20873 met trefwoorden Hallo: "inschakelen &lt;korte naam van actiegroep&gt;'.</span><span class="sxs-lookup"><span data-stu-id="1bd91-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="1bd91-132">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="1bd91-132">Ex.</span></span> <span data-ttu-id="1bd91-133">Een gebruiker die tooresubscribe tooalerts voor een actiegroep met Hallo korte naam 'Azure', zou een SMS toohello Stuur 20873 met de tekst 'Azure inschakelen' verzenden</span><span class="sxs-lookup"><span data-stu-id="1bd91-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="1bd91-134">Resubscribing tooSMS waarschuwingen voor alle actiegroepen</span><span class="sxs-lookup"><span data-stu-id="1bd91-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="1bd91-135">Een gebruiker kan opnieuw abonneren ' tooall SMS voor waarschuwingen voor alle actiegroepen door reageert toohello Stuur 20873 met een Hallo trefwoorden te volgen:</span><span class="sxs-lookup"><span data-stu-id="1bd91-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="1bd91-136">START</span><span class="sxs-lookup"><span data-stu-id="1bd91-136">START</span></span>

<span data-ttu-id="1bd91-137">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="1bd91-137">Ex.</span></span> <span data-ttu-id="1bd91-138">Een gebruiker die toounsubscribe van SMS-berichten worden voor alle actiegroepen, zou een SMS toohello Stuur 20873 met de tekst 'START' verzenden</span><span class="sxs-lookup"><span data-stu-id="1bd91-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="1bd91-139">Hulp via SMS aanvragen</span><span class="sxs-lookup"><span data-stu-id="1bd91-139">Requesting help via SMS</span></span>
<span data-ttu-id="1bd91-140">Een gebruiker kan vragen voor meer informatie over Hallo SMS dat ze door reageert toohello Stuur 20873 hebben ontvangen met een van de volgende trefwoorden Hallo:</span><span class="sxs-lookup"><span data-stu-id="1bd91-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="1bd91-141">HELP</span><span class="sxs-lookup"><span data-stu-id="1bd91-141">HELP</span></span>

<span data-ttu-id="1bd91-142">Een antwoord verzonden toohello gebruiker met een koppeling toothis artikel.</span><span class="sxs-lookup"><span data-stu-id="1bd91-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bd91-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1bd91-143">Next Steps</span></span>
<span data-ttu-id="1bd91-144">Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md) en meer informatie over hoe tooget gewaarschuwd</span><span class="sxs-lookup"><span data-stu-id="1bd91-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="1bd91-145">Meer informatie over [SMS snelheidsbeperking](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="1bd91-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="1bd91-146">Meer informatie over [actiegroepen](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="1bd91-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
