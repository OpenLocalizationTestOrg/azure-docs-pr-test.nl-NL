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
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>Beoordeel beperken voor SMS-berichten, e-mailberichten en webhook advertenties
Snelheidslimieten is een opschorten van meldingen die optreedt wanneer er te veel meldingen worden verzonden tooa bepaalde telefoonnummer of e-mailadres. Snelheidslimieten zorgt ervoor dat waarschuwingen worden beheerd en actie worden uitgevoerd.

Hallo-regels Hallo voor SMS- en e-mailadres zijn dezelfde. Hallo snelheid limiet drempelwaarde is:

 - **SMS**: 10 berichten in een uur.
 - **E-mailadres**: 100 berichten in een uur.

## <a name="rate-limit-rules"></a>Regels voor snelheid
- Een bepaald telefoonnummer of e-mailbericht is snelheid beperkt wanneer het ontvangt geen berichten meer dan de drempelwaarde Hallo mogelijk maakt.
- Een telefoonnummer of e-mailbericht kan deel uitmaken van actiegroepen voor veel abonnementen. Snelheidslimieten geldt voor alle abonnementen. Toepassing zodra Hallo drempelwaarde wordt bereikt, zelfs als berichten van meerdere abonnementen worden verzonden.  
- Wanneer een telefoonnummer of e-mailbericht beperkt snelheid is, een extra melding verzonden toocommunicate Hallo snelheidsbeperking. Hallo melding statussen wanneer hello beoordelen beperken is verlopen.

## <a name="rate-limit-of-webhooks"></a>Frequentielimiet van webhooks. ##
Er is geen snelheidsbeperking voor webhooks.

## <a name="next-steps"></a>Volgende stappen ##
* Meer informatie over [SMS waarschuwing gedrag](monitoring-sms-alert-behavior.md).
* Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over hoe tooreceive waarschuwingen.  
* Meer informatie over hoe te[waarschuwingen configureren wanneer een melding van de health service wordt geboekt](monitoring-activity-log-alerts-on-service-notifications.md).
