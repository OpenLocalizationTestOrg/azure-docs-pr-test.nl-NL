---
title: Azure AD v2 Android aan de slag - testen | Microsoft Docs
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="96f94-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="96f94-103">Test your code</span></span>

1. <span data-ttu-id="96f94-104">Implementeer uw code op uw apparaat/emulator.</span><span class="sxs-lookup"><span data-stu-id="96f94-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="96f94-105">Wanneer u klaar bent om te testen, gebruikt u een Microsoft Azure Active Directory (organisatieaccount) of een Microsoft-Account (live.com, outlook.com)-account aan te melden.</span><span class="sxs-lookup"><span data-stu-id="96f94-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="96f94-106">![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="96f94-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="96f94-107">
![Aanmelden](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="96f94-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="96f94-108">Toestemming</span><span class="sxs-lookup"><span data-stu-id="96f94-108">Consent</span></span>
<span data-ttu-id="96f94-109">De eerste keer dat een gebruiker zich bij uw toepassing aanmeldt ze krijgt een scherm toestemming vergelijkbaar met de hieronder, waar ze moeten expliciet accepteren:</span><span class="sxs-lookup"><span data-stu-id="96f94-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Toestemming](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="96f94-111">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="96f94-111">Expected results</span></span>
<span data-ttu-id="96f94-112">U ziet de resultaten van een aanroep naar Microsoft Graph API 'me' eindpunt dat wordt gebruikt op het gebruikersprofiel - https://graph.microsoft.com/v1.0/me verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="96f94-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="96f94-113">Voor een lijst met algemene Microsoft Graph-eindpunten, raadpleegt u dit [artikel](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="96f94-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="96f94-114">Meer informatie over bereikwaarden en gedelegeerde machtigingen</span><span class="sxs-lookup"><span data-stu-id="96f94-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="96f94-115">De Microsoft Graph API vereist de `user.read` bereik van het gebruikersprofiel lezen.</span><span class="sxs-lookup"><span data-stu-id="96f94-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="96f94-116">Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="96f94-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="96f94-117">Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes.</span><span class="sxs-lookup"><span data-stu-id="96f94-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="96f94-118">Bijvoorbeeld: voor het bereik van Microsoft Graph `Calendars.Read` is vereist voor een lijst met agenda's van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="96f94-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="96f94-119">Voor toegang tot de agenda van de gebruiker in een context van een toepassing, moet u toevoegen de `Calendars.Read` overgedragen machtigingen voor de toepassingsregistratie-informatie en voeg vervolgens de `Calendars.Read` bereik voor de `acquireTokenSilentAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="96f94-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="96f94-120">De gebruiker kan gevraagd om extra toestemmingen als u het aantal scopes verhogen.</span><span class="sxs-lookup"><span data-stu-id="96f94-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
