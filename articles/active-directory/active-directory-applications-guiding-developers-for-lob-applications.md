---
title: apps voor Azure AD aaaDevelop | Microsoft-Docs
description: In dit artikel bevat voor IT-professionals Hallo geschreven, richtlijnen voor het Azure-toepassingen integreren met Active Directory.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="968fa-103">Line-of-business-apps ontwikkelen voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="968fa-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="968fa-104">Deze handleiding biedt een overzicht van de line-of-business (LoB) toepassingen ontwikkelt voor Azure Active Directory (AD) .hello bedoeld doelgroep is globale beheerders Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="968fa-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="968fa-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="968fa-105">Overview</span></span>
<span data-ttu-id="968fa-106">Maken van toepassingen die zijn geïntegreerd met Azure AD geeft gebruikers in uw organisatie eenmalige aanmelding met Office 365.</span><span class="sxs-lookup"><span data-stu-id="968fa-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="968fa-107">Hallo-toepassing hebben in Azure AD-hebt die u meer controle over Hallo verificatiebeleid voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="968fa-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="968fa-108">meer informatie over voorwaardelijke toegang en hoe tooprotect apps met multi-factor authentication (MFA) zien toolearn [toegangsregels configureren](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="968fa-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="968fa-109">Uw toepassing toouse Azure Active Directory registreren.</span><span class="sxs-lookup"><span data-stu-id="968fa-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="968fa-110">Registreren van de toepassing hello betekent dat de ontwikkelaars kunnen gebruikers van Azure AD-tooauthenticate gebruiken en toegang toouser resources zoals e-mail, agenda en documenten aanvragen.</span><span class="sxs-lookup"><span data-stu-id="968fa-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="968fa-111">Elk lid van uw directory (niet gasten) kunt u registreert een toepassing, ook bekend als *maken van een toepassingsobject*.</span><span class="sxs-lookup"><span data-stu-id="968fa-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="968fa-112">Registreren van een toepassing, kunt een gebruiker toodo Hallo aanleiding:</span><span class="sxs-lookup"><span data-stu-id="968fa-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="968fa-113">Een identiteit voor de toepassing die Azure AD herkent ophalen</span><span class="sxs-lookup"><span data-stu-id="968fa-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="968fa-114">Een of meer geheimen/sleutels die toepassing hello tooauthenticate zelf kunt gebruiken tooAD</span><span class="sxs-lookup"><span data-stu-id="968fa-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="968fa-115">Merk Hallo toepassing in hello Azure-portal met een aangepaste naam, het logo, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="968fa-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="968fa-116">Toepassen van Azure AD autorisatie functies tootheir-app, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="968fa-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="968fa-117">RBAC (op rollen gebaseerd toegangsbeheer)</span><span class="sxs-lookup"><span data-stu-id="968fa-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="968fa-118">Azure Active Directory als oAuth-autorisatie-server (een API die worden weergegeven door de toepassing hello beveiligen)</span><span class="sxs-lookup"><span data-stu-id="968fa-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="968fa-119">Declareren vereiste machtigingen nodig zijn voor Hallo toepassing toofunction zoals verwacht, waaronder:</span><span class="sxs-lookup"><span data-stu-id="968fa-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="968fa-120">App-machtigingen (alleen globale beheerders).</span><span class="sxs-lookup"><span data-stu-id="968fa-120">App permissions (global administrators only).</span></span> <span data-ttu-id="968fa-121">Bijvoorbeeld: lidmaatschap van een andere Azure AD-toepassing of rol lidmaatschap relatieve tooan Azure Resource, resourcegroep, de rol- of -abonnement</span><span class="sxs-lookup"><span data-stu-id="968fa-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="968fa-122">Gedelegeerde machtigingen (een willekeurige gebruiker).</span><span class="sxs-lookup"><span data-stu-id="968fa-122">Delegated permissions (any user).</span></span> <span data-ttu-id="968fa-123">Bijvoorbeeld: Azure AD, aanmelden en profiel lezen</span><span class="sxs-lookup"><span data-stu-id="968fa-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="968fa-124">Standaard kan een lid registreert een toepassing.</span><span class="sxs-lookup"><span data-stu-id="968fa-124">By default, any member can register an application.</span></span> <span data-ttu-id="968fa-125">hoe toorestrict machtigingen voor het registreren van toepassingen toospecific leden, Zie toolearn [hoe toepassingen tooAzure AD zijn toegevoegd](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="968fa-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="968fa-126">Dit is wat u, de globale beheerder hello, moeten toodo toohelp ontwikkelaars ervoor dat de toepassing gereed voor productie:</span><span class="sxs-lookup"><span data-stu-id="968fa-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="968fa-127">Toegangsregels (toegang beleid/MFA) configureren</span><span class="sxs-lookup"><span data-stu-id="968fa-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="968fa-128">Hallo app toorequire Gebruikerstoewijzing configureren en toewijzen van gebruikers</span><span class="sxs-lookup"><span data-stu-id="968fa-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="968fa-129">Hallo standaard gebruikerservaring toestemming onderdrukken</span><span class="sxs-lookup"><span data-stu-id="968fa-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="968fa-130">Toegangsregels configureren</span><span class="sxs-lookup"><span data-stu-id="968fa-130">Configure access rules</span></span>
<span data-ttu-id="968fa-131">Configureer regels tooyour SaaS-apps toegang per toepassing.</span><span class="sxs-lookup"><span data-stu-id="968fa-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="968fa-132">U kunt bijvoorbeeld MFA vereisen of dat alleen toegang toousers in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="968fa-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="968fa-133">Hallo-details voor deze zijn beschikbaar in Hallo document [toegangsregels configureren](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="968fa-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="968fa-134">Hallo app toorequire Gebruikerstoewijzing configureren en toewijzen van gebruikers</span><span class="sxs-lookup"><span data-stu-id="968fa-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="968fa-135">Standaard kunnen gebruikers toepassingen openen zonder dat wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="968fa-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="968fa-136">Als de toepassing hello beschrijft de functies of als u Hallo toepassing tooappear op toegangspaneel voor een gebruiker wilt, moet u de Gebruikerstoewijzing van de instellen.</span><span class="sxs-lookup"><span data-stu-id="968fa-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="968fa-137">Gebruikerstoewijzing vereisen</span><span class="sxs-lookup"><span data-stu-id="968fa-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="968fa-138">Als u een Azure AD Premium of Enterprise Mobility Suite (EMS)-abonnee bent, wordt aangeraden met behulp van groepen.</span><span class="sxs-lookup"><span data-stu-id="968fa-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="968fa-139">Toewijzen van groepen toohello toepassing kunt u toodelegate lopende access management toohello eigenaar van Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="968fa-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="968fa-140">U kunt Hallo groep maken of vraag Hallo verantwoordelijke partij in uw organisatie toocreate Hallo groep met behulp van de groep management-functie.</span><span class="sxs-lookup"><span data-stu-id="968fa-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="968fa-141">Toewijzen van gebruikers tooan toepassing</span><span class="sxs-lookup"><span data-stu-id="968fa-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="968fa-142">Toewijzen van groepen tooan toepassing</span><span class="sxs-lookup"><span data-stu-id="968fa-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="968fa-143">Onderdrukken van toestemming van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="968fa-143">Suppress user consent</span></span>
<span data-ttu-id="968fa-144">Elke gebruiker doorloopt een toosign toestemming ervaring in standaard.</span><span class="sxs-lookup"><span data-stu-id="968fa-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="968fa-145">Hallo zijn toestemming, waarin gebruikers toogrant machtigingen tooan toepassing, toegevoegd voor gebruikers die niet bekend bent met dergelijke beslissingen.</span><span class="sxs-lookup"><span data-stu-id="968fa-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="968fa-146">Voor toepassingen die u vertrouwt, kunt u Hallo gebruikerservaring vereenvoudigen door ermee akkoord dat toohello toepassing namens uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="968fa-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="968fa-147">Voor meer informatie over de toestemming van de gebruiker en Hallo toestemming ervaring in Azure, Zie [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="968fa-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="968fa-148">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="968fa-148">Related Articles</span></span>
* [<span data-ttu-id="968fa-149">Veilige externe toegang tooon-premises toepassingen met Azure AD-toepassingsproxy inschakelen</span><span class="sxs-lookup"><span data-stu-id="968fa-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="968fa-150">Voorwaardelijke toegang tot Azure Preview voor SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="968fa-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="968fa-151">Het beheren van toegang tooapps met Azure AD</span><span class="sxs-lookup"><span data-stu-id="968fa-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* <span data-ttu-id="968fa-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="968fa-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
