---
title: aaaHow toochoose welke toepassing toouse typt u bij het toevoegen van een toepassing | Microsoft Docs
description: Hallo ondersteund typen toepassingen die u met Azure AD integreren kunt te begrijpen en hun bijbehorende configuratie-opties
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a><span data-ttu-id="0b2de-103">Hoe toochoose welke toepassing toouse typt u bij het toevoegen van een toepassing</span><span class="sxs-lookup"><span data-stu-id="0b2de-103">How toochoose which application type toouse when adding an application</span></span>

<span data-ttu-id="0b2de-104">In dit artikel helpt u toounderstand Hallo vier belangrijkste typen toepassingen die u met Azure AD integreren kunt:</span><span class="sxs-lookup"><span data-stu-id="0b2de-104">This article help you toounderstand hello four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="0b2de-105">Wat wordt ondersteund door elk van deze</span><span class="sxs-lookup"><span data-stu-id="0b2de-105">What is supported by each of them</span></span>
* <span data-ttu-id="0b2de-106">Waarom u kunt ervoor kiezen welke toepassing</span><span class="sxs-lookup"><span data-stu-id="0b2de-106">Why you might choose which application</span></span>
* <span data-ttu-id="0b2de-107">Hoe tooconfigure kerneigenschappen voor deze toepassing, zoals hoe gebruikers worden **ingericht**, of wat **eenmalige aanmelding** toouse technologie.</span><span class="sxs-lookup"><span data-stu-id="0b2de-107">How tooconfigure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology toouse.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="0b2de-108">De soorten ondersteunde toepassingen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b2de-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="0b2de-109">Azure AD ondersteunt vier hoofdtoepassing typen die u kunt toevoegen met behulp van Hallo **toevoegen** functie gevonden onder **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0b2de-109">Azure AD supports four main application types that you can add using hello **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="0b2de-110">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="0b2de-110">These include:</span></span>

-   <span data-ttu-id="0b2de-111">**Azure AD-galerie toepassingen** : een toepassing die vooraf geïntegreerde voor eenmalige aanmelding met Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="0b2de-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="0b2de-112">**Application Proxy toepassingen** : een toepassing die wordt uitgevoerd in uw on-premises omgeving dat u wilt dat tooprovide beveiligde eenmalige aanmelding tooexternally.</span><span class="sxs-lookup"><span data-stu-id="0b2de-112">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

-   <span data-ttu-id="0b2de-113">**Aangepaste ontwikkelde toepassingen** : een toepassing die uw organisatie wil toodevelop op Azure AD-ontwikkelplatform voor toepassing hello, maar die mogelijk niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="0b2de-113">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="0b2de-114">**Niet-galerie toepassingen** : Breng uw eigen toepassingen!</span><span class="sxs-lookup"><span data-stu-id="0b2de-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="0b2de-115">Een webkoppeling die u wilt dat alle toepassingen die een veld de gebruikersnaam en wachtwoord SAML of OpenID Connect-protocollen ondersteunt of ondersteunt SCIM die u wenst dat toointegrate voor eenmalige aanmelding met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b2de-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a><span data-ttu-id="0b2de-116">Functies en mogelijkheden die worden ondersteund door alle Hallo hierboven toepassingstypen</span><span class="sxs-lookup"><span data-stu-id="0b2de-116">Features and capabilities supported by all hello above application types</span></span>

<span data-ttu-id="0b2de-117">Hallo onderstaande functies worden ondersteund door een Hallo hierboven 4 toepassingstypen in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0b2de-117">hello following features are supported by any of hello above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="0b2de-118">**Snel starten** – snel aan de slag met een toepassing door [eenvoudige implementatiestappen](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="0b2de-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="0b2de-119">**Algemene eigenschappen management** – ophalen van een [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan toepassing, [Hallo huisstijl aanpassen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) van een toepassing of [toepassing hellouitschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) voor alle gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0b2de-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan application, [customize hello branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable hello application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="0b2de-120">**Gebruiker-en groepsbeheer** – [toewijzen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) of [verwijderen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) tooan toepassing voor gebruikers en groepen, en desgewenst toewijzen Hallo specifieke toepassingsrollen deze gebruikers en groepen hebt toegang tot</span><span class="sxs-lookup"><span data-stu-id="0b2de-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups tooan application, and optionally assign hello specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="0b2de-121">**Toegang tot de toepassing zelf** – inschakelen van uw gebruikers toorequest [toegang tot de toepassing zelf](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan toepassing van de toegang tot hun toepassingen deelvensters door rechtstreeks een toepassing toe te voegen of [ toevoegen aan een Selfservice ingeschakeld groep](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)desgewenst vereisen van zakelijke goedkeuring langs Hallo manier</span><span class="sxs-lookup"><span data-stu-id="0b2de-121">**Self-service application access** – enable your users toorequest [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along hello way</span></span>

-   <span data-ttu-id="0b2de-122">**Aanmelden logboeken** – Zie [alle aanmeldingen tooan toepassing hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), of al uw toepassingen</span><span class="sxs-lookup"><span data-stu-id="0b2de-122">**Sign-in logs** – see [all hello sign-ins tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="0b2de-123">**Controlelogboeken** – Zie [controlelogboeken over wijzigingen tooan toepassing gedetailleerde](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), of tooall uw toepassingen</span><span class="sxs-lookup"><span data-stu-id="0b2de-123">**Audit logs** – see [detailed audit logs about modifications tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or tooall your applications</span></span>

-   <span data-ttu-id="0b2de-124">**Voorwaardelijke en risico gebaseerde toegang** – Stel krachtige [regels voor toegang op basis van een voorwaarde](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) die worden afgedwongen wanneer gebruikers toosign in bepaalde tooa-toepassing proberen</span><span class="sxs-lookup"><span data-stu-id="0b2de-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt toosign in tooa specific application</span></span>

-   <span data-ttu-id="0b2de-125">**Machtigingen weergave** – weergeven Hallo [OAuth2 machtigingen](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) een toepassing heeft toegang tooin aan uw directory vanaf één locatie</span><span class="sxs-lookup"><span data-stu-id="0b2de-125">**Permissions view** – view any of hello [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access tooin your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="0b2de-126">Eenmalige aanmelding en modi die worden ondersteund door specifieke toepassingstypen inrichten</span><span class="sxs-lookup"><span data-stu-id="0b2de-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="0b2de-127">Hallo in de volgende tabel beschrijft Hallo verschillende eenmalige aanmelding en modi die worden ondersteund door elk Hallo hierboven toepassingstypen inrichten.</span><span class="sxs-lookup"><span data-stu-id="0b2de-127">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="0b2de-128">U kunt deze tabel toohelp toounderstand u welke toepassing u moet tooadd toosupport een specifiek doel.</span><span class="sxs-lookup"><span data-stu-id="0b2de-128">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![Tabel van App-typen](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="0b2de-130">Hoe toochoose een modus voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b2de-130">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="0b2de-131">Hallo ondersteund **eenmalige aanmelding** modi voor Azure AD-toepassingen worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0b2de-131">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="0b2de-132">**Azure AD eenmalige aanmelding uitgeschakeld** – Kies Azure AD eenmalige aanmelding uitgeschakeld **modus voor één aanmelding** als u nog niet klaar toointegrate deze toepassing met eenmalige aanmelding met Azure AD, of gewoon test het uit</span><span class="sxs-lookup"><span data-stu-id="0b2de-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="0b2de-133">**Eenmalige aanmelding gekoppeld** – Kies Hallo [gekoppelde aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modus voor één aanmelding** als u een toepassing die al is gekoppeld aan een bestaande eenmalige aanmelding oplossing hebt of als u alleen wilt toopublish koppeling met een eenvoudige voor uw gebruikers in hun [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) of [startprogramma voor toepassingen van Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="0b2de-133">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="0b2de-134">**Op basis van wachtwoorden aanmelding** – Kies Hallo [op basis van wachtwoorden aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modus voor één aanmelding** als een HTML-gebruikersnaam en wachtwoord veld Hiermee maakt u uw toepassing en u toostore wilt die gebruikersnaam en wachtwoord veilig toobe replay later toohello-toepassing</span><span class="sxs-lookup"><span data-stu-id="0b2de-134">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="0b2de-135">**Op basis van SAML-aanmelding** – Kies Hallo [op basis van SAML-aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) eenmalige aanmelding modus als uw toepassing hello SAML of OpenID Connect-protocollen ondersteunt, of u wilt dat toobe toomap kunnen gebruikers op basis van rollen van de toepassing toospecific claims voor regels die u in uw SAML definieert *</span><span class="sxs-lookup"><span data-stu-id="0b2de-135">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="0b2de-136">Deze optie is niet beschikbaar wanneer de toepassingsproxy Hallo is geconfigureerd voor een toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b2de-136">This option is not available when hello application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="0b2de-137">**Op basis van een koptekst aanmelding** : Kies deze optie [headers gebaseerde aanmelding](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) aanmelding modus voor één hebt u een toepassing met PingAccess die ondersteuning biedt voor HTTP-header gebaseerde verificatie die u wilt dat tooperform eenmalige aanmelding op te</span><span class="sxs-lookup"><span data-stu-id="0b2de-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="0b2de-138">Deze optie is alleen beschikbaar wanneer de toepassingsproxy Hallo en PingAccess is geconfigureerd voor een toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b2de-138">This option is only available when hello application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="0b2de-139">**Geïntegreerde Windows-verificatie** – Kies Hallo [geïntegreerde Windows-verificatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) eenmalige aanmelding bij het blootstellen van een on-premises WIA-toepassing die u wilt dat tooperform eenmalige aanmelding op te</span><span class="sxs-lookup"><span data-stu-id="0b2de-139">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="0b2de-140">Deze optie is alleen beschikbaar wanneer de toepassingsproxy Hallo is geconfigureerd voor een toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b2de-140">This option is only available when hello application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="0b2de-141">Modi voor eenmalige aanmelding voor aangepaste ontwikkelde toepassingen</span><span class="sxs-lookup"><span data-stu-id="0b2de-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="0b2de-142">Toepassingen u hebt ontwikkeld via Hallo aangepaste [ontwikkelde aangepaste toepassing](#_Custom-Developed_Applications) ervaring bieden ook ondersteuning voor extra eenmalige aanmelding modi niet hierboven worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="0b2de-142">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="0b2de-143">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="0b2de-143">These include:</span></span>

-   <span data-ttu-id="0b2de-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) op basis van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b2de-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="0b2de-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) op basis van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b2de-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="0b2de-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) op basis van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b2de-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="0b2de-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) op basis van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b2de-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="0b2de-148">Lees Hallo [ontwikkelaarshandleiding Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn meer informatie over hoe een aangepaste ontwikkelde toocreate-toepassing die ondersteuning biedt voor deze eenmalige aanmelding modi.</span><span class="sxs-lookup"><span data-stu-id="0b2de-148">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="0b2de-149">Hoe een toepassing tooset enkel de modus voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b2de-149">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="0b2de-150">tooset een toepassing van **eenmalige aanmelding** modus Hallo instructies hieronder:</span><span class="sxs-lookup"><span data-stu-id="0b2de-150">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="0b2de-151">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="0b2de-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0b2de-152">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="0b2de-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0b2de-153">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="0b2de-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0b2de-154">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="0b2de-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0b2de-155">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0b2de-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="0b2de-156">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="0b2de-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0b2de-157">Hallo-toepassing waarvoor u eenmalige aanmelding tooconfigure wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="0b2de-157">Select hello application for which you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="0b2de-158">Nadat de toepassing hello wordt geladen, klikt u op **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="0b2de-158">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="how-toochoose-a-provisioning-mode"></a><span data-ttu-id="0b2de-159">Hoe toochoose een inrichtingsmethode</span><span class="sxs-lookup"><span data-stu-id="0b2de-159">How toochoose a provisioning mode</span></span>

-   <span data-ttu-id="0b2de-160">**Handmatige inrichting** – Kies Hallo [handmatige](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) Inrichtingsmethode als u bestaande accounts hebt of toomanage accounts voor deze toepassing buiten Azure AD wilt.</span><span class="sxs-lookup"><span data-stu-id="0b2de-160">**Manual Provisioning** – choose hello [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish toomanage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="0b2de-161">**Automatische inrichting** – Kies Hallo [automatische](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **inrichtingsmodus** als u wilt dat tooenable automatische API gebaseerde inrichting en/of de inrichting van gebruikersaccounts toothis toepassing</span><span class="sxs-lookup"><span data-stu-id="0b2de-161">**Automatic Provisioning** – choose hello [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want tooenable automatic API-based provisioning and/or de-provisioning of user accounts toothis application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="0b2de-162">Deze optie is alleen beschikbaar voor toepassingen binnen Hallo **aanbevolen** categorie Hallo [Azure AD-Toepassingsgalerie](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="0b2de-162">This option is available only for applications within hello **featured** category of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="0b2de-163">**Automatische inrichting op basis van SCIM** – gebruiken [automatische inrichting op basis van SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) als uw toepassing hello SCIM protocol ondersteunt voor het detecteren van wijzigingen toousers en groepen die automatisch worden verzonden voor wijzigingen tooany toepassing is geïntegreerd met Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b2de-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports hello SCIM protocol for detecting changes toousers and groups, which are automatically emitted for changes tooany application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="0b2de-164">Deze optie wordt niet vermeld als een bepaalde Inrichtingsmethode, maar is standaard ingeschakeld voor alle toepassingen die zijn geïntegreerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b2de-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a><span data-ttu-id="0b2de-165">Hoe een toepassing tooset de Inrichtingsmethode</span><span class="sxs-lookup"><span data-stu-id="0b2de-165">How tooset an application’s provisioning mode</span></span>

<span data-ttu-id="0b2de-166">tooset een toepassing van **inrichting** modus Hallo instructies hieronder:</span><span class="sxs-lookup"><span data-stu-id="0b2de-166">tooset an application’s **provisioning** mode, follow hello instructions below:</span></span>

<span data-ttu-id="0b2de-167">tooset een toepassing van **eenmalige aanmelding** modus Hallo instructies hieronder:</span><span class="sxs-lookup"><span data-stu-id="0b2de-167">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="0b2de-168">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="0b2de-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0b2de-169">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="0b2de-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0b2de-170">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="0b2de-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0b2de-171">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="0b2de-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0b2de-172">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0b2de-172">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="0b2de-173">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="0b2de-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0b2de-174">Hallo-toepassing waarvoor u inrichten tooconfigure wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="0b2de-174">Select hello application for which you want tooconfigure provisioning.</span></span>

7.  <span data-ttu-id="0b2de-175">Nadat de toepassing hello wordt geladen, klikt u op **inrichten** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="0b2de-175">Once hello application loads, click **Provisioning** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b2de-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0b2de-176">Next steps</span></span>
[<span data-ttu-id="0b2de-177">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b2de-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
