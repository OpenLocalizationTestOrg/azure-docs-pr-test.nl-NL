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
## <a name="create-an-application-express"></a><span data-ttu-id="bda9a-103">Maken van een toepassing (snelle)</span><span class="sxs-lookup"><span data-stu-id="bda9a-103">Create an application (Express)</span></span>
<span data-ttu-id="bda9a-104">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="bda9a-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="bda9a-105">Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="bda9a-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="bda9a-106">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="bda9a-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="bda9a-107">Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="bda9a-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="bda9a-108">Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code</span><span class="sxs-lookup"><span data-stu-id="bda9a-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="bda9a-109">Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="bda9a-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="bda9a-110">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="bda9a-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="bda9a-111">Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing</span><span class="sxs-lookup"><span data-stu-id="bda9a-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="bda9a-112">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="bda9a-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="bda9a-113">Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="bda9a-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="bda9a-114">Klik op `Add Platform`, selecteer daarna `Native Application` en klik op Opslaan</span><span class="sxs-lookup"><span data-stu-id="bda9a-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="bda9a-115">Open `MainActivity` (onder `app`  >  `java`  >   *`{host}.{namespace}`* )</span><span class="sxs-lookup"><span data-stu-id="bda9a-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="bda9a-116">Vervang Hallo *[Voer hier Hallo toepassing Id]* in Hallo regel die begint met `final static String CLIENT_ID` met Hallo toepassings-ID u zojuist hebt geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="bda9a-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="bda9a-117">Open `AndroidManifest.xml` (onder `app`  >  `manifests`) toevoegen Hallo activiteit te volgen`manifest\application` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bda9a-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="bda9a-118">Hiermee registreert een `BrowserTabActivity` tooallow Hallo OS tooresume uw toepassing na het Hallo-verificatie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="bda9a-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="bda9a-119">In Hallo `BrowserTabActivity`, Vervang `[Enter hello application Id here]` met Hallo toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="bda9a-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
