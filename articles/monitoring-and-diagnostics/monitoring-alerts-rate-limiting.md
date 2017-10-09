---
title: aaaRate voor SMS, e-mailberichten en webhooks beperken | Microsoft Docs
description: Begrijpen hoe Azure beperkt Hallo aantal mogelijke SMS, e-mail of webhook meldingen van een groep in te grijpen.
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="f8575-103">Beoordeel beperken voor SMS-berichten, e-mailberichten en webhook advertenties</span><span class="sxs-lookup"><span data-stu-id="f8575-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="f8575-104">Snelheidslimieten is een opschorten van meldingen die optreedt wanneer er te veel meldingen worden verzonden tooa bepaalde telefoonnummer of e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="f8575-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="f8575-105">Snelheidslimieten zorgt ervoor dat waarschuwingen worden beheerd en actie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f8575-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="f8575-106">Hallo-regels Hallo voor SMS- en e-mailadres zijn dezelfde.</span><span class="sxs-lookup"><span data-stu-id="f8575-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="f8575-107">Hallo snelheid limiet drempelwaarde is:</span><span class="sxs-lookup"><span data-stu-id="f8575-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="f8575-108">**SMS**: 10 berichten in een uur.</span><span class="sxs-lookup"><span data-stu-id="f8575-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="f8575-109">**E-mailadres**: 100 berichten in een uur.</span><span class="sxs-lookup"><span data-stu-id="f8575-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="f8575-110">Regels voor snelheid</span><span class="sxs-lookup"><span data-stu-id="f8575-110">Rate limit rules</span></span>
- <span data-ttu-id="f8575-111">Een bepaald telefoonnummer of e-mailbericht is snelheid beperkt wanneer het ontvangt geen berichten meer dan de drempelwaarde Hallo mogelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="f8575-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="f8575-112">Een telefoonnummer of e-mailbericht kan deel uitmaken van actiegroepen voor veel abonnementen.</span><span class="sxs-lookup"><span data-stu-id="f8575-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="f8575-113">Snelheidslimieten geldt voor alle abonnementen.</span><span class="sxs-lookup"><span data-stu-id="f8575-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="f8575-114">Toepassing zodra Hallo drempelwaarde wordt bereikt, zelfs als berichten van meerdere abonnementen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="f8575-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="f8575-115">Wanneer een telefoonnummer of e-mailbericht beperkt snelheid is, een extra melding verzonden toocommunicate Hallo snelheidsbeperking.</span><span class="sxs-lookup"><span data-stu-id="f8575-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="f8575-116">Hallo melding statussen wanneer hello beoordelen beperken is verlopen.</span><span class="sxs-lookup"><span data-stu-id="f8575-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="f8575-117">Frequentielimiet van webhooks.</span><span class="sxs-lookup"><span data-stu-id="f8575-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="f8575-118">Er is geen snelheidsbeperking voor webhooks.</span><span class="sxs-lookup"><span data-stu-id="f8575-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8575-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8575-119">Next steps</span></span> ##
* <span data-ttu-id="f8575-120">Meer informatie over [SMS waarschuwing gedrag](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f8575-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="f8575-121">Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over hoe tooreceive waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="f8575-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="f8575-122">Meer informatie over hoe te[waarschuwingen configureren wanneer een melding van de health service wordt geboekt](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="f8575-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
