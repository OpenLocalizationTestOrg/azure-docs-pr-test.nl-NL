---
title: aaaAzure AD v2 iOS Getting Started - Test | Microsoft Docs
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="8dc8b-103">Test uitvoeren van query's Hallo Microsoft Graph API van uw iOS-toepassing</span><span class="sxs-lookup"><span data-stu-id="8dc8b-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="8dc8b-104">Druk op `Command`  +  `R` toorun Hallo code in Hallo simulator.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="8dc8b-106">Wanneer u klaar tootest bent, tikt u op *'Microsoft Graph API aanroepen'* en u na vragen aan gebruiker tootype worden uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="8dc8b-107">Toestemming</span><span class="sxs-lookup"><span data-stu-id="8dc8b-107">Consent</span></span>
<span data-ttu-id="8dc8b-108">Hallo eerste keer dat u zich aanmeldt tooyour toepassing, u krijgt een toestemming scherm vergelijkbare toohello hieronder, wanneer u tooexplicitly accepteren:</span><span class="sxs-lookup"><span data-stu-id="8dc8b-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Toestemming scherm](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="8dc8b-110">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="8dc8b-110">Expected results</span></span>
<span data-ttu-id="8dc8b-111">U ziet gebruikersprofielgegevens geretourneerd door Hallo Microsoft Graph API-aanroep in Hallo *logboekregistratie* sectie.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="8dc8b-112">Meer informatie over bereikwaarden en gedelegeerde machtigingen</span><span class="sxs-lookup"><span data-stu-id="8dc8b-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="8dc8b-113">Hallo Microsoft Graph API vereist Hallo `user.read` tooread Hallo gebruikersprofiel bereik.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="8dc8b-114">Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="8dc8b-115">Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="8dc8b-116">Bijvoorbeeld: voor Microsoft Graph Hallo bereik `Calendars.Read` agenda's van vereiste toolist Hallo gebruikers is.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="8dc8b-117">In volgorde Hallo tooaccess kalender van de gebruiker in een context van een toepassing, moet u tooadd hello `Calendars.Read` registratiegegevens van machtiging toohello toepassing gedelegeerd en voeg vervolgens Hallo `Calendars.Read` bereik toohello `acquireTokenSilent` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="8dc8b-118">Hallo gebruiker mogelijk gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.</span><span class="sxs-lookup"><span data-stu-id="8dc8b-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



