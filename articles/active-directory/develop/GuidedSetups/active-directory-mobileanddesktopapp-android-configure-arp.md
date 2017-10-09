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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Van de toepassing hello registratie informatie tooyour app toevoegen

In deze stap moet u tooadd Hallo Client-ID tooyour project.

1.  Open `MainActivity` (onder `app`  >  `java`  >   *`{host}.{namespace}`* )
2.  Vervang Hallo regel die begint met `final static String CLIENT_ID` met:
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Open:`app` > `manifests` > `AndroidManifest.xml`
4. Hallo activiteit te volgen toevoegen`manifest\application` knooppunt. In dit register een `BrowserTabActivity` tooallow Hallo OS tooresume uw toepassing na het Hallo-verificatie te voltooien:

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

### <a name="what-is-next"></a>Wat is de volgende

[Testen en valideren](active-directory-mobileanddesktopapp-android-test.md)
