---
title: Veelgestelde vragen over Active Directory aaaAzure | Microsoft Docs
description: Azure Active Directory-Veelgestelde vragen antwoorden op vragen over hoe tooaccess Azure en Azure Active Directory, wachtwoordbeheer en toepassing toegang krijgen tot.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="c87bc-103">Veelgestelde vragen over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c87bc-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="c87bc-104">Azure Active Directory (Azure AD) is een uitgebreide IDaaS-oplossing (Identity as a Service) waarin alle aspecten van identiteit, toegangsbeheer en beveiliging zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c87bc-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="c87bc-105">Zie [Wat is Azure Active Directory?](active-directory-whatis.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c87bc-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="c87bc-106">Toegang tot Azure en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c87bc-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="c87bc-107">**V: Waarom krijg ik 'geen abonnementen gevonden' wanneer ik probeer tooaccess Azure AD in Hallo klassieke Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-107">**Q: Why do I get “No subscriptions found” when I try tooaccess Azure AD in hello Azure classic portal?**</span></span>

<span data-ttu-id="c87bc-108">**A:** tooaccess Hallo klassieke Azure-portal, moet elke gebruiker machtigingen met een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c87bc-108">**A:** tooaccess hello Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="c87bc-109">Als u een betaald Office 365 of Azure AD-abonnement hebt, gaat u verder te[http://aka.ms/accessAAD](http://aka.ms/accessAAD) voor een eenmalige activeringsstap.</span><span class="sxs-lookup"><span data-stu-id="c87bc-109">If you have a paid Office 365 or Azure AD subscription, go too[http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="c87bc-110">Anders moet u een gratis tooactivate [Azure-account](https://azure.microsoft.com/pricing/free-trial/) of een betaald abonnement.</span><span class="sxs-lookup"><span data-stu-id="c87bc-110">Otherwise, you will need tooactivate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="c87bc-111">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="c87bc-111">For more information, see:</span></span>

* [<span data-ttu-id="c87bc-112">Hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c87bc-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="c87bc-113">Hallo-directory voor uw Office 365-abonnement in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="c87bc-113">Manage hello directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="c87bc-114">**V: Wat is de relatie Hallo tussen Azure AD, Office 365 en Azure?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-114">**Q: What’s hello relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="c87bc-115">**A:** Azure AD biedt u algemene identiteit en toegang tot tooall webservices.</span><span class="sxs-lookup"><span data-stu-id="c87bc-115">**A:** Azure AD provides you with common identity and access capabilities tooall web services.</span></span> <span data-ttu-id="c87bc-116">Ongeacht of u Office 365, Microsoft Azure, Intune, of anderen, u bent al gebruikmaakt van Azure AD toohelp schakelt u eenmalige aanmelding en toegang tot beheer van al deze services.</span><span class="sxs-lookup"><span data-stu-id="c87bc-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD toohelp turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="c87bc-117">Alle gebruikers die zijn ingesteld met toouse web-services worden gedefinieerd als gebruikersaccounts in een of meer exemplaren van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c87bc-117">All users who are set up toouse web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="c87bc-118">U kunt deze accounts instellen voor gratis Azure AD-functies, zoals toegang tot cloudtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="c87bc-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="c87bc-119">Betaalde Azure AD-services zoals Enterprise Mobility + Security vormen een aanvulling op andere webservices, zoals Office 365 en Microsoft Azure, met uitgebreide oplossingen voor beheer en beveiliging die ook geschikt zijn voor grote organisaties.</span><span class="sxs-lookup"><span data-stu-id="c87bc-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="c87bc-120">**V: Waarom kan ik toohello Azure-portal aanmelden, maar niet Hallo klassieke Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-120">**Q:  Why can I sign in toohello Azure portal but not hello Azure classic portal?**</span></span>

<span data-ttu-id="c87bc-121">**A:** hello Azure-portal geen vereist een geldig abonnement en de klassieke portal Hallo vereist een geldig abonnement.</span><span class="sxs-lookup"><span data-stu-id="c87bc-121">**A:**  hello Azure portal does not require a valid subscription, and hello classic portal does require a valid subscription.</span></span>  <span data-ttu-id="c87bc-122">Als u niet een abonnement hebt, kunt u de klassieke portal toohello kan niet aanmelden.</span><span class="sxs-lookup"><span data-stu-id="c87bc-122">If you do not have a subscription, you can't sign in toohello classic portal.</span></span>
- - -
<span data-ttu-id="c87bc-123">**V: wat zijn Hallo verschillen tussen Abonnementsbeheerder en Directory-beheerder?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-123">**Q:  What are hello differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="c87bc-124">**A:** standaard u Hallo abonnement beheerdersrol toegewezen wanneer u zich aanmeldt voor Azure.</span><span class="sxs-lookup"><span data-stu-id="c87bc-124">**A:** By default, you are assigned hello Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="c87bc-125">Een abonnementsbeheerder kunt gebruiken een Microsoft-account of een werk of schoolaccount van Hallo-map die hello Azure-abonnement is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="c87bc-125">A subscription admin can use either a Microsoft account or a work or school account from hello directory that hello Azure subscription is associated with.</span></span>  <span data-ttu-id="c87bc-126">Deze rol is geautoriseerde toomanage services in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c87bc-126">This role is authorized toomanage services in hello Azure portal.</span></span>

<span data-ttu-id="c87bc-127">Als anderen moeten toosign in en toegang tot services door met behulp van Hallo hetzelfde abonnement, kunt u deze toevoegen als medebeheerders.</span><span class="sxs-lookup"><span data-stu-id="c87bc-127">If others need toosign in and access services by using hello same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="c87bc-128">Deze rol Hallo heeft dezelfde toegangsrechten als de servicebeheerder hello, maar Hallo koppeling met abonnementen tooAzure mappen niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c87bc-128">This role has hello same access privileges as hello service admin, but can’t change hello association of subscriptions tooAzure directories.</span></span>  <span data-ttu-id="c87bc-129">Zie voor meer informatie over abonnementsbeheerders [hoe tooadd of wijzig Azure-beheerdersrollen](../billing-add-change-azure-subscription-administrator.md) en [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-129">For additional information on subscription admins, see [How tooadd or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="c87bc-130">Azure AD heeft een andere set admin rollen toomanage Hallo directory en identiteitsgerelateerde functies.</span><span class="sxs-lookup"><span data-stu-id="c87bc-130">Azure AD has a different set of admin roles toomanage hello directory and identity-related features.</span></span>  <span data-ttu-id="c87bc-131">Deze beheerders zijn toovarious toegangsfuncties in hello Azure-portal of Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c87bc-131">These admins will have access toovarious features in hello Azure portal or hello Azure classic portal.</span></span> <span data-ttu-id="c87bc-132">Hallo beheerdersrol bepaalt wat ze kunnen doen, zoals het maken of bewerken van gebruikers, tooothers beheerdersrollen toewijzen, gebruikerswachtwoorden, Gebruikerslicenties beheren of domeinen beheren.</span><span class="sxs-lookup"><span data-stu-id="c87bc-132">hello admin's role determines what they can do, like create or edit users, assign administrative roles tooothers, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="c87bc-133">Zie [Beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md) voor meer informatie over Directorybeheerders en hun rollen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c87bc-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="c87bc-134">Daarnaast vormen betaalde Azure AD-services zoals Enterprise Mobility + Security een aanvulling op andere webservices, zoals Office 365 en Microsoft Azure, met uitgebreide oplossingen voor beheer en beveiliging die ook geschikt zijn voor grote organisaties.</span><span class="sxs-lookup"><span data-stu-id="c87bc-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="c87bc-135">**V: Is er een rapport waarin staat wanneer mijn Azure AD-gebruikerslicenties verlopen?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="c87bc-136">**A:** Nee.</span><span class="sxs-lookup"><span data-stu-id="c87bc-136">**A:** No.</span></span>  <span data-ttu-id="c87bc-137">Dit is momenteel niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c87bc-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="c87bc-138">Aan de slag met hybride Azure AD</span><span class="sxs-lookup"><span data-stu-id="c87bc-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="c87bc-139">**V: Hoe verlaat ik een tenant wanneer ik ben toegevoegd als samenwerker?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="c87bc-140">**A:** wanneer u tenant van de organisatie van de tooanother worden toegevoegd als een samenwerker, kunt u Hallo 'tenant schakelbaar' in de bovenste rechts tooswitch Hallo tussen de tenants.</span><span class="sxs-lookup"><span data-stu-id="c87bc-140">**A:** When you are added tooanother organization's tenant as a collaborator, you can use hello "tenant switcher" in hello upper right tooswitch between tenants.</span></span>  <span data-ttu-id="c87bc-141">Op dit moment is er geen manier tooleave Hallo organisatie uitnodigen en Microsoft werkt op het bieden van deze functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="c87bc-141">Currently, there is no way tooleave hello inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="c87bc-142">Totdat deze functie beschikbaar is, vraagt u Hallo organisatie tooremove nodigen u uit de tenant.</span><span class="sxs-lookup"><span data-stu-id="c87bc-142">Until this feature is available, you can ask hello inviting organization tooremove you from their tenant.</span></span>
- - -
<span data-ttu-id="c87bc-143">**V: hoe kan ik mijn lokale directory tooAzure AD verbinden?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-143">**Q: How can I connect my on-premises directory tooAzure AD?**</span></span>

<span data-ttu-id="c87bc-144">**A:** uw lokale directory tooAzure AD verbinding kunnen maken met behulp van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c87bc-144">**A:** You can connect your on-premises directory tooAzure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="c87bc-145">Zie [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Uw on-premises identiteiten integreren met Azure Active Directory) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c87bc-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="c87bc-146">**V: Hoe stel ik eenmalige aanmelding in tussen mijn on-premises directory en mijn cloudtoepassingen?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="c87bc-147">**A:** hoeft u alleen tooset van eenmalige aanmelding (SSO) tussen uw on-premises adreslijst en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c87bc-147">**A:** You only need tooset up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="c87bc-148">Als u uw cloudtoepassingen via Azure AD opent, Hallo service automatisch voor gezorgd dat uw gebruikers toocorrectly verifiëren met hun on-premises referenties.</span><span class="sxs-lookup"><span data-stu-id="c87bc-148">As long as you access your cloud applications through Azure AD, hello service automatically drives your users toocorrectly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="c87bc-149">U kunt eenmalige aanmelding eenvoudig on-premises implementeren met federatieoplossingen, zoals Active Directory Federation Services (AD FS), of door wachtwoordhashsynchronisatie te configureren. U kunt beide opties eenvoudig implementeren met behulp van de wizard hello Azure AD Connect-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c87bc-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using hello Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="c87bc-150">Zie [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Uw on-premises identiteiten integreren met Azure Active Directory) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c87bc-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="c87bc-151">**V: Bevat Azure AD een selfserviceportal voor gebruikers in mijn organisatie?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="c87bc-152">**A:** Ja, Azure AD levert u Hello [Azure AD-Toegangsvenster](http://myapps.microsoft.com) voor selfservice van gebruiker en toegang tot toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c87bc-152">**A:** Yes, Azure AD provides you with hello [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="c87bc-153">Als u een Office 365-klant bent, kunt u veel van Hallo dezelfde mogelijkheden vinden in Hallo Office 365-portal.</span><span class="sxs-lookup"><span data-stu-id="c87bc-153">If you are an Office 365 customer, you can find many of hello same capabilities in hello Office 365 portal.</span></span>

<span data-ttu-id="c87bc-154">Zie voor meer informatie [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-154">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="c87bc-155">**V: Helpt Azure AD mij bij het beheren van mijn on-premises infrastructuur?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="c87bc-156">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="c87bc-156">**A:** Yes.</span></span> <span data-ttu-id="c87bc-157">Hello Azure AD Premium-editie biedt u Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="c87bc-157">hello Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="c87bc-158">Azure AD Connect Health kunt u controleren en meer inzicht krijgen in uw on-premises identiteits-infrastructuur en Hallo Synchronisatieservices.</span><span class="sxs-lookup"><span data-stu-id="c87bc-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and hello synchronization services.</span></span>  

<span data-ttu-id="c87bc-159">Zie voor meer informatie [uw lokale identiteit infrastructuur en de synchronisatie-services bewaken in de cloud Hallo](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in hello cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="c87bc-160">Wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="c87bc-160">Password management</span></span>
<span data-ttu-id="c87bc-161">**V: Kan ik Terugschrijven van wachtwoord van Azure AD gebruiken zonder wachtwoordsynchronisatie? (In dit scenario is het mogelijk toouse Azure AD selfservice voor wachtwoordherstel (SSPR) met wachtwoord terugschrijven en niet store wachtwoorden in de cloud Hallo?)**</span><span class="sxs-lookup"><span data-stu-id="c87bc-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible toouse Azure AD self-service password reset (SSPR) with password write-back and not store passwords in hello cloud?)**</span></span>

<span data-ttu-id="c87bc-162">**A:** hoeft u geen toosynchronize uw Active Directory-wachtwoorden tooAzure AD tooenable terugschrijven.</span><span class="sxs-lookup"><span data-stu-id="c87bc-162">**A:** You do not need toosynchronize your Active Directory passwords tooAzure AD tooenable write-back.</span></span> <span data-ttu-id="c87bc-163">In een federatieve omgeving Azure AD eenmalige aanmelding (SSO) is afhankelijk van Hallo on-premises directory tooauthenticate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c87bc-163">In a federated environment, Azure AD single sign-on (SSO) relies on hello on-premises directory tooauthenticate hello user.</span></span> <span data-ttu-id="c87bc-164">Dit scenario vereist geen Hallo lokale wachtwoord toobe bijgehouden in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c87bc-164">This scenario does not require hello on-premises password toobe tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="c87bc-165">**V: hoe lang duurt het voor een wachtwoord toobe tooActive Directory lokaal teruggeschreven?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-165">**Q: How long does it take for a password toobe written back tooActive Directory on-premises?**</span></span>

<span data-ttu-id="c87bc-166">**A:** Het terugschrijven van het wachtwoord wordt in realtime uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c87bc-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="c87bc-167">Zie voor meer informatie [Getting started with password management](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="c87bc-168">**V: Kan ik de functie Terugschrijven van wachtwoord gebruiken met wachtwoorden die worden beheerd door een beheerder?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="c87bc-169">**A:** Ja, als u wachtwoord terugschrijven ingeschakeld hebt, Hallo wachtwoordbewerkingen van een beheerder teruggeschreven tooyour on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="c87bc-169">**A:** Yes, if you have password write-back enabled, hello password operations performed by an admin are written back tooyour on-premises environment.</span></span>  

<span data-ttu-id="c87bc-170">Zie voor meer antwoorden toopassword-gerelateerde vragen [Veelgestelde vragen over wachtwoordbeheer](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-170">For more answers toopassword-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="c87bc-171">**V: wat moet ik doen als ik mijn bestaande Office 365/Azure AD-wachtwoord tijdens een poging toochange mijn wachtwoord vergeten?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying toochange my password?**</span></span>

<span data-ttu-id="c87bc-172">**A:** In een dergelijke situatie zijn er meerdere oplossingen.</span><span class="sxs-lookup"><span data-stu-id="c87bc-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="c87bc-173">Gebruik selfservice voor wachtwoordherstel (SSPR) als deze optie beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="c87bc-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="c87bc-174">Of SSPR werkt, is afhankelijk van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="c87bc-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="c87bc-175">Zie voor meer informatie [hoe Hallo wachtwoordherstel portal werk](active-directory-passwords-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-175">For more information, see [How does hello password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="c87bc-176">Voor Office 365-gebruikers, uw beheerder kan wachtwoord opnieuw instellen Hallo met behulp van Hallo stappen die worden beschreven in [gebruikerswachtwoorden](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="c87bc-176">For Office 365 users, your admin can reset hello password by using hello steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="c87bc-177">Voor Azure AD-accounts, kunnen beheerders opnieuw instellen van wachtwoorden met behulp van een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c87bc-177">For Azure AD accounts, admins can reset passwords by using one of hello following:</span></span>

- [<span data-ttu-id="c87bc-178">Opnieuw instellen van accounts in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c87bc-178">Reset accounts in hello Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="c87bc-179">Opnieuw instellen van accounts in de klassieke portal Hallo</span><span class="sxs-lookup"><span data-stu-id="c87bc-179">Reset accounts in hello classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="c87bc-180">PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="c87bc-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="c87bc-181">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="c87bc-181">Security</span></span>
<span data-ttu-id="c87bc-182">**V: Worden accounts na een bepaald aantal mislukte pogingen vergrendeld of wordt een meer geavanceerde strategie gebruikt?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="c87bc-183">We gebruiken een meer geavanceerde strategie toolock accounts.</span><span class="sxs-lookup"><span data-stu-id="c87bc-183">We use a more sophisticated strategy toolock accounts.</span></span>  <span data-ttu-id="c87bc-184">Dit is gebaseerd op Hallo IP-adres van Hallo-aanvraag en Hallo-wachtwoorden hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="c87bc-184">This is based on hello IP of hello request and hello passwords entered.</span></span> <span data-ttu-id="c87bc-185">Hallo-duur van Hallo accountvergrendeling verhoogt ook op basis van Hallo kans dat het is een aanval.</span><span class="sxs-lookup"><span data-stu-id="c87bc-185">hello duration of hello lockout also increases based on hello likelihood that it is an attack.</span></span>  

<span data-ttu-id="c87bc-186">**V: bepaalde (algemene) wachtwoorden afgewezen Hello berichten 'dit wachtwoord is gebruikt toomany maal', verwijst dit toopasswords gebruikt in de huidige active directory Hallo?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-186">**Q:  Certain (common) passwords get rejected with hello messages ‘this password has been used toomany times’, does this refer toopasswords used in hello current active directory?**</span></span></br>
<span data-ttu-id="c87bc-187">Dit verwijst toopasswords die globaal gemeen hebben, zoals varianten van 'Password' en '123456'.</span><span class="sxs-lookup"><span data-stu-id="c87bc-187">This refers toopasswords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="c87bc-188">**V: Worden aanmeldingsaanvragen van twijfelachtige bronnen (botnets, tor-eindpunten) in een B2C-tenant geblokkeerd of is hiervoor een Basic- of Premium-tenant vereist?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="c87bc-189">We hebben wel een gateway waarmee aanvragen worden gefilterd en die enige bescherming biedt tegen botnets. Deze wordt toegepast op alle B2C-tenants.</span><span class="sxs-lookup"><span data-stu-id="c87bc-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="c87bc-190">Toegang tot toepassingen</span><span class="sxs-lookup"><span data-stu-id="c87bc-190">Application access</span></span>
<span data-ttu-id="c87bc-191">**V: Waar vind ik een lijst met toepassingen die vooraf zijn geïntegreerd met Azure AD en de bijbehorende mogelijkheden?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="c87bc-192">**A:** Azure AD bevat meer dan 2.600 vooraf geïntegreerde toepassingen van Microsoft, toepassingsserviceproviders en partners.</span><span class="sxs-lookup"><span data-stu-id="c87bc-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="c87bc-193">Alle vooraf geïntegreerde toepassingen bieden ondersteuning voor eenmalige aanmelding (SSO).</span><span class="sxs-lookup"><span data-stu-id="c87bc-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="c87bc-194">Eenmalige aanmelding kunt u uw apps voor uw organisatie referenties tooaccess gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c87bc-194">SSO lets you use your organizational credentials tooaccess your apps.</span></span> <span data-ttu-id="c87bc-195">Sommige Hallo toepassingen ondersteunen ook geautomatiseerde inrichting en de inrichting ongedaan.</span><span class="sxs-lookup"><span data-stu-id="c87bc-195">Some of hello applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="c87bc-196">Zie voor een volledige lijst met vooraf geïntegreerde toepassingen Hallo Hallo [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="c87bc-196">For a complete list of hello pre-integrated applications, see hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="c87bc-197">**V: Wat gebeurt er als hello App die ik nodig heeft geen hello Azure AD marketplace?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-197">**Q: What if hello application I need is not in hello Azure AD marketplace?**</span></span>

<span data-ttu-id="c87bc-198">**A:** Met Azure AD Premium kunt u elke gewenste toepassing toevoegen en configureren.</span><span class="sxs-lookup"><span data-stu-id="c87bc-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="c87bc-199">U kunt eenmalige aanmelding en geautomatiseerde inrichting configureren, afhankelijk van de mogelijkheden van uw toepassing en uw voorkeuren.</span><span class="sxs-lookup"><span data-stu-id="c87bc-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="c87bc-200">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="c87bc-200">For more information, see:</span></span>

* [<span data-ttu-id="c87bc-201">Eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="c87bc-201">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="c87bc-202">Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications</span><span class="sxs-lookup"><span data-stu-id="c87bc-202">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="c87bc-203">**V: hoe gebruikers Meld tooapplications met Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-203">**Q: How do users sign in tooapplications by using Azure AD?**</span></span>

<span data-ttu-id="c87bc-204">**A:** Azure AD biedt verschillende manieren voor gebruikers tooview en toegang krijgen tot hun toepassingen, zoals:</span><span class="sxs-lookup"><span data-stu-id="c87bc-204">**A:** Azure AD provides several ways for users tooview and access their applications, such as:</span></span>

* <span data-ttu-id="c87bc-205">Hello Azure AD-Toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="c87bc-205">hello Azure AD access panel</span></span>
* <span data-ttu-id="c87bc-206">toepassingsstartprogramma Hello Office 365</span><span class="sxs-lookup"><span data-stu-id="c87bc-206">hello Office 365 application launcher</span></span>
* <span data-ttu-id="c87bc-207">Direct aanmelden toofederated apps</span><span class="sxs-lookup"><span data-stu-id="c87bc-207">Direct sign-in toofederated apps</span></span>
* <span data-ttu-id="c87bc-208">Dieptekoppelingen toofederated, op basis van wachtwoorden of bestaande apps</span><span class="sxs-lookup"><span data-stu-id="c87bc-208">Deep links toofederated, password-based, or existing apps</span></span>

<span data-ttu-id="c87bc-209">Zie voor meer informatie [Deploying Azure AD integrated applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="c87bc-209">For more information, see [Deploying Azure AD integrated applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="c87bc-210">**V: wat zijn Hallo verschillende manieren waarop Azure AD kunnen u de verificatie en eenmalige aanmelding tooapplications?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-210">**Q: What are hello different ways Azure AD enables authentication and single sign-on tooapplications?**</span></span>

<span data-ttu-id="c87bc-211">**A:** Azure AD biedt ondersteuning voor een groot aantal gestandaardiseerde protocollen voor verificatie en autorisatie, zoals SAML 2.0, OpenID Connect, OAuth 2.0 en WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c87bc-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="c87bc-212">Daarnaast ondersteunt Azure AD het gebruik van wachtwoordkluizen en mogelijkheden voor automatische aanmelding voor apps die alleen ondersteuning bieden voor verificatie op basis van formulieren.</span><span class="sxs-lookup"><span data-stu-id="c87bc-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="c87bc-213">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="c87bc-213">For more information, see:</span></span>

* <span data-ttu-id="c87bc-214">[Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md) (Verificatiescenario's voor Azure AD)</span><span class="sxs-lookup"><span data-stu-id="c87bc-214">[Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md)</span></span>
* [<span data-ttu-id="c87bc-215">Verificatie- en autorisatieprotocollen</span><span class="sxs-lookup"><span data-stu-id="c87bc-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* <span data-ttu-id="c87bc-216">[How does single sign-on with Azure Active Directory work?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work) (Hoe werkt eenmalige aanmelding met Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="c87bc-216">[How does single sign-on with Azure Active Directory work?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span></span>

- - -
<span data-ttu-id="c87bc-217">**V: Kan ik toepassingen toevoegen die ik on-premises uitvoer?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="c87bc-218">**A:** Azure AD-toepassingsproxy biedt eenvoudig en veilig toegang tooon-premises webtoepassingen die u kiest.</span><span class="sxs-lookup"><span data-stu-id="c87bc-218">**A:** Azure AD Application Proxy provides you with easy and secure access tooon-premises web applications that you choose.</span></span> <span data-ttu-id="c87bc-219">U kunt toegang tot deze toepassingen in Hallo dezelfde manier als u toegang hebt tot de software als een service (SaaS)-apps in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c87bc-219">You can access these applications in hello same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="c87bc-220">Er is niet nodig voor een VPN- of toochange uw netwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="c87bc-220">There is no need for a VPN or toochange your network infrastructure.</span></span>  

<span data-ttu-id="c87bc-221">Zie voor meer informatie [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-221">For more information, see [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="c87bc-222">**V: Hoe maak ik Multi-Factor Authentication verplicht voor gebruikers die toegang hebben tot een bepaalde toepassing?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="c87bc-223">**A:** Met voorwaardelijke toegang van Azure AD kunt u een uniek toegangsbeleid toewijzen aan elke toepassing.</span><span class="sxs-lookup"><span data-stu-id="c87bc-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="c87bc-224">U kunt altijd meervoudige verificatie vereisen of wanneer gebruikers niet zijn verbonden toohello lokale netwerk in uw beleid.</span><span class="sxs-lookup"><span data-stu-id="c87bc-224">In your policy, you can require multi-factor authentication always, or when users are not connected toohello local network.</span></span>  

<span data-ttu-id="c87bc-225">Zie voor meer informatie [toegang beveiligen tooOffice 365 en andere apps tooAzure Active Directory verbonden](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-225">For more information, see [Securing access tooOffice 365 and other apps connected tooAzure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="c87bc-226">**V: Wat is geautomatiseerde gebruikersinrichting voor SaaS-apps?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="c87bc-227">**A:** tooautomate Hallo maken, onderhoud en verwijderen van de gebruikers-id's in veel populaire cloudtoepassingen SaaS-apps met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c87bc-227">**A:** Use Azure AD tooautomate hello creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="c87bc-228">Zie voor meer informatie [gebruikers inrichten en opheffen van inrichting tooSaaS toepassingen met Azure Active Directory automatiseren](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="c87bc-228">For more information, see [Automate user provisioning and deprovisioning tooSaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="c87bc-229">**V: Kan ik een veilige LDAP-verbinding instellen met Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="c87bc-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="c87bc-230">**A:** Nee.</span><span class="sxs-lookup"><span data-stu-id="c87bc-230">**A:**  No.</span></span> <span data-ttu-id="c87bc-231">Azure AD biedt geen ondersteuning voor Hallo LDAP-protocol.</span><span class="sxs-lookup"><span data-stu-id="c87bc-231">Azure AD does not support hello LDAP protocol.</span></span>
