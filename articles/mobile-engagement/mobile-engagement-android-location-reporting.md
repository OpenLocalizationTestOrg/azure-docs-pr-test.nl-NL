---
title: aaaLocation rapportage voor Azure Mobile Engagement Android SDK
description: Hierin wordt beschreven hoe tooconfigure locatie rapportage voor Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Locatie rapportage voor Azure Mobile Engagement Android SDK
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Dit onderwerp wordt beschreven hoe toodo locatie rapportage voor uw Android-toepassing.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Locatierapportage
Als u wilt dat locaties toobe gerapporteerd, moet u tooadd een paar regels van configuratie (tussen Hallo `<application>` en `</application>` labels).

### <a name="lazy-area-location-reporting"></a>Vertraagde locatiemelding
Vertraagde locatiemelding kan reporting Hallo land, streek en plaats die zijn gekoppeld aan apparaten. Dit type locatie reporting maakt alleen gebruik van netwerklocaties (gebaseerd op de cel-ID of Wi-Fi). Hallo apparaat gebied wordt maximaal eenmaal per sessie gerapporteerd. Hallo GPS wordt nooit gebruikt en dit type locatie rapport heeft dus lage impact op de accu Hallo.

Gerapporteerde gebieden zijn gebruikte toocompute geografische statistieken over gebruikers, sessies, gebeurtenissen en fouten. Ze kunnen ook worden gebruikt als criterium in Reach-campagnes.

U inschakelen vertraagde locatie voor rapportage met Hallo configuratie die eerder is vermeld in deze procedure:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

U moet ook een machtiging locatie toospecify. Deze code gebruikt ``COARSE`` machtiging:

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Als uw app nodig is, kunt u ``ACCESS_FINE_LOCATION`` in plaats daarvan.

### <a name="real-time-location-reporting"></a>Rapportage van realtime locatie
Rapportage van realtime locatie kunt reporting Hallo-breedtegraad en lengtegraad die zijn gekoppeld aan apparaten. Dit type locatie reporting gebruikt standaard alleen netwerklocaties, op basis van de cel-ID of Wi-Fi. Hallo reporting is alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (bijvoorbeeld tijdens een sessie).

Realtime locaties zijn *niet* toocompute statistieken gebruikt. Het enige doel is tooallow Hallo gebruik van realtime geofencing \<Reach-doelgroep-geofencing\> criterium in Reach-campagnes.

tooenable realtime locatie reporting, een regel toevoegen van code toowhere u Hallo Engagement verbindingsreeks instellen in Hallo launcher activiteit. Hallo resultaat lijkt op Hallo volgende:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>GPS op basis van rapportage
Rapportage van realtime locatie alleen gebruikt standaard locaties op het netwerk. tooenable hello op basis van een GPS-locaties die ver nauwkeurigere, gebruiken Hallo configuration-object:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Achtergrond rapportage
Rapportage van realtime locatie is standaard alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (bijvoorbeeld tijdens een sessie). tooenable hello reporting ook op de achtergrond, gebruik dit configuratieobject:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Wanneer de toepassing hello wordt uitgevoerd op de achtergrond, alleen locaties op het netwerk worden gerapporteerd, zelfs als u ingeschakeld Hallo GPS.
> 
> 

Als het Hallo-gebruikers hun apparaat opnieuw is opgestart, is Hallo achtergrond locatie rapport gestopt. toomake automatisch opnieuw opgestart tijdens het opstarten, voeg deze code.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Android M machtigingen
Vanaf Android M, sommige machtigingen tijdens runtime worden beheerd en goedkeuring van een gebruiker nodig.

Als u Android-API-niveau 23 richt, zijn Hallo runtime machtigingen standaard uitgeschakeld voor nieuwe installaties van de app. Anders zijn ze standaard ingeschakeld.

U kunt in-of uitschakelen die machtigingen in Hallo apparaat instellingen. Het uitschakelen van machtigingen in Hallo Systeemmenu is funest achtergrondprocessen Hallo Hallo-toepassing, dat is het systeemgedrag van een, en heeft geen invloed op de mogelijkheid tooreceive push op de achtergrond.

In de context van de Hallo van Mobile Engagement locatie reporting, zijn Hallo-machtigingen die moeten worden goedgekeurd tijdens runtime:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

Machtigingen van Hallo-gebruiker met een dialoogvenster standaardbesturingssysteem aanvragen. Als de gebruiker Hallo goedkeurt, laat u weten ``EngagementAgent`` tootake die in aanmerking in realtime wijzigen. Hallo wijziging is anders verwerkte Hallo volgende tijd Hallo gebruiker gestart Hallo toepassing.

Hier volgt een voorbeeld code toouse in een activiteit van uw toorequest Toepassingsmachtigingen en voorwaarts Hallo resultaat als positief te``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
