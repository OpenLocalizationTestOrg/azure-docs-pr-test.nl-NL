---
title: Gebruikersinterface van de Mobile Engagement - aaaAzure bereiken How To
description: Overzicht van de gebruikersinterface voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Hoe tooget gestart met en het beheer van pushmeldingen tooreach uit tooyour eindgebruikers
Zodra hello SDK is volledig geïntegreerd in uw app, u kunt aan de slag met Hallo Hallo Reach-sectie van Hallo UI tooPush meldingen toohello gebruikers van uw app.  

## <a name="do-your-first-push-notification-campaign"></a>Uw eerste Pushmeldingcampagne doen
* Bevestig dat uw bereik is geïntegreerd in uw app Hello SDK. 
* Selecteer uw toepassing

![First1][1]

* Ga toohello sectie 'Bereik' en klik op 'nieuwe aankondiging'

![First2][2]

* Maak een nieuwe campagne en noem deze
  
![First3][3]

* Selecteer hoe Hallo melding moet worden weergegeven, als In-app alleen

![First4][4]

* Gewenste toopush Hallo-bericht maken

![First5][5]

* U kunt een titel schrijven op Hallo melding (optioneel).
* Schrijf de inhoud van de push-bericht.
* U kunt een installatiekopie uploaden. Let erop dat Hallo van Hallo-bestand kan niet groter zijn dan 32.768 bytes.
* U hebt ook Hallo mogelijkheid tooselect meer opties, maar voor de focus Hallo van deze zelfstudie, gaan we kijken die later.
* Hallo-inhoudstype alleen als de melding selecteren

![First6][6]

* Uw pushcampagne te maken en deze wordt weergegeven in de lijst van uw campagne.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>Uw Pushmeldingcampagne testen
![Test1][8]

* Registreer uw apparaat.
* Klik op Hallo selectievakje Hallo apparaat gewenste toopush.
* Klik op Hallo 'Test' knop toosend Hallo push toohello apparaat.

![Test2][9]

* Hallo campagne activeren

![Test3][10]

* Nu dat u uw campagne hebt gemaakt, hoeft u alleen tooactivate voor Hallo melding toobe tooyour gebruikers gepusht.

## <a name="send-personalized-pushes"></a>Persoonlijke Pushes verzenden
* In dit voorbeeld maakt een push waar een korting van aangepaste code is ingevoerd in Hallo push-melding.

![Personalize1][11]

Persoonlijke instellingen werkt door een markering door vanuit een app-info-tag dus vervangen, hebt u toomake ervoor Hallo gebruiker heeft Hallo juiste app-info eerst gedefinieerd. In dit voorbeeld Hallo hebt beoogde gebruikers een app-info-tag met de naam rebate_code gedefinieerd.
Als bovenstaande omvat pushmeldinginhoud Hallo Hallo markering ${rebate_code} waarmee wordt aangegeven dat het toobe vervangen door de daadwerkelijke inhoud Hallo van Hallo app info-tag is.

> [!WARNING]
> Als Hallo app info-label is niet gedefinieerd voor de gebruiker hello, ontvangt de gebruiker Hallo Hallo push niet.

* Resultaat

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>U kunt tekst hello uw melding verder aanpassen
![Personalize3][13]

* Waaronder de titel Hallo Hallo-melding
* En Hallo inhoud van het Hallo-bericht.
* Kies Hallo type aankondiging (tekst of webweergave)

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>Hallo-hoofdtekst van een aankondiging kan ook worden aangepast met:
* Hallo-actie-URL als u wilt dat toocustomize Hallo landingspagina
* Hallo-titel
* Hallo-hoofdtekst van het Hallo-bericht.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Uw Push Notification onderscheiden (in of buiten de app)
* Kies Hallo type melding push, selecteer uw toepassing, toohello 'Bereik' sectie gaat, selecteert of maakt een pushcampagne en toohello 'Meldingen' sectie gaan.
* Klik op 'leveringsmethode' hello die u wilt.
* Klik op Hallo "Activiteiten beperken" selectievakje in als u de melding Hallo op specifieke activiteiten (schermen geschiedt).

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>'Alleen buiten App' leveringsmethode
![Differentiate2][16]

'Alleen buiten App' leveringsmethode biedt push-melding wanneer de toepassing hello wordt gesloten. Dit is standaard Hallo-pushmelding.
Wanneer u selecteert 'alleen buiten app', moet u al hebt opgegeven Hallo certificaten uit Hallo-platform die het bouwen van uw toepassing op (APNS of GCM).

### <a name="see-also"></a>Zie ook
* [Apple Push Notification Service – certificaten](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging-certificaat](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>'in-App alleen' leveringsmethode
![Differentiate3][17]

'In-App alleen' leveringsmethode biedt push-melding wanneer het Hallo-toepassing wordt uitgevoerd.
Voor deze melding hoeft u niet toogo via Hallo APNS en GCM-systeem.
U kunt uw eindgebruikers Hallo in-app-levering system tooreach.
U kunt volledig Hallo-bericht aanpassen en bepalen in welke activiteit (scherm) Hallo melding wordt weergegeven.

### <a name="anytime-delivery-mode"></a>'Op elk gewenst moment' leveringsmethode
U kunt ervoor kiezen een 'Op elk gewenst moment' leveringsmethode, zorgt ervoor dat u uw eindgebruikers Hallo of tooreach toepassing wordt uitgevoerd of niet.
Als u "Op elk gewenst moment" selecteert, moet u al hebt opgegeven Hallo certificaten uit Hallo-platform die het bouwen van uw toepassing bij (APNS of GCM). 

## <a name="schedule-a-push-campaign"></a>Een Pushcampagne plannen
### <a name="plan-toostart-a-campaign"></a>TooStart een campagne plannen
![Shedule1][18]

Het Hallo-21 maart is en u hebt een aankondiging toomake geschaafd voor Hallo 22e van maart om middernacht. U hebt geen toostay voor Hallo interface toodo een push! U kunt plannen van tevoren Hallo exacte minuut meldingen worden verzonden.

* Ongedaan maken selectievakje 'None' Hallo selectievakje in en selecteer een begintijd 
* Kies Hallo datum- en Hallo die toostart Hallo push campagne.

### <a name="plan-tooend-a-campaign"></a>Tooend een campagne plannen
![Shedule2][19]

U wilt dat uw campagne toostop op Hallo 25e van maart op liquiditeitsoverbrugging: 00 uur, maar u weet dat u niet er toodo deze.
U hebt geen toostay voor Hallo interface toopush! U kunt plannen van tevoren Hallo exacte minuut die uw campagne gestopt.

* Klik op Hallo 'None' selectievakje in of Selecteer een eindtijd
* Kies Hallo datum- en Hallo die toofinish Hallo push campagne.

### <a name="end-a-campaign-manually"></a>Een campagne handmatig beëindigen
![Shedule3][20]

Standaard Hallo 'None' selectievakjes zijn geselecteerd.
Dit betekent dat Hallo campagne wordt gestart zodra u deze in Hallo activeert sectie bereiken en beëindigen wanneer u deze op Hallo wordt gestopt tot komen sectie.

> [!NOTE]
> Campagnes gemaakt zonder een einddatum Hallo push lokaal opslaan op Hallo-apparaat en weergeven Hallo volgende keer Hallo-app wordt geopend, zelfs als Hallo campagne handmatig wordt beëindigd.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Een Push-bericht met een tekstweergave verbeteren
### <a name="what-is-a-text-view"></a>Wat is een tekstweergave?
![TextView1][21]

Een tekstweergave is een pop-upvenster met tekstinhoud. Dit pop-upvenster wordt weergegeven nadat Hallo door eindgebruikers op Hallo pushmelding heeft geklikt.
Een tekstweergave kunt u toopresent meer inhoud tooyour door eindgebruikers. Dit is ook Hallo kans toopresent een aanroep van tooaction zoals springen tooa pagina van uw app, omleiden tooa Store openen van een webpagina een e-mail te verzenden vanaf een geografisch gelokaliseerde zoeken, enzovoort...

### <a name="example-text-view"></a>Voorbeeld: Tekst weergeven
* Uw pushmeldingcampagne in Hallo "Bereikt" sectie maken en geef uw campagne een naam

![TextView2][22]

* Schrijf Hallo-bericht dat wordt weergegeven op Hallo-bericht.
* Aankondiging inhoudstype van 'tekst' Hallo selecteren

![TextView3][23]

> [!NOTE]
> Als u een tekstweergave pushen, beschikt altijd u over een melding eerst. 

* Hallo-tekst (na hebben geselecteerd Hallo-tekstinhoud aankondiging Hallo subsectie wordt weergegeven, zodat u toodefine Hallo tekst die u wilt dat toobe weergegeven.) definiëren

![TextView4][24]

* Schrijf Hallo titel die Hallo boven aan het Hallo-bericht wordt weergegeven.
* Schrijf Hallo belangrijkste inhoud van de tekstweergave Hallo.
* Schrijf Hallo-inhoud die wordt weergegeven op Hallo actieknop (een actieknop kan Hallo toepassing toomake een specifieke actie, zoals het openen van een pagina van de toepassing hello, omleiden tooan appstore of een type bronnen die u kunt opgeven).
* Schrijven Hallo inhoud die wordt weergegeven op de knop Afsluiten hello (door te klikken op de knop Afsluiten hello, Hallo tekstweergave verdwijnt.)
* Maak uw pushmeldingcampagne en wordt deze weergegeven op Hallo campagne lijst.

![TextView5][25]

* Uw gebruikers push notification campagne toosend Hallo tekst weergeven tooyour activeren.

![TextView6][26]

* Resultaat

![TextView7][27]

* Hallo gebruiker ontvangt een melding Hallo en klik op het.
* Hallo weergegeven tekst als met een pop-waardoor Hallo gebruiker toointeract aan.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Een Push-bericht met een webweergave verbeteren
### <a name="what-is-a-web-view"></a>Wat is er een webweergave?
![WebView1][28]

Een webweergave is een pop-upvenster met webinhoud. Dit pop-upvenster wordt weergegeven wanneer Hallo door eindgebruikers op Hallo pushmelding heeft geklikt.
Een webweergave kunt toohave meer interactie met Hallo door eindgebruikers.
Dit is ook Hallo kans toopresent een aanroep van tooaction zoals omleiding tooApp Store openen van een webpagina een e-mail te verzenden vanaf een geografisch gelokaliseerde zoeken, enzovoort...

### <a name="example-web-view"></a>Voorbeeld: Webweergave
* Uw pushcampagne in Hallo "Bereikt" sectie maken en uw campagne een naam geven.

![WebView2][29]

* Schrijf Hallo-bericht dat wordt weergegeven op Hallo-bericht.
* Hallo aankondiging inhoudstype selecteren als 'web'

![WebView3][30]

### <a name="about-announcement-types"></a>Over aankondiging typen:
* Alleen melding: Er is een eenvoudige standaard melding. Dit betekent dat tooit wordt uitgevoerd als een gebruiker erop, geen extra weergave wordt weergegeven, maar alleen Hallo actie die is gekoppeld.
* Tekst-aankondiging: Er is een melding die Hallo gebruiker toohave kijken een tekstweergave stelt.
* Web-aankondiging: Er is een melding die Hallo gebruiker toohave kijken een webweergave stelt.
  Selecteer Hallo 'Web aankondiging' inhoud.

> [!NOTE]
> Als u een webweergave pushen, beschikt altijd u over een melding eerst.

* Hallo webinhoud (na hebben geselecteerd Hallo aankondiging webinhoud, Hallo subsectie wordt weergegeven, zodat u toodefine Hallo webinhoud toobe weergegeven gewenste.) definiëren

![WebView4][31]

* Schrijf Hallo titel die wordt weergegeven boven Hallo aan het Hallo-bericht (optioneel).
* Schrijf hier de HTML-code.
* Klik op Hallo bron modus knop tooswitch edition bewerken en hoe het eruit ziet.
* Schrijf Hallo-inhoud die wordt weergegeven op Hallo actieknop (een actieknop kan Hallo toepassing toomake een specifieke actie, zoals het openen van een pagina van de toepassing hello, omleiden tooa Store of een type bronnen die u kunt opgeven).
* Schrijven Hallo inhoud die wordt weergegeven op de knop Afsluiten hello (door te klikken op de knop Afsluiten hello, webweergave Hallo verdwijnt).
* Resultaat

![WebView5][32]

* Hallo gebruiker Hallo ontvangen en klikt u op.
* Hallo weergegeven tekst als met een pop-waardoor Hallo gebruiker toointeract aan.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

