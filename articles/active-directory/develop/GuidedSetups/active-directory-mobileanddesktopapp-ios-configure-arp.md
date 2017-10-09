---
title: aaaAzure AD v2 iOS Getting Started - configureren (ARP) | Microsoft Docs
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
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Van de toepassing hello registratie informatie tooyour app toevoegen

In deze stap moet u tooadd Hallo toepassings-Id tooyour project:

1.  In `ViewController.swift`, vervang Hallo regel die begint met '`let kClientID`' met:
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
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
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
