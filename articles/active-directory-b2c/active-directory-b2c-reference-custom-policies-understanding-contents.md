---
title: 'Azure Active Directory B2C: Informatie over aangepaste beleidsregels van het starter pack | Microsoft Docs'
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
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="01bb1-103">Wat is de aangepaste beleidsregels van het Azure AD B2C aangepast beleid starter pack?</span><span class="sxs-lookup"><span data-stu-id="01bb1-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="01bb1-104">Deze sectie vindt u de belangrijkste elementen van het beleid B2C_1A_base die wordt geleverd met de **Starter Pack** en die wordt gebruikt voor het ontwerpen van uw eigen beleid via de overname van de *B2C_1A_base_extensions beleid*.</span><span class="sxs-lookup"><span data-stu-id="01bb1-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="01bb1-105">Als zodanig het met name is gericht op de reeds gedefinieerde claimtypen, claimtransformaties, definities van inhoud, claimproviders met hun technische profielen en de gebruiker core trajecten.</span><span class="sxs-lookup"><span data-stu-id="01bb1-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01bb1-106">Microsoft biedt geen enkele expliciete of impliciete met betrekking tot de informatie hieronder.</span><span class="sxs-lookup"><span data-stu-id="01bb1-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="01bb1-107">Wijzigingen kunnen worden ingevoerd op elk moment vóór GA tijdstip, GA tijdens of na.</span><span class="sxs-lookup"><span data-stu-id="01bb1-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="01bb1-108">Zowel uw eigen beleid en het beleid B2C_1A_base_extensions deze definities overschrijven en dit beleid bovenliggende door extra velden naar behoefte uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="01bb1-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="01bb1-109">De belangrijkste elementen van de *B2C_1A_base beleid* zijn claimtypen, claimtransformaties en inhoud definities.</span><span class="sxs-lookup"><span data-stu-id="01bb1-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="01bb1-110">Deze elementen kunnen vatbaar verwezen in uw eigen beleid ook als in de *B2C_1A_base_extensions beleid*.</span><span class="sxs-lookup"><span data-stu-id="01bb1-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="01bb1-111">Claims schema 's</span><span class="sxs-lookup"><span data-stu-id="01bb1-111">Claims schemas</span></span>

<span data-ttu-id="01bb1-112">Dit claims schema's is onderverdeeld in drie secties:</span><span class="sxs-lookup"><span data-stu-id="01bb1-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="01bb1-113">Een gedeelte van het eerste met een lijst met de minimale claims die vereist zijn voor de gebruiker trajecten goed te laten werken.</span><span class="sxs-lookup"><span data-stu-id="01bb1-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="01bb1-114">Een tweede sectie de claims worden die zijn vereist voor queryreeksparameters en andere speciale parameters worden doorgegeven aan andere claimproviders, met name login.microsoftonline.com voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="01bb1-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="01bb1-115">**Wijzig geen deze claims**.</span><span class="sxs-lookup"><span data-stu-id="01bb1-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="01bb1-116">En uiteindelijk een derde sectie met een lijst met aanvullende, optionele claims die kunnen worden verzameld van de gebruiker opgeslagen in de map en tokens verzonden tijdens het aanmelden.</span><span class="sxs-lookup"><span data-stu-id="01bb1-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="01bb1-117">Nieuwe claims type verzameld van de gebruiker en/of verzonden in het token kan in deze sectie worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="01bb1-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01bb1-118">Het schema claims bevat beperkingen op bepaalde claims zoals wachtwoorden en gebruikersnamen.</span><span class="sxs-lookup"><span data-stu-id="01bb1-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="01bb1-119">Het beleid vertrouwen Framework (TF) behandelt Azure AD als andere claimprovider en alle bijbehorende beperkingen zijn gemodelleerd in het premium-beleid.</span><span class="sxs-lookup"><span data-stu-id="01bb1-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="01bb1-120">Een beleid kan worden gewijzigd zodat meer beperkingen toevoegen, of gebruik een andere claimprovider voor opslag van referenties waarvoor een eigen beperkingen.</span><span class="sxs-lookup"><span data-stu-id="01bb1-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="01bb1-121">De beschikbare claimtypen worden hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="01bb1-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="01bb1-122">Claims die vereist voor de gebruiker trajecten zijn</span><span class="sxs-lookup"><span data-stu-id="01bb1-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="01bb1-123">De volgende claims zijn vereist voor de gebruiker trajecten goed te laten werken:</span><span class="sxs-lookup"><span data-stu-id="01bb1-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="01bb1-124">Claims type</span><span class="sxs-lookup"><span data-stu-id="01bb1-124">Claims type</span></span> | <span data-ttu-id="01bb1-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="01bb1-126">*Gebruikers-id*</span><span class="sxs-lookup"><span data-stu-id="01bb1-126">*UserId*</span></span> | <span data-ttu-id="01bb1-127">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="01bb1-127">Username</span></span> |
| <span data-ttu-id="01bb1-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="01bb1-128">*signInName*</span></span> | <span data-ttu-id="01bb1-129">Meld u aan de naam</span><span class="sxs-lookup"><span data-stu-id="01bb1-129">Sign in name</span></span> |
| <span data-ttu-id="01bb1-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-130">*tenantId*</span></span> | <span data-ttu-id="01bb1-131">Tenant-id (ID) van het gebruikersobject in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="01bb1-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="01bb1-132">*object-id*</span><span class="sxs-lookup"><span data-stu-id="01bb1-132">*objectId*</span></span> | <span data-ttu-id="01bb1-133">Object-id (ID) van het gebruikersobject in Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="01bb1-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="01bb1-134">*wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="01bb1-134">*password*</span></span> | <span data-ttu-id="01bb1-135">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="01bb1-135">Password</span></span> |
| <span data-ttu-id="01bb1-136">*NieuwWachtwoord*</span><span class="sxs-lookup"><span data-stu-id="01bb1-136">*newPassword*</span></span> | |
| <span data-ttu-id="01bb1-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="01bb1-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="01bb1-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="01bb1-138">*passwordPolicies*</span></span> | <span data-ttu-id="01bb1-139">Wachtwoordbeleid gebruikt door Azure AD B2C Premium om te bepalen van de Wachtwoordsterkte, verlopen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="01bb1-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="01bb1-140">*Sub*</span><span class="sxs-lookup"><span data-stu-id="01bb1-140">*sub*</span></span> | |
| <span data-ttu-id="01bb1-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="01bb1-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="01bb1-142">*identityProvider*</span></span> | |
| <span data-ttu-id="01bb1-143">*Weergavenaam*</span><span class="sxs-lookup"><span data-stu-id="01bb1-143">*displayName*</span></span> | |
| <span data-ttu-id="01bb1-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="01bb1-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="01bb1-145">Het telefoonnummer van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="01bb1-145">User's telephone number</span></span> |
| <span data-ttu-id="01bb1-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="01bb1-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="01bb1-147">*E-mail*</span><span class="sxs-lookup"><span data-stu-id="01bb1-147">*email*</span></span> | <span data-ttu-id="01bb1-148">E-mailadres dat kan worden gebruikt om contact op met de gebruiker</span><span class="sxs-lookup"><span data-stu-id="01bb1-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="01bb1-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="01bb1-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="01bb1-150">E-mailadres waarmee de gebruiker kunt aanmelden</span><span class="sxs-lookup"><span data-stu-id="01bb1-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="01bb1-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="01bb1-151">*otherMails*</span></span> | <span data-ttu-id="01bb1-152">E-mailadressen die kunnen worden gebruikt om contact op met de gebruiker</span><span class="sxs-lookup"><span data-stu-id="01bb1-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="01bb1-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="01bb1-153">*userPrincipalName*</span></span> | <span data-ttu-id="01bb1-154">De gebruikersnaam die is opgeslagen in de Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="01bb1-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="01bb1-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="01bb1-155">*upnUserName*</span></span> | <span data-ttu-id="01bb1-156">Gebruikersnaam voor het maken van de UPN-naam</span><span class="sxs-lookup"><span data-stu-id="01bb1-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="01bb1-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="01bb1-157">*mailNickName*</span></span> | <span data-ttu-id="01bb1-158">De naam van gebruiker e-mail nick die is opgeslagen in de Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="01bb1-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="01bb1-159">*nieuwegebruiker*</span><span class="sxs-lookup"><span data-stu-id="01bb1-159">*newUser*</span></span> | |
| <span data-ttu-id="01bb1-160">*uitgevoerd SelfAsserted invoer*</span><span class="sxs-lookup"><span data-stu-id="01bb1-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="01bb1-161">Claim die aangeeft of de kenmerken van de gebruiker zijn verzameld</span><span class="sxs-lookup"><span data-stu-id="01bb1-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="01bb1-162">*uitgevoerd PhoneFactor invoer*</span><span class="sxs-lookup"><span data-stu-id="01bb1-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="01bb1-163">Claim waarmee wordt aangegeven of een nieuw telefoonnummer van de gebruiker is verzameld</span><span class="sxs-lookup"><span data-stu-id="01bb1-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="01bb1-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="01bb1-164">*authenticationSource*</span></span> | <span data-ttu-id="01bb1-165">Hiermee geeft u op of de gebruiker is geverifieerd op sociale id-Provider, login.microsoftonline.com of lokale account</span><span class="sxs-lookup"><span data-stu-id="01bb1-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="01bb1-166">Claims die vereist zijn voor queryreeksparameters en andere speciale parameters</span><span class="sxs-lookup"><span data-stu-id="01bb1-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="01bb1-167">De volgende claims zijn vereist om door te geven op de speciale parameters (inclusief een aantal queryreeksparameters) voor andere claimproviders:</span><span class="sxs-lookup"><span data-stu-id="01bb1-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="01bb1-168">Claims type</span><span class="sxs-lookup"><span data-stu-id="01bb1-168">Claims type</span></span> | <span data-ttu-id="01bb1-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="01bb1-170">*Nux*</span><span class="sxs-lookup"><span data-stu-id="01bb1-170">*nux*</span></span> | <span data-ttu-id="01bb1-171">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-172">*NCA*</span><span class="sxs-lookup"><span data-stu-id="01bb1-172">*nca*</span></span> | <span data-ttu-id="01bb1-173">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="01bb1-174">*prompt*</span></span> | <span data-ttu-id="01bb1-175">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-176">*Mkt*</span><span class="sxs-lookup"><span data-stu-id="01bb1-176">*mkt*</span></span> | <span data-ttu-id="01bb1-177">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-178">*kredietbrief*</span><span class="sxs-lookup"><span data-stu-id="01bb1-178">*lc*</span></span> | <span data-ttu-id="01bb1-179">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="01bb1-180">*grant_type*</span></span> | <span data-ttu-id="01bb1-181">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-182">*bereik*</span><span class="sxs-lookup"><span data-stu-id="01bb1-182">*scope*</span></span> | <span data-ttu-id="01bb1-183">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="01bb1-184">*client_id*</span></span> | <span data-ttu-id="01bb1-185">Speciale parameter doorgegeven voor de verificatie van lokale account aan login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01bb1-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="01bb1-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="01bb1-186">*objectIdFromSession*</span></span> | <span data-ttu-id="01bb1-187">Parameter geleverd door de standaardprovider voor het beheer van sessie om aan te geven dat de object-id is opgehaald van een sessie voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="01bb1-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="01bb1-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="01bb1-188">*isActiveMFASession*</span></span> | <span data-ttu-id="01bb1-189">Opgegeven door de MFA-sessiebeheer om aan te geven dat de gebruiker een actieve sessie voor MFA heeft-parameter</span><span class="sxs-lookup"><span data-stu-id="01bb1-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="01bb1-190">Aanvullende (optioneel) claims die kunnen worden verzameld</span><span class="sxs-lookup"><span data-stu-id="01bb1-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="01bb1-191">De volgende claims zijn extra claims die kunnen worden verzameld van de gebruikers, opgeslagen in de map en in het token is verzonden.</span><span class="sxs-lookup"><span data-stu-id="01bb1-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="01bb1-192">Zoals beschreven voordat, kunnen aanvullende claims worden toegevoegd aan deze lijst.</span><span class="sxs-lookup"><span data-stu-id="01bb1-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="01bb1-193">Claims type</span><span class="sxs-lookup"><span data-stu-id="01bb1-193">Claims type</span></span> | <span data-ttu-id="01bb1-194">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="01bb1-195">*Voornaam*</span><span class="sxs-lookup"><span data-stu-id="01bb1-195">*givenName*</span></span> | <span data-ttu-id="01bb1-196">Van de gebruiker opgegeven naam (ook wel bekend als voornaam)</span><span class="sxs-lookup"><span data-stu-id="01bb1-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="01bb1-197">*Achternaam*</span><span class="sxs-lookup"><span data-stu-id="01bb1-197">*surname*</span></span> | <span data-ttu-id="01bb1-198">De achternaam van de gebruiker (ook wel bekend als familienaam of achternaam)</span><span class="sxs-lookup"><span data-stu-id="01bb1-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="01bb1-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="01bb1-199">*Extension_picture*</span></span> | <span data-ttu-id="01bb1-200">Afbeelding van de gebruiker op sociale</span><span class="sxs-lookup"><span data-stu-id="01bb1-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="01bb1-201">Claimtransformaties</span><span class="sxs-lookup"><span data-stu-id="01bb1-201">Claim transformations</span></span>

<span data-ttu-id="01bb1-202">De beschikbare claimtransformaties worden hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="01bb1-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="01bb1-203">Claim-transformatie</span><span class="sxs-lookup"><span data-stu-id="01bb1-203">Claim transformation</span></span> | <span data-ttu-id="01bb1-204">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="01bb1-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="01bb1-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="01bb1-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="01bb1-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="01bb1-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="01bb1-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="01bb1-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="01bb1-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="01bb1-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="01bb1-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="01bb1-211">Definities van inhoud</span><span class="sxs-lookup"><span data-stu-id="01bb1-211">Content definitions</span></span>

<span data-ttu-id="01bb1-212">Deze sectie beschrijft de inhoud definities is al gedeclareerd in de *B2C_1A_base* beleid.</span><span class="sxs-lookup"><span data-stu-id="01bb1-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="01bb1-213">Deze inhoud definities zijn vatbaar voor worden waarnaar wordt verwezen, genegeerd en/of uitgebreid naar behoefte in uw eigen beleid ook als in de *B2C_1A_base_extensions* beleid.</span><span class="sxs-lookup"><span data-stu-id="01bb1-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="01bb1-214">Claimprovider</span><span class="sxs-lookup"><span data-stu-id="01bb1-214">Claims provider</span></span> | <span data-ttu-id="01bb1-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="01bb1-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="01bb1-216">*Facebook*</span></span> | |
| <span data-ttu-id="01bb1-217">*Aanmelding voor lokaal Account*</span><span class="sxs-lookup"><span data-stu-id="01bb1-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="01bb1-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="01bb1-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="01bb1-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="01bb1-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="01bb1-220">*Self die wordt beweerd*</span><span class="sxs-lookup"><span data-stu-id="01bb1-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="01bb1-221">*Lokaal Account*</span><span class="sxs-lookup"><span data-stu-id="01bb1-221">*Local Account*</span></span> | |
| <span data-ttu-id="01bb1-222">*Sessiebeheer*</span><span class="sxs-lookup"><span data-stu-id="01bb1-222">*Session Management*</span></span> | |
| <span data-ttu-id="01bb1-223">*Beleidsengine Trustframework*</span><span class="sxs-lookup"><span data-stu-id="01bb1-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="01bb1-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="01bb1-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="01bb1-225">*Uitgever van beveiligingstoken*</span><span class="sxs-lookup"><span data-stu-id="01bb1-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="01bb1-226">Technische profielen</span><span class="sxs-lookup"><span data-stu-id="01bb1-226">Technical profiles</span></span>

<span data-ttu-id="01bb1-227">Deze sectie beschrijft de technische profielen is al gedeclareerd voor de claimprovider in de *B2C_1A_base* beleid.</span><span class="sxs-lookup"><span data-stu-id="01bb1-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="01bb1-228">Deze technische profielen zijn vatbaar voor worden verder waarnaar wordt verwezen, genegeerd en/of uitgebreid naar behoefte in uw eigen beleid ook als in de *B2C_1A_base_extensions* beleid.</span><span class="sxs-lookup"><span data-stu-id="01bb1-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="01bb1-229">Technische profielen voor Facebook</span><span class="sxs-lookup"><span data-stu-id="01bb1-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="01bb1-230">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-230">Technical profile</span></span> | <span data-ttu-id="01bb1-231">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-232">*Facebook OAUTH*</span><span class="sxs-lookup"><span data-stu-id="01bb1-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="01bb1-233">Technische profielen voor lokale aanmelding met Account</span><span class="sxs-lookup"><span data-stu-id="01bb1-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="01bb1-234">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-234">Technical profile</span></span> | <span data-ttu-id="01bb1-235">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-236">*Aanmelding niet-interactieve*</span><span class="sxs-lookup"><span data-stu-id="01bb1-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="01bb1-237">Technische profielen voor Phone Factor</span><span class="sxs-lookup"><span data-stu-id="01bb1-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="01bb1-238">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-238">Technical profile</span></span> | <span data-ttu-id="01bb1-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-240">*PhoneFactor-invoer*</span><span class="sxs-lookup"><span data-stu-id="01bb1-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="01bb1-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="01bb1-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="01bb1-242">*PhoneFactor controleren*</span><span class="sxs-lookup"><span data-stu-id="01bb1-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="01bb1-243">Technische profielen voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01bb1-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="01bb1-244">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-244">Technical profile</span></span> | <span data-ttu-id="01bb1-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-246">*AAD-algemeen*</span><span class="sxs-lookup"><span data-stu-id="01bb1-246">*AAD-Common*</span></span> | <span data-ttu-id="01bb1-247">Technische profiel die zijn opgenomen in de andere technische AAD-xxx-profielen</span><span class="sxs-lookup"><span data-stu-id="01bb1-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="01bb1-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="01bb1-249">Technische profiel voor het sociaal-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="01bb1-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="01bb1-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="01bb1-251">Technische profiel voor het sociaal-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="01bb1-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="01bb1-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="01bb1-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="01bb1-253">Technische profiel voor het sociaal-aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="01bb1-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="01bb1-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="01bb1-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="01bb1-255">Technische profiel voor lokale accounts</span><span class="sxs-lookup"><span data-stu-id="01bb1-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="01bb1-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="01bb1-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="01bb1-257">Technische profiel voor lokale accounts</span><span class="sxs-lookup"><span data-stu-id="01bb1-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="01bb1-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="01bb1-259">Technische profiel voor het bijwerken van de gebruikersrecord met object-id</span><span class="sxs-lookup"><span data-stu-id="01bb1-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="01bb1-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="01bb1-261">Technische profiel voor het bijwerken van de gebruikersrecord met object-id</span><span class="sxs-lookup"><span data-stu-id="01bb1-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="01bb1-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="01bb1-263">Technische profiel voor het bijwerken van de gebruikersrecord met object-id</span><span class="sxs-lookup"><span data-stu-id="01bb1-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="01bb1-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="01bb1-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="01bb1-265">Technische profiel wordt gebruikt om gegevens te lezen nadat de gebruiker wordt geverifieerd</span><span class="sxs-lookup"><span data-stu-id="01bb1-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="01bb1-266">Technische profielen voor Self die wordt beweerd</span><span class="sxs-lookup"><span data-stu-id="01bb1-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="01bb1-267">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-267">Technical profile</span></span> | <span data-ttu-id="01bb1-268">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-269">*SelfAsserted sociale*</span><span class="sxs-lookup"><span data-stu-id="01bb1-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="01bb1-270">*SelfAsserted ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="01bb1-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="01bb1-271">Technische profielen voor lokaal Account</span><span class="sxs-lookup"><span data-stu-id="01bb1-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="01bb1-272">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-272">Technical profile</span></span> | <span data-ttu-id="01bb1-273">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="01bb1-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="01bb1-275">Technische profielen voor sessiebeheer</span><span class="sxs-lookup"><span data-stu-id="01bb1-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="01bb1-276">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-276">Technical profile</span></span> | <span data-ttu-id="01bb1-277">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-278">*SM-NoOperation*</span><span class="sxs-lookup"><span data-stu-id="01bb1-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="01bb1-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="01bb1-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="01bb1-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="01bb1-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="01bb1-281">Profielnaam wordt gebruikt voor het AAD-sessie tussen sign up heffen en aanmelden</span><span class="sxs-lookup"><span data-stu-id="01bb1-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="01bb1-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="01bb1-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="01bb1-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="01bb1-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="01bb1-284">Technische profielen voor Trustframework beleid Engine TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="01bb1-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="01bb1-285">Momenteel geen technische profielen zijn gedefinieerd voor de **Trustframework beleid Engine TechnicalProfiles** claimprovider.</span><span class="sxs-lookup"><span data-stu-id="01bb1-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="01bb1-286">Technische profielen voor uitgever van beveiligingstoken</span><span class="sxs-lookup"><span data-stu-id="01bb1-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="01bb1-287">Technische profiel</span><span class="sxs-lookup"><span data-stu-id="01bb1-287">Technical profile</span></span> | <span data-ttu-id="01bb1-288">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="01bb1-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="01bb1-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="01bb1-290">Gebruiker trajecten</span><span class="sxs-lookup"><span data-stu-id="01bb1-290">User journeys</span></span>

<span data-ttu-id="01bb1-291">Deze sectie beschrijft de trajecten gebruiker is al gedeclareerd in de *B2C_1A_base* beleid.</span><span class="sxs-lookup"><span data-stu-id="01bb1-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="01bb1-292">Deze gebruiker trajecten zijn vatbaar voor worden verder waarnaar wordt verwezen, genegeerd en/of uitgebreid naar behoefte in uw eigen beleid ook als in de *B2C_1A_base_extensions* beleid.</span><span class="sxs-lookup"><span data-stu-id="01bb1-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="01bb1-293">Gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="01bb1-293">User journey</span></span> | <span data-ttu-id="01bb1-294">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="01bb1-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="01bb1-295">*Aanmelden*</span><span class="sxs-lookup"><span data-stu-id="01bb1-295">*SignUp*</span></span> | |
| <span data-ttu-id="01bb1-296">*Aanmelding*</span><span class="sxs-lookup"><span data-stu-id="01bb1-296">*SignIn*</span></span> | |
| <span data-ttu-id="01bb1-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="01bb1-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="01bb1-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="01bb1-298">*EditProfile*</span></span> | |
| <span data-ttu-id="01bb1-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="01bb1-299">*PasswordReset*</span></span> | |
