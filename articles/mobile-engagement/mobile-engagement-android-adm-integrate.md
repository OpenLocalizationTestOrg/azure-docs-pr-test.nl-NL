---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a>Hoe tooIntegrate ADM met Engagement
> [!IMPORTANT]
> U moet volgen Hallo integratie procedure wordt beschreven in Hallo hoe tooIntegrate Engagement op Android-document voordat u deze handleiding.
> 
> Dit document is alleen nuttig als u al is geïntegreerd Hallo Reach-module en plan toopush Amazon-apparaten. toointegrate Reach-campagnes in uw toepassing, lees eerst hoe tooIntegrate Engagement bereiken op Android.
> 
> 

## <a name="introduction"></a>Inleiding
Integratie van ADM, kunt uw toepassing toobe gepusht wanneer de doelcomputer Amazon Android-apparaten.

ADM-nettoladingen toohello SDK altijd gepusht bevatten Hallo `azme` sleutel in het Hallo-gegevensobject. Dus als u in uw toepassing ADM voor een ander doel gebruikt, kunt u filteren op basis van die sleutel pushes.

> [!IMPORTANT]
> Alleen Amazon Kindle apparaten met Android 4.0.3 of hoger worden ondersteund door de Amazon Device Messaging; u kunt echter deze code veilig op andere apparaten integreren.
> 
> 

## <a name="sign-up-tooadm"></a>TooADM aanmelden
Als u niet hebt gedaan, moet u de ADM inschakelen op de Amazon-account.

Hallo procedure wordt beschreven op: [ <https://developer.amazon.com/sdk/adm/credentials.html>].

U krijgt bij voltooiing van Hallo procedure:

* OAuth-referenties (een Client-ID en een Clientgeheim) voor Engagement toobe kunnen toopush uw apparaten.
* Een API-sleutel die moet worden geïntegreerd in uw toepassing.

## <a name="sdk-integration"></a>SDK-integratie
### <a name="managing-device-registrations"></a>Het beheren van apparaat-registraties
Elk apparaat een opdracht registratie toohello moet verzenden ADM-servers, anders ze kunnen niet worden bereikt.

Als u al Hallo [ADM-clientbibliotheek], en al [ADM geïntegreerd] u rechtstreeks kunt gaan tooandroid-sdk-adm-ontvangen.

Als u niet ADM geïntegreerd nog Engagement een eenvoudigere manier tooenable heeft in uw toepassing:

Bewerk uw `AndroidManifest.xml` bestand:

* Hallo Amazon-naamruimte, Hallo-bestand moet beginnen met het als volgt toevoegen:
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* Hallo binnen `<application/>` tag, het toevoegen van deze sectie:
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Na het toevoegen van Hallo amazon tag mogelijk hebt u een opbouwfout als uw doel van de Projectbuild lager dan Android 2.1 is. U hebt toouse een **Android 2.1 +** doel bouwen (Maak je geen zorgen, kunt u nog steeds een `minSdkVersion` too4 instellen).
* Hallo ADM-API-sleutel integreren als een actief door [deze procedure].

Volg de instructies van de volgende secties Hallo Hallo.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Registratie-id toohello Engagement Push service communiceren en meldingen ontvangen
In de volgorde toocommunicate Hallo registratie-id van Hallo apparaat toohello Engagement Push service en de meldingen ontvangen, Hallo na tooyour toevoegen `AndroidManifest.xml` bestand binnen Hallo `<application/>` tag (zelfs als u de ADM zonder Engagement gebruiken):

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

Zorg ervoor dat u hebt Hallo volgende machtigingen in uw `AndroidManifest.xml` (voordat Hallo `</application>` label).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Verleen Engagement OAuth-referenties
Dien uw OAuth-referenties (Client-ID en Clientgeheim) in de Engagement-Portal.

[< https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM-clientbibliotheek]:https://developer.amazon.com/sdk/adm/setup.html
[ADM geïntegreerd]:https://developer.amazon.com/sdk/adm/integrating-app.html
[deze procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
