---
title: aaaAdvanced configuratie voor Azure Mobile Engagement Android SDK
description: Hierin wordt beschreven Hallo geavanceerde configuratieopties, met inbegrip van Hallo Android Manifest met Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Geavanceerde configuratie voor Azure Mobile Engagement Android SDK
> [!div class="op_single_selector"]
> * [Universeel Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

Deze procedure wordt beschreven hoe tooconfigure verschillende configuratieopties voor Azure Mobile Engagement Android-apps.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>Machtigingsvereisten
Sommige opties vereisen specifieke machtigingen, die hier worden weergegeven voor de referentie- en in de regel in een specifieke functie Hallo. Toevoegen van deze machtigingen toohello AndroidManifest.xml van uw project direct vóór of na Hallo `<application>` label.

Hallo machtiging code moet toolook zoals Hallo volgende, waarbij u de juiste machtiging Hallo van de volgende tabel Hallo invullen.

    <uses-permission android:name="android.permission.[specific permission]"/>


| Machtiging | Wanneer gebruikt |
| --- | --- |
| INTERNET |Vereist. Voor eenvoudige rapportage |
| ACCESS_NETWORK_STATE |Vereist. Voor eenvoudige rapportage |
| RECEIVE_BOOT_COMPLETED |Vereist. tooshow van Hallo meldingen center na opnieuw opstarten van apparaat |
| WAKE_LOCK |Aanbevolen. Schakelt het verzamelen van gegevens bij gebruik van Wi-Fi of als het scherm is uitgeschakeld |
| TRILLEN |Optioneel. Trillingen ingeschakeld wanneer er worden meldingen ontvangen |
| DOWNLOAD_WITHOUT_NOTIFICATION |Optioneel. Hiermee kunt Android grote afbeelding melding |
| WRITE_EXTERNAL_STORAGE |Optioneel. Hiermee kunt Android grote afbeelding melding |
| ACCESS_COARSE_LOCATION |Optioneel. Rapportage van realtime locatie kunt |
| ACCESS_FINE_LOCATION |Optioneel. Schakelt op basis van een GPS-locatie rapportage |

Vanaf Android M [sommige machtigingen worden beheerd tijdens runtime](mobile-engagement-android-location-reporting.md#android-m-permissions).

Als u al ``ACCESS_FINE_LOCATION``, hoeft u geen tooalso gebruiken ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Android Manifest configuratieopties
### <a name="crash-report"></a>Foutrapportage
foutenrapporten toodisable, voeg deze code tussen Hallo `<application>` en `</application>` tags:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Burst drempelwaarde
Standaard Hallo Engagement servicerapporten Logboeken in realtime. Als uw rapport toepassingslogboeken vaak verschillen, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base ('burst modus' genoemd). dus, voeg deze code tussen Hallo toodo `<application>` en `</application>` tags:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Burst-modus enigszins verhoogt de batterij Hallo maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken). De drempelwaarde burst mag niet langer zijn dan 30000 (30s).

### <a name="session-timeout"></a>Sessietime-out
 U kunt een activiteit beëindigen door Hallo drukken **Start** of **terug** sleutel telefonisch instelling Hallo inactief of door te gaan naar een andere toepassing. Standaard wordt een sessie tien seconden na het einde van de laatste activiteit Hallo beëindigd. Zo voorkomt u een sessie-splitsing van elke gebruiker tijd hello wordt afgesloten en retourneert toohello toepassing snel, dat kan gebeuren wanneer Hallo gebruiker opneemt in een afbeelding controleert een melding, enzovoort. U kunt deze parameter toomodify. dus, voeg deze code tussen Hallo toodo `<application>` en `</application>` tags:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Melden van logboek uitschakelen
### <a name="using-a-method-call"></a>Met behulp van een methodeaanroep van
Als u Engagement toostop logboeken verzenden wilt, kunt u bellen:

    EngagementAgent.getInstance(context).setEnabled(false);

Deze aanroep is permanent: een gedeelde voorkeuren-bestand wordt gebruikt.

Als bij het aanroepen van deze functie Engagement actief is, kan een minuut voor Hallo service toostop duren. Maar deze won't start Hallo-service op alle Hallo volgende keer dat u de toepassing hello starten.

U kunt reporting opnieuw door het aanroepen van dezelfde functie met Hallo logboek inschakelen `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integratie in uw eigen`PreferenceActivity`
In plaats van deze functie aanroept, kunt u deze instelling ook integreren rechtstreeks in uw bestaande `PreferenceActivity`.

U kunt Engagement toouse uw voorkeuren bestand (met de gewenste modus Hallo) configureren in Hallo `AndroidManifest.xml` het bestand met `application meta-data`:

* Hallo `engagement:agent:settings:name` sleutel is de naam van de gebruikte toodefine Hallo van Hallo gedeelde voorkeurenbestand.
* Hallo `engagement:agent:settings:mode` sleutel gebruikte toodefine Hallo modus van Hallo gedeelde voorkeurenbestand is. Gebruik dezelfde Hallo-modus als in uw `PreferenceActivity`. Hallo-modus moet worden doorgegeven als een getal: als u een combinatie van constante vlaggen in uw code gebruikt, controleert u Hallo totale waarde.

Engagement altijd gebruikt Hallo `engagement:key` Booleaanse sleutel binnen Hallo voorkeurenbestand voor het beheren van deze instelling.

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
