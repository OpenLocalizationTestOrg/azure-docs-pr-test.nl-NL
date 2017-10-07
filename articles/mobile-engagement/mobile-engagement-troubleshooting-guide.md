---
title: aaaAzure Mobile Engagement probleemoplossing handleidingen
description: Gids voor probleemoplossing voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement - Gids problemen oplossen
## <a name="introduction"></a>Inleiding
Hallo voorbereidingshandleiding voor het oplossen van problemen krijgt u inzicht hoofdoorzaken van enkele regelmatig terugkomt en wordt u in staat stellen tootroubleshoot zelf. 

## <a name="general"></a>Algemeen
In het algemeen, zorg er altijd Hallo volgende:

1. Zorg ervoor dat u alle vereiste voor integratie, zoals beschreven in Hallo stappen hebt doorlopen onze [zelfstudies aan de slag](mobile-engagement-windows-store-dotnet-get-started.md)
2. U gebruikt de meest recente versie Hallo van Hallo platform SDK's. 
3. Testen op een daadwerkelijk apparaat en een emulator omdat sommige problemen alleen specifieke tooemulator zijn. 
4. U niet alle limieten/vertragingen van Mobile Engagement die worden beschreven zijn roept [hier](../azure-subscription-service-limits.md)
5. Als u niet kunt tooconnect toohello Mobile Engagement service back-end- of gegevens die niet voortdurend wordt geladen en zorg ervoor dat er geen actieve service incidenten door te controleren [hier](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>'Monitor' problemen
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>Ik zie mijn apparaat weergegeven op het tabblad van de Monitor Hallo niet
Tabblad Monitor bevat Hallo apparaten verbonden tooyour Mobile Engagement-platform in realtime. Als u fouten van een emulator en een apparaat opspoort, ziet u hier ten minste één sessie. Als het Hallo-app is gedistribueerd, ziet u Hallo actieve sessies meter Hallo-apparaten die zijn verbonden toohello platform in realtime geven. 

Als u uw apparaat niet op het tabblad Hallo-Monitor ziet is waarschijnlijk een probleem SDK-integratie. Sommige algemene stappen tootake tootroubleshoot zijn als volgt:

1. Zorg ervoor dat u de juiste verbindingsreeks Hallo in Hallo mobiele app en het afkomstig van Hallo SDK sleutels en niet Hallo API-sleutels sectie is. Hallo-verbindingsreeks verbindt uw exemplaar van de mobiele app toohello van Hallo Mobile Engagement-app waarin u uw apparaat op het tabblad Hallo-Monitor ziet. 
2. Voor Windows-platform - als uw pagina Hallo overschrijft `OnNavigatedTo` methode, zorg ervoor dat toocall `base.OnNavigatedTo(e)`.
3. Als u bij het integreren van Mobile Engagement in een bestaande mobiele app en vervolgens u ook ervoor zorgen kunt dat u niet in de stappen door te kijken Hallo geavanceerde integratiestappen ontbreekt [hier](mobile-engagement-windows-store-integrate-engagement.md)
4. Zorg ervoor dat u ten minste één schermactiviteiten verzendt overschrijft Hallo pagina met EngagementActivity afhankelijk van Hallo platform werkt zoals beschreven in Hallo [zelfstudies aan de slag](mobile-engagement-windows-store-dotnet-get-started.md).

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>Ik ben tabblad Hallo-Monitor met een sessie te zien zelfs wanneer ik heb verbroken of gesloten mijn app / emulator.
Als u Hallo slechts één verbonden toohello platform op dit moment bent en u een emulator tooopen Hallo-app gebruikt vervolgens is dit waarschijnlijk vanwege tooemulator quirks. In het algemeen moet u tooensure dat u toohello beginscherm op Hallo emulator voor Hallo app sessie toodisconnect is terugkomen. Bovendien op Windows-platform, tijdens foutopsporing met Visual Studio, moet u wellicht dat in Visual Studio u toohello gaan tooensure **Lifecycle Events** menubalk en klik op **onderbreken** tooreally sluiten Hallo-sessie. Zie [Windows zelfstudie](mobile-engagement-windows-store-dotnet-get-started.md) voor meer informatie. 

## <a name="analytics-issues"></a>'Analytics' problemen
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>Ik ben niet alle gegevens ziet / gegevens op tabblad Analytics vernieuwd
Analytische gegevens regelmatig wordt berekend en het kan tot 24 uur duren voordat deze vernieuwen. Deze gegevens niet realtime en ziet u dat deze vernieuwd binnen deze 24 uur periode.
Controleer of echter dat u ten minste één scherm of activiteit toohello platform backend met beide overschrijvende ten minste één pagina met verzendt `EngagementActivity` of aan te roepen `SendActivity` explcitly. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>Ik ben onjuist vastgelegde datum/tijd voor een apparaat op Hallo Analytics tabblad te zien
Hallo is periode voor analyses gebaseerd op Hallo datum in de apparaatinstellingen Hallo gebruikers. Dus zorg ervoor dat Hallo apparaat heeft Hallo datum correct ingesteld. 

## <a name="segment-issues"></a>'Segment' problemen
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>Ik heb een segment hebt gemaakt en wordt weergegeven als grijs of niet alle gegevens worden weergegeven
Maken van het segment niet realtime op Hallo moment. Dit wordt berekend op Hallo dat dezelfde tijd als Hallo analytische gegevens wordt geaggregeerd en dus kan het maximaal 24 uur duren. U moet later terugkomen maar ondertussen moet u ook ervoor zorgen dat uw mobiele apps inderdaad Hallo gegevens verzendt op Hallo basis waarvan u Hallo segmenten vormen. Bijvoorbeeld Als een gebeurtenis zegt "foo" wordt niet door de mobiele apparaten worden verzonden en er niet zou geen segmentgegevens voor een segment dat is gemaakt met EventName = foo als Hallo criterium. Controleer ook de SDK-integratie tooensure uw mobiele app is correct hello gegevens verzenden. 

## <a name="reach-or-push-notifications-issues"></a>Problemen met de bereiken' of Pushmeldingen
### <a name="my-push-messages-are-not-being-delivered"></a>Mijn pushberichten worden niet geleverd
1. Probeer te verzenden van meldingen tooa test apparaat eerste tooensure alle Hallo-onderdelen - mobiele app, SDK en Hallo service goed verbonden en kunnen toodeliver pushmeldingen zijn. 
2. Verzend Hallo eenvoudigste 'melding out van de toepassing' altijd eerst via een campagne die is niet gepland en of er doelgroepcriterium opgegeven. Dit is opnieuw tooprove die melding connectiviteit correct werkt. 
3. Als u met stap problemen bij het leveren van in app-meldingen is ook een goede eerst tootry eerst een out-van-app-melding verzenden. 
4. Zorg ervoor dat Hallo die native Pushbericht correct is geconfigureerd voor uw mobiele app. Afhankelijk van Hallo platform deze ofwel eruit ziet sleutels (Android, Windows) of certificaten (iOS). Zie [gebruikersinterface - instellingen](mobile-engagement-user-interface-settings.md)
5. Gebruiker via Hallo die mobiel besturingssysteem dus zorg ervoor deze dat is buiten de app-meldingen kunnen ook worden geblokkeerd door Hallo niet Hallo geval. 
6. Zorg ervoor dat u niet Hallo instelt *doelgroep negeren push wordt verzonden toousers via Hallo API* optie in Hallo **campagne** gedeelte van een Reach-campagne omdat dit ervoor zorgt dat push meldingen kan alleen worden verzonden via API's. 
7. Zorg ervoor dat u uw pushcampagne met zowel een apparaat is verbonden via Wi-Fi- en phone operator tooeliminate Hallo netwerk netwerkverbinding als mogelijke bron van problemen testen wilt.
8. Zorg ervoor dat systeem Hallo datum/tijd op uw apparaat/emulator omdat elk synchroon apparaat ook Hallo Push Notification Service van de mogelijkheid toodeliver meldingen verstoren juist is. 

Meer platformspecifiek probleemoplossing van de onderstaande instructies:

1. **iOS** 
   
   * Zorg ervoor dat Hallo certificaten voor iOS-Pushmeldingen pushreferenties die geldig en zijn. 
   * Zorg ervoor dat u goed configureert een *productie* certificaat in uw Mobile Engagement-app. 
   * Zorg ervoor dat u wilt testen op een *echte apparaat.* Hallo iOS-simulator kan geen pushberichten verwerken.
   * Zorg ervoor dat bundel-id correct is geconfigureerd in de mobiele app Hallo Hallo. Zie Hallo instructies [hier](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * Bij het testen, moet u 'Ad-Hoc' verdeling in uw mobiele inrichtingsprofiel gebruiken. U zich niet kunnen tooreceive melding als uw app wordt gecompileerd met 'Debug'
2. **Android**
   
   * Zorg ervoor dat u het juiste Project number Hallo hebt opgegeven in uw mobiele app AndroidManifest.xml bestand dat wordt gevolgd door \n teken. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * Ervoor zorgen dat u niet ontbreekt of verkeerd geconfigureerd alle machtigingen in Hallo manifestbestand van Android 
   * Zorg ervoor dat Hallo-projectnummer u tooyour client-app toevoegt van Hallo dezelfde account waar u Hallo GCM-serversleutel hebt verkregen. Een discrepantie tussen Hallo twee wordt voorkomen dat uw pushes wordt verzonden. 
   * Als u system ontvangt meldingen maar niet in-app vervolgens bekijken Hallo [opgeven van een pictogram voor meldingen sectie](mobile-engagement-android-get-started.md) als waarschijnlijk u geeft niet de juiste pictogram Hallo in Hallo manifestbestand van Android. 
   * Als u een melding BigPicture verzendt, zorg ervoor dat als u de installatiekopie van de externe servers hebt moeten ze toobe kunnen toosupport HTTP opnieuw 'Ophalen' en 'HEAD'.
3. **Windows**
   
   * Zorg ervoor dat u Hallo app hebt gekoppeld met een geldig Windows Store-app. In Visual Studio - hebt tooright op Hallo-project en selecteer de optie 'App met de Store koppelen' en selecteer Hallo app die u hebt gemaakt in Windows Store Hallo. Deze Windows Store-app moet dezelfde Hallo van waar u Hallo native pushberichten referenties tooconfigure in Hallo Mobile Engagement-portal hebt verkregen.
   * Als u pushmeldingen out van de toepassing, maar niet in-app-meldingen met ontvangt `EngagementOverlay` integratie vervolgens Zorg dat er een raster hoofdelement in uw pagina. EngagementOverlay gebruikt Hallo eerste 'Raster'-element in de xaml-bestand tooadd twee webweergaven op de pagina gevonden. Als u wilt dat toolocate waar webweergaven wordt ingesteld, kunt u een raster met 'EngagementGrid' als volgt de naam maar u tooensure hebt definiëren er voldoende hoogte en breedte voor Hallo twee opeenvolgende web-weergaven die wordt Hallo melding weergeven en Hallo na aankondiging als in het app-melding:
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>Ik heb een push-melding/aankondiging gemaakt/campagne en zelfs nadat het mij Hallo-bericht verzonden, wordt weergegeven als 'Actief'. Wat betekent dit?
Hallo **campagne** zodat omdat het een langdurige betekenis van de push-melding zoals nieuwe apparaten verbinding maken met tooyour mobile engagement-platform, automatisch hello melding verzonden worden die u in Mobile Engagement gemaakt wordt aangeroepen u configureert hier, zolang ze voldoen aan Hallo criterium die u in Hallo campagne instellen. Dit is niet een schermopname één melding setup. Hebt uitgevoerd, klikt u op Hallo toomanually **voltooien** tooterminate Hallo campagne knop zodat deze niet meer meldingen verzenden. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>Ik heb een pushcampagne gemaakt en ik ontvang meldingen is maar wanneer ik Hallo app opent, krijg ik Hallo dezelfde melding zelfs wanneer ik had ondernomen het eerder?
Dit is waarschijnlijk toohappen tijdens het testen en als u van emulators of sommige testframework zoals TestFlight gebruikmaakt. Wat gebeurt er hier is op elke app exemplaar uitvoeren, is het ophalen van een nieuw apparaat-id en verzenden van back-end van tooour waardoor Hallo Mobile Engagement-platform tootreat als een nieuw apparaat en het Hallo-bericht verzenden. 

## <a name="getting-support"></a>Ondersteuning van
Als u tooresolve Hallo probleem zelf vervolgens kunt u:

1. Zoeken naar uw probleem in de bestaande threads Hallo op StackOverflow-forum en [MSDN-forum](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) en als dat niet vervolgens vraagt u er een vraag. 
2. Als u een functie die vervolgens toevoegen/stem voor Hallo aanvraag ontbreekt op vinden onze [UserVoice forum](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Als u geopend voor ondersteuning van Microsoft een ondersteuningsincident hebt doordat Hallo volgende details: 
   * Azure-abonnement-ID
   * Platform (bijvoorbeeld iOS, Android, enzovoort)
   * App-ID
   * Campagne-ID (voor problemen met push-melding)
   * Apparaat-id
   * Mobile Engagement SDK-versie (bijvoorbeeld Android SDK v2.1.0)
   * Details van fouten met de exacte foutbericht en het scenario

