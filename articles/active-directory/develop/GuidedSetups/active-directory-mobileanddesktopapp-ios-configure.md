---
title: aaaAzure AD v2 iOS aan de slag - configureren | Microsoft Docs
description: Hoe iOS (Swift)-toepassingen met een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Maken van een toepassing (snelle)
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:
1. Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Voer een naam voor uw toepassing en uw e-mailadres
3.  Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld
4.  Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)

1.  Ga te[Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app)
2.  Voer een naam voor uw toepassing en uw e-mailadres
3.  Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld
4.  Klik op `Add Platform`, selecteer daarna `Native Application` en klikt u op`Save`
5.  Ga terug tooXcode. In `ViewController.swift`, vervang Hallo regel die begint met '`let kClientID`' met Hallo toepassings-ID u zojuist hebt geregistreerd:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Control + klik <code>Info.plist</code> toobring Hallo contextafhankelijke menu omhoog en klik vervolgens op: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
Onder Hallo <code>dict</code> de hoofd-knooppunt, voeg de volgende Hallo:
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
Vervang <i> <code>[Your_Application_Id_Here]</code> </i> Hello toepassings-Id die u zojuist hebt geregistreerd
</li>
</ol>
