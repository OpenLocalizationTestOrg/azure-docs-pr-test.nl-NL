---
title: Beheren van eenmalige aanmelding voor Azure AD-toepassingsproxy | Microsoft Docs
description: Meer informatie over de basisprincipes van eenmalige aanmelding met toepassingsproxy
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 1deb3d91049d45fe26791783e13bd23e0a7d9f95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="f542c-103">Hoe biedt Azure AD-toepassingsproxy eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f542c-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="f542c-104">Eenmalige aanmelding is een essentieel element van Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="f542c-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="f542c-105">Het biedt de beste gebruikerservaring omdat uw gebruikers alleen aan te melden bij Azure Active Directory in de cloud.</span><span class="sxs-lookup"><span data-stu-id="f542c-105">It provides the best user experience because your users only have to sign in to Azure Active Directory in the cloud.</span></span> <span data-ttu-id="f542c-106">Zodra ze naar Azure Active Directory verifiëren, wordt door de connector voor toepassingsproxy de verificatie naar de on-premises toepassing verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f542c-106">Once they authenticate to Azure Active Directory, the Application Proxy connector handles the authentication to the on-premises application.</span></span> <span data-ttu-id="f542c-107">De back-end-toepassing kan niet het verschil tussen een externe gebruiker aanmelden via toepassingsproxy en een reguliere gebruik op een apparaat domein niet bepalen.</span><span class="sxs-lookup"><span data-stu-id="f542c-107">The backend application can't tell the difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="f542c-108">Voor het gebruik van Azure Active Directory voor eenmalige aanmelding voor uw toepassingen, moet u selecteren **Azure Active Directory** als de methode voor verificatie vooraf.</span><span class="sxs-lookup"><span data-stu-id="f542c-108">To use Azure Active Directory for single sign-on to your applications, you need to select **Azure Active Directory** as the pre-authentication method.</span></span> <span data-ttu-id="f542c-109">Als u selecteert **Passthrough** en vervolgens uw gebruikers helemaal niet met Azure Active Directory verifiëren, maar direct door naar de toepassing omgeleid.</span><span class="sxs-lookup"><span data-stu-id="f542c-109">If you select **Passthrough** then your users don't authenticate to Azure Active Directory at all, but are directed straight to the application.</span></span> <span data-ttu-id="f542c-110">U kunt deze instelling kunt configureren wanneer u eerst een toepassing publiceren of navigeer naar uw toepassing in de Azure portal en de Application Proxy-instellingen bewerken.</span><span class="sxs-lookup"><span data-stu-id="f542c-110">You can configure this setting when you first publish an application, or navigate to your application in the Azure portal and edit the Application Proxy settings.</span></span> 

<span data-ttu-id="f542c-111">Overzicht van de opties voor eenmalige aanmelding als volgt:</span><span class="sxs-lookup"><span data-stu-id="f542c-111">To see your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="f542c-112">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f542c-112">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f542c-113">Navigeer naar **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f542c-113">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="f542c-114">Selecteer de app waarvan opties voor eenmalige aanmelding u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="f542c-114">Select the app whose single sign-on options you want to manage.</span></span>
4. <span data-ttu-id="f542c-115">Selecteer **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f542c-115">Select **Single sign-on**.</span></span>

   ![Het vervolgmenu van eenmalige aanmelding](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="f542c-117">Het vervolgkeuzemenu ziet vijf opties voor eenmalige aanmelding voor uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="f542c-117">The dropdown menu shows five options for single sign-on to your application:</span></span>

* <span data-ttu-id="f542c-118">Azure AD eenmalige aanmelding uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="f542c-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="f542c-119">Op basis van wachtwoorden eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f542c-119">Password-based sign-on</span></span>
* <span data-ttu-id="f542c-120">Gekoppelde aanmelding</span><span class="sxs-lookup"><span data-stu-id="f542c-120">Linked sign-on</span></span>
* <span data-ttu-id="f542c-121">Geïntegreerde Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="f542c-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="f542c-122">Op basis van een koptekst eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f542c-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="f542c-123">Azure AD eenmalige aanmelding uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="f542c-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="f542c-124">Als u niet wilt met Azure Active Directory-integratie voor eenmalige aanmelding voor uw toepassing, kiest u **Azure AD eenmalige aanmelding uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="f542c-124">If you don't want to use Azure Active Directory integration for single sign-on to your application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="f542c-125">Met deze optie selecteert, kunnen uw gebruikers tweemaal verifiëren.</span><span class="sxs-lookup"><span data-stu-id="f542c-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="f542c-126">Eerst geverifieerd bij Azure Active Directory en vervolgens weer aanmelden op de toepassing zelf.</span><span class="sxs-lookup"><span data-stu-id="f542c-126">First, they authenticate to Azure Active Directory and then sign in to the application itself.</span></span> 

<span data-ttu-id="f542c-127">Deze optie is een goede keuze als uw on-premises toepassing niet vereisen dat gebruikers om te verifiëren, maar u wilt toevoegen van Azure Active Directory als een beveiligingslaag voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="f542c-127">This option is a good choice if your on-premises application doesn't require users to authenticate, but you want to add Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="f542c-128">Op basis van wachtwoorden eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f542c-128">Password-based sign-on</span></span>

<span data-ttu-id="f542c-129">Als u gebruiken van Azure Active Directory als een kluis wachtwoord voor uw on-premises toepassingen wilt, kiest u **op basis van wachtwoorden aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f542c-129">If you want to use Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="f542c-130">Deze optie is een goede keuze als uw toepassing wordt geverifieerd met een gebruikersnaam en wachtwoord keuzelijst met invoervak in plaats van de toegangstokens of headers.</span><span class="sxs-lookup"><span data-stu-id="f542c-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="f542c-131">Met op basis van wachtwoorden aanmelding moeten uw gebruikers zich aanmelden bij de toepassing de eerste keer dat ze het willen openen.</span><span class="sxs-lookup"><span data-stu-id="f542c-131">With password-based sign-on, your users need to sign in to the application the first time they access it.</span></span> <span data-ttu-id="f542c-132">Daarna biedt Azure Active Directory de gebruikersnaam en wachtwoord namens de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f542c-132">After that, Azure Active Directory supplies the username and password on behalf of the user.</span></span> 

<span data-ttu-id="f542c-133">Zie voor meer informatie over het instellen van wachtwoorden gebaseerde aanmelding [wachtwoord vaulting voor eenmalige aanmelding met toepassingsproxy](application-proxy-sso-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f542c-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="f542c-134">Gekoppelde aanmelding</span><span class="sxs-lookup"><span data-stu-id="f542c-134">Linked sign-on</span></span>

<span data-ttu-id="f542c-135">Als u al een oplossing voor eenmalige aanmelding instellen voor uw on-premises identiteiten, kiest u **gekoppelde aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f542c-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="f542c-136">Deze optie kunt Azure Active Directory voor het benutten van bestaande oplossingen voor eenmalige aanmelding, maar nog steeds geeft uw gebruikers externe toegang tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f542c-136">This option enables Azure Active Directory to leverage existing SSO solutions, but still gives your users remote access to the application.</span></span> 

<span data-ttu-id="f542c-137">Zie voor meer informatie over de gekoppelde aanmelding (voorheen bekend als bestaande eenmalige aanmelding) [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="f542c-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="f542c-138">Geïntegreerde Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="f542c-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="f542c-139">Als uw on-premises toepassingen met geïntegreerde Windows-Authentication(IWA) gebruikt of als u wilt gebruiken van Kerberos-beperkt delegatie (KCD) voor eenmalige aanmelding, kiest u **geïntegreerde Windows-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="f542c-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want to use Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="f542c-140">Met deze optie hoeft alleen uw gebruikers te verifiëren bij Azure Active Directory en vervolgens de connector voor toepassingsproxy de gebruiker een Kerberos-token verkrijgen en meld u bij de toepassing imiteert.</span><span class="sxs-lookup"><span data-stu-id="f542c-140">With this option, your users only need to authenticate to Azure Active Directory, and then the Application Proxy connector impersonates the user to get a Kerberos token and sign in to the application.</span></span> 

<span data-ttu-id="f542c-141">Zie voor meer informatie over het instellen van geïntegreerde Windows-verificatie [Kerberos-beperkte delegatie voor eenmalige aanmelding met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="f542c-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="f542c-142">Op basis van een koptekst eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f542c-142">Header-based sign-on</span></span> 

<span data-ttu-id="f542c-143">Als uw toepassingen headers voor verificatie gebruikt, kiest u **headers gebaseerde aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f542c-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="f542c-144">Met deze optie kunnen hoeft uw gebruikers alleen te verificatie de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f542c-144">With this option, your users only need to authentication the Azure Active Directory.</span></span> <span data-ttu-id="f542c-145">Microsoft werkt samen met een derde partij verificatieservice aangeroepen PingAccess waarmee het toegangstoken van Azure Active Directory vertaald naar een header-indeling voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f542c-145">Microsoft partners with a third-party authentication service called PingAccess, which translated the Azure Active Directory access token into a header format for the application.</span></span> 

<span data-ttu-id="f542c-146">Zie voor meer informatie over het instellen van verificatie op basis van een koptekst [verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy](application-proxy-ping-access.md).</span><span class="sxs-lookup"><span data-stu-id="f542c-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f542c-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f542c-147">Next steps</span></span>

- [<span data-ttu-id="f542c-148">Wachtwoord voor eenmalige aanmelding met toepassingsproxy vaulting</span><span class="sxs-lookup"><span data-stu-id="f542c-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="f542c-149">Kerberos-beperkte delegatie voor eenmalige aanmelding met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="f542c-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="f542c-150">Verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="f542c-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
