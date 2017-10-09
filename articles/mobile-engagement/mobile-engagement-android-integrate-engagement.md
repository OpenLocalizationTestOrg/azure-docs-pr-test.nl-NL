---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>Hoe tooIntegrate Engagement voor Android
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Engagement Analytics en bewaking van functies in uw Android-toepassing.

> [!IMPORTANT]
> Het minimale Android SDK-API-niveau moet 10 of hoger (Android 2.3.3 of hoger).
> 
> 

Hallo stappen te volgen zijn dat onvoldoende tooactivates Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals. rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement in uw Android-API tagging geavanceerde](mobile-engagement-android-use-engagement-api.md) sinds deze statistieken zijn afhankelijk van de toepassing.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Hallo Engagement SDK en service insluiten in uw Android-project
Download de Android SDK van Hallo [hier](https://aka.ms/vq9mfn) ophalen `mobile-engagement-VERSION.jar` naar Hallo `libs` map van uw Android-project (de map libs Hallo maken als deze nog niet bestaat).

> [!IMPORTANT]
> Als u uw toepassingspakket met ProGuard bouwt, moet u tookeep sommige klassen. U kunt na configuratie codefragment hello gebruiken:
> 
> -openbare klasse houden * breidt android.os.IInterface-klasse com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {houden
> 
> <methods>; }
> 
> 

Geef de verbindingsreeks Engagement door aanroepen Hallo methode in Hallo launcher activiteit te volgen:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op de Azure Portal.

* Indien deze ontbreken, Hallo volgende Android machtigingen toevoegen (voordat Hallo `<application>` tag):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Toevoegen van de volgende sectie hello (tussen Hallo `<application>` en `</application>` labels):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Wijziging `<Your application name>` door Hallo-naam van uw toepassing.

> [!TIP]
> Hallo `android:label` kenmerk kunt u toochoose Hallo naam Hallo Engagement service die toohello eindgebruikers in 'Services wordt uitgevoerd' welkomstscherm van hun telefoonnummer wordt weergegeven. Het is aanbevolen tooset dit kenmerk te`"<Your application name>Service"` (bijvoorbeeld `"AcmeFunGameService"`).
> 
> 

Geven Hallo `android:process` kenmerk zorgt ervoor dat Hallo Engagement service wordt uitgevoerd in een eigen proces (Engagement uitgevoerd in dezelfde verwerken als uw toepassing wordt Controleer uw main/UI-thread mogelijk minder goed Hallo).

> [!NOTE]
> Alle code die u in plaatsen `Application.onCreate()` en andere retouraanroepen toepassing wordt uitgevoerd voor de processen van uw toepassing, met inbegrip van Hallo Engagement service. Er kunnen ongewenste neveneffecten (zoals overbodige geheugentoewijzingen en threads in Hallo Engagement proces, dubbele broadcast ontvangers of services).
> 
> 

Als u negeren `Application.onCreate()`, het is aanbevolen tooadd Hallo volgende codefragment aan Hallo begin van uw `Application.onCreate()` functie:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

U kunt doen Hallo hetzelfde geldt voor `Application.onTerminate()`, `Application.onLowMemory()` en `Application.onConfigurationChanged(...)`.

U kunt ook uitbreiden `EngagementApplication` in plaats van het uitbreiden van `Application`: Hallo callback `Application.onCreate()` Hallo proces controleren en aanroepen `Application.onApplicationProcessCreate()` alleen als het huidige proces Hallo niet Hallo één hosting Hallo Engagement service, hello gelden dezelfde regels voor Hallo andere retouraanroepen.

## <a name="basic-reporting"></a>Basic-rapportage
### <a name="recommended-method-overload-your-activity-classes"></a>Aanbevolen methode: overbelasting uw `Activity` klassen
In de volgorde tooactivate Hallo rapport van alle Hallo logboeken vereist voor Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken, hebt u alleen toomake alle uw `*Activity` onderliggende klassen overnemen Hallo overeenkomt `Engagement*Activity` klassen (bijvoorbeeld als uw verouderde activiteit breidt `ListActivity`, zorg er breidt `EngagementListActivity`).

**Zonder Engagement:**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**Met Engagement:**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> Wanneer u `EngagementListActivity` of `EngagementExpandableListActivity`, zorg ervoor dat alle aanroepen te`requestWindowFeature(...);` voor Hallo-aanroep is uitgevoerd, te`super.onCreate(...);`, anders een crash wordt uitgevoerd.
> 
> 

U vindt deze klassen in Hallo `src` map, en kunt kopiëren naar uw project. Hallo klassen bevinden zich ook in Hallo **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Alternatieve methode: call `startActivity()` en `endActivity()` handmatig
Als u niet kunt of toooverload niet wilt dat uw `Activity` klassen, u kunt in plaats daarvan starten en beëindigen van uw activiteiten door aan te roepen `EngagementAgent`van methoden rechtstreeks.

> [!IMPORTANT]
> Hallo Android SDK wordt nooit aangeroepen door Hallo `endActivity()` methode, zelfs als de toepassing hello is gesloten (voor Android toepassingen zijn daadwerkelijk nooit gesloten). Het is dus *maximaal* toocall Hallo aanbevolen `startActivity()` methode in Hallo `onResume` retouraanroep van *alle* uw activiteiten en Hallo `endActivity()` methode in Hallo `onPause()` retouraanroep van *alle* uw activiteiten. Dit is Hallo alleen manier toobe ervoor dat sessies niet wordt gelekt. Als een sessie is gelekt, verbreekt Hallo Engagement service nooit van back-end Hallo Engagement (omdat Hallo service verbonden blijft als een sessie in behandeling is).
> 
> 

Hier volgt een voorbeeld:

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

In dit voorbeeld vergelijkbaar toohello `EngagementActivity` klasse en varianten, waarvan de broncode wordt verstrekt in Hallo `src` map.

## <a name="test"></a>Test
Nu uw integratie controleren door te voeren van uw mobiele app in een emulator of het apparaat en verifiëren van de registratie van een sessie op het tabblad Hallo-Monitor.

de volgende secties Hallo zijn optioneel.

## <a name="location-reporting"></a>Locatierapportage
Als u wilt dat locaties toobe gerapporteerd, moet u tooadd een paar regels van configuratie (tussen Hallo `<application>` en `</application>` labels).

### <a name="lazy-area-location-reporting"></a>Vertraagde locatiemelding
Vertraagde locatiemelding kunt tooreport Hallo land, streek en plaats die zijn gekoppeld toodevices. Dit type locatie reporting maakt alleen gebruik van netwerklocaties (gebaseerd op de cel-ID of Wi-Fi). Hallo apparaat gebied wordt maximaal eenmaal per sessie gerapporteerd. Hallo GPS wordt nooit gebruikt en dit type locatie rapport heeft slechts weinig dus (geen toosay geen) impact op de accu Hallo.

Gerapporteerde gebieden zijn gebruikte toocompute geografische statistieken over gebruikers, sessies, gebeurtenissen en fouten. Ze kunnen ook worden gebruikt als criterium in Reach-campagnes.

tooenable vertraagde locatie voor rapportage, u kunt dit doen met behulp van Hallo configuratie die eerder is vermeld in deze procedure:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Of u kunt blijven gebruiken ``ACCESS_FINE_LOCATION`` als u al in uw toepassing gebruikt.

### <a name="real-time-location-reporting"></a>Rapportage van realtime locatie
Rapportage van realtime locatie kunt tooreport Hallo breedtegraad en lengtegraad gekoppeld toodevices. Standaard alleen gebruik van dit type locatie reporting netwerklocaties (gebaseerd op de cel-ID of Wi-Fi), en Hallo reporting is alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie).

Realtime-locaties zijn *niet* toocompute statistieken gebruikt. Het enige doel is tooallow Hallo gebruik van realtime geofencing \<Reach-doelgroep-geofencing\> criterium in Reach-campagnes.

tooenable realtime locatie rapportage, u kunt dit doen met behulp van Hallo configuratie die eerder is vermeld in deze procedure:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Of u kunt blijven gebruiken ``ACCESS_FINE_LOCATION`` als u al in uw toepassing gebruikt.

#### <a name="gps-based-reporting"></a>GPS op basis van rapportage
Rapportage van realtime locatie alleen gebruikt standaard op basis van netwerklocaties. tooenable hello gebruik van GPS op basis van locaties (die veel meer nauwkeurige), gebruikt u Hallo configuration-object:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Achtergrond rapportage
Rapportage van realtime locatie is standaard alleen actief wanneer Hallo toepassing wordt uitgevoerd op voorgrond (dat wil zeggen tijdens een sessie). tooenable hello ook op de achtergrond, worden gebruikt door reporting Hallo configuration-object:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Wanneer de toepassing hello wordt uitgevoerd op de achtergrond, alleen op basis van netwerklocaties worden gerapporteerd, zelfs als u ingeschakeld Hallo GPS.
> 
> 

Hallo achtergrond locatie rapport wordt gestopt als Hallo gebruiker het apparaat opnieuw is opgestart, kunt u deze automatisch opnieuw opgestart tijdens het opstarten toomake toevoegen:

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

U moet ook tooadd Hallo machtiging te volgen, indien deze ontbreken:

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Android M machtigingen
Vanaf Android M, sommige machtigingen tijdens runtime worden beheerd en moet de goedkeuring van een gebruiker.

Hallo runtime machtigingen worden uitgeschakeld voor nieuwe installaties van apps standaard als u Android-API-niveau 23 richt. Anders zal het worden standaard ingeschakeld.

Hallo-gebruiker kunt in-of uitschakelen die machtigingen in Hallo apparaat instellingen. Het uitschakelen van machtigingen van Systeemmenu is funest achtergrondprocessen van de toepassing hello, dit is een systeemgedrag en heeft geen invloed op de mogelijkheid tooreceive push op de achtergrond.

In de context van de Hallo van Mobile Engagement zijn Hallo-machtigingen die moeten worden goedgekeurd tijdens runtime:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE`(alleen bij Android-API-niveau 23 voor deze doelen)

Hallo externe opslag wordt alleen gebruikt voor Reach grote afbeelding functie. Als u gebruikers vragen over deze machtiging toobe verstoren, kunt u deze verwijderen als u deze gebruikt voor Mobile Engagement alleen maar op Hallo kosten van het uitschakelen van de functie grote afbeelding.

Voor Hallo locatie functies, moet u machtigingen toouser met een dialoogvenster standaardbesturingssysteem aanvragen. Als de gebruiker Hallo goedkeurt, moet u tootell ``EngagementAgent`` tootake die in aanmerking in realtime (anders Hallo wijziging worden verwerkte Hallo volgende tijd Hallo gestart Hallo-Gebruikerstoepassing) wijzigen.

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>Geavanceerde rapportage
Eventueel, als u tooreport toepassing specifieke gebeurtenissen, fouten en taken wilt, moet u toouse Hallo Engagement API via de methoden Hallo Hallo `EngagementAgent` klasse. Een object van deze klasse kan worden opgehaald door de aanroepende Hallo `EngagementAgent.getInstance()` statische methode.

Hallo Engagement API toouse kunnen alle Engagement geavanceerde mogelijkheden en wordt beschreven in Hallo hoe tooUse de Engagement-API voor Android (en van de technische documentatie Hallo Hallo `EngagementAgent` klasse).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Geavanceerde configuratie (in AndroidManifest.xml)
### <a name="wake-locks"></a>Wake-vergrendelingen
Als u toobe ervoor wilt dat de statistieken worden verzonden in realtime bij gebruik van Wi-Fi of wanneer het welkomstscherm is uitgeschakeld, voegt u Hallo optionele machtiging te volgen:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Foutrapportage
Als u de foutenrapporten toodisable wilt, voeg deze toe (tussen Hallo `<application>` en `</application>` labels):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Burst drempelwaarde
Standaard Hallo Engagement servicerapporten Logboeken in realtime. Als uw toepassing Logboeken heel vaak rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base (dit wordt Hallo 'burst modus' genoemd). toodo dus toevoegen (tussen Hallo `<application>` en `</application>` labels):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Hallo burst-modus iets langer Hallo accu levensduur maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken). Het is aanbevolen toouse een ' burst ' drempelwaarde niet langer dan 30000 (30s).

### <a name="session-timeout"></a>Sessietime-out
Een sessie is beëindigd per 10 standaard, na het Hallo-einde van de laatste activiteit (die doorgaans optreedt, door te drukken Hallo start of Back-sleutel, telefonisch instelling Hallo inactief of door te gaan naar een andere toepassing). Dit is tooavoid een sessie-splitsing van elke gebruiker tijd Hallo afsluiten en toohello toepassing zeer snel terug (dit kan gebeuren wanneer hij een installatiekopie worden opgepikt controleren een melding, enz.). U kunt deze parameter toomodify. toodo dus toevoegen (tussen Hallo `<application>` en `</application>` labels):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Melden van logboek uitschakelen
### <a name="using-a-method-call"></a>Met behulp van een methodeaanroep van
Als u Engagement toostop logboeken verzenden wilt, kunt u bellen:

            EngagementAgent.getInstance(context).setEnabled(false);

Deze aanroep is permanent: een gedeelde voorkeuren-bestand wordt gebruikt.

Als bij het aanroepen van deze functie Engagement actief is, kan 1 minuut voor Hallo service toostop duren. Maar deze won't start Hallo-service op alle Hallo volgende keer dat u de toepassing hello starten.

U kunt reporting opnieuw door het aanroepen van dezelfde functie met Hallo logboek inschakelen `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integratie in uw eigen`PreferenceActivity`
In plaats van deze functie aanroept, kunt u deze instelling ook integreren rechtstreeks in uw bestaande `PreferenceActivity`.

U kunt Engagement toouse uw voorkeuren bestand (met de gewenste modus Hallo) configureren in Hallo `AndroidManifest.xml` het bestand met `application meta-data`:

* Hallo `engagement:agent:settings:name` sleutel is de naam van de gebruikte toodefine Hallo van Hallo gedeelde voorkeurenbestand.
* Hallo `engagement:agent:settings:mode` sleutel gebruikte toodefine Hallo modus van Hallo gedeelde voorkeurenbestand is, moet u Hallo dezelfde modus als in uw `PreferenceActivity`. Hallo-modus moet worden doorgegeven als een getal: als u een combinatie van constante vlaggen in uw code gebruikt, controleert u Hallo totale waarde.

Engagement altijd gebruik Hallo `engagement:key` Booleaanse sleutel binnen Hallo voorkeurenbestand voor het beheren van deze instelling.

Hallo volgende voorbeeld van `AndroidManifest.xml` toont Hallo standaardwaarden:

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

Vervolgens kunt u toevoegen een `CheckBoxPreference` in de indeling van uw voorkeur zoals Hallo volgt:

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
