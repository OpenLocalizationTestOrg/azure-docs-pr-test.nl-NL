---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>Hoe tooIntegrate GCM met Mobile Engagement
> [!IMPORTANT]
> U moet volgen Hallo integratie procedure wordt beschreven in Hallo hoe tooIntegrate Engagement op Android-document voordat u deze handleiding.
> 
> Dit document is alleen nuttig als u al geïntegreerde Hallo module en plan toopush Google Play apparaten bereiken. toointegrate Reach-campagnes in uw toepassing, lees eerst hoe tooIntegrate Engagement bereiken op Android.
> 
> 

## <a name="introduction"></a>Inleiding
Integratie van GCM, kunt uw toepassing toobe gepusht.

GCM-nettoladingen toohello SDK altijd gepusht bevatten Hallo `azme` sleutel in het Hallo-gegevensobject. Dus als u GCM voor een ander doel in uw toepassing gebruiken, kunt u filteren op basis van die sleutel pushes.

> [!IMPORTANT]
> Alleen apparaten met Android 2.2 of hoger, met Google Play geïnstalleerd en met Google achtergrond verbinding ingeschakeld kan worden geactiveerd via GCM; u kunt echter integreren deze code veilig op niet-ondersteunde apparaten (alleen intents wordt gebruikt).
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>Met API-sleutel een Google Cloud Messaging-project maken
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>SDK-integratie
### <a name="managing-device-registrations"></a>Het beheren van apparaat-registraties
Elk apparaat een opdracht registratie toohello moet verzenden Google-servers, anders ze kunnen niet worden bereikt.

Een apparaat kan ook Hef de registratie van GCM-meldingen (Hallo apparaat wordt automatisch verwijderd als toepassing hello wordt verwijderd).

Als u geen [Google Play-SDK] of u niet al verzend Hallo registratie opzet, kunt u Engagement Hallo apparaat automatisch voor u geregistreerd.

tooenable dit toevoegen Hallo tooyour na `AndroidManifest.xml` bestand binnen Hallo `<application/>` tag:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Registratie-id toohello Engagement Push service communiceren en meldingen ontvangen
In de volgorde toocommunicate Hallo registratie-id van Hallo apparaat toohello Engagement Push service en de meldingen ontvangen, Hallo na tooyour toevoegen `AndroidManifest.xml` bestand binnen Hallo `<application/>` tag (zelfs als u apparaten registraties zelf beheren):

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

Zorg ervoor dat u hebt Hallo volgende machtigingen in uw `AndroidManifest.xml` (na Hallo `</application>` label).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Verleen Mobile Engagement toegang tooyour GCM-API-sleutel
Ga als volgt [in deze handleiding](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement toegang tooyour GCM-API-sleutel.

[Google Play-SDK]:https://developers.google.com/cloud-messaging/android/start
