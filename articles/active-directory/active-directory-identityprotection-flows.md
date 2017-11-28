---
title: Aanmelden-ervaringen met Azure AD Identity Protection | Microsoft Docs
description: Biedt een overzicht van de gebruikerservaring als Identity Protection is verholpen of hersteld van een gebruiker of als de multi-factor authentication-server is vereist voor een beleid.
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="16ac7-104">Aanmelden-ervaring met Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="16ac7-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="16ac7-105">U kunt met Azure Active Directory: Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="16ac7-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="16ac7-106">vereisen dat gebruikers zich registreren voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="16ac7-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="16ac7-107">riskant aanmeldingen en verdachte gebruikers verwerken</span><span class="sxs-lookup"><span data-stu-id="16ac7-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="16ac7-108">Het antwoord van het systeem op deze problemen invloed is op een gebruiker-aanmeldingservaring aanpast omdat alleen rechtstreeks aanmelden door op te geven van een gebruikersnaam en een wachtwoord zijn niet mogelijk meer.</span><span class="sxs-lookup"><span data-stu-id="16ac7-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="16ac7-109">Er zijn extra stappen nodig om op te halen van een gebruiker veilig weer in bedrijf.</span><span class="sxs-lookup"><span data-stu-id="16ac7-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="16ac7-110">In dit onderwerp biedt een overzicht van de aanmeldingservaring van een gebruiker in alle gevallen die zich kunnen voordoen.</span><span class="sxs-lookup"><span data-stu-id="16ac7-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="16ac7-111">**Multi-factor authentication**</span><span class="sxs-lookup"><span data-stu-id="16ac7-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="16ac7-112">Registratie voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="16ac7-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="16ac7-113">**Meld u aan risico**</span><span class="sxs-lookup"><span data-stu-id="16ac7-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="16ac7-114">Herstel voor riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="16ac7-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="16ac7-115">Riskant aanmelden geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="16ac7-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="16ac7-116">Registratie van de multi-factor authentication-server tijdens een riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="16ac7-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="16ac7-117">**Gebruiker risico**</span><span class="sxs-lookup"><span data-stu-id="16ac7-117">**User at risk**</span></span>

* <span data-ttu-id="16ac7-118">Verdacht accountherstel</span><span class="sxs-lookup"><span data-stu-id="16ac7-118">Compromised account recovery</span></span>
* <span data-ttu-id="16ac7-119">Verdacht account geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="16ac7-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="16ac7-120">Registratie voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="16ac7-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="16ac7-121">De beste gebruikerservaring voor zowel de verdacht account recovery stroom en de stroom voor riskante aanmelden is wanneer de gebruiker zelf kunt herstellen.</span><span class="sxs-lookup"><span data-stu-id="16ac7-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="16ac7-122">Als gebruikers zijn geregistreerd voor multi-factor authentication, hebben ze al een telefoonnummer dat is gekoppeld aan hun account die kan worden gebruikt om door te geven van beveiligingsproblemen met zich mee.</span><span class="sxs-lookup"><span data-stu-id="16ac7-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="16ac7-123">Geen help helpdesk of beheerder betrokkenheid is nodig voor het herstellen van inbreuk op het account.</span><span class="sxs-lookup"><span data-stu-id="16ac7-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="16ac7-124">Dus is het raadzaam om op te halen van de gebruikers die zijn geregistreerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="16ac7-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="16ac7-125">Beheerders kunnen:</span><span class="sxs-lookup"><span data-stu-id="16ac7-125">Administrators can:</span></span>

* <span data-ttu-id="16ac7-126">een beleid instellen dat gebruikers moeten hun accounts instellen voor aanvullende beveiligingsverificatie.</span><span class="sxs-lookup"><span data-stu-id="16ac7-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="16ac7-127">bieden registratie voor meervoudige verificatie overslaan voor maximaal 30 dagen, als deze gebruikers geven een respijtperiode wilt voordat u registreert.</span><span class="sxs-lookup"><span data-stu-id="16ac7-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="16ac7-128">**De registratie van de multi-factor authentication-server heeft drie stappen:**</span><span class="sxs-lookup"><span data-stu-id="16ac7-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="16ac7-129">In de eerste stap van ontvangt de gebruiker een melding over de vereiste van het account voor multi-factor authentication instellen.</span><span class="sxs-lookup"><span data-stu-id="16ac7-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="16ac7-130">![Herstel](./media/active-directory-identityprotection-flows/140.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="16ac7-131">Multi-factor authentication-server als u wilt instellen, moet u laten weten hoe u wilt verbinding worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16ac7-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="16ac7-132">![Herstel](./media/active-directory-identityprotection-flows/141.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="16ac7-133">Het systeem verzendt een uitdaging voor u en u moet reageren.</span><span class="sxs-lookup"><span data-stu-id="16ac7-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="16ac7-134">![Herstel](./media/active-directory-identityprotection-flows/142.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="16ac7-135">Herstel voor riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="16ac7-135">Risky sign-in recovery</span></span>
<span data-ttu-id="16ac7-136">Wanneer een beheerder heeft een beleid voor aanmelden risico's geconfigureerd, wordt de betreffende gebruikers worden gewaarschuwd wanneer ze proberen om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="16ac7-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="16ac7-137">**De stroom voor riskante aanmelden bestaat uit twee stappen:**</span><span class="sxs-lookup"><span data-stu-id="16ac7-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="16ac7-138">De gebruiker wordt geïnformeerd dat ongewone activiteit over hun aanmelden gevonden is, zoals het aanmelden vanaf een nieuwe locatie, apparaat of app.</span><span class="sxs-lookup"><span data-stu-id="16ac7-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="16ac7-139">![Herstel](./media/active-directory-identityprotection-flows/120.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="16ac7-140">De gebruiker is vereist voor hun identiteit bewijzen door een beveiligingsvraag op te lossen.</span><span class="sxs-lookup"><span data-stu-id="16ac7-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="16ac7-141">Als de gebruiker is geregistreerd voor multi-factor authentication moeten ze interactie een beveiligingscode naar hun telefoonnummer.</span><span class="sxs-lookup"><span data-stu-id="16ac7-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="16ac7-142">Aangezien dit een zojuist een riskante aanmelden en geen account waarmee is geknoeid, wordt de gebruiker hoeft te wijzigen van het wachtwoord in deze stroom.</span><span class="sxs-lookup"><span data-stu-id="16ac7-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="16ac7-143">![Herstel](./media/active-directory-identityprotection-flows/121.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="16ac7-144">Riskant aanmelden geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="16ac7-144">Risky sign-in blocked</span></span>
<span data-ttu-id="16ac7-145">Beheerders kunnen ook kiezen een beleid voor aanmelden risico voorkomen dat gebruikers bij het aanmelden, afhankelijk van het risiconiveau instellen.</span><span class="sxs-lookup"><span data-stu-id="16ac7-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="16ac7-146">Als u gedeblokkeerd, eindgebruikers moet contact opnemen met een netwerkbeheerder of de helpdesk of proberen ze aanmelden vanaf een vertrouwde locatie of het apparaat.</span><span class="sxs-lookup"><span data-stu-id="16ac7-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="16ac7-147">Automatisch herstellen door het oplossen van multi-factor authentication-server kan niet worden gebruikt in dit geval.</span><span class="sxs-lookup"><span data-stu-id="16ac7-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="16ac7-148">![Herstel](./media/active-directory-identityprotection-flows/200.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="16ac7-149">Verdacht accountherstel</span><span class="sxs-lookup"><span data-stu-id="16ac7-149">Compromised account recovery</span></span>
<span data-ttu-id="16ac7-150">Wanneer een gebruiker risico-beveiligingsbeleid is geconfigureerd, gebruikers die voldoen aan de gebruiker risiconiveau opgegeven in het beleid (en zijn daarom aangenomen geknoeid) door de gebruiker inbreuk herstel stroom moet gaan voordat ze kunnen aanmelden.</span><span class="sxs-lookup"><span data-stu-id="16ac7-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="16ac7-151">**De gebruiker inbreuk herstel-stroom heeft drie stappen:**</span><span class="sxs-lookup"><span data-stu-id="16ac7-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="16ac7-152">De gebruiker wordt geïnformeerd dat de accountbeveiliging van hun risico vanwege verdachte activiteiten loopt of referenties gelekte.</span><span class="sxs-lookup"><span data-stu-id="16ac7-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="16ac7-153">![Herstel](./media/active-directory-identityprotection-flows/101.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="16ac7-154">De gebruiker is vereist voor hun identiteit bewijzen door een beveiligingsvraag op te lossen.</span><span class="sxs-lookup"><span data-stu-id="16ac7-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="16ac7-155">Als de gebruiker is geregistreerd voor multi-factor authentication kunnen ze zelf herstellen van wordt aangetast.</span><span class="sxs-lookup"><span data-stu-id="16ac7-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="16ac7-156">Ze moet interactie een beveiligingscode naar hun telefoonnummer.</span><span class="sxs-lookup"><span data-stu-id="16ac7-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="16ac7-157">![Herstel](./media/active-directory-identityprotection-flows/110.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="16ac7-158">Ten slotte wordt de gebruiker gedwongen hun wachtwoord wijzigen omdat iemand anders mogelijk toegang heeft gehad tot hun account.</span><span class="sxs-lookup"><span data-stu-id="16ac7-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="16ac7-159">Schermopnamen van deze ervaring zijn hieronder.</span><span class="sxs-lookup"><span data-stu-id="16ac7-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="16ac7-160">![Herstel](./media/active-directory-identityprotection-flows/111.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="16ac7-161">Verdacht account geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="16ac7-161">Compromised account blocked</span></span>
<span data-ttu-id="16ac7-162">Als u een gebruiker die is geblokkeerd door een gebruiker risico beveiligingsbeleid gedeblokkeerd, moet de gebruiker contact op met een beheerder of helpdesk.</span><span class="sxs-lookup"><span data-stu-id="16ac7-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="16ac7-163">Automatisch herstellen door het oplossen van multi-factor authentication-server kan niet worden gebruikt in dit geval.</span><span class="sxs-lookup"><span data-stu-id="16ac7-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="16ac7-164">![Herstel](./media/active-directory-identityprotection-flows/104.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="16ac7-165">Wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="16ac7-165">Reset password</span></span>
<span data-ttu-id="16ac7-166">Als verdachte gebruikers hebben geen toegang tot het aanmelden, kan een beheerder een tijdelijk wachtwoord genereren voor deze.</span><span class="sxs-lookup"><span data-stu-id="16ac7-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="16ac7-167">De gebruikers hebben hun wachtwoord wijzigen tijdens een volgende keer aanmelden.</span><span class="sxs-lookup"><span data-stu-id="16ac7-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="16ac7-168">![Herstel](./media/active-directory-identityprotection-flows/160.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="16ac7-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="16ac7-169">Zie ook</span><span class="sxs-lookup"><span data-stu-id="16ac7-169">See also</span></span>
* [<span data-ttu-id="16ac7-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="16ac7-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

