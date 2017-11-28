---
title: aaaSecuring bevoorrechte toegang in Azure AD | Microsoft Docs
description: Dit onderwerp wordt beschreven Hallo benadert voor bevoegde toegang beveiligen in Azure, Azure Active Directory en Microsoft Online Services.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="8f956-103">Bevoegde toegang beveiligen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f956-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="8f956-104">Beveiligen van bevoegde toegang is een belangrijke eerste stap toohelp bedrijfsmiddelen in een moderne organisatie beveiligen.</span><span class="sxs-lookup"><span data-stu-id="8f956-104">Securing privileged access is a critical first step toohelp protect business assets in a modern organization.</span></span> <span data-ttu-id="8f956-105">Bevoegde accounts zijn accounts dat beheren en het beheer van IT-systemen.</span><span class="sxs-lookup"><span data-stu-id="8f956-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="8f956-106">Cyberbeveiliging aanvallers doel voor deze accounts toogain toegang tooan van gegevens en organisatie-systemen.</span><span class="sxs-lookup"><span data-stu-id="8f956-106">Cyber-attackers target these accounts toogain access tooan organization’s data and systems.</span></span> <span data-ttu-id="8f956-107">toosecure bevoegde toegang, moet u Hallo accounts isoleren en systemen van Hallo risico worden blootgesteld tooa kwaadwillende gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8f956-107">toosecure privileged access, you should isolate hello accounts and systems from hello risk of being exposed tooa malicious user.</span></span>

<span data-ttu-id="8f956-108">Meer gebruikers zijn tooget bevoegde toegang via cloud-services wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8f956-108">More users are starting tooget privileged access through cloud services.</span></span> <span data-ttu-id="8f956-109">Dit kunnen bijvoorbeeld globale beheerders van Office365, Azure-abonnementbeheerders en gebruikers die beheerderstoegang op de SaaS-apps of virtuele machines hebben.</span><span class="sxs-lookup"><span data-stu-id="8f956-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="8f956-110">Microsoft raadt u Volg deze roadmap op [bevoegde toegang beveiligen](https://technet.microsoft.com/library/mt631194.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f956-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="8f956-111">Deze principes toepassen voor klanten met Azure Active Directory, Office 365 of andere Microsoft-services en toepassingen, of gebruikersaccounts worden beheerd en geverifieerd door Active Directory of in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f956-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="8f956-112">Hallo volgende secties bevatten meer informatie over Azure AD-functies toosupport bevoegde toegang beveiligen.</span><span class="sxs-lookup"><span data-stu-id="8f956-112">hello following sections provide more information on Azure AD features toosupport securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="8f956-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="8f956-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="8f956-114">tooincrease hello beveiliging van de verificatie door de beheerder, moet u de verificatie in twee stappen voordat u verleent rechten vereisen.</span><span class="sxs-lookup"><span data-stu-id="8f956-114">tooincrease hello security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="8f956-115">Verificatie in twee stappen is een methode om te controleren wie u bent die Hallo gebruik van meer dan alleen een gebruikersnaam en wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="8f956-115">Two-step verification is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="8f956-116">Het biedt een tweede beveiligingslaag beveiliging toouser aanmeldingen en transacties.</span><span class="sxs-lookup"><span data-stu-id="8f956-116">It provides a second layer of security toouser sign-ins and transactions.</span></span>

<span data-ttu-id="8f956-117">Azure multi-factor Authentication (MFA) is een oplossing van Microsoft in twee stappen verificatie, welke u beveiligt toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="8f956-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="8f956-118">Sterke verificatie via een bereik van eenvoudige verificatie-opties zoals levert:</span><span class="sxs-lookup"><span data-stu-id="8f956-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="8f956-119">telefoongesprekken</span><span class="sxs-lookup"><span data-stu-id="8f956-119">phone calls</span></span>
- <span data-ttu-id="8f956-120">SMS-berichten</span><span class="sxs-lookup"><span data-stu-id="8f956-120">text messages</span></span>
- <span data-ttu-id="8f956-121">mobiele app-meldingen</span><span class="sxs-lookup"><span data-stu-id="8f956-121">mobile app notifications</span></span>
- <span data-ttu-id="8f956-122">mobiele app verificatiecodes</span><span class="sxs-lookup"><span data-stu-id="8f956-122">mobile app verification codes</span></span>
- <span data-ttu-id="8f956-123">OATH-tokens van derde partij</span><span class="sxs-lookup"><span data-stu-id="8f956-123">third-party OATH tokens</span></span>

<span data-ttu-id="8f956-124">Zie voor een overzicht van de werking van Azure multi-factor Authentication Hallo video te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f956-124">For an overview of how Azure Multi-Factor Authentication works see hello following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="8f956-125">Zie voor meer informatie [MFA voor Office 365 en MFA voor Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="8f956-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="8f956-126">Tijdsgebonden bevoegdheden</span><span class="sxs-lookup"><span data-stu-id="8f956-126">Time-bound privileges</span></span>
<span data-ttu-id="8f956-127">Sommige organisaties kunnen het gebeuren dat ze te veel gebruikers in maximaal bevoorrechte rollen hebben.</span><span class="sxs-lookup"><span data-stu-id="8f956-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="8f956-128">Een gebruiker mogelijk toegevoegd toohello rol voor een bepaalde activiteit, zoals toosign voor een service, maar deze rechten niet vaak later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8f956-128">A user might have been added toohello role for a particular activity, like toosign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="8f956-129">toolower hello blootstellingstijd bevoegdheden en het verhogen van de zichtbaarheid van hun gebruik, limiet gebruikers tooonly nemen over hun bevoegdheden 'just in time' (Just in time), wanneer ze een taak tooperform nodig.</span><span class="sxs-lookup"><span data-stu-id="8f956-129">toolower hello exposure time of privileges and increase your visibility into their use, limit users tooonly taking on their privileges "just in time" (JIT), when they need tooperform a task.</span></span> <span data-ttu-id="8f956-130">Voor Azure Active Directory en Microsoft Online Services, kunt u [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="8f956-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM-dashboard][2]

## <a name="attack-detection"></a><span data-ttu-id="8f956-132">Aanvalsdetectie</span><span class="sxs-lookup"><span data-stu-id="8f956-132">Attack detection</span></span>
<span data-ttu-id="8f956-133">[Azure Active Directory: Identity Protection](../active-directory-identityprotection.md) biedt een geconsolideerde weergave risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="8f956-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="8f956-134">Op basis van de risico's, Identity Protection berekent het risiconiveau van een gebruiker voor elke gebruiker, zodat u tooconfigure risico beleid op basis van tooautomatically beveiligen Hallo identiteiten van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="8f956-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you tooconfigure risk-based policies tooautomatically protect hello identities of your organization.</span></span> <span data-ttu-id="8f956-135">Dit beleid, samen met andere besturingselementen voorwaardelijke toegang is verstrekt door Azure Active Directory en EMS, kunnen automatisch Hallo gebruiker blokkeren of suggesties met wachtwoord opnieuw instellen en afdwingen van multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="8f956-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block hello user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD-identiteitsbeveiliging][3]

## <a name="conditional-access"></a><span data-ttu-id="8f956-137">Voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="8f956-137">Conditional access</span></span>
<span data-ttu-id="8f956-138">Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van een gebruiker, alvorens deze toegang tooan toepassing kiezen.</span><span class="sxs-lookup"><span data-stu-id="8f956-138">With conditional access control, Azure Active Directory checks hello specific conditions you choose when authenticating a user, before allowing access tooan application.</span></span> <span data-ttu-id="8f956-139">Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan.</span><span class="sxs-lookup"><span data-stu-id="8f956-139">Once those conditions are met, hello user is authenticated and allowed access toohello application.</span></span>

![Instellen van regels voor voorwaardelijke toegang met MFA][4]

## <a name="related-articles"></a><span data-ttu-id="8f956-141">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="8f956-141">Related articles</span></span>
* <span data-ttu-id="8f956-142">Schakel [Azure multi-factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="8f956-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="8f956-143">Schakel [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="8f956-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="8f956-144">Schakel [Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="8f956-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="8f956-145">Schakel [voorwaardelijk toegangsbeheer](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="8f956-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="8f956-146">Zie voor meer informatie over het bouwen van een volledige beveiliging roadmap Hallo 'verantwoordelijkheden van de klant en roadmap' sectie Hallo [Microsoft Cloud Security voor Enterprise-architecten](http://aka.ms/securecustomer) document.</span><span class="sxs-lookup"><span data-stu-id="8f956-146">For more information on building a complete security roadmap, see hello “Customer responsibilities and roadmap” section of hello [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="8f956-147">Voor meer informatie over Microsoft-services tooassist met een van deze onderwerpen bezighouden, neem contact op met uw Microsoft-vertegenwoordiger of gaat u naar onze [Cybersecurity oplossingen pagina](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f956-147">For more information on engaging Microsoft services tooassist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
