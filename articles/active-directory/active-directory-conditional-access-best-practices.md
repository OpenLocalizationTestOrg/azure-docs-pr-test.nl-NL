---
title: aaaBest procedures voor voorwaardelijke toegang in Azure Active Directory | Microsoft Docs
description: Meer informatie over wat die u moet weten en wat het is raadzaam doen bij het configureren van beleidsregels voor voorwaardelijke toegang.
services: active-directory
keywords: voorwaardelijke toegang tooapps, voorwaardelijke toegang in Azure AD, beveiligde toegang tot resources toocompany, beleidsregels voor voorwaardelijke toegang
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
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="6e116-104">Aanbevolen procedures voor voorwaardelijke toegang in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e116-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="6e116-105">In dit onderwerp vindt u informatie over wat die u moet weten en wat het is raadzaam doen bij het configureren van beleidsregels voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="6e116-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="6e116-106">Voordat u dit onderwerp leest, moet u vertrouwd raken met Hallo concepten en terminologie Hallo die worden beschreven in [voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6e116-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="6e116-107">Wat u moet weten</span><span class="sxs-lookup"><span data-stu-id="6e116-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="6e116-108">Wat is een beleid werk toomake vereist?</span><span class="sxs-lookup"><span data-stu-id="6e116-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="6e116-109">Wanneer u een nieuw beleid maakt, zijn er geen gebruikers, groepen, apps of toegangsbeheer geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6e116-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Cloud-apps](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="6e116-111">toomake uw beleid werken, moet u de volgende Hallo configureren:</span><span class="sxs-lookup"><span data-stu-id="6e116-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="6e116-112">Wat</span><span class="sxs-lookup"><span data-stu-id="6e116-112">What</span></span>           | <span data-ttu-id="6e116-113">Hoe</span><span class="sxs-lookup"><span data-stu-id="6e116-113">How</span></span>                                  | <span data-ttu-id="6e116-114">Waarom</span><span class="sxs-lookup"><span data-stu-id="6e116-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="6e116-115">**Cloud-apps**</span><span class="sxs-lookup"><span data-stu-id="6e116-115">**Cloud apps**</span></span> |<span data-ttu-id="6e116-116">U moet een of meer apps tooselect.</span><span class="sxs-lookup"><span data-stu-id="6e116-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="6e116-117">Hallo-doel van een beleid voor voorwaardelijke toegang is tooenable toofine-afstemmen hoe gemachtigde gebruikers toegang uw apps tot hebben.</span><span class="sxs-lookup"><span data-stu-id="6e116-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="6e116-118">**Gebruikers en groepen**</span><span class="sxs-lookup"><span data-stu-id="6e116-118">**Users and groups**</span></span> | <span data-ttu-id="6e116-119">U moet tooselect ten minste één gebruiker of groep die is gemachtigd tooaccess Hallo cloud-apps die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6e116-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="6e116-120">Beleid voor voorwaardelijke toegang dat er geen gebruikers en groepen die zijn toegewezen, wordt nooit geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="6e116-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="6e116-121">**Toegangsbeheer**</span><span class="sxs-lookup"><span data-stu-id="6e116-121">**Access controls**</span></span> | <span data-ttu-id="6e116-122">U moet tooselect ten minste één toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="6e116-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="6e116-123">De processor van uw beleid moet tooknow welke toodo indien uw voorwaarden is voldaan.</span><span class="sxs-lookup"><span data-stu-id="6e116-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="6e116-124">In aanvulling toothese basisvereisten, in veel gevallen moet u ook een voorwaarde configureren.</span><span class="sxs-lookup"><span data-stu-id="6e116-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="6e116-125">Een beleid zou ook werken zonder een geconfigureerde voorwaarde, zijn voorwaarden Hallo aangedreven factor voor toegang tot tooyour apps aan te passen.</span><span class="sxs-lookup"><span data-stu-id="6e116-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![Cloud-apps](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="6e116-127">Hoe worden toewijzingen geëvalueerd</span><span class="sxs-lookup"><span data-stu-id="6e116-127">How are assignments evaluated?</span></span>

<span data-ttu-id="6e116-128">Alle toewijzingen zijn logische **and**.</span><span class="sxs-lookup"><span data-stu-id="6e116-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="6e116-129">Als u geconfigureerd, meer dan één toewijzing tootrigger een beleid hebt, moeten alle toewijzingen worden voldaan.</span><span class="sxs-lookup"><span data-stu-id="6e116-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="6e116-130">Als u tooconfigure een locatie-voorwaarde die van toepassing tooall verbindingen moet is vanaf buiten het netwerk van uw organisatie, kunt u dit doen door:</span><span class="sxs-lookup"><span data-stu-id="6e116-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="6e116-131">Inclusief **alle locaties**</span><span class="sxs-lookup"><span data-stu-id="6e116-131">Including **All locations**</span></span>
- <span data-ttu-id="6e116-132">Met uitzondering van **alle goedgekeurde IP-adressen**</span><span class="sxs-lookup"><span data-stu-id="6e116-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="6e116-133">Wat gebeurt er als er beleid in Hallo klassieke Azure-portal en Azure-portal geconfigureerd?</span><span class="sxs-lookup"><span data-stu-id="6e116-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="6e116-134">Beide beleidsregels worden afgedwongen door Azure Active Directory en Hallo gebruiker krijgt toegang alleen wanneer alle vereisten wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="6e116-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="6e116-135">Wat gebeurt er als u een beleid in Intune Silverlight portal Hallo en hello Azure Portal hebt?</span><span class="sxs-lookup"><span data-stu-id="6e116-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="6e116-136">Beide beleidsregels worden afgedwongen door Azure Active Directory en Hallo gebruiker krijgt toegang alleen wanneer alle vereisten wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="6e116-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="6e116-137">Wat gebeurt er als ik heb meerdere beleidsregels voor dezelfde gebruiker geconfigureerd Hallo?</span><span class="sxs-lookup"><span data-stu-id="6e116-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="6e116-138">Voor elke aanmelding, Azure Active Directory evalueert alle beleidsregels en zorgt ervoor dat alle vereisten wordt voldaan voordat verleende toegang toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6e116-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="6e116-139">Werkt voorwaardelijke toegang met Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="6e116-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="6e116-140">Ja, kunt u Exchange ActiveSync in een beleid voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="6e116-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="6e116-141">Wat moet u niet doen</span><span class="sxs-lookup"><span data-stu-id="6e116-141">What you should avoid doing</span></span>

<span data-ttu-id="6e116-142">Hallo voorwaardelijke toegang framework biedt u de flexibiliteit van een geweldige configuratie.</span><span class="sxs-lookup"><span data-stu-id="6e116-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="6e116-143">Echter hoge mate van flexibiliteit betekent ook dat u zorgvuldig elke configuratie beleid voorafgaande tooreleasing het tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="6e116-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="6e116-144">In deze context moet u speciale aandacht schenken tooassignments zoals die invloed hebben op volledige set betalen **alle gebruikers / groepen / cloud-apps**.</span><span class="sxs-lookup"><span data-stu-id="6e116-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="6e116-145">In uw omgeving, moet u voorkomen Hallo volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="6e116-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="6e116-146">**Voor alle gebruikers alle cloud-apps:**</span><span class="sxs-lookup"><span data-stu-id="6e116-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="6e116-147">**Toegang blokkeren** -uw hele organisatie, absoluut niet verstandig is deze configuratie wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="6e116-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="6e116-148">**Vereisen dat apparaat compatibel** - voor gebruikers die niet hun apparaten hebben ingeschreven, maar dit beleid wordt alle toegang inclusief toohello Intune-portal toegang geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="6e116-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="6e116-149">Als u een beheerder met een geregistreerd apparaat, wordt dit beleid u uit om terug te zetten naar hello Azure portal toochange Hallo beleid blokkeert.</span><span class="sxs-lookup"><span data-stu-id="6e116-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="6e116-150">**Domeinlidmaatschap vereisen** : dit beleid blok toegang heeft ook Hallo potentiële tooblock toegang voor alle gebruikers in uw organisatie als u een apparaat domein nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="6e116-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="6e116-151">**Voor alle gebruikers, alle cloud-apps, alle platforms:**</span><span class="sxs-lookup"><span data-stu-id="6e116-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="6e116-152">**Toegang blokkeren** -uw hele organisatie, absoluut niet verstandig is deze configuratie wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="6e116-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="6e116-153">Algemene scenario's</span><span class="sxs-lookup"><span data-stu-id="6e116-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="6e116-154">Meervoudige verificatie vereisen voor apps</span><span class="sxs-lookup"><span data-stu-id="6e116-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="6e116-155">Veel omgevingen hebben apps waarvoor een hoger niveau van beveiliging dan Hallo anderen.</span><span class="sxs-lookup"><span data-stu-id="6e116-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="6e116-156">Dit is bijvoorbeeld Hallo geval voor apps die u toegang tot toosensitive gegevens hebt.</span><span class="sxs-lookup"><span data-stu-id="6e116-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="6e116-157">Als u op een andere laag van beveiliging toothese apps tooadd wilt, kunt u een beleid voor voorwaardelijke toegang waarvoor multi-factor authentication-server is vereist wanneer gebruikers toegang hebben tot deze apps kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="6e116-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="6e116-158">Meervoudige verificatie vereisen voor toegang via netwerken die geen vertrouwde</span><span class="sxs-lookup"><span data-stu-id="6e116-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="6e116-159">Dit scenario is vergelijkbaar toohello vorige scenario, omdat een vereiste voor multi-factor authentication wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6e116-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="6e116-160">Hallo belangrijkste verschil is echter Hallo voorwaarde voor deze vereiste.</span><span class="sxs-lookup"><span data-stu-id="6e116-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="6e116-161">Tijdens het Hallo focus van het vorige scenario Hallo werd op apps met toegang tot toosensitve gegevens, wordt dit scenario Hallo richt zich op vertrouwde locaties.</span><span class="sxs-lookup"><span data-stu-id="6e116-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="6e116-162">U wellicht een vereiste voor multi-factor authentication met andere woorden, als een app wordt geopend door een gebruiker vanaf een netwerk dat u niet vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="6e116-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="6e116-163">Alleen vertrouwde apparaten hebben toegang tot Office 365-services</span><span class="sxs-lookup"><span data-stu-id="6e116-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="6e116-164">Als u van Intune in uw omgeving gebruikmaakt, kunt u onmiddellijk starten met Hallo voorwaardelijk beleid interface in hello Azure-console.</span><span class="sxs-lookup"><span data-stu-id="6e116-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="6e116-165">Veel klanten van Intune voorwaardelijke toegang tooensure of alleen vertrouwde apparaten toegang Office 365-services tot gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6e116-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="6e116-166">Dit betekent dat mobiele apparaten zijn ingeschreven bij Intune en voldoen aan nalevingsvereisten van beleid en de Windows-pc's die zijn gekoppeld tooan lokaal domein.</span><span class="sxs-lookup"><span data-stu-id="6e116-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="6e116-167">Een verbetering van de belangrijkste is dat u geen hebt tooset Hallo hetzelfde beleid voor elk Hallo Office 365-services.</span><span class="sxs-lookup"><span data-stu-id="6e116-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="6e116-168">Wanneer u een nieuw beleid maakt, configureert u Hallo Cloud-apps tooinclude elke Hallo O365-Apps die u wenst dat tooprotect met met voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="6e116-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e116-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e116-169">Next steps</span></span>

<span data-ttu-id="6e116-170">Als u wilt dat tooknow hoe tooconfigure beleid voor voorwaardelijke toegang, Zie [aan de slag met voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e116-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
