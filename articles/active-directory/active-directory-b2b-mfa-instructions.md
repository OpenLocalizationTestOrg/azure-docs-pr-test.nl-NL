---
title: aaaConditional-toegang voor gebruikers van Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt multi-factor authentication (MFA) voor selectieve toegang tooyour zakelijke toepassingen
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="81cd5-103">Voorwaardelijke toegang voor gebruikers voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="81cd5-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="81cd5-104">Multi-factor authentication voor B2B-gebruikers</span><span class="sxs-lookup"><span data-stu-id="81cd5-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="81cd5-105">Met de Azure AD B2B-samenwerking organisaties kunnen multi-factor authentication (MFA) beleid afdwingen voor B2B-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="81cd5-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="81cd5-106">Dit beleid kunnen worden afgedwongen op het Hallo-tenant, app of afzonderlijke gebruikersniveau, hello dezelfde manier als ze zijn ingeschakeld voor fulltime werknemers en leden van het Hallo-organisatie.</span><span class="sxs-lookup"><span data-stu-id="81cd5-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="81cd5-107">MFA-beleid wordt afgedwongen op Hallo bronorganisatie.</span><span class="sxs-lookup"><span data-stu-id="81cd5-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="81cd5-108">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="81cd5-108">Example:</span></span>
1. <span data-ttu-id="81cd5-109">Beheerder of de werknemer in bedrijf A nodigt gebruiker uit bedrijf B tooan toepassing *Foo* in bedrijf A.</span><span class="sxs-lookup"><span data-stu-id="81cd5-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="81cd5-110">Toepassing *Foo* in bedrijf is een geconfigureerde toorequire MFA op toegang.</span><span class="sxs-lookup"><span data-stu-id="81cd5-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="81cd5-111">Wanneer de gebruiker Hallo van bedrijf B tooaccess app probeert *Foo* in Hallo bedrijf een tenant, zijn ze toocomplete gevraagd een challenge MFA.</span><span class="sxs-lookup"><span data-stu-id="81cd5-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="81cd5-112">Hallo gebruiker hun MFA met bedrijf A kunt instellen en de MFA-optie kiest.</span><span class="sxs-lookup"><span data-stu-id="81cd5-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="81cd5-113">Dit scenario is geschikt voor een identiteit (Azure AD of MSA, bijvoorbeeld, als gebruikers van bedrijf B zich verifiëren met behulp van sociale ID)</span><span class="sxs-lookup"><span data-stu-id="81cd5-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="81cd5-114">Bedrijf A moet voldoende Azure AD Premium-licenties die ondersteuning bieden voor MFA hebt.</span><span class="sxs-lookup"><span data-stu-id="81cd5-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="81cd5-115">Hallo gebruiker uit bedrijf B verbruikt deze licentie van bedrijf A.</span><span class="sxs-lookup"><span data-stu-id="81cd5-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="81cd5-116">Hallo nodigen tenancymodus is altijd verantwoordelijk zijn voor MFA voor gebruikers van de partnerorganisatie Hallo, zelfs als Hallo partnerorganisatie MFA mogelijkheden heeft.</span><span class="sxs-lookup"><span data-stu-id="81cd5-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="81cd5-117">MFA in te stellen voor gebruikers voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="81cd5-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="81cd5-118">toodiscover hoe eenvoudig het is tooset van MFA voor B2B-samenwerking gebruikers, Zie hoe in Hallo volgende video:</span><span class="sxs-lookup"><span data-stu-id="81cd5-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="81cd5-119">B2B-gebruikers MFA voor ervaren bieden inwisseling</span><span class="sxs-lookup"><span data-stu-id="81cd5-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="81cd5-120">Bekijk Hallo animatie toosee Hallo inwisseling ervaring te volgen:</span><span class="sxs-lookup"><span data-stu-id="81cd5-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="81cd5-121">MFA voor B2B-samenwerking gebruikers opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="81cd5-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="81cd5-122">Op dit moment Hallo beheerder kan vereisen B2B-samenwerking gebruikers tooproof up opnieuw alleen met behulp van PowerShell-cmdlets volgen Hallo:</span><span class="sxs-lookup"><span data-stu-id="81cd5-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="81cd5-123">Verbinding maken met tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="81cd5-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="81cd5-124">Alle gebruikers krijgen met bewijs van methoden</span><span class="sxs-lookup"><span data-stu-id="81cd5-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="81cd5-125">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="81cd5-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="81cd5-126">Hallo MFA-methode voor een specifieke gebruiker toorequire Hallo B2B-samenwerking gebruiker tooset bewijs van methoden opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="81cd5-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="81cd5-127">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="81cd5-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="81cd5-128">Waarom we MFA op Hallo resource tenancymodus uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="81cd5-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="81cd5-129">In de huidige release Hallo is MFA altijd in Hallo resource tenancymodus omwille van de hoge voorspelbaarheid is vereist.</span><span class="sxs-lookup"><span data-stu-id="81cd5-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="81cd5-130">Stel dat bijvoorbeeld een gebruiker Contoso (Sandra) uitgenodigde tooFabrikam en Fabrikam MFA voor B2B-gebruikers heeft ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="81cd5-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="81cd5-131">Als Contoso ingeschakeld voor App1, maar niet App2 MFA-beleid heeft, klikt u vervolgens als we hello Contoso MFA claim in Hallo-token bekijkt, mogelijk zien we Hallo na:</span><span class="sxs-lookup"><span data-stu-id="81cd5-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="81cd5-132">Dag 1: Een gebruiker heeft MFA in Contoso en toegang heeft tot App1 en er zijn geen extra MFA prompt wordt weergegeven in Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="81cd5-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="81cd5-133">Dag 2: Hallo gebruiker toegang heeft gehad tot 2 van de App in Contoso, dus bij het openen van Fabrikam, moeten ze zich registreren voor MFA er.</span><span class="sxs-lookup"><span data-stu-id="81cd5-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="81cd5-134">Dit proces kan verwarrend zijn en leiden toodrop in aanmelden voltooiingen.</span><span class="sxs-lookup"><span data-stu-id="81cd5-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="81cd5-135">Bovendien, zelfs als Contoso MFA-mogelijkheid heeft, is het niet altijd Hallo case Hallo Fabrikam zou vertrouwen Hallo Contoso MFA-beleid.</span><span class="sxs-lookup"><span data-stu-id="81cd5-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="81cd5-136">Tot slot werkt resource tenant MFA ook voor MSA's en sociale-id's en voor de partner-organisaties waarvoor geen MFA instellen.</span><span class="sxs-lookup"><span data-stu-id="81cd5-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="81cd5-137">Hallo aanbeveling voor MFA voor B2B-gebruikers is daarom tooalways MFA in Hallo uitnodigen tenant vereisen.</span><span class="sxs-lookup"><span data-stu-id="81cd5-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="81cd5-138">Deze vereiste toodouble MFA in sommige gevallen kan leiden, maar wanneer toegang tot Hallo nodigen tenant, Hallo-ervaring voor eindgebruikers is voorspelbaar: Sandra moet registreren voor MFA bij Hallo nodigen tenant.</span><span class="sxs-lookup"><span data-stu-id="81cd5-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="81cd5-139">Op basis van apparaten, op basis van locatie en risico gebaseerde voorwaardelijke toegang voor B2B-gebruikers</span><span class="sxs-lookup"><span data-stu-id="81cd5-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="81cd5-140">Wanneer Contoso beleidsregels voor voorwaardelijke toegang op basis van apparaten voor hun zakelijke gegevens kunt, wordt toegang niet van apparaten die niet worden beheerd door Contoso en niet compatibel zijn met beleidsregels Hallo Contoso-apparaten.</span><span class="sxs-lookup"><span data-stu-id="81cd5-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="81cd5-141">Als Hallo B2B gebruikersapparaat wordt niet beheerd door Contoso, toegang van gebruikers van Hallo partnerorganisaties B2B geblokkeerd en in welke context deze beleidsregels worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="81cd5-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="81cd5-142">Contoso kan echter uitsluiting lijsten met specifieke partner gebruikers tooexclude Hallo van beleid voor voorwaardelijke toegang op basis van apparaten te maken.</span><span class="sxs-lookup"><span data-stu-id="81cd5-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="81cd5-143">Voorwaardelijke toegang voor B2B op basis van locatie</span><span class="sxs-lookup"><span data-stu-id="81cd5-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="81cd5-144">Beleid voor voorwaardelijke toegang op basis van locatie kunnen worden afgedwongen voor B2B-gebruikers als Hallo nodigen organisatie kunnen toocreate een vertrouwde IP-adresbereik dat hun partnerorganisaties definieert.</span><span class="sxs-lookup"><span data-stu-id="81cd5-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="81cd5-145">Voorwaardelijke toegang op basis van een risico voor B2B</span><span class="sxs-lookup"><span data-stu-id="81cd5-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="81cd5-146">Op dit moment aanmelden beleid op basis van risico's die toegepaste tooB2B gebruikers kunnen niet worden, omdat Hallo risico-evaluatie wordt uitgevoerd op thuisorganisatie Hallo B2B van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="81cd5-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81cd5-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81cd5-147">Next steps</span></span>

<span data-ttu-id="81cd5-148">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="81cd5-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="81cd5-149">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="81cd5-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="81cd5-150">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="81cd5-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="81cd5-151">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="81cd5-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="81cd5-152">Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="81cd5-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="81cd5-153">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="81cd5-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="81cd5-154">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="81cd5-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="81cd5-155">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="81cd5-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="81cd5-156">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="81cd5-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="81cd5-157">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="81cd5-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="81cd5-158">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="81cd5-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="81cd5-159">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="81cd5-159">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
