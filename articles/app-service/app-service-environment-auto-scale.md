---
title: aaaAutoscaling en App Service-omgeving v1
description: Automatisch schalen en App-serviceomgeving
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>Automatisch schalen en App Service-omgeving v1

> [!NOTE]
> In dit artikel gaat over het Hallo v1 App Service-omgeving.  Er is een nieuwere versie van App Service-omgeving die eenvoudiger toouse en wordt uitgevoerd op krachtiger infrastructuur Hallo. meer informatie over de nieuwe versie Hallo met Hallo beginnen toolearn [inleiding toohello App Service-omgeving](../app-service/app-service-environment/intro.md).
> 

Ondersteuning voor Azure App Service-omgevingen *automatisch schalen*. U kunt afzonderlijke werknemersgroepen automatisch schalen op basis van de metrische gegevens of schema.

![Opties voor automatisch schalen voor een worker-groep.][intro]

Automatisch schalen optimaliseert de Resourcegebruik door automatisch vergroten en verkleinen van een App Service-omgeving toofit uw budget en of de load-profiel.

## <a name="configure-worker-pool-autoscale"></a>Worker-groep automatisch schalen configureren
Hallo-functionaliteit voor automatisch schalen is toegankelijk vanuit Hallo **instellingen** tabblad van Hallo werknemersgroep.

![Tabblad instellingen van Hallo werknemersgroep.][settings-scale]

Van daaruit is Hallo-interface moet bekend zijn omdat het Hallo dezelfde ervaring dat u ziet wanneer u een App Service schalen plannen. 

![De instellingen handmatig schalen.][scale-manual]

U kunt ook een profiel voor automatisch schalen configureren.

![Instellingen voor automatisch schalen.][scale-profile]

Profielen voor automatisch schalen zijn handig tooset beperkingen met betrekking tot de schaal. Op deze manier kunt u een consistente prestaties ervaren door een ondergrens schaalwaarde (1) en een voorspelbare uitgaven initiaal door in te stellen van een bovengrens (2) hebben.

![Scale-instellingen in het profiel.][scale-profile2]

Nadat u een profiel definieert, kunt u automatisch schalen regels tooscale toevoegen omhoog of omlaag Hallo aantal exemplaren in een werknemersgroep Hallo binnen Hallo grenzen die zijn gedefinieerd door Hallo-profiel. Regels voor automatisch schalen die zijn gebaseerd op metrische gegevens.

![Schaalregel.][scale-rule]

 Een werknemersgroep of de front-metrische gegevens kan worden gebruikt toodefine automatisch schalen regels. Deze metrische gegevens zijn Hallo dezelfde metrische gegevens kunt u bewaken in Hallo resource blade grafieken of instellen voor waarschuwingen.

## <a name="autoscale-example"></a>Voorbeeld voor automatisch schalen
Automatisch schalen van een App Service-omgeving kan best worden geïllustreerd door het doorlopen van een scenario.

Dit artikel wordt uitgelegd van alle benodigde Hallo-overwegingen bij het instellen van automatisch schalen. Hallo artikel begeleidt u bij Hallo interacties die binnenkomen afgespeeld wanneer u App Service-omgevingen die worden gehost in App Service-omgeving rekening te houden in automatisch schalen.

### <a name="scenario-introduction"></a>Scenario Inleiding
Frank is een sysadmin voor een onderneming die een deel van Hallo werkbelastingen beheert Hij tooan App Service-omgeving is gemigreerd.

Hallo App Service-omgeving toomanual scale als volgt geconfigureerd:

* **FrontPage-ends:** 3
* **Worker-groep 1**: 10
* **Werknemersgroep 2**: 5
* **Werknemersgroep 3**: 5

Worker-groep 1 wordt gebruikt voor productieworkloads, hoewel werknemersgroep 2 en 3 van werknemersgroep worden gebruikt voor kwaliteit assurance (QA) en ontwikkeling werkbelastingen.

Hallo App Service-plannen voor QA en dev zijn geconfigureerd toomanual schaal. Hallo productie-App Service-abonnement instellen tooautoscale toodeal met variaties in belasting en verkeer.

Frank zeer vertrouwd is met de toepassing hello. Hij weet dat de piekuren Hallo voor load tussen 9:00 uur en 18:00 uur zijn omdat dit een line-of-business (LOB)-toepassing die werknemers gebruiken als ze in Hallo office. Gebruik zakt hierna wanneer gebruikers klaar bent voor die dag. Buiten de piekuren is er nog steeds bepaalde laden omdat gebruikers toegang Hallo-app op afstand tot hebben via hun mobiele apparaten of thuiscomputers. Hallo productie-App Service-abonnement al is geconfigureerd op basis van CPU-gebruik Hello volgens de regels voor tooautoscale:

![Specifieke instellingen voor LOB-app.][asp-scale]

| **Profiel voor automatisch schalen: weekdagen-App Service-abonnement** | **Profiel voor automatisch schalen: tijdens het weekend-App Service-abonnement** |
| --- | --- |
| **Naam:** profiel weekdag |**Naam:** profiel voor het Weekend |
| **Schaal door:** regels voor planning en prestaties |**Schaal door:** regels voor planning en prestaties |
| **Profiel:** weekdagen |**Profiel:** Weekend |
| **Type:** terugkeerpatroon |**Type:** terugkeerpatroon |
| **Doelbereik:** 5 too20 exemplaren |**Doelbereik:** 3 too10 exemplaren |
| **Aantal dagen:** maandag, dinsdag, woensdag, donderdag en vrijdag |**Aantal dagen:** zaterdag, zondag |
| **Begintijd:** 9:00 uur |**Begintijd:** 9:00 uur |
| **Tijdzone:** UTC-08 |**Tijdzone:** UTC-08 |
|  | |
| **Regel voor automatisch schalen (Omhoog schalen)** |**Regel voor automatisch schalen (Omhoog schalen)** |
| **Bron:** productie (App Service-omgeving) |**Bron:** productie (App Service-omgeving) |
| **Metrische gegevens:** CPU-percentage |**Metrische gegevens:** CPU-percentage |
| **Bewerking:** groter zijn dan 60% |**Bewerking:** groter is dan 80% |
| **Duur:** 5 minuten |**Duur:** 10 minuten |
| **Tijd aggregatie:** gemiddelde |**Tijd aggregatie:** gemiddelde |
| **Actie:** aantal verhogen door 2 |**Actie:** aantal verhoogd met 1 |
| **Cool omlaag (minuten):** 15 |**Cool omlaag (minuten):** 20 |
|  | |
| **Regel voor automatisch schalen (schaal omlaag)** |**Regel voor automatisch schalen (schaal omlaag)** |
| **Bron:** productie (App Service-omgeving) |**Bron:** productie (App Service-omgeving) |
| **Metrische gegevens:** CPU-percentage |**Metrische gegevens:** CPU-percentage |
| **Bewerking:** minder dan 30% |**Bewerking:** minder dan 20% |
| **Duur:** 10 minuten |**Duur:** 15 minuten |
| **Tijd aggregatie:** gemiddelde |**Tijd aggregatie:** gemiddelde |
| **Actie:** aantal verlagen door 1 |**Actie:** aantal verlagen door 1 |
| **Cool omlaag (minuten):** 20 |**Cool omlaag (minuten):** 10 |

### <a name="app-service-plan-inflation-rate"></a>De snelheid van App Service-abonnement
App Service-abonnementen die geconfigureerd tooautoscale zijn doen op de maximale overdrachtssnelheid per uur. Deze snelheid kan worden berekend op basis van Hallo waarden op Hallo automatisch schalen regel.

Meer informatie over en berekenen Hallo *App Service plan de frequentie* is belangrijk voor App Service-omgeving voor automatisch schalen omdat scale wijzigingen tooa werknemersgroep niet onmiddellijk.

Hallo-App Service plan de frequentie is als volgt berekend:

![De frequentie waarmee de berekening van App Service-abonnement.][ASP-Inflation]

Op basis van Hallo automatisch schalen – omhoog schalen-regel voor Hallo werkdag profiel van Hallo productie-App Service-abonnement:

![App Service plan de snelheid voor weekdagen op basis van automatisch schalen – omhoog schalen-regel.][Equation1]

In geval van Hallo Hallo automatisch schalen – omhoog schalen-regel voor Hallo Weekend profiel van Hallo productie-App Service-abonnement zou Hallo formule omzetten in:

![App Service plan de snelheid voor het weekend op basis van automatisch schalen – omhoog schalen-regel.][Equation2]

Deze waarde kan ook worden berekend voor omlaag schalen bewerkingen.

Op basis van Hallo automatisch schalen: Scale omlaag regel voor Hallo werkdag profiel van Hallo productie-App Service-plan ziet dit er als volgt:

![App Service plan de snelheid voor weekdagen op basis van automatisch schalen: Scale omlaag regel.][Equation3]

In geval van Hallo Hallo automatisch schalen: Scale omlaag regel voor Hallo Weekend profiel van Hallo productie-App Service-abonnement zou Hallo formule omzetten in:  

![App Service plan de snelheid voor het weekend op basis van automatisch schalen: Scale omlaag regel.][Equation4]

Hallo productie-App Service-abonnement kan op een maximale snelheid van acht exemplaren per uur tijdens Hallo week en vier exemplaren per uur tijdens Hallo weekend groeien. Deze kunt vrijgeven exemplaren met een maximale snelheid van vier exemplaren per uur tijdens Hallo week en zes exemplaren per uur tijdens het weekend.

Als meerdere App Service-abonnementen worden wordt gehost in een werknemersgroep, hebt u toocalculate hello *totale frequentie van de* als Hallo som van Hallo de frequentie voor alle Hallo App Service-abonnementen die worden host in die worker-groep.

![De berekening van de totale frequentie van de voor meerdere App Service-abonnementen die in een werknemersgroep worden gehost.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>Gebruik Hallo App Service plan de frequentie waarmee toodefine worker pool automatisch schalen regels
Werknemer die host App Service-abonnementen die geconfigureerd tooautoscale zijn moeten een buffer van de capaciteit worden toegewezen aan de groep. Hallo buffer kunt Hallo automatisch schalen operations toogrow en de App Service-abonnement verkleinen naar behoefte. minimale buffer Hallo zou zijn Hallo totale App Service Plan de frequentie berekend.

Omdat App Service-omgeving schaalbewerkingen enige tijd tooapply neemt, wordt elke wijziging moet rekening houden met verder vraag verandert die optreden kunnen wanneer een schaalaanpassing uitgevoerd wordt. tooaccommodate deze latentie, het is raadzaam dat u Hallo totale App Service Plan de frequentie berekend als Hallo minimum aantal exemplaren die voor elke bewerking voor automatisch schalen die zijn toegevoegd.

Met deze informatie kunt Frank Hallo kunt definiëren voor automatisch schalen profiel en regels te volgen:

![Regels voor automatisch schalen profiel voor LOB-voorbeeld.][Worker-Pool-Scale]

| **Profiel voor automatisch schalen: weekdagen** | **Profiel voor automatisch schalen: tijdens het weekend** |
| --- | --- |
| **Naam:** profiel weekdag |**Naam:** profiel voor het Weekend |
| **Schaal door:** regels voor planning en prestaties |**Schaal door:** regels voor planning en prestaties |
| **Profiel:** weekdagen |**Profiel:** Weekend |
| **Type:** terugkeerpatroon |**Type:** terugkeerpatroon |
| **Doelbereik:** 13 too25 exemplaren |**Doelbereik:** 6 too15 exemplaren |
| **Aantal dagen:** maandag, dinsdag, woensdag, donderdag en vrijdag |**Aantal dagen:** zaterdag, zondag |
| **Begintijd:** 7:00 uur |**Begintijd:** 9:00 uur |
| **Tijdzone:** UTC-08 |**Tijdzone:** UTC-08 |
|  | |
| **Regel voor automatisch schalen (Omhoog schalen)** |**Regel voor automatisch schalen (Omhoog schalen)** |
| **Bron:** werknemersgroep 1 |**Bron:** werknemersgroep 1 |
| **Metrische gegevens:** WorkersAvailable |**Metrische gegevens:** WorkersAvailable |
| **Bewerking:** minder dan 8 |**Bewerking:** minder dan 3 |
| **Duur:** 20 minuten |**Duur:** 30 minuten |
| **Tijd aggregatie:** gemiddelde |**Tijd aggregatie:** gemiddelde |
| **Actie:** aantal verhogen door 8 |**Actie:** aantal verhogen door 3 |
| **Cool omlaag (minuten):** 180 |**Cool omlaag (minuten):** 180 |
|  | |
| **Regel voor automatisch schalen (schaal omlaag)** |**Regel voor automatisch schalen (schaal omlaag)** |
| **Bron:** werknemersgroep 1 |**Bron:** werknemersgroep 1 |
| **Metrische gegevens:** WorkersAvailable |**Metrische gegevens:** WorkersAvailable |
| **Bewerking:** groter is dan 8 |**Bewerking:** groter is dan 3 |
| **Duur:** 20 minuten |**Duur:** 15 minuten |
| **Tijd aggregatie:** gemiddelde |**Tijd aggregatie:** gemiddelde |
| **Actie:** aantal verlagen door 2 |**Actie:** aantal verlagen door 3 |
| **Cool omlaag (minuten):** 120 |**Cool omlaag (minuten):** 120 |

Hallo doelbereik gedefinieerd in het Hallo-profiel wordt berekend door Hallo minimale exemplaren gedefinieerd in het profiel voor Hallo App Service-abonnement + buffer.

Hallo som van alle Hallo maximale bereiken voor alle App Service-abonnementen die worden gehost in een werknemersgroep Hallo zijn Hallo Maximum bereik.

Hallo verhoging van het aantal voor Hallo opschaling van de regels moet set tooat minimaal 1 X-App Service Plan de frequentie voor scale-.

Verklein het aantal kan aangepaste toosomething tussen 1/2 X of X 1 Hallo App Service Plan de Rate voor schaal omlaag.

### <a name="autoscale-for-front-end-pool"></a>Voor de front-toepassingen voor automatisch schalen
Regels voor front-automatisch schalen zijn eenvoudiger dan voor werknemersgroepen. U dient voornamelijk om  
Zorg ervoor dat de duur van de meting Hallo en Hallo cooldown timers rekening houdt scale-bewerkingen op een App Service-abonnement zijn niet onmiddellijk.

In dit scenario kent Frank die Foutfrequentie Hallo neemt toe nadat front-ends CPU-gebruik 80% bereiken en stelt automatisch schalen Hallo regel tooincrease exemplaren als volgt:

![Instellingen voor automatisch schalen voor de front-toepassingen.][Front-End-Scale]

| **Profiel voor automatisch schalen: begin eindigt** |
| --- |
| **Naam:** automatisch schalen: begin eindigt |
| **Schaal door:** regels voor planning en prestaties |
| **Profiel:** dagelijkse |
| **Type:** terugkeerpatroon |
| **Doelbereik:** 3 too10 exemplaren |
| **Aantal dagen:** dagelijkse |
| **Begintijd:** 9:00 uur |
| **Tijdzone:** UTC-08 |
|  |
| **Regel voor automatisch schalen (Omhoog schalen)** |
| **Bron:** front-groep |
| **Metrische gegevens:** CPU-percentage |
| **Bewerking:** groter zijn dan 60% |
| **Duur:** 20 minuten |
| **Tijd aggregatie:** gemiddelde |
| **Actie:** aantal verhogen door 3 |
| **Cool omlaag (minuten):** 120 |
|  |
| **Regel voor automatisch schalen (schaal omlaag)** |
| **Bron:** werknemersgroep 1 |
| **Metrische gegevens:** CPU-percentage |
| **Bewerking:** minder dan 30% |
| **Duur:** 20 minuten |
| **Tijd aggregatie:** gemiddelde |
| **Actie:** aantal verlagen door 3 |
| **Cool omlaag (minuten):** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
