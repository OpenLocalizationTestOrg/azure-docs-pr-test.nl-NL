---
title: aaaAzure AD v2 Windows Desktop aan de slag - Test | Microsoft Docs
description: Hoe Windows Desktop .NET (XAML) toepassingen een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="20714-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="20714-103">Test your code</span></span>

<span data-ttu-id="20714-104">In volgorde tootest uw toepassing, drukt u op `F5` toorun uw project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="20714-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="20714-105">Het hoofdvenster moet worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="20714-105">Your Main Window should appear:</span></span>

![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="20714-107">Wanneer u klaar tootest bent, klikt u op *Microsoft Graph-API aanroepen* en gebruik een Microsoft Azure Active Directory (organisatieaccount) of een Microsoft-Account (live.com, outlook.com) account toosign in.</span><span class="sxs-lookup"><span data-stu-id="20714-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="20714-108">Het Hallo eerst is, ziet u een venster waarin de gebruiker toosign in:</span><span class="sxs-lookup"><span data-stu-id="20714-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![Aanmelden](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="20714-110">Toestemming</span><span class="sxs-lookup"><span data-stu-id="20714-110">Consent</span></span>
<span data-ttu-id="20714-111">Hallo eerste keer dat u zich aanmeldt tooyour toepassing, u krijgt een toestemming scherm vergelijkbare toohello hieronder, wanneer u tooexplicitly accepteren:</span><span class="sxs-lookup"><span data-stu-id="20714-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Toestemming scherm](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="20714-113">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="20714-113">Expected results</span></span>
<span data-ttu-id="20714-114">U ziet gebruikersprofielgegevens door Hallo Microsoft Graph API-aanroep voor welkomstscherm API aanroepen resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="20714-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="20714-115">U ziet ook basisinformatie over Hallo token verkregen `AcquireTokenAsync` of `AcquireTokenSilentAsync` in Hallo Token informatie in:</span><span class="sxs-lookup"><span data-stu-id="20714-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="20714-116">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="20714-116">Property</span></span>  |<span data-ttu-id="20714-117">Indeling</span><span class="sxs-lookup"><span data-stu-id="20714-117">Format</span></span>  |<span data-ttu-id="20714-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="20714-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="20714-119">Naam</span><span class="sxs-lookup"><span data-stu-id="20714-119">Name</span></span> | <span data-ttu-id="20714-120">{De volledige gebruikersnaam}</span><span class="sxs-lookup"><span data-stu-id="20714-120">{User Full name}</span></span> |<span data-ttu-id="20714-121">de voor- en achternaam van de gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="20714-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="20714-122">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="20714-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="20714-123">Hallo gebruikersnaam gebruikt tooidentify Hallo gebruiker</span><span class="sxs-lookup"><span data-stu-id="20714-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="20714-124">Token is verlopen</span><span class="sxs-lookup"><span data-stu-id="20714-124">Token Expires</span></span> |<span data-ttu-id="20714-125">{Datum-/}</span><span class="sxs-lookup"><span data-stu-id="20714-125">{DateTime}</span></span>         |<span data-ttu-id="20714-126">Hallo tijd op welke Hallo-token verloopt.</span><span class="sxs-lookup"><span data-stu-id="20714-126">hello time on which hello token expires.</span></span> <span data-ttu-id="20714-127">MSAL wordt de vervaldatum Hallo uitbreiden voor u te vernieuwen Hallo token indien nodig</span><span class="sxs-lookup"><span data-stu-id="20714-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="20714-128">Toegangstoken</span><span class="sxs-lookup"><span data-stu-id="20714-128">Access token</span></span> |<span data-ttu-id="20714-129">{Tekenreeks}</span><span class="sxs-lookup"><span data-stu-id="20714-129">{String}</span></span>         |<span data-ttu-id="20714-130">de tokentekenreeks Hallo verzonden die tooHTTP aanvragen waarvoor de autorisatie-header wordt verzonden</span><span class="sxs-lookup"><span data-stu-id="20714-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="20714-131">Meer informatie over bereikwaarden en gedelegeerde machtigingen</span><span class="sxs-lookup"><span data-stu-id="20714-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="20714-132">Graph API vereist Hallo `user.read` tooread gebruikersprofiel bereik.</span><span class="sxs-lookup"><span data-stu-id="20714-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="20714-133">Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="20714-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="20714-134">Vereist extra scopes sommige andere Graph API's, evenals aangepaste API's voor uw back-endserver.</span><span class="sxs-lookup"><span data-stu-id="20714-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="20714-135">Bijvoorbeeld: voor de grafiek, `Calendars.Read` agenda's van de gebruiker vereist toolist is.</span><span class="sxs-lookup"><span data-stu-id="20714-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="20714-136">In volgorde Hallo tooaccess kalender van de gebruiker in een context van een toepassing, moet u tooadd `Calendars.Read` toepassing registratiegegevens gedelegeerd en voeg vervolgens `Calendars.Read` toohello `AcquireTokenAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="20714-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="20714-137">Gebruiker kan worden gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.</span><span class="sxs-lookup"><span data-stu-id="20714-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



