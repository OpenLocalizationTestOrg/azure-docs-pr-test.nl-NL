---
title: aaaAzure AD v2 Android aan de slag - Test | Microsoft Docs
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="158ed-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="158ed-103">Test your code</span></span>

1. <span data-ttu-id="158ed-104">Implementeer uw code tooyour apparaat/emulator.</span><span class="sxs-lookup"><span data-stu-id="158ed-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="158ed-105">Als u gereed tootest bent, gebruikt u een Microsoft Azure Active Directory (organisatieaccount) of een Microsoft-Account (live.com, outlook.com) account toosign in.</span><span class="sxs-lookup"><span data-stu-id="158ed-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="158ed-106">![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="158ed-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="158ed-107">
![Aanmelden](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="158ed-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="158ed-108">Toestemming</span><span class="sxs-lookup"><span data-stu-id="158ed-108">Consent</span></span>
<span data-ttu-id="158ed-109">Hallo eerst die een gebruiker zich aanmeldt tooyour toepassing, ze krijgt een toestemming scherm vergelijkbare toohello hieronder, waar ze nodig hebben tooexplicitly accepteren:</span><span class="sxs-lookup"><span data-stu-id="158ed-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Toestemming](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="158ed-111">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="158ed-111">Expected results</span></span>
<span data-ttu-id="158ed-112">U ziet Hallo resultaten van een aanroep tooMicrosoft Graph API 'me' eindpunt gebruikt tootooobtain Hallo gebruikersprofiel - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="158ed-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="158ed-113">Voor een lijst met algemene Microsoft Graph-eindpunten, raadpleegt u dit [artikel](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="158ed-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="158ed-114">Meer informatie over bereikwaarden en gedelegeerde machtigingen</span><span class="sxs-lookup"><span data-stu-id="158ed-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="158ed-115">Hallo Microsoft Graph API vereist Hallo `user.read` tooread Hallo gebruikersprofiel bereik.</span><span class="sxs-lookup"><span data-stu-id="158ed-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="158ed-116">Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="158ed-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="158ed-117">Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes.</span><span class="sxs-lookup"><span data-stu-id="158ed-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="158ed-118">Bijvoorbeeld: voor Microsoft Graph Hallo bereik `Calendars.Read` agenda's van vereiste toolist Hallo gebruikers is.</span><span class="sxs-lookup"><span data-stu-id="158ed-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="158ed-119">In volgorde Hallo tooaccess kalender van de gebruiker in een context van een toepassing, moet u tooadd hello `Calendars.Read` registratiegegevens van machtiging toohello toepassing gedelegeerd en voeg vervolgens Hallo `Calendars.Read` bereik toohello `acquireTokenSilentAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="158ed-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="158ed-120">Hallo gebruiker mogelijk gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.</span><span class="sxs-lookup"><span data-stu-id="158ed-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
