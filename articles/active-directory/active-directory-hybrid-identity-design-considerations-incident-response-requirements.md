---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - incident rResponse vereisten bepalen | Microsoft Docs
description: "Controle- en rapportagefuncties mogelijkheden voor Hallo hybride identiteitsoplossing die kan worden gebruikt door IT tootake acties tooidentify en een potentiële bedreigingen te verhelpen vaststellen"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Vereisten voor respons op incidenten voor uw oplossing voor hybride identiteit bepalen
Grote of middelgrote organisaties waarschijnlijk heeft een [beveiliging respons op incidenten](https://technet.microsoft.com/library/cc700825.aspx) in place toohelp IT dienovereenkomstig acties uitvoeren toohello niveau van incident. Hallo identiteitsbeheersysteem is een belangrijk onderdeel in Hallo respons op incidenten proces omdat gebruikte toohelp identificeren wie een specifieke actie op Hallo doel is uitgevoerd. Hallo hybride identiteitsoplossing moet kunnen tooprovide controle en rapportage van de mogelijkheden die kunnen worden gebruikt door IT tootake acties tooidentify en een mogelijke bedreiging beperken. In een typische beveiligingsplan hebt Hallo fasen als onderdeel van Hallo plan te volgen:

1. Eerste beoordeling.
2. Incident communicatie.
3. Beschadiging van het en het risico te beperken.
4. Identificatie van wat er inbreuk en de ernst.
5. Bewijs bewaring.
6. Melding tooappropriate partijen.
7. Systeemherstel van het.
8. Documentatie.
9. Beoordeling schade en de kosten.
10. Proces en plan revisie.

Tijdens het Hallo-identificatie van dit was inbreuk en de ernst fase, wordt deze nodig tooidentify Hallo systemen die zijn aangetast, bestanden die zijn geopend en Hallo gevoeligheid van die bestanden bepalen. Uw systeem van hybride identiteit moet kunnen toofulfill deze tooassist vereisten bepalen wat de Hallo-gebruiker die deze wijzigingen aangebracht. 

## <a name="monitoring-and-reporting"></a>Controle en rapportage
Vaak Hallo identiteitsbeheersysteem kan ook helpen in de beoordelingsfase voor initiële hoofdzakelijk als Hallo-systeem ingebouwde met controle- en rapportagemogelijkheden. Tijdens de eerste beoordeling hello, IT-beheerder moet kunnen tooidentify een verdachte activiteit of Hallo systeem moet kunnen tootrigger die automatisch op basis van een vooraf geconfigureerde taak. Voor veel activiteiten kunnen duiden op een mogelijke aanvallen, maar in andere gevallen is een onjuist geconfigureerde systeem tooa aantal valse positieven inbraakdetectie detectie van het systeem kan leiden. 

Hallo identiteitsbeheersysteem moet helpen IT-beheerders tooidentify en rapporteren van deze verdachte activiteiten. Meestal kunnen deze technische vereisten worden voldaan door de bewaking van alle systemen en met een rapportagemogelijkheid die mogelijke bedreigingen kunt markeren. Hallo vragen hieronder toohelp u uw oplossing voor hybride identiteit waarbij rekening vereisten voor respons op incidenten overweging ontwerpen:

* Uw bedrijf beschikt over een respons op incidenten beveiliging?
  * Zo ja, wordt hello huidige identiteitsbeheersysteem gebruikt als onderdeel van Hallo proces?
* Heeft uw bedrijf behoefte aan tooidentify verdachte aanmeldingspogingen van gebruikers op verschillende apparaten?
* Heeft uw bedrijf behoefte aan toodetect potentiële verdachte referenties van gebruiker?
* Heeft uw bedrijf behoefte toegang en de actie van de gebruiker tooaudit?
* Heeft uw bedrijf behoefte aan tooknow wanneer een gebruiker zijn/haar wachtwoord opnieuw instellen?

## <a name="policy-enforcement"></a>Afdwingen van beleid
Tijdens de beschadiging van het en risico's te beperken-fase is het belangrijk tooquickly Hallo werkelijke en de mogelijke effecten van een aanval verminderen. Deze actie die u onderneemt kan op dit moment Hallo verschil tussen een klein en een primaire maken. Hallo daadwerkelijke reactie afhankelijk van uw organisatie en Hallo aard van Hallo-aanval die u mee te maken. Als de eerste beoordeling Hallo gesloten dat een account is geknoeid, moet u tooenforce beleid tooblock dit account. Dit is slechts één voorbeeld waarin de identiteitsbeheersysteem hello worden gebruikt. Hallo vragen hieronder toohelp die u uw hybride identiteitsoplossing ontwerpt terwijl tooreact tooan lopende incident rekening houdend met hoe het beleid worden afgedwongen gebruiken:

* Uw bedrijf heeft beleidsregels in place tooblock gebruikers toegang tot het netwerk Hallo indien nodig?
  * Zo ja, Hallo huidige oplossing geïntegreerd met Hallo hybride identity management-systeem dat u momenteel tooadopt bent?
* Heeft uw bedrijf behoefte aan tooenforce voorwaardelijke toegang voor gebruikers die in quarantaine? 

> [!NOTE]
> Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt. [Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties voor Hallo en de voor-en nadelen van elke optie.  Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
[Strategie voor beveiliging van gegevens definiëren](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

