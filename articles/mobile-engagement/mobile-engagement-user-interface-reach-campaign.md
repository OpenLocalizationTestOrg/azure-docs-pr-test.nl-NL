---
title: aaaAzure gebruikersinterface van de Mobile Engagement - Reach-campagne
description: Laern hoe toocreate en beheren met behulp van Azure Mobile Engagement campagnes met pushmeldingen
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>Hoe toocreate en beheren van campagnes met pushmeldingen
Hallo Reach-sectie van Hallo UI toocreate een nieuwe pushcampagne kunt u met een complexe formule door te geven van alle benodigde toosend een push-melding Hallo-gegevens. Hallo opties van een pushcampagne enigszins afwijken, afhankelijk van Hallo vier campagne soorten: aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone).

### <a name="option-applies-to"></a>Is van toepassing op:
* Talen: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)
* Campagne: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)
* Melding: Aankondigingen, Polls
* Inhoud: Uniek zijn voor elk campagnetype
* Doelgroep: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)
* Tijdsbestek: aankondigingen, Polls, tegels
* Test: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)

![Reach-Campaign1][20]

## <a name="languages"></a>Talen
U kunt Hallo talen vervolgkeuzelijst menu toosend een andere versie van de Push-toodevices die zijn ingesteld in verschillende talen toouse gebruiken. Alle apparaten ontvangen standaard Hallo dezelfde Push ongeacht welke taal zijn ze toouse ingesteld. Hallo standaard taalversie van Hallo Push ontvangen gebruikers met hun apparaat set tooa andere taal. Veel van Hallo push campagne opties kunnen u alternatieve toospecify-inhoud voor elke Hallo extra talen die u selecteert. 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a>Taalverschillen van toepassing op:
* Talen: Unieke talen worden geselecteerd in de standaardtaal voor toevoeging toohello
* Campagne: Gelijk voor alle talen
* Melding: Uniek voor elke taal bovendien toohello standaardtaal
* Inhoud: Uniek voor elke taal bovendien toohello standaardtaal
* Doelgroep: Kan worden gefilterd door het criterium van een afzonderlijke taal
* Tijdsbestek: hetzelfde voor alle talen
* Test: Kunnen tooeach taal worden verzonden op een tijdstip

### <a name="supported-languages"></a>Ondersteunde talen:
* Arabisch (ar) 
* Bulgaars (bg) 
* Catalaans (ca) 
* Chinees (zh) 
* Kroatisch (uur) 
* Czech (CS) 
* Deens (da) 
* Nederlands (nl) 
* Engels (en) 
* Fins (fi) 
* Frans (fr) 
* Duits (de) 
* Grieks (el) 
* Hebreeuwse (hij) 
* Hindi (hoog) 
* Hongaars (hu) 
* Indonesisch (id) 
* Italiaans (it) 
* Japans (ja) 
* Koreaans (ko) 
* Lets (lv) 
* Litouws (lt) 
* Maleis (macrolanguage) (ms) 
* Noors, Bokmål (nb) 
* Pools (pl) 
* Portugees (pt) 
* Roemeens (ro) 
* Russisch (ru) 
* Servisch (sr) 
* Slowaaks (sk) 
* Sloveens (sl) 
* Spaans (es) 
* Zweeds (sv) 
* Tagalog (tl) 
* Thais (e) 
* Turks (tr) 
* Oekraïens (GB) 
* Vietnamees (vi) 

## <a name="campaign"></a>Campagne
U kunt gebruiken Hallo campagne tooset Hallo sectienaam en categorie van uw campagne ook als tooignore Hallo doelgroep sectie van een pushcampagne te plannen en verzenden van deze campagne via Hallo Reach API (en een aantal elementen met geringe Hallo Push-API) in plaats daarvan. Categorieën kunnen worden gebruikt met een aangepaste melding sjabloon toocontrol in-app-meldingen op basis van vooraf gedefinieerde instellingen. U kunt een lijst met uw bestaande 'categorieën' via Hallo Reach API ophalen.

> [!WARNING]
> Als u 'Doelgroep negeren, push wordt verzonden toousers via API Hallo' Hallo-optie gebruikt in 'Campagne' Hallo-sectie van een Reach-campagne Hallo campagne wordt niet automatisch verzenden, moet u toosend handmatig via Hallo Reach API.

![Reach-Campaign3][22]

### <a name="option-applies-to"></a>Is van toepassing op:
* Naam: alle
* Categorie: Aankondigingen, Polls
* Doelgroep negeren, push toousers via Hallo API worden verzonden: alle

## <a name="notification"></a>Melding
U kunt Hallo melding sectie tooset basisinstellingen voor het opnemen van uw push: Hallo titel Hallo-Push, het Hallo-bericht, de installatiekopie van een in-app of als deze worden weggeklikt. Veel meldingsinstellingen zijn platform-specifieke toohello van uw apparaat. U kunt aangeven of uw push 'in-app' of 'out of app' worden verzonden of beide. (Houd er rekening mee dat gebruikers kunnen 'opt-in' of 'opt-out' van 'buiten app' Pushes op Hallo besturingssysteem niveau op hun apparaten en Azure Mobile Engagement niet wordt kunnen toooverride worden deze instelling. Denk eraan dat Hallo Reach API 'in-app verwerkt' en 'out van app' duwt. Hallo Push API kan gebruikte toohandle 'buiten app' pushes te zijn.) Pushes kunnen worden aangepast met afbeeldingen of HTML-inhoud, inclusief dieptekoppelingen voor het koppelen van buiten uw App of tooanother locatie in uw App (Android SDK 2.1.0 of hoger opzet categorieën vereist). U kunt wijzigen Hallo-pictogram of iOS-badge en -tekst of web-inhoud (een pop-up met HTML-inhoud, URL koppeling tooanother locatie binnen of buiten de app Hallo) kunt verzenden. U kunt ook Android-apparaten beltoon laten horen of Trillen Hello Push. (Vergeet niet dat u juist SDK machtigingen in uw Android manifest tooring bestand of een apparaat laten Trillen Hallo wordt nodig.) Er is momenteel geen bedrijfstak standaard voor Android 'grote afbeelding' grootten, aangezien schermgrootte verschillen op elk apparaat maar 400 x 100 afbeeldingen op bijna elke schermgrootte werken.

### <a name="delivery-types"></a>Levering typen:
* Alleen buiten app: Hallo-melding worden geleverd wanneer gebruiker Hallo Hallo toepassing niet gebruikt.
* Hallo buiten alleen appmelding vereist een certificaat van Apple of Google (APNS of GCM-certificaat).
* In-app alleen: Hallo melding wordt weergegeven wanneer er op Hallo-toepassing wordt uitgevoerd.
* Hallo melding Hallo Capptain levering tooreach Hallo systeemgebruiker gebruikt. U kunt volledig Hallo visuele lay-out/weergave van uw push aanpassen.
* Op elk gewenst moment: Deze optie zorgt ervoor dat u een melding dat de toepassing hello wordt uitgevoerd of niet verzenden.

![Reach-Campaign4][23]

### <a name="option-applies-to"></a>Is van toepassing op:
* Melding: Aankondigingen, Polls

## <a name="content"></a>Inhoud
U kunt Hallo sectie inhoud toomodify Hallo inhoud van uw aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone) gebruiken. Hallo is inhoud deze instelling van pushcampagnes specifieke toohello type campagne. 

### <a name="see-also"></a>Zie ook
* [UI-documentatie - bereiken - Push-inhoud][Link 29]

![Reach-Campaign5][24]

## <a name="audience"></a>Doelgroep
U kunt Hallo doelgroep sectie toodefine een standaard lijst met items toolimit uw campagne of limieten uw campagne op basis van aangepaste criteria. Hallo standaardset opties tooLimit uw doelgroep kunt u toopush tooeither nieuwe of oude gebruikers of alleen voor gebruikers van native pushberichten. U kunt ook een quotum toolimit Hallo aantal gebruikers die Hallo push ontvangen instellen. U kunt handmatig bewerken Hallo-expressie voor hoe uw campagne gefilterde tooinclude is een of meer criterium tootarget gebruikers. U kunt handmatig een doelgroepexpressie typen. Een dergelijke expressie moet expliciet Hallo relatie tussen criteria definiëren. Een criterium is beschreven door een id die met een hoofdletter moet beginnen en mag geen spaties bevatten. relatie tussen criteria Hallo Hallo kan worden beschreven met behulp van 'en', 'of', 'not' operators, evenals '(',')'. Voorbeeld: 'Criterion1 of (Criterion1 en niet Criterion2)'.

> [!NOTE]
> Met een grote doelgroep opgenomen in de campagnes, Hallo serverzijde die gericht is op scan kan traag zijn, met name als u probeert toostart Hallo meerdere campagnes op hetzelfde moment.

* Alleen indien mogelijk een campagne start tegelijk.
* Hallo maximaal vier campagnes alleen start op een tijdstip op.
* Alleen actieve gebruikers met tooyour push (selectievakje ' alleen gebruikers benaderen die kunnen worden bereikt met behulp van Native Pushberichten' en 'Alleen actieve gebruikers benaderen') zodat alleen gebruikers die nog steeds Hallo-app hebt geïnstalleerd en deze gebruiken toobe gescand moet.
  Als uw doelgroep is gedefinieerd, kunt u Hallo knop toofind uit hoeveel gebruikers deze Push ontvangt simuleren. Dit wilt aantal bekende gebruikers mogelijk doel voor deze doelgroep (dit is een schatting op basis van een steekproef van gebruikers) Hallo berekenen. Vergeet niet dat gebruikers die u hebt verwijderd van de toepassing hello eveneens deel van deze doelgroep uitmaken, maar kunnen niet worden bereikt.

### <a name="see-also"></a>Zie ook
* [UI - Reach - documentatie nieuw Push criterium][Link 28]

![Reach-Campaign6][25]

### <a name="edit-expression"></a>Expressie bewerken
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>Limiet voor die uw doelgroep is van toepassing op:
* Alleen een subset van gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)
* Alleen oude gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)
* Alleen nieuwe gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)
* Alleen niet-actieve gebruikers benaderen: aankondigingen, Polls, tegels
* Alleen actieve gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)
* Alleen gebruikers benaderen die kunnen worden bereikt via een Native Pushbericht: aankondigingen, Polls

## <a name="time-frame"></a>Tijdsbestek
U kunt Hallo tijdsbestek sectie tooset Hallo push wordt verzonden of u kunt Hallo tijdsbestek leeg toostart Hallo campagne onmiddellijk laten. Houd er rekening mee dat met behulp van de tijdzone Hallo eindgebruikers mogelijk Hallo campagne start een dag eerder dan u voor uw eindgebruikers in Azië verwacht en klein batches van pushes tegelijkertijd totdat alle tijdzones in hello world overeen Hallo-periode is ingesteld voor uw campagne te verzenden. Met behulp van de tijdzone Hallo eindgebruikers kan ook vertragingen veroorzaken bij campagnes omdat het toorequest Hallo actief zijn op Hallo telefoon voordat Hallo push heeft.

> [!NOTE]
> Zonder een einddatum in cache campagnes pushes lokaal en nog steeds weergegeven nadat u handmatig voltooid campagnes. tooavoid dit gedrag, de specifieke eindtijd voor campagnes.

### <a name="see-also"></a>Zie ook
* [Bereiken - hoe Tos – plannen][Link 3] 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a>Instellingen van toepassing op:
* Tijdsbestek: aankondigingen, Polls, tegels

## <a name="test"></a>Test
Kunt u Hallo Test sectie toosend dit apparaat push tooyour eigen test voordat u opslaat Hallo campagne. Als u de aangepaste talen voor deze campagne hebt geconfigureerd, kunt u Hallo push testen in elke taal. U kunt een testapparaat van 'Mijn Account' instellen.

> [!NOTE]
> Er zijn geen gegevens worden geregistreerd wanneer u de knop Hallo serverzijde te 'test' pushes, gegevens alleen worden geregistreerd voor echte pushcampagnes.

### <a name="see-also"></a>Zie ook
* [UI-documentatie - Mijn Account][Link 14]

![Reach-Campaign9][28]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

