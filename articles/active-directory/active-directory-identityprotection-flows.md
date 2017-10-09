---
title: aaaSign in ervaringen met Azure AD Identity Protection | Microsoft Docs
description: Biedt een overzicht van de gebruikerservaring Hallo wanneer Identity Protection heeft verholpen of een gebruiker of wanneer de multi-factor authentication-server is vereist voor een beleid dat is hersteld.
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
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="bad6c-104">Aanmelden-ervaring met Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bad6c-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="bad6c-105">U kunt met Azure Active Directory: Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="bad6c-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="bad6c-106">gebruikers tooregister voor meervoudige verificatie vereisen</span><span class="sxs-lookup"><span data-stu-id="bad6c-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="bad6c-107">riskant aanmeldingen en verdachte gebruikers verwerken</span><span class="sxs-lookup"><span data-stu-id="bad6c-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="bad6c-108">antwoord Hallo Hallo system toothese problemen heeft een invloed op de aanmeldingservaring van een gebruiker omdat alleen rechtstreeks aanmelden met een gebruikersnaam en een wachtwoord niet mogelijk meer zijn.</span><span class="sxs-lookup"><span data-stu-id="bad6c-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="bad6c-109">Er zijn extra stappen vereist tooget een gebruiker terug veilig in bedrijf.</span><span class="sxs-lookup"><span data-stu-id="bad6c-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="bad6c-110">In dit onderwerp biedt een overzicht van de aanmeldingservaring van een gebruiker in alle gevallen die zich kunnen voordoen.</span><span class="sxs-lookup"><span data-stu-id="bad6c-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="bad6c-111">**Multi-factor authentication**</span><span class="sxs-lookup"><span data-stu-id="bad6c-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="bad6c-112">Registratie voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="bad6c-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="bad6c-113">**Meld u aan risico**</span><span class="sxs-lookup"><span data-stu-id="bad6c-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="bad6c-114">Herstel voor riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="bad6c-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="bad6c-115">Riskant aanmelden geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="bad6c-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="bad6c-116">Registratie van de multi-factor authentication-server tijdens een riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="bad6c-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="bad6c-117">**Gebruiker risico**</span><span class="sxs-lookup"><span data-stu-id="bad6c-117">**User at risk**</span></span>

* <span data-ttu-id="bad6c-118">Verdacht accountherstel</span><span class="sxs-lookup"><span data-stu-id="bad6c-118">Compromised account recovery</span></span>
* <span data-ttu-id="bad6c-119">Verdacht account geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="bad6c-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="bad6c-120">Registratie voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="bad6c-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="bad6c-121">Hallo beste gebruikerservaring voor beide, Hallo verdacht account recovery stroom en Hallo riskant aanmelden stroom, is wanneer de gebruiker Hallo zelf kunt herstellen.</span><span class="sxs-lookup"><span data-stu-id="bad6c-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="bad6c-122">Als gebruikers zijn geregistreerd voor multi-factor authentication, hebben ze al een telefoonnummer dat is gekoppeld aan hun account die kan worden gebruikt toopass beveiligingsproblemen met zich mee.</span><span class="sxs-lookup"><span data-stu-id="bad6c-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="bad6c-123">Er is geen help helpdesk of beheerder betrokkenheid is benodigde toorecover tegen inbreuk account.</span><span class="sxs-lookup"><span data-stu-id="bad6c-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="bad6c-124">Dus het is raadzaam tooget uw gebruikers geregistreerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="bad6c-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="bad6c-125">Beheerders kunnen:</span><span class="sxs-lookup"><span data-stu-id="bad6c-125">Administrators can:</span></span>

* <span data-ttu-id="bad6c-126">een beleid instellen dat gebruikers tooset van hun account voor aanvullende beveiligingsverificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="bad6c-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="bad6c-127">Multi-factor authentication-registratie voor too30 dagen, wordt overgeslagen als ze toogive gebruikers willen toestaan een respijtperiode voordat u registreert.</span><span class="sxs-lookup"><span data-stu-id="bad6c-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="bad6c-128">**Hallo-registratie voor multi-factor authentication-server heeft drie stappen:**</span><span class="sxs-lookup"><span data-stu-id="bad6c-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="bad6c-129">In de eerste stap Hallo opgehaald Hallo gebruiker een melding over Hallo vereiste tooset Hallo account voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="bad6c-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="bad6c-130">![Herstel](./media/active-directory-identityprotection-flows/140.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="bad6c-131">up tooset multi-factor Authentication-verificatie, moet u toolet Hallo system weet hoe u toobe bereikt.</span><span class="sxs-lookup"><span data-stu-id="bad6c-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="bad6c-132">![Herstel](./media/active-directory-identityprotection-flows/141.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="bad6c-133">Hallo system verzendt een challenge tooyou en moet u toorespond.</span><span class="sxs-lookup"><span data-stu-id="bad6c-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="bad6c-134">![Herstel](./media/active-directory-identityprotection-flows/142.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="bad6c-135">Herstel voor riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="bad6c-135">Risky sign-in recovery</span></span>
<span data-ttu-id="bad6c-136">Wanneer een beheerder heeft een beleid voor aanmelden risico's geconfigureerd, Hallo van invloed op een gebruikers een melding krijgen wanneer ze proberen toosign in.</span><span class="sxs-lookup"><span data-stu-id="bad6c-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="bad6c-137">**riskant Hallo aanmelden stroom bestaat uit twee stappen:**</span><span class="sxs-lookup"><span data-stu-id="bad6c-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="bad6c-138">Hallo-gebruiker wordt geïnformeerd dat ongewone activiteit over hun aanmelden gevonden is, zoals het aanmelden vanaf een nieuwe locatie, apparaat of app.</span><span class="sxs-lookup"><span data-stu-id="bad6c-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="bad6c-139">![Herstel](./media/active-directory-identityprotection-flows/120.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="bad6c-140">Hallo-gebruiker is vereist tooprove hun identiteit met een beveiligingsvraag op te lossen.</span><span class="sxs-lookup"><span data-stu-id="bad6c-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="bad6c-141">Als het Hallo-gebruiker is geregistreerd voor multi-factor authentication moet een telefoonnummer beveiliging code tootheir tooround-reis.</span><span class="sxs-lookup"><span data-stu-id="bad6c-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="bad6c-142">Aangezien dit een zojuist een riskante aanmelden en verdacht account, Hallo gebruiker geen toochange Hallo wachtwoord in deze stroom.</span><span class="sxs-lookup"><span data-stu-id="bad6c-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="bad6c-143">![Herstel](./media/active-directory-identityprotection-flows/121.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="bad6c-144">Riskant aanmelden geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="bad6c-144">Risky sign-in blocked</span></span>
<span data-ttu-id="bad6c-145">Beheerders kunnen tooset ook kiezen een aanmeldingspagina risico beleid tooblock gebruikers bij het aanmelden, afhankelijk van het risiconiveau Hallo.</span><span class="sxs-lookup"><span data-stu-id="bad6c-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="bad6c-146">tooget gedeblokkeerd, eindgebruikers moet contact opnemen met een beheerder of de helpdesk of proberen ze aanmelden vanaf een vertrouwde locatie of het apparaat.</span><span class="sxs-lookup"><span data-stu-id="bad6c-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="bad6c-147">Automatisch herstellen door het oplossen van multi-factor authentication-server kan niet worden gebruikt in dit geval.</span><span class="sxs-lookup"><span data-stu-id="bad6c-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="bad6c-148">![Herstel](./media/active-directory-identityprotection-flows/200.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="bad6c-149">Verdacht accountherstel</span><span class="sxs-lookup"><span data-stu-id="bad6c-149">Compromised account recovery</span></span>
<span data-ttu-id="bad6c-150">Wanneer een gebruiker risico-beveiligingsbeleid is geconfigureerd, gebruikers die voldoen aan de gebruiker Hallo risiconiveau opgegeven in het Hallo-beleid (en zijn daarom aangenomen geknoeid) moet doorlopen inbreuk Hallo-herstel gebruikersstroom voordat ze kunnen aanmelden.</span><span class="sxs-lookup"><span data-stu-id="bad6c-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="bad6c-151">**inbreuk op Hallo-herstel gebruikersstroom heeft drie stappen:**</span><span class="sxs-lookup"><span data-stu-id="bad6c-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="bad6c-152">Hallo-gebruiker wordt geïnformeerd dat de accountbeveiliging van hun risico vanwege verdachte activiteiten loopt of referenties gelekte.</span><span class="sxs-lookup"><span data-stu-id="bad6c-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="bad6c-153">![Herstel](./media/active-directory-identityprotection-flows/101.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="bad6c-154">Hallo-gebruiker is vereist tooprove hun identiteit met een beveiligingsvraag op te lossen.</span><span class="sxs-lookup"><span data-stu-id="bad6c-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="bad6c-155">Hallo-gebruiker is geregistreerd voor multi-factor authentication kunnen zichzelf herstellen van wordt aangetast.</span><span class="sxs-lookup"><span data-stu-id="bad6c-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="bad6c-156">Ze moet een telefoonnummer beveiliging code tootheir tooround-reis.</span><span class="sxs-lookup"><span data-stu-id="bad6c-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="bad6c-157">![Herstel](./media/active-directory-identityprotection-flows/110.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="bad6c-158">Ten slotte Hallo gebruiker is toochange gedwongen hun wachtwoord, omdat iemand anders tootheir-toegangsaccount heeft gehad.</span><span class="sxs-lookup"><span data-stu-id="bad6c-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="bad6c-159">Schermopnamen van deze ervaring zijn hieronder.</span><span class="sxs-lookup"><span data-stu-id="bad6c-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="bad6c-160">![Herstel](./media/active-directory-identityprotection-flows/111.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="bad6c-161">Verdacht account geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="bad6c-161">Compromised account blocked</span></span>
<span data-ttu-id="bad6c-162">tooget een gebruiker die is geblokkeerd door een gebruiker risico beveiligingsbeleid gedeblokkeerd, Hallo gebruiker, moet contact opnemen met een netwerkbeheerder of de helpdesk.</span><span class="sxs-lookup"><span data-stu-id="bad6c-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="bad6c-163">Automatisch herstellen door het oplossen van multi-factor authentication-server kan niet worden gebruikt in dit geval.</span><span class="sxs-lookup"><span data-stu-id="bad6c-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="bad6c-164">![Herstel](./media/active-directory-identityprotection-flows/104.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="bad6c-165">Wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="bad6c-165">Reset password</span></span>
<span data-ttu-id="bad6c-166">Als verdachte gebruikers hebben geen toegang tot het aanmelden, kan een beheerder een tijdelijk wachtwoord genereren voor deze.</span><span class="sxs-lookup"><span data-stu-id="bad6c-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="bad6c-167">Hallo hebben gebruikers toochange hun wachtwoord tijdens een volgende keer aanmelden.</span><span class="sxs-lookup"><span data-stu-id="bad6c-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="bad6c-168">![Herstel](./media/active-directory-identityprotection-flows/160.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="bad6c-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="bad6c-169">Zie ook</span><span class="sxs-lookup"><span data-stu-id="bad6c-169">See also</span></span>
* [<span data-ttu-id="bad6c-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bad6c-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

