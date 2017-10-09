---
title: aaaAzure AD v2 Android aan de slag - configureren | Microsoft Docs
description: Hoe een Android-app kunt ophalen van een toegangstoken en Microsoft Graph API of API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Maken van een toepassing (snelle)
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:
1. Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Voer een naam voor uw toepassing en uw e-mailadres
3.  Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld
4.  Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:
1. Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing
2. Voer een naam voor uw toepassing en uw e-mailadres 
3. Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld
4. Klik op `Add Platform`, selecteer daarna `Native Application` en klik op Opslaan
5.  Open `MainActivity` (onder `app`  >  `java`  >   *`{host}.{namespace}`* )
6.  Vervang Hallo *[Voer hier Hallo toepassing Id]* in Hallo regel die begint met `final static String CLIENT_ID` met Hallo toepassings-ID u zojuist hebt geregistreerd:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Open `AndroidManifest.xml` (onder `app`  >  `manifests`) toevoegen Hallo activiteit te volgen`manifest\application` knooppunt. Hiermee registreert een `BrowserTabActivity` tooallow Hallo OS tooresume uw toepassing na het Hallo-verificatie te voltooien:
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
In Hallo `BrowserTabActivity`, Vervang `[Enter hello application Id here]` met Hallo toepassings-ID.
</li>
</ol>
