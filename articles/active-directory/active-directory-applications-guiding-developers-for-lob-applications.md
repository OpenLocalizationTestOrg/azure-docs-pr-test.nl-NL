---
title: Apps ontwikkelen voor Azure AD | Microsoft-Docs
description: In dit artikel bevat voor IT-professionals wordt geschreven, richtlijnen voor het Azure-toepassingen integreren met Active Directory.
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
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="8c83b-103">Line-of-business-apps ontwikkelen voor Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c83b-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="8c83b-104">Deze handleiding biedt een overzicht van het ontwikkelen van line-of-business (LoB)-toepassingen voor Azure Active Directory (AD). De doelgroep is globale beheerders Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="8c83b-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="8c83b-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8c83b-105">Overview</span></span>
<span data-ttu-id="8c83b-106">Maken van toepassingen die zijn geïntegreerd met Azure AD geeft gebruikers in uw organisatie eenmalige aanmelding met Office 365.</span><span class="sxs-lookup"><span data-stu-id="8c83b-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="8c83b-107">De toepassing is in Azure AD-hebt die u meer controle over het verificatiebeleid voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c83b-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="8c83b-108">Voor meer informatie over voorwaardelijke toegang en het beveiligen van apps met multi-factor authentication (MFA) Zie [toegangsregels configureren](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="8c83b-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="8c83b-109">Uw toepassing te gebruiken van Azure Active Directory registreren.</span><span class="sxs-lookup"><span data-stu-id="8c83b-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="8c83b-110">Registreren van de toepassing, betekent dat ontwikkelaars van uw Azure AD gebruiken kunnen voor het verifiëren van gebruikers en toegang vragen tot Gebruikersresources zoals e-mail, agenda en documenten.</span><span class="sxs-lookup"><span data-stu-id="8c83b-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="8c83b-111">Elk lid van uw directory (niet gasten) kunt u registreert een toepassing, ook bekend als *maken van een toepassingsobject*.</span><span class="sxs-lookup"><span data-stu-id="8c83b-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="8c83b-112">Registreren van een toepassing kan elke gebruiker het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="8c83b-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="8c83b-113">Een identiteit voor de toepassing die Azure AD herkent ophalen</span><span class="sxs-lookup"><span data-stu-id="8c83b-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="8c83b-114">Een of meer geheimen/sleutels ophalen die de toepassing gebruiken kunt om zichzelf te verifiëren naar AD</span><span class="sxs-lookup"><span data-stu-id="8c83b-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="8c83b-115">Merk de toepassing in de Azure-portal met een aangepaste naam, het logo, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="8c83b-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="8c83b-116">Azure AD-functies voor autorisatie van toepassing op hun app, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="8c83b-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="8c83b-117">RBAC (op rollen gebaseerd toegangsbeheer)</span><span class="sxs-lookup"><span data-stu-id="8c83b-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="8c83b-118">Azure Active Directory als oAuth-autorisatie-server (een API die worden weergegeven door de toepassing beveiligen)</span><span class="sxs-lookup"><span data-stu-id="8c83b-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="8c83b-119">Declareren vereiste machtigingen voor de toepassing naar de functie nodig, zoals verwacht, waaronder:</span><span class="sxs-lookup"><span data-stu-id="8c83b-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="8c83b-120">App-machtigingen (alleen globale beheerders).</span><span class="sxs-lookup"><span data-stu-id="8c83b-120">App permissions (global administrators only).</span></span> <span data-ttu-id="8c83b-121">Bijvoorbeeld: lidmaatschap van de rol in een andere Azure AD-toepassing of functie lidmaatschap ten opzichte van een Azure Resource, resourcegroep, of -abonnement</span><span class="sxs-lookup"><span data-stu-id="8c83b-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="8c83b-122">Gedelegeerde machtigingen (een willekeurige gebruiker).</span><span class="sxs-lookup"><span data-stu-id="8c83b-122">Delegated permissions (any user).</span></span> <span data-ttu-id="8c83b-123">Bijvoorbeeld: Azure AD, aanmelden en profiel lezen</span><span class="sxs-lookup"><span data-stu-id="8c83b-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="8c83b-124">Standaard kan een lid registreert een toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c83b-124">By default, any member can register an application.</span></span> <span data-ttu-id="8c83b-125">Zie voor informatie over het beperken van machtigingen voor het registreren van toepassingen naar specifieke leden, [hoe toepassingen worden toegevoegd aan Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="8c83b-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="8c83b-126">Dit is wat u als globale beheerder moet doen om ervoor dat de toepassing gereed voor productie ontwikkelaars helpen bij het:</span><span class="sxs-lookup"><span data-stu-id="8c83b-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="8c83b-127">Toegangsregels (toegang beleid/MFA) configureren</span><span class="sxs-lookup"><span data-stu-id="8c83b-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="8c83b-128">De app configureren om te vereisen Gebruikerstoewijzing en gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="8c83b-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="8c83b-129">De standaard toestemming gebruikerservaring onderdrukken</span><span class="sxs-lookup"><span data-stu-id="8c83b-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="8c83b-130">Toegangsregels configureren</span><span class="sxs-lookup"><span data-stu-id="8c83b-130">Configure access rules</span></span>
<span data-ttu-id="8c83b-131">Configureer regels voor toegang per toepassing naar uw SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8c83b-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="8c83b-132">U kunt bijvoorbeeld MFA vereisen of dat alleen toegang tot gebruikers in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="8c83b-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="8c83b-133">De details voor deze zijn beschikbaar in het document [toegangsregels configureren](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="8c83b-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="8c83b-134">De app configureren om te vereisen Gebruikerstoewijzing en gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="8c83b-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="8c83b-135">Standaard kunnen gebruikers toepassingen openen zonder dat wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8c83b-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="8c83b-136">Als de toepassing ook functies of als u wilt dat de toepassing worden weergegeven op het toegangsvenster van een gebruiker, moet u de Gebruikerstoewijzing van de instellen.</span><span class="sxs-lookup"><span data-stu-id="8c83b-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="8c83b-137">Gebruikerstoewijzing vereisen</span><span class="sxs-lookup"><span data-stu-id="8c83b-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="8c83b-138">Als u een Azure AD Premium of Enterprise Mobility Suite (EMS)-abonnee bent, wordt aangeraden met behulp van groepen.</span><span class="sxs-lookup"><span data-stu-id="8c83b-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="8c83b-139">Groepen toewijzen aan de toepassing, kunt u actieve toegangsbeheer naar de eigenaar van de groep te delegeren.</span><span class="sxs-lookup"><span data-stu-id="8c83b-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="8c83b-140">U kunt de groep te maken of vraag de verantwoordelijke partij in uw organisatie te maken van de groep met behulp van de groep management-functie.</span><span class="sxs-lookup"><span data-stu-id="8c83b-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="8c83b-141">Gebruikers toewijzen aan een toepassing</span><span class="sxs-lookup"><span data-stu-id="8c83b-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="8c83b-142">Groepen toewijzen aan een toepassing</span><span class="sxs-lookup"><span data-stu-id="8c83b-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="8c83b-143">Onderdrukken van toestemming van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="8c83b-143">Suppress user consent</span></span>
<span data-ttu-id="8c83b-144">Standaard is elke gebruiker doorloopt van een ervaring toestemming aan te melden.</span><span class="sxs-lookup"><span data-stu-id="8c83b-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="8c83b-145">De ervaring van de toestemming, gebruikers vragen om te machtigen om een toepassing kan worden toegevoegd voor gebruikers die niet bekend bent met deze beslissingen zijn.</span><span class="sxs-lookup"><span data-stu-id="8c83b-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="8c83b-146">Voor toepassingen die u vertrouwt, kunt u de gebruikerservaring met ermee akkoord dat de toepassing namens uw organisatie te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="8c83b-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="8c83b-147">Zie voor meer informatie over de toestemming van de gebruiker en de toestemming in Azure optreden, [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="8c83b-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="8c83b-148">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="8c83b-148">Related Articles</span></span>
* [<span data-ttu-id="8c83b-149">Veilige externe toegang tot on-premises toepassingen met Azure AD-toepassingsproxy inschakelen</span><span class="sxs-lookup"><span data-stu-id="8c83b-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="8c83b-150">Voorwaardelijke toegang tot Azure Preview voor SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="8c83b-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="8c83b-151">Het beheren van toegang tot apps met Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c83b-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* <span data-ttu-id="8c83b-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="8c83b-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
