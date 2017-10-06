---
title: aaaManage SSO voor Azure AD-toepassingsproxy | Microsoft Docs
description: Meer informatie over de basisprincipes Hallo van eenmalige aanmelding met toepassingsproxy
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
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="7cc7e-103">Hoe biedt Azure AD-toepassingsproxy eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cc7e-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="7cc7e-104">Eenmalige aanmelding is een essentieel element van Azure AD-toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="7cc7e-105">Het biedt de beste gebruikerservaring Hallo omdat uw gebruikers slechts toosign in Active Directory in de cloud Hallo tooAzure hebben.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-105">It provides hello best user experience because your users only have toosign in tooAzure Active Directory in hello cloud.</span></span> <span data-ttu-id="7cc7e-106">Nadat ze zich tooAzure Active Directory verifiëren, verwerkt Hallo Application Proxy connector Hallo verificatie toohello on-premises toepassing.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-106">Once they authenticate tooAzure Active Directory, hello Application Proxy connector handles hello authentication toohello on-premises application.</span></span> <span data-ttu-id="7cc7e-107">Hallo back-end-toepassing kan niet zien Hallo verschil tussen een externe gebruiker aanmelden via toepassingsproxy en een reguliere gebruik op een apparaat voor het domein.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-107">hello backend application can't tell hello difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="7cc7e-108">toouse Azure Active Directory voor eenmalige aanmelding tooyour toepassingen, moet u tooselect **Azure Active Directory** als Hallo-methode voor verificatie vooraf.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-108">toouse Azure Active Directory for single sign-on tooyour applications, you need tooselect **Azure Active Directory** as hello pre-authentication method.</span></span> <span data-ttu-id="7cc7e-109">Als u selecteert **Passthrough** en vervolgens uw gebruikers tooAzure Active Directory niet helemaal niet worden geverifieerd, maar gerichte rechte toohello toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-109">If you select **Passthrough** then your users don't authenticate tooAzure Active Directory at all, but are directed straight toohello application.</span></span> <span data-ttu-id="7cc7e-110">U kunt deze instelling kunt configureren wanneer u eerst een toepassing publiceren of navigeer tooyour toepassing hello Azure-portal en Hallo Application Proxy-instellingen bewerken.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-110">You can configure this setting when you first publish an application, or navigate tooyour application in hello Azure portal and edit hello Application Proxy settings.</span></span> 

<span data-ttu-id="7cc7e-111">toosee uw opties voor eenmalige aanmelding als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="7cc7e-111">toosee your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="7cc7e-112">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7cc7e-112">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7cc7e-113">Navigeer te**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-113">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="7cc7e-114">Selecteer Hallo-app waarvan eenmalige aanmelding u opties wilt toomanage.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-114">Select hello app whose single sign-on options you want toomanage.</span></span>
4. <span data-ttu-id="7cc7e-115">Selecteer **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-115">Select **Single sign-on**.</span></span>

   ![Het vervolgmenu van eenmalige aanmelding](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="7cc7e-117">Hallo vervolgkeuzemenu ziet u vijf opties voor eenmalige aanmelding tooyour toepassing:</span><span class="sxs-lookup"><span data-stu-id="7cc7e-117">hello dropdown menu shows five options for single sign-on tooyour application:</span></span>

* <span data-ttu-id="7cc7e-118">Azure AD eenmalige aanmelding uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="7cc7e-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="7cc7e-119">Op basis van wachtwoorden eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cc7e-119">Password-based sign-on</span></span>
* <span data-ttu-id="7cc7e-120">Gekoppelde aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cc7e-120">Linked sign-on</span></span>
* <span data-ttu-id="7cc7e-121">Geïntegreerde Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="7cc7e-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="7cc7e-122">Op basis van een koptekst eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cc7e-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="7cc7e-123">Azure AD eenmalige aanmelding uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="7cc7e-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="7cc7e-124">Als u niet dat Azure Active Directory-integratie voor eenmalige aanmelding tooyour toepassing toouse wilt, kiest u **Azure AD eenmalige aanmelding uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-124">If you don't want toouse Azure Active Directory integration for single sign-on tooyour application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="7cc7e-125">Met deze optie selecteert, kunnen uw gebruikers tweemaal verifiëren.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="7cc7e-126">Eerst geverifieerd tooAzure Active Directory en vervolgens weer aanmelden toohello toepassing zelf.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-126">First, they authenticate tooAzure Active Directory and then sign in toohello application itself.</span></span> 

<span data-ttu-id="7cc7e-127">Deze optie is een goede keuze als uw on-premises toepassing geen gebruikers tooauthenticate vereist, maar u wilt tooadd Azure Active Directory gebruiken als een beveiligingslaag voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-127">This option is a good choice if your on-premises application doesn't require users tooauthenticate, but you want tooadd Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="7cc7e-128">Op basis van wachtwoorden eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cc7e-128">Password-based sign-on</span></span>

<span data-ttu-id="7cc7e-129">Als u toouse Azure Active Directory als de kluis van een wachtwoord voor uw on-premises toepassingen wilt, kiest u **op basis van wachtwoorden aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-129">If you want toouse Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="7cc7e-130">Deze optie is een goede keuze als uw toepassing wordt geverifieerd met een gebruikersnaam en wachtwoord keuzelijst met invoervak in plaats van de toegangstokens of headers.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="7cc7e-131">Met op basis van wachtwoorden aanmelding moeten uw gebruikers toosign in toohello toepassing hello eerste keer dat ze het willen openen.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-131">With password-based sign-on, your users need toosign in toohello application hello first time they access it.</span></span> <span data-ttu-id="7cc7e-132">Daarna biedt Azure Active Directory Hallo gebruikersnaam en wachtwoord namens Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-132">After that, Azure Active Directory supplies hello username and password on behalf of hello user.</span></span> 

<span data-ttu-id="7cc7e-133">Zie voor meer informatie over het instellen van wachtwoorden gebaseerde aanmelding [wachtwoord vaulting voor eenmalige aanmelding met toepassingsproxy](application-proxy-sso-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7cc7e-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="7cc7e-134">Gekoppelde aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cc7e-134">Linked sign-on</span></span>

<span data-ttu-id="7cc7e-135">Als u al een oplossing voor eenmalige aanmelding instellen voor uw on-premises identiteiten, kiest u **gekoppelde aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="7cc7e-136">Deze optie kunt Azure Active Directory tooleverage bestaande SSO-oplossingen, maar nog steeds RAS toohello toepassing geeft uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-136">This option enables Azure Active Directory tooleverage existing SSO solutions, but still gives your users remote access toohello application.</span></span> 

<span data-ttu-id="7cc7e-137">Zie voor meer informatie over de gekoppelde aanmelding (voorheen bekend als bestaande eenmalige aanmelding) [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="7cc7e-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="7cc7e-138">Geïntegreerde Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="7cc7e-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="7cc7e-139">Als uw on-premises toepassingen met geïntegreerde Windows-Authentication(IWA) of als u wilt dat toouse Kerberos-beperkt delegatie (KCD) voor eenmalige aanmelding, kiest u **geïntegreerde Windows-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want toouse Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="7cc7e-140">Met deze optie uw gebruikers hoeven alleen tooauthenticate tooAzure Active Directory en vervolgens Hallo Application Proxy connector Hallo gebruiker tooget een Kerberos-token en meld u aan toohello toepassing imiteert.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-140">With this option, your users only need tooauthenticate tooAzure Active Directory, and then hello Application Proxy connector impersonates hello user tooget a Kerberos token and sign in toohello application.</span></span> 

<span data-ttu-id="7cc7e-141">Zie voor meer informatie over het instellen van geïntegreerde Windows-verificatie [Kerberos-beperkte delegatie voor eenmalige aanmelding met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="7cc7e-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="7cc7e-142">Op basis van een koptekst eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cc7e-142">Header-based sign-on</span></span> 

<span data-ttu-id="7cc7e-143">Als uw toepassingen headers voor verificatie gebruikt, kiest u **headers gebaseerde aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="7cc7e-144">Met deze optie kunnen vereist uw gebruikers alleen tooauthentication hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-144">With this option, your users only need tooauthentication hello Azure Active Directory.</span></span> <span data-ttu-id="7cc7e-145">Microsoft werkt samen met een derde partij verificatieservice PingAccess die hello Azure Active Directory-toegangstoken vertaald naar een header-indeling voor de toepassing hello genoemd.</span><span class="sxs-lookup"><span data-stu-id="7cc7e-145">Microsoft partners with a third-party authentication service called PingAccess, which translated hello Azure Active Directory access token into a header format for hello application.</span></span> 

<span data-ttu-id="7cc7e-146">Zie voor meer informatie over het instellen van verificatie op basis van een koptekst [verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy](application-proxy-ping-access.md).</span><span class="sxs-lookup"><span data-stu-id="7cc7e-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cc7e-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7cc7e-147">Next steps</span></span>

- [<span data-ttu-id="7cc7e-148">Wachtwoord voor eenmalige aanmelding met toepassingsproxy vaulting</span><span class="sxs-lookup"><span data-stu-id="7cc7e-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="7cc7e-149">Kerberos-beperkte delegatie voor eenmalige aanmelding met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="7cc7e-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="7cc7e-150">Verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="7cc7e-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
