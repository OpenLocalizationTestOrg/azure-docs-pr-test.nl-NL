---
title: Azure AD v2 iOS aan de slag - configureren | Microsoft Docs
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
ms.openlocfilehash: 0ebca65585fc87bd4a85ba092cd423fce9540f58
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="1fa13-103">Maken van een toepassing (snelle)</span><span class="sxs-lookup"><span data-stu-id="1fa13-103">Create an application (Express)</span></span>
<span data-ttu-id="1fa13-104">Nu gaat u naar het registreren van uw toepassing in de *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="1fa13-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="1fa13-105">Registreren van uw toepassingen via de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="1fa13-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="1fa13-106">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="1fa13-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="1fa13-107">Zorg ervoor dat de optie voor begeleide Setup is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="1fa13-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="1fa13-108">Volg de instructies voor het verkrijgen van de toepassings-ID en plak deze in uw code</span><span class="sxs-lookup"><span data-stu-id="1fa13-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="1fa13-109">De registratiegegevens van uw toepassing toevoegen aan uw oplossing (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="1fa13-109">Add your application registration information to your solution (Advanced)</span></span>

1.  <span data-ttu-id="1fa13-110">Ga naar [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="1fa13-110">Go to [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="1fa13-111">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="1fa13-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="1fa13-112">Zorg ervoor dat de optie voor begeleide Setup is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="1fa13-112">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="1fa13-113">Klik op `Add Platform`, selecteer daarna `Native Application` en klikt u op`Save`</span><span class="sxs-lookup"><span data-stu-id="1fa13-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="1fa13-114">Ga terug naar Xcode.</span><span class="sxs-lookup"><span data-stu-id="1fa13-114">Go back to Xcode.</span></span> <span data-ttu-id="1fa13-115">In `ViewController.swift`, vervangt u de regel die begint met '`let kClientID`' met de toepassings-ID die u zojuist hebt geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="1fa13-115">In `ViewController.swift`, replace the line starting with '`let kClientID`' with the application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="1fa13-116">Control + klik <code>Info.plist</code> online zetten van het contextafhankelijke menu en klik vervolgens op: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="1fa13-116">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="1fa13-117">Onder de <code>dict</code> de hoofd-knooppunt, voeg de volgende:</span><span class="sxs-lookup"><span data-stu-id="1fa13-117">Under the <code>dict</code> root node, add the following:</span></span>
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
<span data-ttu-id="1fa13-118">Vervang <i> <code>[Your_Application_Id_Here]</code> </i> met de toepassings-Id die u zojuist hebt geregistreerd</span><span class="sxs-lookup"><span data-stu-id="1fa13-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with the Application Id you just registered</span></span>
</li>
</ol>
