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
# <a name="sms-alert-behavior-in-action-groups"></a>SMS gedrag in Actiegroepen waarschuwing
## <a name="overview"></a>Overzicht ##
Actiegroepen kunnen u een lijst met ontvangers tooconfigure. Deze groepen kunnen vervolgens worden gebruikt bij het definiëren van de activiteit logboek waarschuwingen; ervoor te zorgen dat een bepaalde actie-groep wordt geïnformeerd wanneer Hallo activiteit logboek waarschuwing wordt geactiveerd. Een Hallo waarschuwingen mechanismen ondersteund is SMS; Hallo waarschuwingen ondersteuning voor bidirectionele communicatie. Er kan een gebruiker reageren tooan waarschuwing naar:

- **Afmelden bij meldingen:** een gebruiker kan afmelden bij alle SMS-waarschuwingen voor alle actiegroepen of een actiegroep enkelvoud.  
- **Opnieuw abonneren ' tooalerts:** een gebruiker kan opnieuw abonneren ' tooall SMS-berichten voor alle actiegroepen of een actiegroep enkelvoud.  
- **Hulp vragen:** een gebruiker kunt vragen voor meer informatie over Hallo SMS. Ze worden omgeleid toothis artikel

Dit artikel behandelt Hallo gedrag van de SMS-berichten Hallo en hello antwoord acties Hallo gebruiker kunt onderneemt op basis van landinstellingen Hallo van Hallo gebruiker:

## <a name="usacanada-sms-behavior"></a>Verenigde Staten/Canada SMS-gedrag
### <a name="receiving-an-sms-alert"></a>Een SMS-bericht ontvangen
Een SMS-ontvanger die is geconfigureerd als onderdeel van een actiegroep, ontvangt een SMS-bericht wanneer een waarschuwing wordt geactiveerd. Hallo SMS voert u Hallo volgende informatie:
* Korte naam van groep van Hallo actie deze waarschuwing is verzonden naar
- Titel van de waarschuwing Hallo

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Afmelden bij de SMS-berichten voor een actiegroep
Een gebruiker kan zich afmeldt SMS voor waarschuwingen voor de groep één actie door reageert toohello Stuur 20873 met trefwoorden Hallo: "uitschakelen &lt;korte naam van actiegroep&gt;'.

Bijvoorbeeld Een gebruiker die toounsubscribe van waarschuwingen voor een actiegroep met Hallo korte naam 'Azure', zou een SMS toohello Stuur 20873 met de tekst 'Uitschakelen Azure' verzenden

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Afmelden bij de SMS-berichten voor alle actiegroepen
Een gebruiker kan afmelden bij alle SMS-berichten voor alle actiegroepen door reageert toohello Stuur 20873 met een Hallo trefwoorden te volgen:
* STOPPEN

Bijvoorbeeld Een gebruiker die toounsubscribe van SMS-berichten worden voor alle actiegroepen, zou een SMS toohello Stuur 20873 met de tekst 'STOP' verzenden

>[!NOTE]
>Als een gebruiker heeft zich afgemeld SMS gewaarschuwd, maar wordt vervolgens toegevoegd tooa nieuwe actiegroep; ze worden ontvangen van de SMS-berichten voor de nieuwe groep in te grijpen, maar blijven afgemeld alle vorige Actiegroepen.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Waarschuwingen voor één actiegroep tooSMS resubscribing
Een gebruiker kan opnieuw abonneren ' tooSMS voor waarschuwingen voor de groep één actie door reageert toohello Stuur 20873 met trefwoorden Hallo: "inschakelen &lt;korte naam van actiegroep&gt;'.

Bijvoorbeeld Een gebruiker die tooresubscribe tooalerts voor een actiegroep met Hallo korte naam 'Azure', zou een SMS toohello Stuur 20873 met de tekst 'Azure inschakelen' verzenden

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Resubscribing tooSMS waarschuwingen voor alle actiegroepen
Een gebruiker kan opnieuw abonneren ' tooall SMS voor waarschuwingen voor alle actiegroepen door reageert toohello Stuur 20873 met een Hallo trefwoorden te volgen:

* START

Bijvoorbeeld Een gebruiker die toounsubscribe van SMS-berichten worden voor alle actiegroepen, zou een SMS toohello Stuur 20873 met de tekst 'START' verzenden

### <a name="requesting-help-via-sms"></a>Hulp via SMS aanvragen
Een gebruiker kan vragen voor meer informatie over Hallo SMS dat ze door reageert toohello Stuur 20873 hebben ontvangen met een van de volgende trefwoorden Hallo:
* HELP

Een antwoord verzonden toohello gebruiker met een koppeling toothis artikel.

## <a name="next-steps"></a>Volgende stappen
Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md) en meer informatie over hoe tooget gewaarschuwd  
Meer informatie over [SMS snelheidsbeperking](monitoring-alerts-rate-limiting.md)  
Meer informatie over [actiegroepen](monitoring-action-groups.md)
