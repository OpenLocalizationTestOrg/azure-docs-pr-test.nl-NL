---
title: aaaAzure Mobile Engagement-gebruikersinterface - bereik
description: Meer informatie over hoe tooreach toohello gebruikers van uw toepassing met behulp van Azure Mobile Engagement pushmeldingen
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Hoe tooreach toohello gebruikers van uw toepassing met pushmeldingen
Dit artikel wordt beschreven Hallo **bereiken** tabblad Hallo **Mobile Engagement** portal. Gebruik van Hallo **Mobile Engagement** portal toomonitor en beheren van uw mobiele apps. Houd er rekening mee dat toostart met Hallo portal toocreate moet u eerst een **Azure Mobile Engagement** account. Zie voor meer informatie [een Azure Mobile Engagement-account maken](mobile-engagement-create.md).

Hallo sectie van de gebruikersinterface is Hallo Hallo Push campagne beheerprogramma u maken/bewerken/activeren/voltooien/monitor kunt bereiken en statistieken over campagnes met pushmeldingen en functies die ook toegankelijk via Hallo Reach API (en bepaalde elementen van Hallo lage ophalen niveau Push-API). Houd er rekening mee dat of u Hallo API's of Hallo gebruikersinterface gebruikt, u toointegrate moet zowel Azure Mobile Engagement en het bereik in uw toepassing voor elk platform Hello SDK voordat u kunt bereiken campagnes.

> [!NOTE]
> Veel secties Hallo **Mobile Engagement** gebruikersinterface portal bevatten Hallo **HELP weergeven** knop. Druk op deze knop tooget meer contextuele informatie over een sectie.
> 
> 

## <a name="four-types-of-push-notifications"></a>Vier typen pushmeldingen
1. Aankondigingen - kunt u toosend reclame berichten toousers die hen tooanother locatie in uw app of toosend omleidt ze tooa webpagina of buiten uw app worden opgeslagen. 
2. Polls - kunt u toogather gegevens van eindgebruikers door vragen aan hen te vragen.
3. Gegevens-Pushes - kunt u toosend een binair of base64-gegevensbestand. Hallo-gegevens in een gegevens-push tooyour toepassing toomodify van uw huidige gebruikerservaring in uw app verzonden. Uw toepassing moet toobe kunnen tooprocess Hallo gegevens in een gegevens-push.

## <a name="campaign-details"></a>Campagnedetails
Bewerken, kopiëren, verwijderen of campagnes die u hebt nog niet geactiveerd door de muiswijzer op hun namen activeren of u kunt klikken op tooopen ze. U kunt de campagnes die al zijn geactiveerd door de muiswijzer op hun namen klonen of u kunt klikken op tooopen ze. U kunt echter een campagne niet wijzigen zodra deze is geactiveerd.

![Reach1][18]

## <a name="reach-feedback"></a>Feedback bereiken
Klik op **statistieken** toosee Hallo details van een Reach-campagne. Hallo **eenvoudige** weergave biedt een visuele representatie in Hallo vorm van een kolom staafdiagram over wat is er gebeurd nadat een campagne is geactiveerd. Hallo **Geavanceerd** weergave biedt meer gedetailleerde informatie over Hallo pushcampagne. Deze gegevens meer niet beschikbaar als u een campagne test dat wil zeggen een push verzonden tooa test-apparaat verzendt. Hier ziet u hoe deze gegevens moeten worden geïnterpreteerd:

1. **Gepusht** -Hiermee geeft u het aantal berichten gepusht toohello apparaten Hallo. Dit nummer is afhankelijk van Hallo doelgroep die u hebt opgegeven tijdens het Hallo pushcampagne te maken. Als u een doelgroep niet opgeeft, wordt deze push uit tooall Hallo ingeschreven apparaten worden verzonden. Net als alle andere pushservices we niet Hallo meldingen push rechtstreeks toohello apparaten, maar in plaats daarvan push ze het desbetreffende platform toohello specifieke Push Notification Services (PNS - GCM-APNS/WNS) zodat ze Hallo meldingen toohello apparaten kunnen leveren. 
2. **Bezorgd** -Hiermee geeft u het aantal berichten dat is geleverd door Hallo PNS toohello apparaat en bevestigd Hallo als ontvangen door Mobile Engagement SDK. 
   
   *Redenen voor geleverd tellen lager is dan het aantal Pushed:*
   
   1. Als gebruiker Hallo Hallo app van Hallo-apparaat is verwijderd maar Hallo PNS niet kent het gelijktijdig Hallo die we Hallo push toohello PNS sturen wordt het Hallo-bericht worden verwijderd.
   2. Als Hallo apparaat Hallo app heeft maar Hallo apparaten zelf voor langere tijd offline was, mislukken hello PNS toodeliver Hallo-bericht toohello apparaat. 
   3. Als het Hallo-bericht toohello apparaat verzonden maar Hallo Mobile Engagement SDK in de app Hallo Hallo inhoud van het Hallo-bericht niet herkent, komt het bericht. Dit kan gebeuren als het Hallo-aanpassing van Hallo melding in Hallo-app genereert een uitzondering die we catch in Hallo SDK en verwijder het Hallo-bericht. Dit kan ook optreden als Hallo-app op Hallo-apparaat met een versie van Hallo Mobile Engagement SDK die niet kunnen toounderstand Hallo nieuwere versie van push het Hallo-bericht verzonden vanuit Hallo-platform, maar dit is alleen wanneer het Hallo-app is bijgewerkt na de Hallo kennisgeving uit de service-platform Hallo is verzonden. Hallo **Geavanceerd** tabblad vertelt u hoeveel berichten zijn verwijderd. 
   4. Op iOS-apparaten kunnen berichten soms niet verzonden als het Hallo-apparaat op de accu of als Hallo app aanzienlijke hoeveelheid energie verbruikt bij het verwerken van externe meldingen. Dit is een beperking van Hallo iOS-apparaten.   
3. **Weergegeven** -Hiermee geeft u het aantal berichten die met succes toohello app gebruiker op Hallo-apparaat in Hallo vorm van een Systeemmelding push/out-van-app in het meldingencentrum hello of een in-app-melding binnen Hallo mobiele weergegeven Hallo App.  Hallo **Geavanceerd** tabblad vertelt u hoeveel systeemmeldingen zijn en hoeveel waren in app-meldingen. 
   
   *Redenen voor het weergegeven aantal lager is dan het aantal afgeleverde (wachten toobe weergegeven)*
   
   1. Als Hallo melding campagne een einddatum op deze had, dan is het mogelijk dat Hallo melding is geleverd, maar wanneer Hallo tijd tooopen documentatie en het toohello app gebruiker weergeven, is het al verlopen zodat deze nooit is weergegeven.   
   2. Als het Hallo-bericht is een melding in de app vervolgens Hallo melding alleen weergegeven als Hallo app gebruiker Hallo app opent. In gevallen waarbij Hallo app gebruikers Hallo app nog niet geopend Hallo SDK rapporteert dat Hallo melding is geleverd, maar nog niet weergegeven totdat het Hallo-app wordt geopend. 
   3. Als Hallo-bericht een melding in de app is en toobe weergegeven op een specifieke activiteit en/of vervolgens ook de Hallo-melding worden gerapporteerd, zoals geleverd is geconfigureerd, maar nog niet is geleverd tot opent Hallo gebruiker Hallo-app op een bepaald scherm. 
4. **Gebruikersinteracties** -Hiermee geeft u het aantal berichten welke gebruiker Hallo-app heeft gecommuniceerd met en bevat Hallo-berichten die ondernomen of afgesloten zijn Hallo. 
   
   * *Hallo app gebruiker kan actie een melding in een van de volgende manieren Hallo:*
     
     1. Als hello notification system/out-van-app-melding is of een in-app-melding verzonden als de melding alleen-lezen en Hallo app gebruiker klikt op Hallo-melding.
     2. Als Hallo-bericht een melding in de app met een tekst- of webweergave is of polls Hallo vervolgens app gebruiker klikt op Hallo actieknop in Hallo melding.
     3. Als het Hallo-bericht is een melding in de app met een webweergave vervolgens app de gebruiker klikt op een URL in de webweergave [alleen Android] Hallo Hallo
   * *Hallo app gebruiker kan een melding in een van de volgende manieren Hallo afsluiten:*
     
     1. Hallo knop Sluiten te klikken op Hallo melding rechtstreeks. 
     2. Lezer weg of Hallo melding verwijderen. 
     3. In-app-meldingen met tekst of web-inhoud en polls zijn doorgaans weergegeven toohello app gebruiker in een proces in twee stappen. Ze eerst een melding te zien en wanneer ze op het klikt, zien ze Hallo daaropvolgende tekst/web/poll-inhoud. Hallo app gebruiker een melding in een van deze stappen kunt afsluiten en details in de geavanceerde weergave Hallo Hallo wordt dit vastgelegd. 
5. **Ondernomen** -Hiermee geeft u het aantal berichten die expliciet waarop actie is ondernomen door Hallo app gebruiker waren Hallo. Dit is de meest interessante aantal Hallo zoals dit geeft aan hoeveel gebruikers van de app zijn geïnteresseerd zijn door u in Hallo melding gepusht het Hallo-bericht. 

> [!NOTE]
> Op iOS & Windows-platforms, als de gebruiker Hallo Hallo app openen en Hallo campagne is een campagne 'Op elk gewenst moment' dan is het mogelijk dat beide buiten de app en in-app-meldingen worden weergegeven op Hallo hetzelfde moment. Dit kan leiden tot een telling weergegeven hoger is dan Hallo geleverd. Als gebruiker Hallo werkt of acties Hallo melding vervolgens zelfs Hallo gebruiker interacties/Actioned aantal kan niet groter zijn dan geleverd. 
> 
> 

![Reach2][19]

## <a name="see-also"></a>Zie ook
* [Concepten][Link 6]
* [Troubleshooting Guide-Service][Link 24]

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

