---
title: Bevoegde toegang beveiligen in Azure AD | Microsoft Docs
description: "Een onderwerp met uitleg over de strategieën voor het beveiligen van bevoegde toegang in Azure, Azure Active Directory en Microsoft Online Services."
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
ms.openlocfilehash: acd1c11cecfa37f607fe5d82a76a40647093f43f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="ee189-103">Bevoegde toegang beveiligen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee189-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="ee189-104">Bevoegde toegang beveiligen is een belangrijke eerste stap ter bescherming van zakelijke activa in een moderne organisatie.</span><span class="sxs-lookup"><span data-stu-id="ee189-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span></span> <span data-ttu-id="ee189-105">Bevoegde accounts zijn accounts dat beheren en het beheer van IT-systemen.</span><span class="sxs-lookup"><span data-stu-id="ee189-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="ee189-106">Cyberbeveiliging aanvallers gericht zijn op deze accounts toegang krijgen tot gegevens en systemen van een organisatie.</span><span class="sxs-lookup"><span data-stu-id="ee189-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span></span> <span data-ttu-id="ee189-107">Als u wilt beveiligen bevoorrechte toegang, moet u de accounts en systemen van het risico worden blootgesteld aan een kwaadwillende gebruiker isoleren.</span><span class="sxs-lookup"><span data-stu-id="ee189-107">To secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span></span>

<span data-ttu-id="ee189-108">Meer gebruikers zijn bevoorrechte om toegang te krijgen via cloudservices gestart.</span><span class="sxs-lookup"><span data-stu-id="ee189-108">More users are starting to get privileged access through cloud services.</span></span> <span data-ttu-id="ee189-109">Dit kunnen bijvoorbeeld globale beheerders van Office365, Azure-abonnementbeheerders en gebruikers die beheerderstoegang op de SaaS-apps of virtuele machines hebben.</span><span class="sxs-lookup"><span data-stu-id="ee189-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="ee189-110">Microsoft raadt u Volg deze roadmap op [bevoegde toegang beveiligen](https://technet.microsoft.com/library/mt631194.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee189-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="ee189-111">Deze principes toepassen voor klanten met Azure Active Directory, Office 365 of andere Microsoft-services en toepassingen, of gebruikersaccounts worden beheerd en geverifieerd door Active Directory of in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ee189-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="ee189-112">De volgende secties bevatten meer informatie over Azure AD-functies voor de ondersteuning van bevoegde toegang beveiligen.</span><span class="sxs-lookup"><span data-stu-id="ee189-112">The following sections provide more information on Azure AD features to support securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="ee189-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ee189-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="ee189-114">Voor een verhoging van de beveiliging van de verificatie door de beheerder moet u de verificatie in twee stappen voordat u verleent rechten vereisen.</span><span class="sxs-lookup"><span data-stu-id="ee189-114">To increase the security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="ee189-115">Verificatie in twee stappen is een methode om te controleren wie u bent die het gebruik van meer dan alleen een gebruikersnaam en wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="ee189-115">Two-step verification is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="ee189-116">Het biedt een tweede beveiligingslaag op gebruikersaanmeldingen en transacties.</span><span class="sxs-lookup"><span data-stu-id="ee189-116">It provides a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="ee189-117">Azure multi-factor Authentication (MFA) is oplossing van Microsoft in twee stappen verificatie, welke helpt beveiliging toegang tot gegevens en toepassingen en te voldoen aan de gebruiker vragen voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ee189-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ee189-118">Sterke verificatie via een bereik van eenvoudige verificatie-opties zoals levert:</span><span class="sxs-lookup"><span data-stu-id="ee189-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="ee189-119">telefoongesprekken</span><span class="sxs-lookup"><span data-stu-id="ee189-119">phone calls</span></span>
- <span data-ttu-id="ee189-120">SMS-berichten</span><span class="sxs-lookup"><span data-stu-id="ee189-120">text messages</span></span>
- <span data-ttu-id="ee189-121">mobiele app-meldingen</span><span class="sxs-lookup"><span data-stu-id="ee189-121">mobile app notifications</span></span>
- <span data-ttu-id="ee189-122">mobiele app verificatiecodes</span><span class="sxs-lookup"><span data-stu-id="ee189-122">mobile app verification codes</span></span>
- <span data-ttu-id="ee189-123">OATH-tokens van derde partij</span><span class="sxs-lookup"><span data-stu-id="ee189-123">third-party OATH tokens</span></span>

<span data-ttu-id="ee189-124">Zie de volgende video voor een overzicht van de werking van Azure multi-factor Authentication:</span><span class="sxs-lookup"><span data-stu-id="ee189-124">For an overview of how Azure Multi-Factor Authentication works see the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="ee189-125">Zie voor meer informatie [MFA voor Office 365 en MFA voor Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="ee189-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="ee189-126">Tijdsgebonden bevoegdheden</span><span class="sxs-lookup"><span data-stu-id="ee189-126">Time-bound privileges</span></span>
<span data-ttu-id="ee189-127">Sommige organisaties kunnen het gebeuren dat ze te veel gebruikers in maximaal bevoorrechte rollen hebben.</span><span class="sxs-lookup"><span data-stu-id="ee189-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="ee189-128">Een gebruiker kan zijn toegevoegd aan de rol voor een bepaalde activiteit, zoals aanmelden voor een service, maar deze rechten niet vaak later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee189-128">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="ee189-129">Om te verlagen van de blootstellingstijd van bevoegdheden en vergroot de zichtbaarheid van het gebruik ervan, gebruikers beperken tot alleen nemen over hun bevoegdheden 'just in time' (Just in time), wanneer u wilt een taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ee189-129">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges "just in time" (JIT), when they need to perform a task.</span></span> <span data-ttu-id="ee189-130">Voor Azure Active Directory en Microsoft Online Services, kunt u [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="ee189-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM-dashboard][2]

## <a name="attack-detection"></a><span data-ttu-id="ee189-132">Aanvalsdetectie</span><span class="sxs-lookup"><span data-stu-id="ee189-132">Attack detection</span></span>
<span data-ttu-id="ee189-133">[Azure Active Directory: Identity Protection](../active-directory-identityprotection.md) biedt een geconsolideerde weergave risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ee189-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="ee189-134">Op basis van de risico's, berekent Identity Protection het risiconiveau van een gebruiker voor elke gebruiker, zodat u kunt beleid op basis van een risico voor het automatisch beveiligen van de identiteit van uw organisatie configureren.</span><span class="sxs-lookup"><span data-stu-id="ee189-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span> <span data-ttu-id="ee189-135">Dit beleid, samen met andere besturingselementen voorwaardelijke toegang is verstrekt door Azure Active Directory en EMS, kunnen automatisch worden voorkomen dat de gebruiker of suggesties met wachtwoord opnieuw instellen en afdwingen van multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="ee189-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD-identiteitsbeveiliging][3]

## <a name="conditional-access"></a><span data-ttu-id="ee189-137">Voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="ee189-137">Conditional access</span></span>
<span data-ttu-id="ee189-138">Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory de specifieke voorwaarden die u bij het verifiëren van een gebruiker, alvorens deze toegang tot een toepassing kiezen.</span><span class="sxs-lookup"><span data-stu-id="ee189-138">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span></span> <span data-ttu-id="ee189-139">Als deze voorwaarden is voldaan, wordt de gebruiker geverifieerd en toegang te krijgen tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee189-139">Once those conditions are met, the user is authenticated and allowed access to the application.</span></span>

![Instellen van regels voor voorwaardelijke toegang met MFA][4]

## <a name="related-articles"></a><span data-ttu-id="ee189-141">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="ee189-141">Related articles</span></span>
* <span data-ttu-id="ee189-142">Schakel [Azure multi-factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="ee189-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="ee189-143">Schakel [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ee189-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="ee189-144">Schakel [Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="ee189-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="ee189-145">Schakel [voorwaardelijk toegangsbeheer](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="ee189-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="ee189-146">Voor meer informatie over het bouwen van een volledige beveiliging roadmap, Zie de sectie 'verantwoordelijkheden van de klant en roadmap' van de [Microsoft Cloud Security voor Enterprise-architecten](http://aka.ms/securecustomer) document.</span><span class="sxs-lookup"><span data-stu-id="ee189-146">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="ee189-147">Voor meer informatie over Microsoft-services om te helpen bij deze onderwerpen bezighouden, neem contact op met uw Microsoft-vertegenwoordiger of gaat u naar onze [Cybersecurity oplossingen pagina](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee189-147">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
