---
title: Voorwaardelijke toegang voor gebruikers van Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt multi-factor authentication (MFA) voor selectief toegang tot uw zakelijke toepassingen
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
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="5c68d-103">Voorwaardelijke toegang voor gebruikers voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="5c68d-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="5c68d-104">Multi-factor authentication voor B2B-gebruikers</span><span class="sxs-lookup"><span data-stu-id="5c68d-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="5c68d-105">Met de Azure AD B2B-samenwerking organisaties kunnen multi-factor authentication (MFA) beleid afdwingen voor B2B-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5c68d-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="5c68d-106">Dit beleid kunnen worden afgedwongen op de tenant, app niveau of een afzonderlijke gebruiker, dezelfde manier als ze zijn ingeschakeld voor fulltime werknemers en leden van de organisatie.</span><span class="sxs-lookup"><span data-stu-id="5c68d-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="5c68d-107">MFA-beleid worden afgedwongen voor de organisatie van de bronpartner.</span><span class="sxs-lookup"><span data-stu-id="5c68d-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="5c68d-108">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5c68d-108">Example:</span></span>
1. <span data-ttu-id="5c68d-109">Beheerder of de werknemer in bedrijf A nodigt gebruiker uit bedrijf B naar een toepassing *Foo* in bedrijf A.</span><span class="sxs-lookup"><span data-stu-id="5c68d-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="5c68d-110">Toepassing *Foo* in bedrijf A is geconfigureerd voor MFA vereisen voor toegang.</span><span class="sxs-lookup"><span data-stu-id="5c68d-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="5c68d-111">Wanneer de gebruiker van bedrijf B probeert toegang tot app *Foo* in het bedrijf een tenant wordt gevraagd een challenge MFA voltooien.</span><span class="sxs-lookup"><span data-stu-id="5c68d-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="5c68d-112">De gebruiker hun MFA met bedrijf A kunt instellen en de MFA-optie kiest.</span><span class="sxs-lookup"><span data-stu-id="5c68d-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="5c68d-113">Dit scenario is geschikt voor een identiteit (Azure AD of MSA, bijvoorbeeld, als gebruikers van bedrijf B zich verifiëren met behulp van sociale ID)</span><span class="sxs-lookup"><span data-stu-id="5c68d-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="5c68d-114">Bedrijf A moet voldoende Azure AD Premium-licenties die ondersteuning bieden voor MFA hebt.</span><span class="sxs-lookup"><span data-stu-id="5c68d-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="5c68d-115">De gebruiker uit bedrijf B verbruikt deze licentie van bedrijf A.</span><span class="sxs-lookup"><span data-stu-id="5c68d-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="5c68d-116">De uitnodiging tenancymodus is altijd verantwoordelijk zijn voor MFA voor gebruikers van de partnerorganisatie, zelfs als de andere organisatie MFA mogelijkheden heeft.</span><span class="sxs-lookup"><span data-stu-id="5c68d-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="5c68d-117">MFA in te stellen voor gebruikers voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="5c68d-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="5c68d-118">Als u wilt ontdekken hoe eenvoudig het is voor het instellen van MFA voor B2B-samenwerking gebruikers, Zie hoe in de volgende video:</span><span class="sxs-lookup"><span data-stu-id="5c68d-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="5c68d-119">B2B-gebruikers MFA voor ervaren bieden inwisseling</span><span class="sxs-lookup"><span data-stu-id="5c68d-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="5c68d-120">Bekijk de volgende animatie om te zien van de inwisselcode ervaring:</span><span class="sxs-lookup"><span data-stu-id="5c68d-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="5c68d-121">MFA voor B2B-samenwerking gebruikers opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="5c68d-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="5c68d-122">Op dit moment wordt kan de beheerder vereisen B2B-samenwerking gebruikers bewijs van opnieuw alleen met behulp van de volgende PowerShell-cmdlets:</span><span class="sxs-lookup"><span data-stu-id="5c68d-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="5c68d-123">Verbinding maken met Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c68d-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="5c68d-124">Alle gebruikers krijgen met bewijs van methoden</span><span class="sxs-lookup"><span data-stu-id="5c68d-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="5c68d-125">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5c68d-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="5c68d-126">De MFA-methode voor een specifieke gebruiker moet de gebruiker B2B-samenwerking opnieuw in te stellen bewijs van methoden Reset.</span><span class="sxs-lookup"><span data-stu-id="5c68d-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="5c68d-127">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5c68d-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="5c68d-128">Waarom we MFA op de resource-tenancymodus uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="5c68d-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="5c68d-129">In de huidige versie is MFA altijd in de tenancymodus bron omwille van de hoge voorspelbaarheid is vereist.</span><span class="sxs-lookup"><span data-stu-id="5c68d-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="5c68d-130">Stel dat bijvoorbeeld een gebruiker Contoso (Sandra) wordt verzocht Fabrikam en Fabrikam MFA voor B2B-gebruikers heeft ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5c68d-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="5c68d-131">Als Contoso ingeschakeld voor App1, maar niet App2 MFA-beleid heeft, klikt u vervolgens als we de claim Contoso MFA in het token kijken mogelijk zien we het volgende probleem:</span><span class="sxs-lookup"><span data-stu-id="5c68d-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="5c68d-132">Dag 1: Een gebruiker heeft MFA in Contoso en toegang heeft tot App1 en er zijn geen extra MFA prompt wordt weergegeven in Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="5c68d-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="5c68d-133">Dag 2: De gebruiker toegang heeft gehad tot 2 van de App in Contoso, dus bij het openen van Fabrikam, moeten ze zich registreren voor MFA er.</span><span class="sxs-lookup"><span data-stu-id="5c68d-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="5c68d-134">Dit proces kan verwarrend zijn en kan leiden tot neerzetten in aanmelden voltooiingen.</span><span class="sxs-lookup"><span data-stu-id="5c68d-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="5c68d-135">Bovendien, zelfs als Contoso MFA-mogelijkheid heeft, is het niet altijd dat het geval de Fabrikam zou vertrouwt de Contoso-MFA-beleid.</span><span class="sxs-lookup"><span data-stu-id="5c68d-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="5c68d-136">Tot slot werkt resource tenant MFA ook voor MSA's en sociale-id's en voor de partner-organisaties waarvoor geen MFA instellen.</span><span class="sxs-lookup"><span data-stu-id="5c68d-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="5c68d-137">Daarom is de aanbeveling voor MFA voor B2B gebruikers altijd om MFA te vereisen in de uitnodiging tenant.</span><span class="sxs-lookup"><span data-stu-id="5c68d-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="5c68d-138">Deze vereiste kan ertoe leiden dat dubbele MFA in sommige gevallen, maar wanneer toegang tot de uitnodiging tenant, de ervaring voor eindgebruikers is voorspelbaar: Sandra moet registreren voor MFA bij de uitnodiging tenant.</span><span class="sxs-lookup"><span data-stu-id="5c68d-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="5c68d-139">Op basis van apparaten, op basis van locatie en risico gebaseerde voorwaardelijke toegang voor B2B-gebruikers</span><span class="sxs-lookup"><span data-stu-id="5c68d-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="5c68d-140">Wanneer Contoso beleidsregels voor voorwaardelijke toegang op basis van apparaten voor hun zakelijke gegevens kunt, wordt toegang niet van apparaten die niet beheerd door Contoso en niet compatibel zijn met het apparaatbeleid Contoso worden.</span><span class="sxs-lookup"><span data-stu-id="5c68d-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="5c68d-141">Als het apparaat van de B2B-gebruiker niet wordt beheerd door Contoso, wordt toegang van gebruikers van de partnerorganisaties B2B geblokkeerd in welke context deze beleidsregels worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="5c68d-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="5c68d-142">Contoso kan echter uitsluitingslijsten met specifieke partner-gebruikers uitgesloten van het beleid voor voorwaardelijke toegang op basis van apparaten te maken.</span><span class="sxs-lookup"><span data-stu-id="5c68d-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="5c68d-143">Voorwaardelijke toegang voor B2B op basis van locatie</span><span class="sxs-lookup"><span data-stu-id="5c68d-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="5c68d-144">Beleid voor voorwaardelijke toegang op basis van locatie kunnen worden afgedwongen voor B2B-gebruikers als de organisatie uitnodigen kunnen maken van een vertrouwde IP-adresbereik dat hun partnerorganisaties definieert.</span><span class="sxs-lookup"><span data-stu-id="5c68d-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="5c68d-145">Voorwaardelijke toegang op basis van een risico voor B2B</span><span class="sxs-lookup"><span data-stu-id="5c68d-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="5c68d-146">Worden op dit moment aanmelden beleid op basis van risico's kunnen niet toegepast voor B2B-gebruikers de risico-evaluatie wordt uitgevoerd op de B2B-gebruiker thuisorganisatie.</span><span class="sxs-lookup"><span data-stu-id="5c68d-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c68d-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5c68d-147">Next steps</span></span>

<span data-ttu-id="5c68d-148">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="5c68d-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="5c68d-149">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="5c68d-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="5c68d-150">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="5c68d-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="5c68d-151">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="5c68d-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="5c68d-152">De elementen van de uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="5c68d-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="5c68d-153">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="5c68d-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="5c68d-154">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="5c68d-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="5c68d-155">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="5c68d-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="5c68d-156">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="5c68d-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="5c68d-157">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="5c68d-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="5c68d-158">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="5c68d-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="5c68d-159">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="5c68d-159">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
