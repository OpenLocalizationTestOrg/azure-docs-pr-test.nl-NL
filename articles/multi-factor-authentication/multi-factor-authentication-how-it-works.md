---
title: Multi-factor Authentication - aaaAzure hoe het werkt
description: Azure multi-factor Authentication helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Deze extra beveiliging biedt doordat een tweede vorm van verificatie en sterke verificatie via een bereik van eenvoudige verificatie-opties te bezorgen.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>De werking van Azure multi-factor Authentication
Hallo beveiliging van verificatie in twee stappen ligt de gelaagde benadering. Inbreuk op meerdere verificatiefactoren geeft een belangrijke uitdaging voor kwaadwillende personen. Zelfs als een aanvaller erin toolearn Hallo het wachtwoord van gebruiker slaagt, is deze onbruikbaar zonder dat ook het bezit van Hallo vertrouwd apparaat. 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

Azure multi-factor Authentication helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.  Deze extra beveiliging biedt doordat een tweede vorm van verificatie en sterke verificatie via een bereik van eenvoudige verificatie-opties te bezorgen.


## <a name="methods-available-for-two-step-verification"></a>Methoden voor verificatie in twee stappen
Wanneer een gebruiker zich aanmeldt, wordt een aanvullende verificatie toohello gebruiker verzonden.  Hallo hieronder vindt u een lijst met methoden die kunnen worden gebruikt voor deze tweede verificatie.

| Verificatiemethode | Beschrijving |
| --- | --- |
| Telefoonoproep |Het geregistreerde telefoonnummer van de gebruiker van de tooa is gebeld. Hallo-gebruiker een PINCODE invoert, indien nodig vervolgens Hallo #-toets indrukt. |
| SMS-bericht |Een SMS-bericht verzonden van de gebruiker tooa mobiele telefoon met een code van zes cijfers. Hallo gebruiker voert deze code aan de aanmeldingspagina Hallo. |
| Meldingen voor mobiele Apps |Een verzoek voor identiteitverificatie verzonden Smartphone tooa van de gebruiker. Hallo gebruiker een PINCODE invoert, indien nodig en vervolgens selecteert **controleren** op Hallo mobiele app. |
| Verificatiecode van mobiele app |Hallo mobiele app, die wordt uitgevoerd op de Smartphone van een gebruiker, wordt een bevestigingscode die elke 30 seconden wordt gewijzigd. Hallo gebruiker zoeken naar de meest recente code Hallo en krijgt de op de aanmeldingspagina Hallo. |
| OATH-tokens van derde partij | Azure multi-factor Authentication-Server kan worden geconfigureerd tooaccept verificatiemethoden van derden te gebruiken. |

Azure multi-factor Authentication biedt selecteerbare verificatiemethoden voor zowel cloud als de server. U kunt kiezen welke methoden zijn beschikbaar voor uw gebruikers: telefoonoproep, tekst, app-melding of app-codes. Zie voor meer informatie [selecteerbare verificatiemethoden](multi-factor-authentication-whats-next.md#selectable-verification-methods).

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over andere Hallo [versies en verbruikmethoden voor Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md)

- Kies of toodeploy Azure MFA [in Hallo cloud of on-premises](multi-factor-authentication-get-started.md)

- Lees de antwoorden voor [Veelgestelde vragen](multi-factor-authentication-faq.md)