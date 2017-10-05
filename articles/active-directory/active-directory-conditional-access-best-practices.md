---
title: Aanbevolen procedures voor voorwaardelijke toegang in Azure Active Directory | Microsoft Docs
description: Meer informatie over wat die u moet weten en wat het is raadzaam doen bij het configureren van beleidsregels voor voorwaardelijke toegang.
services: active-directory
keywords: voorwaardelijke toegang tot apps, voorwaardelijke toegang met Azure AD, beveiligde toegang tot bedrijfsresources, beleidsregels voor voorwaardelijke toegang
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="7f772-104">Aanbevolen procedures voor voorwaardelijke toegang in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f772-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="7f772-105">In dit onderwerp vindt u informatie over wat die u moet weten en wat het is raadzaam doen bij het configureren van beleidsregels voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="7f772-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="7f772-106">Voordat u dit onderwerp leest, moet u vertrouwd raken met de concepten en termen die worden beschreven in [voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7f772-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="7f772-107">Wat u moet weten</span><span class="sxs-lookup"><span data-stu-id="7f772-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="7f772-108">Wat is vereist voor het maken van een beleid werken?</span><span class="sxs-lookup"><span data-stu-id="7f772-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="7f772-109">Wanneer u een nieuw beleid maakt, zijn er geen gebruikers, groepen, apps of toegangsbeheer geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7f772-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Cloud-apps](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="7f772-111">Als u uw beleid wilt werken, moet u het volgende configureren:</span><span class="sxs-lookup"><span data-stu-id="7f772-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="7f772-112">Wat</span><span class="sxs-lookup"><span data-stu-id="7f772-112">What</span></span>           | <span data-ttu-id="7f772-113">Hoe</span><span class="sxs-lookup"><span data-stu-id="7f772-113">How</span></span>                                  | <span data-ttu-id="7f772-114">Waarom</span><span class="sxs-lookup"><span data-stu-id="7f772-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="7f772-115">**Cloud-apps**</span><span class="sxs-lookup"><span data-stu-id="7f772-115">**Cloud apps**</span></span> |<span data-ttu-id="7f772-116">U moet een of meer apps selecteren.</span><span class="sxs-lookup"><span data-stu-id="7f772-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="7f772-117">Het doel van een beleid voor voorwaardelijke toegang is zodat u kunt aanpassen hoe gemachtigde gebruikers toegang uw apps tot hebben.</span><span class="sxs-lookup"><span data-stu-id="7f772-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="7f772-118">**Gebruikers en groepen**</span><span class="sxs-lookup"><span data-stu-id="7f772-118">**Users and groups**</span></span> | <span data-ttu-id="7f772-119">U moet ten minste één gebruiker of groep die is gemachtigd voor toegang tot de cloud-apps die u hebt geselecteerd selecteren.</span><span class="sxs-lookup"><span data-stu-id="7f772-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="7f772-120">Beleid voor voorwaardelijke toegang dat er geen gebruikers en groepen die zijn toegewezen, wordt nooit geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7f772-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="7f772-121">**Toegangsbeheer**</span><span class="sxs-lookup"><span data-stu-id="7f772-121">**Access controls**</span></span> | <span data-ttu-id="7f772-122">U moet ten minste één toegangsbeheer selecteren.</span><span class="sxs-lookup"><span data-stu-id="7f772-122">You need to select at least one access control.</span></span> | <span data-ttu-id="7f772-123">De processor van uw beleid moet weten wat te doen als uw voorwaarden is voldaan.</span><span class="sxs-lookup"><span data-stu-id="7f772-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="7f772-124">Naast deze basisvereisten moet in veel gevallen u ook configureren een voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="7f772-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="7f772-125">Een beleid zou ook werken zonder een geconfigureerde voorwaarde, zijn voorwaarden de aangedreven factor voor toegang tot uw apps aan te passen.</span><span class="sxs-lookup"><span data-stu-id="7f772-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![Cloud-apps](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="7f772-127">Hoe worden toewijzingen geëvalueerd</span><span class="sxs-lookup"><span data-stu-id="7f772-127">How are assignments evaluated?</span></span>

<span data-ttu-id="7f772-128">Alle toewijzingen zijn logische **and**.</span><span class="sxs-lookup"><span data-stu-id="7f772-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="7f772-129">Als u meer dan één toewijzing geconfigureerd hebt, om te activeren van een beleid moeten alle toewijzingen worden voldaan.</span><span class="sxs-lookup"><span data-stu-id="7f772-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="7f772-130">Als u nodig hebt voor het configureren van de voorwaarde van een locatie die van toepassing op alle verbindingen van buiten het netwerk van uw organisatie, kunt u dit doen door:</span><span class="sxs-lookup"><span data-stu-id="7f772-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="7f772-131">Inclusief **alle locaties**</span><span class="sxs-lookup"><span data-stu-id="7f772-131">Including **All locations**</span></span>
- <span data-ttu-id="7f772-132">Met uitzondering van **alle goedgekeurde IP-adressen**</span><span class="sxs-lookup"><span data-stu-id="7f772-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="7f772-133">Wat gebeurt er als het beleid in de klassieke Azure-portal en de Azure portal geconfigureerd?</span><span class="sxs-lookup"><span data-stu-id="7f772-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="7f772-134">Beide beleidsregels worden afgedwongen door Azure Active Directory en de gebruiker krijgt toegang alleen wanneer alle vereisten wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="7f772-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="7f772-135">Wat gebeurt er als u een beleid in de Intune Silverlight-portal en de Azure-Portal hebt?</span><span class="sxs-lookup"><span data-stu-id="7f772-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="7f772-136">Beide beleidsregels worden afgedwongen door Azure Active Directory en de gebruiker krijgt toegang alleen wanneer alle vereisten wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="7f772-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="7f772-137">Wat gebeurt er als ik heb meerdere beleidsregels voor dezelfde gebruiker geconfigureerd?</span><span class="sxs-lookup"><span data-stu-id="7f772-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="7f772-138">Voor elke aanmelding, Azure Active Directory evalueert alle beleidsregels en zorgt ervoor dat alle vereisten wordt voldaan voordat toegang verleend aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7f772-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="7f772-139">Werkt voorwaardelijke toegang met Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="7f772-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="7f772-140">Ja, kunt u Exchange ActiveSync in een beleid voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="7f772-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="7f772-141">Wat moet u niet doen</span><span class="sxs-lookup"><span data-stu-id="7f772-141">What you should avoid doing</span></span>

<span data-ttu-id="7f772-142">Het framework voor voorwaardelijke toegang biedt u de flexibiliteit van een geweldige configuratie.</span><span class="sxs-lookup"><span data-stu-id="7f772-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="7f772-143">Hoge mate van flexibiliteit ook betekent echter dat u zorgvuldig elke configuratiebeleid vóór vrijgeven om ongewenste resultaten voorkomen.</span><span class="sxs-lookup"><span data-stu-id="7f772-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="7f772-144">In deze context moet u speciale aandacht schenken aan toewijzingen zoals die invloed hebben op volledige set betalen **alle gebruikers / groepen / cloud-apps**.</span><span class="sxs-lookup"><span data-stu-id="7f772-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="7f772-145">In uw omgeving, moet u de volgende configuraties voorkomen:</span><span class="sxs-lookup"><span data-stu-id="7f772-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="7f772-146">**Voor alle gebruikers alle cloud-apps:**</span><span class="sxs-lookup"><span data-stu-id="7f772-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="7f772-147">**Toegang blokkeren** -uw hele organisatie, absoluut niet verstandig is deze configuratie wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="7f772-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="7f772-148">**Vereisen dat apparaat compatibel** - voor gebruikers die niet hun apparaten hebben ingeschreven, maar dit beleid blokkeert alle toegang, waaronder toegang tot de Intune-portal.</span><span class="sxs-lookup"><span data-stu-id="7f772-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="7f772-149">Als u een beheerder met een geregistreerd apparaat, blokkeert dit beleid u uit om terug te zetten in de Azure-portal om het beleid te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7f772-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="7f772-150">**Aan domein toevoegen vereisen** : dit beleid blok toegang heeft ook de mogelijkheid om toegang te blokkeren voor alle gebruikers in uw organisatie als u een apparaat domein nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="7f772-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="7f772-151">**Voor alle gebruikers, alle cloud-apps, alle platforms:**</span><span class="sxs-lookup"><span data-stu-id="7f772-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="7f772-152">**Toegang blokkeren** -uw hele organisatie, absoluut niet verstandig is deze configuratie wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="7f772-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="7f772-153">Algemene scenario's</span><span class="sxs-lookup"><span data-stu-id="7f772-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="7f772-154">Meervoudige verificatie vereisen voor apps</span><span class="sxs-lookup"><span data-stu-id="7f772-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="7f772-155">Veel omgevingen hebben apps waarvoor een hoger niveau van beveiliging dan de andere.</span><span class="sxs-lookup"><span data-stu-id="7f772-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="7f772-156">Dit is bijvoorbeeld het geval voor apps die toegang tot gevoelige gegevens hebben.</span><span class="sxs-lookup"><span data-stu-id="7f772-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="7f772-157">Als u een andere beschermingslaag toevoegen aan deze apps wilt, kunt u een beleid voor voorwaardelijke toegang waarvoor multi-factor authentication-server is vereist wanneer gebruikers toegang hebben tot deze apps kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="7f772-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="7f772-158">Meervoudige verificatie vereisen voor toegang via netwerken die geen vertrouwde</span><span class="sxs-lookup"><span data-stu-id="7f772-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="7f772-159">Dit scenario is vergelijkbaar met het vorige scenario, omdat een vereiste voor multi-factor authentication wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7f772-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="7f772-160">Het belangrijkste verschil is echter de voorwaarde voor deze vereiste.</span><span class="sxs-lookup"><span data-stu-id="7f772-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="7f772-161">Tijdens de focus van het vorige scenario op apps met toegang tot sensitve gegevens, is de focus van dit scenario op vertrouwde locaties.</span><span class="sxs-lookup"><span data-stu-id="7f772-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="7f772-162">U wellicht een vereiste voor multi-factor authentication met andere woorden, als een app wordt geopend door een gebruiker vanaf een netwerk dat u niet vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="7f772-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="7f772-163">Alleen vertrouwde apparaten hebben toegang tot Office 365-services</span><span class="sxs-lookup"><span data-stu-id="7f772-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="7f772-164">Als u van Intune in uw omgeving gebruikmaakt, kunt u onmiddellijk starten via de interface van het beleid voor voorwaardelijke toegang in de Azure-console.</span><span class="sxs-lookup"><span data-stu-id="7f772-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="7f772-165">Veel klanten van Intune voorwaardelijke toegang gebruiken om ervoor te zorgen dat alleen vertrouwde apparaten toegang krijgen Office 365-services tot.</span><span class="sxs-lookup"><span data-stu-id="7f772-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="7f772-166">Dit betekent dat mobiele apparaten zijn ingeschreven bij Intune en voldoen aan nalevingsvereisten van beleid en dat Windows-pc's lid zijn van een lokaal domein.</span><span class="sxs-lookup"><span data-stu-id="7f772-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="7f772-167">Een verbetering van de belangrijkste is dat er geen hetzelfde beleid instellen voor elk van de Office 365-services.</span><span class="sxs-lookup"><span data-stu-id="7f772-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="7f772-168">Wanneer u een nieuw beleid maakt, moet u de Cloud-apps zodat elk van de O365-apps die u beveiligen wilt met met voorwaardelijke toegang configureren.</span><span class="sxs-lookup"><span data-stu-id="7f772-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f772-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f772-169">Next steps</span></span>

<span data-ttu-id="7f772-170">Als u weten hoe beleid voor voorwaardelijke toegang configureren wilt, Zie [aan de slag met voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7f772-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
