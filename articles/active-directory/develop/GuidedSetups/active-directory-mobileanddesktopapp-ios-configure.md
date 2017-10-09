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
## <a name="create-an-application-express"></a><span data-ttu-id="47cbf-103">Maken van een toepassing (snelle)</span><span class="sxs-lookup"><span data-stu-id="47cbf-103">Create an application (Express)</span></span>
<span data-ttu-id="47cbf-104">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="47cbf-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="47cbf-105">Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="47cbf-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="47cbf-106">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="47cbf-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="47cbf-107">Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="47cbf-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="47cbf-108">Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code</span><span class="sxs-lookup"><span data-stu-id="47cbf-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="47cbf-109">Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="47cbf-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="47cbf-110">Ga te[Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="47cbf-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="47cbf-111">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="47cbf-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="47cbf-112">Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="47cbf-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="47cbf-113">Klik op `Add Platform`, selecteer daarna `Native Application` en klikt u op`Save`</span><span class="sxs-lookup"><span data-stu-id="47cbf-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="47cbf-114">Ga terug tooXcode.</span><span class="sxs-lookup"><span data-stu-id="47cbf-114">Go back tooXcode.</span></span> <span data-ttu-id="47cbf-115">In `ViewController.swift`, vervang Hallo regel die begint met '`let kClientID`' met Hallo toepassings-ID u zojuist hebt geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="47cbf-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="47cbf-116">Control + klik <code>Info.plist</code> toobring Hallo contextafhankelijke menu omhoog en klik vervolgens op: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="47cbf-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="47cbf-117">Onder Hallo <code>dict</code> de hoofd-knooppunt, voeg de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="47cbf-117">Under hello <code>dict</code> root node, add hello following:</span></span>
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
<span data-ttu-id="47cbf-118">Vervang <i> <code>[Your_Application_Id_Here]</code> </i> Hello toepassings-Id die u zojuist hebt geregistreerd</span><span class="sxs-lookup"><span data-stu-id="47cbf-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
