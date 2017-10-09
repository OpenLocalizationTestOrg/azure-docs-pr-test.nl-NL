---
title: aaaAzure AD v2 ASP.NET Web Server aan de slag - Test | Microsoft Docs
description: Implementeren van Microsoft-aanmeldingspagina op een ASP.NET-oplossing met een traditioneel browser gebaseerde webtoepassing met behulp van standaard OpenID Connect
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
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="952de-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="952de-103">Test your code</span></span>

<span data-ttu-id="952de-104">Druk op `F5` toorun uw project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="952de-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="952de-105">Hallo browser openen en u te sturen*http://localhost: {poort}* Hier ziet u Hallo *aanmelden met Microsoft* knop.</span><span class="sxs-lookup"><span data-stu-id="952de-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="952de-106">Opwekken en klikt u op het toosign in.</span><span class="sxs-lookup"><span data-stu-id="952de-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="952de-107">Wanneer u bent klaar tootest, een werk- of schoolaccount (Azure Active Directory) of een persoonlijke (live.com, outlook.com) account toosign in gebruik.</span><span class="sxs-lookup"><span data-stu-id="952de-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Aanmelden met Microsoft-browservenster](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Aanmelden met Microsoft-browservenster](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="952de-110">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="952de-110">Expected results</span></span>
<span data-ttu-id="952de-111">Hallo-gebruiker is na het aanmelden, omgeleide toohello startpagina van de website die HTTPS-URL opgegeven in uw toepassing registratie-informatie in de Portal voor registratie van Microsoft-toepassing hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="952de-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="952de-112">Deze pagina wordt nu *Hallo {User}* en een koppeling toosign-out en een koppeling toosee Hallo claims van de gebruiker – dit is een koppeling toohello autoriseren controller eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="952de-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="952de-113">Zie de claims van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="952de-113">See user's claims</span></span>
<span data-ttu-id="952de-114">Selecteer Hallo hyperlink toosee Hallo claims van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="952de-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="952de-115">Dit leidt u toohello controller en de weergave die alleen beschikbaar toousers die worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="952de-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="952de-116">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="952de-116">Expected results</span></span>
 <span data-ttu-id="952de-117">Hier ziet u een tabel met Hallo basiseigenschappen van Hallo geregistreerde gebruiker:</span><span class="sxs-lookup"><span data-stu-id="952de-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="952de-118">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="952de-118">Property</span></span> | <span data-ttu-id="952de-119">Waarde</span><span class="sxs-lookup"><span data-stu-id="952de-119">Value</span></span> | <span data-ttu-id="952de-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="952de-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="952de-121">Naam</span><span class="sxs-lookup"><span data-stu-id="952de-121">Name</span></span> | <span data-ttu-id="952de-122">{De volledige gebruikersnaam}</span><span class="sxs-lookup"><span data-stu-id="952de-122">{User Full Name}</span></span> | <span data-ttu-id="952de-123">de voor- en achternaam van de gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="952de-123">hello user’s first and last name</span></span>
|<span data-ttu-id="952de-124">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="952de-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="952de-125">Hallo gebruikersnaam gebruikt tooidentify Hallo geregistreerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="952de-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="952de-126">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="952de-126">Subject</span></span>| <span data-ttu-id="952de-127">{Onderwerp}</span><span class="sxs-lookup"><span data-stu-id="952de-127">{Subject}</span></span>|<span data-ttu-id="952de-128">Een tekenreeks toouniquely Hallo gebruikersaanmelding op Hallo web identificeren</span><span class="sxs-lookup"><span data-stu-id="952de-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="952de-129">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="952de-129">Tenant ID</span></span>| <span data-ttu-id="952de-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="952de-130">{Guid}</span></span>| <span data-ttu-id="952de-131">Een *guid* toouniquely vertegenwoordigen de Azure Active Directory-organisatie van de gebruiker van het Hallo.</span><span class="sxs-lookup"><span data-stu-id="952de-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="952de-132">Bovendien ziet u een tabel met inbegrip van alle gebruikersclaims in verificatieaanvraag opgenomen.</span><span class="sxs-lookup"><span data-stu-id="952de-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="952de-133">Voor een lijst van alle claims in een Token Id en de uitleg raadpleegt u dit [artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "lijst van Claims in Token Id").</span><span class="sxs-lookup"><span data-stu-id="952de-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="952de-134">Test een methode die heeft toegang tot een *[autoriseren]* kenmerk (optioneel)</span><span class="sxs-lookup"><span data-stu-id="952de-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="952de-135">In deze stap maakt test u toegang tot Hallo geverifieerde domeincontroller als anonieme gebruiker:</span><span class="sxs-lookup"><span data-stu-id="952de-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="952de-136">Selecteer Hallo koppeling toosign-out Hallo gebruikers- en afmelden voltooid Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="952de-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="952de-137">Typ nu in uw browser http://localhost: {poort} / tooaccess uw domeincontroller die is beveiligd met Hallo geverifieerde `[Authorize]` kenmerk</span><span class="sxs-lookup"><span data-stu-id="952de-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="952de-138">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="952de-138">Expected results</span></span>
<span data-ttu-id="952de-139">U ontvangt Hallo prompt waarvoor u tooauthenticate toosee Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="952de-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="952de-140">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="952de-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="952de-141">Beveiligen van uw hele website</span><span class="sxs-lookup"><span data-stu-id="952de-141">Protect your entire web site</span></span>
<span data-ttu-id="952de-142">tooprotect uw hele website toevoegen Hallo `AuthorizeAttribute` te`GlobalFilters` in `Global.asax` `Application_Start` methode:</span><span class="sxs-lookup"><span data-stu-id="952de-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="952de-143">**Hoe toorestrict gebruikers slechts één organisatie toosign in tooyour toepassing**</span><span class="sxs-lookup"><span data-stu-id="952de-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="952de-144">Standaard persoonlijke accounts (waaronder outlook.com, live.com en anderen), evenals een werk- en schoolaccounts accounts van een bedrijf of organisatie die is geïntegreerd met Azure Active Directory kunnen aanmelden tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="952de-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="952de-145">Als u wilt dat uw toepassing tooaccept aanmeldingen van slechts één Azure Active Directory-organisatie, vervangt u Hallo `Tenant` parameter in *web.config* van `Common` toohello tenantnaam van de organisatie Hallo-voorbeeld *contoso.onmicrosoft.com*. Daarna wijzigen Hallo `ValidateIssuer` argument in uw *OWIN-Opstartklasse* te`true`.</span><span class="sxs-lookup"><span data-stu-id="952de-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="952de-146">gebruikers uit alleen een lijst met specifieke organisaties tooallow ingesteld `ValidateIssuer` tootrue en gebruik Hallo `ValidIssuers` parameter toospecify een lijst met organisaties.</span><span class="sxs-lookup"><span data-stu-id="952de-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="952de-147">Een andere optie is een aangepaste methode tooimplement toovalidate Hallo uitgevers van certificaten met de parameter IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="952de-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="952de-148">Voor meer informatie over `TokenValidationParameters`, Zie [dit](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN-artikel") MSDN-artikel.</span><span class="sxs-lookup"><span data-stu-id="952de-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

