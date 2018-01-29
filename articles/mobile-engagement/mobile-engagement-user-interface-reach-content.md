---
title: Azure Mobile Engagement-gebruikersinterface - Reach-inhoud
description: Informatie over het beheren van de unieke inhoud van de verschillende soorten campagnes met pushmeldingen in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a>Het beheren van de unieke inhoud van de verschillende soorten campagnes met pushmeldingen
Wijzigen van de inhoud van uw aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone) kunt u de sectie inhoud van een nieuwe reach-campagne. De instelling van de inhoud van pushcampagnes is specifiek voor het type campagne. 

### <a name="content-types"></a>Typen inhoud:
* Aankondigingen
* Polls
* Gegevens-pushes
* Tegels (alleen Windows Phone)

## <a name="content-of-announcements"></a>Inhoud van aankondigingen
 ![Reach-Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a>Kies het type van uw aankondiging:
* Alleen melding: Er is een eenvoudige standaard melding. Dit betekent dat als een gebruiker erop, geen extra weergave wordt weergegeven, maar alleen de actie die is gekoppeld aan deze wordt uitgevoerd.
* Tekst-aankondiging: Er is een melding die stelt de gebruiker een tekstweergave bekijken.
* Web-aankondiging: Er is een melding die stelt de gebruiker een webweergave bekijken.

### <a name="see-also"></a>Zie ook
* [Bereiken - hoe Tos - aankondigingen][Link 3] 

### <a name="about-web-view-announcements"></a>Over aankondigingen van webweergave:
Instanties van het patroon '{deviceid}' in de HTML-code of JavaScript-code die u hier opgeeft, wordt automatisch vervangen door de id van het apparaat waarop de aankondiging. Dit is een eenvoudige manier voor het ophalen van Azure Mobile Engagement apparaat-id's in een externe webservice die op uw back-office wordt gehost.
Als u een webweergave in een volledig scherm wilt maken (zonder de door ons verschafte standaardknoppen Actie en Afsluiten), kunt u de volgende functies uit de JavaScript-code van uw webweergave-aankondiging gebruiken: 

* de aankondigingsactie uitvoeren: ReachContent.actionContent()
* de aankondiging afsluiten: ReachContent.exitContent()

### <a name="choose-your-action"></a>Kies uw actie:
### <a name="about-action-urls"></a>Over het actie-URL's:
Elke URL die kan worden geïnterpreteerd door het besturingssysteem kan worden gebruikt als een actie-URL.
Elke toegewezen URL die uw toepassing mogelijk ondersteunt (bijv. om ervoor te zorgen dat gebruikers naar een bepaald scherm springen) kan ook worden gebruikt als een actie-URL.
Elk exemplaar van het patroon {deviceid} automatisch wordt vervangen door de id van het apparaat dat u de actie uitvoert. Dit kan worden gebruikt voor het ophalen van eenvoudig Azure Mobile Engagement apparaat-id's via een externe webservice die op uw back-office wordt gehost.

* **Android en iOS-acties**
  * Een webpagina openen
  * http://\[web-site-domein\] 
  * Voorbeeld: http://www.azure.com
  * E-mail verzenden
  * mailto:\[e-mail-ontvanger\]? onderwerp =\[onderwerp\]& body =\[bericht\] 
  * Example:mailto:foo@example.com? onderwerp begroetingen % 20from % 20Azure % 20Mobile % 20Engagement =! & body = goede % 20stuff!
  * Sms-bericht verzenden
  * SMS:\[-telefoonnummer\] 
  * Voorbeeld: sms:2125551212
  * Kies een telefoonnummer
  * Tel:\[-telefoonnummer\] 
  * Voorbeeld: tel:2125551212
* **Android alleen acties**
  * Een toepassing op de Play Store downloaden
  * market://details?id=\[app-pakket\] 
  * Voorbeeld: market://details?id=com.microsoft.office.word
  * Een geografisch gelokaliseerde zoekopdracht uitvoeren
  * geo:0, 0? q =\[zoekopdracht\] 
  * Voorbeeld: geo:0, 0? q = starbucks, Parijs
* **iOS alleen acties**
  * Een toepassing op de App Store downloaden
  * http://iTunes.Apple.com/ [Land] /app/ [app-naam] /id [app-id]? mt = 8 
  * Voorbeeld: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8
  * Windows-acties
  * Een webpagina openen
  * http://\[web-site-domein\] 
  * Voorbeeld: http://www.azure.com
  * E-mail verzenden
  * mailto:\[e-mail-ontvanger\]? onderwerp =\[onderwerp\]& body =\[bericht\] 
  * Example:mailto:foo@example.com? onderwerp begroetingen % 20from % 20Azure % 20Mobile % 20Engagement =! & body = goede % 20stuff!
  * Een sms-bericht verzenden (Skype Store App vereist)
  * SMS:\[-telefoonnummer\] 
  * Voorbeeld: sms:2125551212
  * Een telefoonnummer kiezen (Skype Store App vereist)
  * Tel:\[-telefoonnummer\] 
  * Voorbeeld: tel:2125551212
  * Een toepassing op de Play Store downloaden
  * MS-windows-store: PDP? PFN =\[app-pakket-ID\] 
  * Voorbeeld: ms-windows-store: PDP? PFN 4d91298a-07cb-40fb-aecc-4cb5615d53c1 =
  * Een bingmaps zoekopdracht starten
  * bingmaps:? q =\[zoekopdracht\] 
  * Voorbeeld: bingmaps:? q = starbucks, Parijs
  * Een aangepast schema gebruiken
  * \[aangepaste schema\]://\[params aangepast schema\] 
  * Voorbeeld: myCustomProtocol://myCustomParams
  * Gebruik de pakketgegevens van een (Store App voor uitbreiding lezen vereist)
  * \[map\]\[gegevens\].\[ de extensie\] 
  * Example:myfolderdata.txt

### <a name="build-a-tracking-url"></a>Een bijhouden-URL maken:
* Zie de sectie 'Instellingen' van de <UI Documentation> voor instructies over het bouwen van een URL bijhouden die, kunnen gebruikers een van de andere toepassingen downloaden.

### <a name="define-the-texts-of-your-announcement"></a>De tekst van uw aankondiging kiezen
Vul in de titel, de inhoud en de tekst van knop van uw aankondiging. U kunt een doelgroep van een toekomstige campagne op basis van de feedback reach van hoe gebruikers gereageerd op de campagne richten. Doelgroepen kan zijn gebaseerd op de feedback van of deze campagne zojuist, beantwoorde, ondernomen of afgesloten gepusht is.

### <a name="see-also"></a>Zie ook
* [UI - Reach - documentatie nieuw Push criterium][Link 28]

## <a name="content-of-polls"></a>Inhoud van Polls
![Reach-Content2][31] 

Vul in de titel, beschrijving en knop tekst van uw aankondiging. Vervolgens voegt u vragen en opties voor de antwoorden op vragen.
U kunt een doelgroep van een toekomstige campagne op basis van de feedback reach van hoe gebruikers gereageerd op de campagne richten. Doelgroepen kan zijn gebaseerd op of deze campagne zojuist, beantwoorde, ondernomen of afgesloten gepusht is. Doelgroepen kan ook worden gebaseerd op Poll antwoord feedback, waar de vraag en antwoord keuze worden gebruikt als criteria.

### <a name="see-also"></a>Zie ook
* [UI - Reach - documentatie nieuw Push criterium][Link 28]

## <a name="content-of-data-pushes"></a>Inhoud van het gegevens-Pushes
![Reach-Content3][32] 

### <a name="choose-the-type-of-your-data"></a>Kies het type van uw gegevens:
* Tekst
* Binaire gegevens
* Base64-gegevens

### <a name="define-the-content-of-your-data"></a>De inhoud van uw gegevens definiëren
* Als u hebt geselecteerd voor de push-tekstgegevens, kopieer en plak de tekst in het vak 'inhoud'.
* Als u hebt geselecteerd voor de push-binair of base64-gegevens, gebruikt u de knop 'uw bestand uploadt' uw bestand te uploaden.
* U kunt een doelgroep van een toekomstige campagne op basis van de feedback reach van hoe gebruikers gereageerd op de campagne richten. Doelgroepen kan zijn gebaseerd op of deze campagne zojuist, beantwoorde, ondernomen of afgesloten gepusht is.

### <a name="see-also"></a>Zie ook
* [UI - Reach - documentatie nieuw Push criterium][Link 28]

## <a name="content-of-tiles-windows-phone-only"></a>Inhoud van de tegels (alleen Windows Phone)
![Reach-Content4][33]

### <a name="define-the-content-of-your-tile"></a>De inhoud van uw tegel definiëren
De nettolading van de tegel is de tekst die moet worden weergegeven in de tegel van uw app op Windows Phone-apparaten.
Een tegel push is de Microsoft Push Notification Service (MPNS) versie van een native pushberichten voor Windows Phone. De tegel push-type is het enige push-type dat geen antwoord en dus de doelgroep van toekomstige campagnes kan niet worden gemaakt van de resultaten van een tegel pushcampagne. 

### <a name="see-also"></a>Zie ook
* [API - Reach API - documentatie Native Pushberichten][Link 4]

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

