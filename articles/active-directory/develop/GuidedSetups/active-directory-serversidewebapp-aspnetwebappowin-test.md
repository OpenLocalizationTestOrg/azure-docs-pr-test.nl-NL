---
title: Azure AD v2 ASP.NET Web Server ophalen gestart - testen | Microsoft Docs
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
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="df734-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="df734-103">Test your code</span></span>

<span data-ttu-id="df734-104">Druk op `F5` uw project in Visual Studio wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="df734-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="df734-105">De browser wordt geopend en u directe *http://localhost: {poort}* Hier ziet u de *aanmelden met Microsoft* knop.</span><span class="sxs-lookup"><span data-stu-id="df734-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="df734-106">Opwekken en klik op aan te melden.</span><span class="sxs-lookup"><span data-stu-id="df734-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="df734-107">Wanneer u klaar bent om te testen, gebruikt u een werk- of schoolaccount (Azure Active Directory) of een persoonlijke (live.com, outlook.com)-account aan te melden.</span><span class="sxs-lookup"><span data-stu-id="df734-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Aanmelden met Microsoft-browservenster](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Aanmelden met Microsoft-browservenster](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="df734-110">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="df734-110">Expected results</span></span>
<span data-ttu-id="df734-111">Na het aanmelden, wordt de gebruiker omgeleid naar de startpagina van de website die de HTTPS-URL die is opgegeven in uw toepassing registratie-informatie in de Registratieportal voor Microsoft-toepassing.</span><span class="sxs-lookup"><span data-stu-id="df734-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="df734-112">Deze pagina wordt nu *Hallo {User}* en een koppeling naar afmelden en een koppeling om te zien van claims van de gebruiker – dit is een koppeling naar de controller autoriseren eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="df734-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="df734-113">Zie de claims van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="df734-113">See user's claims</span></span>
<span data-ttu-id="df734-114">Selecteer de hyperlink om te zien van claims van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="df734-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="df734-115">Dit leidt u naar de domeincontroller en de weergave die alleen beschikbaar voor gebruikers die zijn geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="df734-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="df734-116">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="df734-116">Expected results</span></span>
 <span data-ttu-id="df734-117">Hier ziet u een tabel met de basiseigenschappen van de aangemelde gebruiker:</span><span class="sxs-lookup"><span data-stu-id="df734-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="df734-118">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="df734-118">Property</span></span> | <span data-ttu-id="df734-119">Waarde</span><span class="sxs-lookup"><span data-stu-id="df734-119">Value</span></span> | <span data-ttu-id="df734-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="df734-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="df734-121">Naam</span><span class="sxs-lookup"><span data-stu-id="df734-121">Name</span></span> | <span data-ttu-id="df734-122">{De volledige gebruikersnaam}</span><span class="sxs-lookup"><span data-stu-id="df734-122">{User Full Name}</span></span> | <span data-ttu-id="df734-123">De voor- en achternaam van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="df734-123">The user’s first and last name</span></span>
|<span data-ttu-id="df734-124">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="df734-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="df734-125">De gebruikersnaam die wordt gebruikt voor het identificeren van de aangemelde gebruiker</span><span class="sxs-lookup"><span data-stu-id="df734-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="df734-126">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="df734-126">Subject</span></span>| <span data-ttu-id="df734-127">{Onderwerp}</span><span class="sxs-lookup"><span data-stu-id="df734-127">{Subject}</span></span>|<span data-ttu-id="df734-128">Een tekenreeks als unieke identificatie van de aanmelding van de gebruiker op het web</span><span class="sxs-lookup"><span data-stu-id="df734-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="df734-129">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="df734-129">Tenant ID</span></span>| <span data-ttu-id="df734-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="df734-130">{Guid}</span></span>| <span data-ttu-id="df734-131">Een *guid* uniek vertegenwoordigt de organisatie Azure Active Directory van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="df734-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="df734-132">Bovendien ziet u een tabel met inbegrip van alle gebruikersclaims in verificatieaanvraag opgenomen.</span><span class="sxs-lookup"><span data-stu-id="df734-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="df734-133">Voor een lijst van alle claims in een Token Id en de uitleg raadpleegt u dit [artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "lijst van Claims in Token Id").</span><span class="sxs-lookup"><span data-stu-id="df734-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="df734-134">Test een methode die heeft toegang tot een *[autoriseren]* kenmerk (optioneel)</span><span class="sxs-lookup"><span data-stu-id="df734-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="df734-135">In deze stap wordt u de toegang tot de controller geverifieerd als anonieme gebruiker testen:</span><span class="sxs-lookup"><span data-stu-id="df734-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="df734-136">Selecteer de koppeling voor afmelden van de gebruiker en de afmelden proces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="df734-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="df734-137">Typ nu in uw browser http://localhost: {poort} / geverifieerde toegang tot uw domeincontroller die is beveiligd met de `[Authorize]` kenmerk</span><span class="sxs-lookup"><span data-stu-id="df734-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="df734-138">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="df734-138">Expected results</span></span>
<span data-ttu-id="df734-139">U ontvangt de prompt dat u hoeft te worden geverifieerd om te zien van de weergave.</span><span class="sxs-lookup"><span data-stu-id="df734-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="df734-140">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="df734-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="df734-141">Beveiligen van uw hele website</span><span class="sxs-lookup"><span data-stu-id="df734-141">Protect your entire web site</span></span>
<span data-ttu-id="df734-142">Omwille van de gehele website toevoegen de `AuthorizeAttribute` naar `GlobalFilters` in `Global.asax` `Application_Start` methode:</span><span class="sxs-lookup"><span data-stu-id="df734-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="df734-143">**Hoe kunt u voorkomen dat gebruikers slechts één organisatie aan te melden bij uw toepassing**</span><span class="sxs-lookup"><span data-stu-id="df734-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="df734-144">Standaard persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts van een bedrijf of organisatie die is geïntegreerd met Azure Active Directory kunnen aanmelden bij uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="df734-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="df734-145">Als u wilt dat uw toepassing te accepteren aanmeldingen van slechts één Azure Active Directory-organisatie, vervangt u de `Tenant` parameter in *web.config* van `Common` naar de tenantnaam van de organisatie – bijvoorbeeld *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="df734-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="df734-146">Daarna wijzigen de `ValidateIssuer` argument in uw *OWIN-Opstartklasse* naar `true`.</span><span class="sxs-lookup"><span data-stu-id="df734-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="df734-147">Instellen zodat gebruikers alleen een lijst met specifieke organisaties `ValidateIssuer` op waar en gebruik de `ValidIssuers` parameter om een lijst met organisaties.</span><span class="sxs-lookup"><span data-stu-id="df734-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="df734-148">Er is een andere optie voor het implementeren van een aangepaste methode voor het valideren van de uitgevers van certificaten met de parameter IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="df734-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="df734-149">Voor meer informatie over `TokenValidationParameters`, Zie [dit](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN-artikel") MSDN-artikel.</span><span class="sxs-lookup"><span data-stu-id="df734-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

