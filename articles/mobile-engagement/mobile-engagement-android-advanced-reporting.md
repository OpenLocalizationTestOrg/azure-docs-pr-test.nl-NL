---
title: aaaAdvanced rapportageopties voor Azure Mobile Engagement Android SDK
description: Hierin wordt beschreven hoe toodo reporting toocapture analytics geavanceerde voor Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Geavanceerde Reporting met Engagement voor Android
> [!div class="op_single_selector"]
> * [Universeel Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Dit onderwerp beschrijft aanvullende scenario's voor rapportage in uw Android-toepassing. U kunt deze opties toohello app gemaakt in Hallo toepassen [aan de slag](mobile-engagement-android-get-started.md) zelfstudie.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

Hallo-zelfstudie u voltooid is opzettelijk direct en eenvoudig, maar er zijn geavanceerde opties die u kunt kiezen.

## <a name="modifying-your-activity-classes"></a>Wijzigen van uw `Activity` klassen
In Hallo [zelfstudie aan de slag](mobile-engagement-android-get-started.md), alle moest u toodo toomake is uw `*Activity` subklassen overnemen van Hallo overeenkomt `Engagement*Activity` klassen. Bijvoorbeeld, als uw verouderde activiteit uitgebreid `ListActivity`, brengt u deze uitbreiden `EngagementListActivity`.

> [!IMPORTANT]
> Wanneer u `EngagementListActivity` of `EngagementExpandableListActivity`, zorg ervoor dat alle aanroepen te`requestWindowFeature(...);` voor Hallo-aanroep is uitgevoerd, te`super.onCreate(...);`, anders een crash plaatsvindt.
> 
> 

U vindt deze klassen in Hallo `src` map, en kunt kopiëren naar uw project. Hallo klassen bevinden zich ook in Hallo **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Alternatieve methode: call `startActivity()` en `endActivity()` handmatig
Als u niet kunt of toooverload niet wilt dat uw `Activity` klassen, u kunt in plaats daarvan beginnen en eindigen uw activiteiten door het aanroepen van Hallo `EngagementAgent`van methoden rechtstreeks.

> [!IMPORTANT]
> Hallo Android SDK wordt nooit aangeroepen door Hallo `endActivity()` methode, zelfs als de toepassing hello is gesloten (voor Android toepassingen zijn nooit gesloten). Het is dus *maximaal* toocall Hallo aanbevolen `startActivity()` methode in Hallo `onResume` retouraanroep van *alle* uw activiteiten en Hallo `endActivity()` methode in Hallo `onPause()` retouraanroep van *alle* uw activiteiten. Dit is Hallo alleen manier toobe ervoor dat sessies niet gelekt. Als een sessie is gelekt, verbreekt Hallo Engagement service back-end Hallo Engagement nooit (omdat Hallo service verbonden blijft als een sessie in behandeling is).
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

In dit voorbeeld is vergelijkbaar toohello `EngagementActivity` klasse en varianten, waarvan de broncode wordt verstrekt in Hallo `src` map.

## <a name="using-applicationoncreate"></a>Met behulp van Application.onCreate()
Alle code die u in plaatsen `Application.onCreate()` en in andere toepassingen retouraanroepen voor de processen van uw toepassing, met inbegrip van Hallo Engagement service wordt uitgevoerd. Deze mogelijk ongewenste neveneffecten hebben, zoals overbodige geheugentoewijzingen en threads in Hallo Engagement proces, of dubbel broadcast ontvangers of services.

Als u negeren `Application.onCreate()`, het is raadzaam toe te voegen Hallo volgende codefragment aan Hallo begin van uw `Application.onCreate()` functie:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

U kunt doen Hallo hetzelfde geldt voor `Application.onTerminate()`, `Application.onLowMemory()`, en `Application.onConfigurationChanged(...)`.

U kunt ook uitbreiden `EngagementApplication` in plaats van het uitbreiden van `Application`: Hallo callback `Application.onCreate()` Hallo proces controleren en aanroepen `Application.onApplicationProcessCreate()` alleen als het huidige proces Hallo niet Hallo één hosting Hallo Engagement service, hello gelden dezelfde regels voor Hallo andere retouraanroepen.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Labels in Hallo AndroidManifest.xml bestand
Hallo in Hallo servicetag in Hallo AndroidManifest.xml bestand `android:label` kenmerk kunt u toochoose Hallo naam Hallo Engagement service wanneer deze tooend gebruikers in 'Services wordt uitgevoerd' welkomstscherm van hun telefoonnummer wordt weergegeven. Het is raadzaam te dit kenmerk instelt`"<Your application name>Service"` (bijvoorbeeld `"AcmeFunGameService"`).

Geven Hallo `android:process` kenmerk zorgt ervoor dat Hallo Engagement service wordt uitgevoerd in een eigen proces (Engagement in Hallo dezelfde verwerken wanneer uw toepassing uw main/UI-thread mogelijk minder goed wordt uitgevoerd).

## <a name="building-with-proguard"></a>Bouwen met ProGuard
Als u uw toepassingspakket met ProGuard bouwt, moet u tookeep sommige klassen. U kunt na configuratie codefragment hello gebruiken:

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
