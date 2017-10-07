---
title: 'Azure Active Directory B2C: Informatie over aangepaste beleidsregels van Hallo starter pack | Microsoft Docs'
description: Een onderwerp op Azure Active Directory B2C aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="d5685-103">Aangepaste beleidsregels van hello Azure AD B2C aangepast beleid starter pack Hallo begrijpen</span><span class="sxs-lookup"><span data-stu-id="d5685-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="d5685-104">Deze sectie vindt u alle Hallo core elementen van Hallo B2C_1A_base beleid dat wordt geleverd met Hallo **Starter Pack** en die wordt gebruikt voor het ontwerpen van uw eigen beleid via overname Hallo Hallo *B2C_1A_base_ beleid voor uitbreidingen*.</span><span class="sxs-lookup"><span data-stu-id="d5685-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="d5685-105">Als zodanig deze meer met name is gericht op het Hallo al gedefinieerd claim typen, claimtransformaties, definities van inhoud, claimproviders met hun technische profielen en core gebruiker trajecten Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5685-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5685-106">Microsoft biedt geen enkele expliciete of impliciete, met ten opzichte van toohello informatie hierna opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d5685-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="d5685-107">Wijzigingen kunnen worden ingevoerd op elk moment vóór GA tijdstip, GA tijdens of na.</span><span class="sxs-lookup"><span data-stu-id="d5685-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="d5685-108">Uw eigen beleid en de Hallo B2C_1A_base_extensions beleid kunnen deze definities overschrijven en uitbreiden van het beleid van dit bovenliggende verstrekken die aanvullende bepalingen nodig.</span><span class="sxs-lookup"><span data-stu-id="d5685-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="d5685-109">hoofdonderdelen van Hallo Hallo *B2C_1A_base beleid* zijn claimtypen, claimtransformaties en inhoud definities.</span><span class="sxs-lookup"><span data-stu-id="d5685-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="d5685-110">Deze elementen kunnen vatbaar toobe waarnaar wordt verwezen in uw eigen beleid ook als in Hallo *B2C_1A_base_extensions beleid*.</span><span class="sxs-lookup"><span data-stu-id="d5685-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="d5685-111">Claims schema 's</span><span class="sxs-lookup"><span data-stu-id="d5685-111">Claims schemas</span></span>

<span data-ttu-id="d5685-112">Dit claims schema's is onderverdeeld in drie secties:</span><span class="sxs-lookup"><span data-stu-id="d5685-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="d5685-113">Een eerste sectie worden de minimale Hallo-claims die vereist voor Hallo gebruiker trajecten toowork goed zijn.</span><span class="sxs-lookup"><span data-stu-id="d5685-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="d5685-114">Een tweede sectie dat een lijst met claims die zijn vereist voor queryreeksparameters Hallo en andere toobe speciale parameters tooother claimproviders doorgegeven, met name login.microsoftonline.com voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="d5685-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="d5685-115">**Wijzig geen deze claims**.</span><span class="sxs-lookup"><span data-stu-id="d5685-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="d5685-116">En uiteindelijk een derde sectie met een lijst met aanvullende, optionele claims die kunnen worden verzameld van de gebruiker hello, opgeslagen in de directory hello en in tokens verzonden tijdens het aanmelden.</span><span class="sxs-lookup"><span data-stu-id="d5685-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="d5685-117">Nieuwe claims type toobe verzameld van Hallo gebruiker en/of verzonden in Hallo token kunnen in deze sectie worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d5685-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5685-118">Hallo claims schema bevat beperkingen op bepaalde claims zoals wachtwoorden en gebruikersnamen.</span><span class="sxs-lookup"><span data-stu-id="d5685-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="d5685-119">Hallo vertrouwen Framework (TF) beleid behandelt Azure AD als andere claimprovider en alle bijbehorende beperkingen zijn gemodelleerd in Hallo premium beleid.</span><span class="sxs-lookup"><span data-stu-id="d5685-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="d5685-120">Een beleid kan worden gewijzigd tooadd meer beperkingen of een andere claimprovider gebruiken voor de opslag van referenties waarvoor een eigen beperkingen.</span><span class="sxs-lookup"><span data-stu-id="d5685-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="d5685-121">Hallo beschikbaar claimtypen worden hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="d5685-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="d5685-122">Claims die vereist voor Hallo gebruiker trajecten zijn</span><span class="sxs-lookup"><span data-stu-id="d5685-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="d5685-123">Hallo na claims zijn vereist voor gebruiker trajecten toowork correct:</span><span class="sxs-lookup"><span data-stu-id="d5685-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="d5685-124">Claims type</span><span class="sxs-lookup"><span data-stu-id="d5685-124">Claims type</span></span> | <span data-ttu-id="d5685-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="d5685-126">*Gebruikers-id*</span><span class="sxs-lookup"><span data-stu-id="d5685-126">*UserId*</span></span> | <span data-ttu-id="d5685-127">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="d5685-127">Username</span></span> |
| <span data-ttu-id="d5685-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="d5685-128">*signInName*</span></span> | <span data-ttu-id="d5685-129">Meld u aan de naam</span><span class="sxs-lookup"><span data-stu-id="d5685-129">Sign in name</span></span> |
| <span data-ttu-id="d5685-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="d5685-130">*tenantId*</span></span> | <span data-ttu-id="d5685-131">Tenant-id (ID) van het gebruikersobject Hallo in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="d5685-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d5685-132">*object-id*</span><span class="sxs-lookup"><span data-stu-id="d5685-132">*objectId*</span></span> | <span data-ttu-id="d5685-133">Object-id (ID) van het gebruikersobject Hallo in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="d5685-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d5685-134">*wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="d5685-134">*password*</span></span> | <span data-ttu-id="d5685-135">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="d5685-135">Password</span></span> |
| <span data-ttu-id="d5685-136">*NieuwWachtwoord*</span><span class="sxs-lookup"><span data-stu-id="d5685-136">*newPassword*</span></span> | |
| <span data-ttu-id="d5685-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="d5685-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="d5685-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="d5685-138">*passwordPolicies*</span></span> | <span data-ttu-id="d5685-139">Wachtwoordbeleid gebruikt door Azure AD B2C Premium toodetermine Wachtwoordsterkte, verlopen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="d5685-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="d5685-140">*Sub*</span><span class="sxs-lookup"><span data-stu-id="d5685-140">*sub*</span></span> | |
| <span data-ttu-id="d5685-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d5685-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="d5685-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="d5685-142">*identityProvider*</span></span> | |
| <span data-ttu-id="d5685-143">*Weergavenaam*</span><span class="sxs-lookup"><span data-stu-id="d5685-143">*displayName*</span></span> | |
| <span data-ttu-id="d5685-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="d5685-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="d5685-145">Het telefoonnummer van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="d5685-145">User's telephone number</span></span> |
| <span data-ttu-id="d5685-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="d5685-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="d5685-147">*E-mail*</span><span class="sxs-lookup"><span data-stu-id="d5685-147">*email*</span></span> | <span data-ttu-id="d5685-148">E-mailadres dat gebruikt toocontact Hallo gebruiker worden kan</span><span class="sxs-lookup"><span data-stu-id="d5685-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="d5685-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="d5685-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="d5685-150">E-mailadres dat Hallo gebruiker kunt toosign in gebruiken</span><span class="sxs-lookup"><span data-stu-id="d5685-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="d5685-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="d5685-151">*otherMails*</span></span> | <span data-ttu-id="d5685-152">E-mailadressen die gebruikt toocontact Hallo gebruiker worden kunnen</span><span class="sxs-lookup"><span data-stu-id="d5685-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="d5685-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="d5685-153">*userPrincipalName*</span></span> | <span data-ttu-id="d5685-154">De gebruikersnaam die is opgeslagen in Azure AD B2C Premium Hallo</span><span class="sxs-lookup"><span data-stu-id="d5685-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d5685-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="d5685-155">*upnUserName*</span></span> | <span data-ttu-id="d5685-156">Gebruikersnaam voor het maken van de UPN-naam</span><span class="sxs-lookup"><span data-stu-id="d5685-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="d5685-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="d5685-157">*mailNickName*</span></span> | <span data-ttu-id="d5685-158">De naam van gebruiker e-mail nick die is opgeslagen in Azure AD B2C Premium Hallo</span><span class="sxs-lookup"><span data-stu-id="d5685-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d5685-159">*nieuwegebruiker*</span><span class="sxs-lookup"><span data-stu-id="d5685-159">*newUser*</span></span> | |
| <span data-ttu-id="d5685-160">*uitgevoerd SelfAsserted invoer*</span><span class="sxs-lookup"><span data-stu-id="d5685-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="d5685-161">Claim die aangeeft of de kenmerken van de gebruiker Hallo zijn verzameld</span><span class="sxs-lookup"><span data-stu-id="d5685-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="d5685-162">*uitgevoerd PhoneFactor invoer*</span><span class="sxs-lookup"><span data-stu-id="d5685-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="d5685-163">Claim waarmee wordt aangegeven of een nieuw telefoonnummer Hallo gebruiker is verzameld</span><span class="sxs-lookup"><span data-stu-id="d5685-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="d5685-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="d5685-164">*authenticationSource*</span></span> | <span data-ttu-id="d5685-165">Hiermee geeft u op of Hallo gebruiker is geverifieerd op sociale id-Provider, login.microsoftonline.com of lokale account</span><span class="sxs-lookup"><span data-stu-id="d5685-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="d5685-166">Claims die vereist zijn voor queryreeksparameters en andere speciale parameters</span><span class="sxs-lookup"><span data-stu-id="d5685-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="d5685-167">Hallo zijn volgende claims vereiste toopass op speciale parameters (inclusief een aantal queryreeksparameters) tooother claimproviders:</span><span class="sxs-lookup"><span data-stu-id="d5685-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="d5685-168">Claims type</span><span class="sxs-lookup"><span data-stu-id="d5685-168">Claims type</span></span> | <span data-ttu-id="d5685-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="d5685-170">*Nux*</span><span class="sxs-lookup"><span data-stu-id="d5685-170">*nux*</span></span> | <span data-ttu-id="d5685-171">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-172">*NCA*</span><span class="sxs-lookup"><span data-stu-id="d5685-172">*nca*</span></span> | <span data-ttu-id="d5685-173">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="d5685-174">*prompt*</span></span> | <span data-ttu-id="d5685-175">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-176">*Mkt*</span><span class="sxs-lookup"><span data-stu-id="d5685-176">*mkt*</span></span> | <span data-ttu-id="d5685-177">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-178">*kredietbrief*</span><span class="sxs-lookup"><span data-stu-id="d5685-178">*lc*</span></span> | <span data-ttu-id="d5685-179">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="d5685-180">*grant_type*</span></span> | <span data-ttu-id="d5685-181">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-182">*bereik*</span><span class="sxs-lookup"><span data-stu-id="d5685-182">*scope*</span></span> | <span data-ttu-id="d5685-183">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="d5685-184">*client_id*</span></span> | <span data-ttu-id="d5685-185">Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d5685-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="d5685-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="d5685-186">*objectIdFromSession*</span></span> | <span data-ttu-id="d5685-187">Opgegeven door Hallo standaard sessie management provider tooindicate die Hallo object-id-parameter is opgehaald van een sessie voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d5685-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="d5685-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="d5685-188">*isActiveMFASession*</span></span> | <span data-ttu-id="d5685-189">De parameter opgegeven door Hallo MFA sessie management tooindicate dat die Hallo de gebruiker heeft een actieve sessie voor MFA</span><span class="sxs-lookup"><span data-stu-id="d5685-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="d5685-190">Aanvullende (optioneel) claims die kunnen worden verzameld</span><span class="sxs-lookup"><span data-stu-id="d5685-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="d5685-191">Hallo volgende claims zijn extra claims die kunnen worden verzameld van Hallo gebruikers, opgeslagen in de directory hello en in Hallo token verzonden.</span><span class="sxs-lookup"><span data-stu-id="d5685-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="d5685-192">Zoals beschreven voordat, kunnen aanvullende claims toothis lijst worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d5685-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="d5685-193">Claims type</span><span class="sxs-lookup"><span data-stu-id="d5685-193">Claims type</span></span> | <span data-ttu-id="d5685-194">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="d5685-195">*Voornaam*</span><span class="sxs-lookup"><span data-stu-id="d5685-195">*givenName*</span></span> | <span data-ttu-id="d5685-196">Van de gebruiker opgegeven naam (ook wel bekend als voornaam)</span><span class="sxs-lookup"><span data-stu-id="d5685-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="d5685-197">*Achternaam*</span><span class="sxs-lookup"><span data-stu-id="d5685-197">*surname*</span></span> | <span data-ttu-id="d5685-198">De achternaam van de gebruiker (ook wel bekend als familienaam of achternaam)</span><span class="sxs-lookup"><span data-stu-id="d5685-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="d5685-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="d5685-199">*Extension_picture*</span></span> | <span data-ttu-id="d5685-200">Afbeelding van de gebruiker op sociale</span><span class="sxs-lookup"><span data-stu-id="d5685-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="d5685-201">Claimtransformaties</span><span class="sxs-lookup"><span data-stu-id="d5685-201">Claim transformations</span></span>

<span data-ttu-id="d5685-202">Hallo beschikbaar claimtransformaties worden hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="d5685-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="d5685-203">Claim-transformatie</span><span class="sxs-lookup"><span data-stu-id="d5685-203">Claim transformation</span></span> | <span data-ttu-id="d5685-204">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="d5685-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="d5685-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="d5685-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="d5685-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="d5685-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="d5685-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="d5685-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="d5685-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="d5685-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d5685-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="d5685-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d5685-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="d5685-211">Definities van inhoud</span><span class="sxs-lookup"><span data-stu-id="d5685-211">Content definitions</span></span>

<span data-ttu-id="d5685-212">Deze sectie beschrijft Hallo inhoud definities al gedeclareerd in Hallo *B2C_1A_base* beleid.</span><span class="sxs-lookup"><span data-stu-id="d5685-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="d5685-213">Deze inhoud definities zijn vatbaar toobe waarnaar wordt verwezen, genegeerd en/of uitgebreid desgewenst ook uw eigen beleid zoals in Hallo *B2C_1A_base_extensions* beleid.</span><span class="sxs-lookup"><span data-stu-id="d5685-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="d5685-214">Claimprovider</span><span class="sxs-lookup"><span data-stu-id="d5685-214">Claims provider</span></span> | <span data-ttu-id="d5685-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="d5685-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="d5685-216">*Facebook*</span></span> | |
| <span data-ttu-id="d5685-217">*Aanmelding voor lokaal Account*</span><span class="sxs-lookup"><span data-stu-id="d5685-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="d5685-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="d5685-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="d5685-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="d5685-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="d5685-220">*Self die wordt beweerd*</span><span class="sxs-lookup"><span data-stu-id="d5685-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="d5685-221">*Lokaal Account*</span><span class="sxs-lookup"><span data-stu-id="d5685-221">*Local Account*</span></span> | |
| <span data-ttu-id="d5685-222">*Sessiebeheer*</span><span class="sxs-lookup"><span data-stu-id="d5685-222">*Session Management*</span></span> | |
| <span data-ttu-id="d5685-223">*Beleidsengine Trustframework*</span><span class="sxs-lookup"><span data-stu-id="d5685-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="d5685-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="d5685-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="d5685-225">*Uitgever van beveiligingstoken*</span><span class="sxs-lookup"><span data-stu-id="d5685-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="d5685-226">Technische profielen</span><span class="sxs-lookup"><span data-stu-id="d5685-226">Technical profiles</span></span>

<span data-ttu-id="d5685-227">Deze sectie beschrijft Hallo technische profielen al gedeclareerd voor de claimprovider in Hallo *B2C_1A_base* beleid.</span><span class="sxs-lookup"><span data-stu-id="d5685-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="d5685-228">Deze technische profielen zijn vatbaar toobe verdere waarnaar wordt verwezen, genegeerd en/of uitgebreid desgewenst ook uw eigen beleid zoals in Hallo *B2C_1A_base_extensions* beleid.</span><span class="sxs-lookup"><span data-stu-id="d5685-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="d5685-229">Technische profielen voor Facebook</span><span class="sxs-lookup"><span data-stu-id="d5685-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="d5685-230">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-230">Technical profile</span></span> | <span data-ttu-id="d5685-231">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-232">*Facebook OAUTH*</span><span class="sxs-lookup"><span data-stu-id="d5685-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="d5685-233">Technische profielen voor lokale aanmelding met Account</span><span class="sxs-lookup"><span data-stu-id="d5685-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="d5685-234">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-234">Technical profile</span></span> | <span data-ttu-id="d5685-235">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-236">*Aanmelding niet-interactieve*</span><span class="sxs-lookup"><span data-stu-id="d5685-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="d5685-237">Technische profielen voor Phone Factor</span><span class="sxs-lookup"><span data-stu-id="d5685-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="d5685-238">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-238">Technical profile</span></span> | <span data-ttu-id="d5685-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-240">*PhoneFactor-invoer*</span><span class="sxs-lookup"><span data-stu-id="d5685-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="d5685-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="d5685-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="d5685-242">*PhoneFactor controleren*</span><span class="sxs-lookup"><span data-stu-id="d5685-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="d5685-243">Technische profielen voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5685-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="d5685-244">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-244">Technical profile</span></span> | <span data-ttu-id="d5685-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-246">*AAD-algemeen*</span><span class="sxs-lookup"><span data-stu-id="d5685-246">*AAD-Common*</span></span> | <span data-ttu-id="d5685-247">Technische profiel die zijn opgenomen in de Hallo andere technische AAD-xxx-profielen</span><span class="sxs-lookup"><span data-stu-id="d5685-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="d5685-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d5685-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="d5685-249">Technische profiel voor het sociaal-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="d5685-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="d5685-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d5685-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="d5685-251">Technische profiel voor het sociaal-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="d5685-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="d5685-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="d5685-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="d5685-253">Technische profiel voor het sociaal-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="d5685-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="d5685-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="d5685-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="d5685-255">Technische profiel voor lokale accounts</span><span class="sxs-lookup"><span data-stu-id="d5685-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="d5685-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="d5685-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="d5685-257">Technische profiel voor lokale accounts</span><span class="sxs-lookup"><span data-stu-id="d5685-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="d5685-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d5685-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="d5685-259">Technische profiel voor het bijwerken van de gebruikersrecord met object-id</span><span class="sxs-lookup"><span data-stu-id="d5685-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="d5685-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d5685-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="d5685-261">Technische profiel voor het bijwerken van de gebruikersrecord met object-id</span><span class="sxs-lookup"><span data-stu-id="d5685-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="d5685-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d5685-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="d5685-263">Technische profiel voor het bijwerken van de gebruikersrecord met object-id</span><span class="sxs-lookup"><span data-stu-id="d5685-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="d5685-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d5685-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="d5685-265">Technische profiel is gebruikte tooread gegevens nadat de gebruiker wordt geverifieerd</span><span class="sxs-lookup"><span data-stu-id="d5685-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="d5685-266">Technische profielen voor Self die wordt beweerd</span><span class="sxs-lookup"><span data-stu-id="d5685-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="d5685-267">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-267">Technical profile</span></span> | <span data-ttu-id="d5685-268">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-269">*SelfAsserted sociale*</span><span class="sxs-lookup"><span data-stu-id="d5685-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="d5685-270">*SelfAsserted ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="d5685-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="d5685-271">Technische profielen voor lokaal Account</span><span class="sxs-lookup"><span data-stu-id="d5685-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="d5685-272">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-272">Technical profile</span></span> | <span data-ttu-id="d5685-273">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="d5685-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="d5685-275">Technische profielen voor sessiebeheer</span><span class="sxs-lookup"><span data-stu-id="d5685-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="d5685-276">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-276">Technical profile</span></span> | <span data-ttu-id="d5685-277">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-278">*SM-NoOperation*</span><span class="sxs-lookup"><span data-stu-id="d5685-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="d5685-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="d5685-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="d5685-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="d5685-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="d5685-281">Profielnaam wordt gebruikte toodisambiguate AAD sessie tussen sign up en aanmelden</span><span class="sxs-lookup"><span data-stu-id="d5685-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="d5685-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="d5685-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="d5685-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="d5685-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="d5685-284">Technische profielen voor Trustframework beleid Engine TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="d5685-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="d5685-285">Momenteel geen technische profielen zijn gedefinieerd voor Hallo **Trustframework beleid Engine TechnicalProfiles** claimprovider.</span><span class="sxs-lookup"><span data-stu-id="d5685-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="d5685-286">Technische profielen voor uitgever van beveiligingstoken</span><span class="sxs-lookup"><span data-stu-id="d5685-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="d5685-287">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="d5685-287">Technical profile</span></span> | <span data-ttu-id="d5685-288">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d5685-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="d5685-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="d5685-290">Gebruiker trajecten</span><span class="sxs-lookup"><span data-stu-id="d5685-290">User journeys</span></span>

<span data-ttu-id="d5685-291">Deze sectie beschrijft Hallo gebruiker trajecten is al gedeclareerd in Hallo *B2C_1A_base* beleid.</span><span class="sxs-lookup"><span data-stu-id="d5685-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="d5685-292">Deze gebruiker trajecten zijn vatbaar toobe verdere waarnaar wordt verwezen, genegeerd en/of uitgebreid desgewenst ook uw eigen beleid zoals in Hallo *B2C_1A_base_extensions* beleid.</span><span class="sxs-lookup"><span data-stu-id="d5685-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="d5685-293">Gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="d5685-293">User journey</span></span> | <span data-ttu-id="d5685-294">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5685-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="d5685-295">*Aanmelden*</span><span class="sxs-lookup"><span data-stu-id="d5685-295">*SignUp*</span></span> | |
| <span data-ttu-id="d5685-296">*Aanmelding*</span><span class="sxs-lookup"><span data-stu-id="d5685-296">*SignIn*</span></span> | |
| <span data-ttu-id="d5685-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="d5685-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="d5685-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="d5685-298">*EditProfile*</span></span> | |
| <span data-ttu-id="d5685-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="d5685-299">*PasswordReset*</span></span> | |
