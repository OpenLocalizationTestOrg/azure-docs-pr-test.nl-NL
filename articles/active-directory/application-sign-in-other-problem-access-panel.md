---
title: aaaProblems tooan toepassing hello Toegangsvenster aanmelden | Microsoft Docs
description: Hoe tootroubleshoot problemen met toegang tot een toepassing van Microsoft Azure AD-Toegangsvenster op myapps.microsoft.com Hallo
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="b0a66-103">Problemen met aanmelden tooan toepassing hello Toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="b0a66-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="b0a66-104">Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="b0a66-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="b0a66-105">Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="b0a66-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="b0a66-106">Hallo-toepassing moet correct worden geconfigureerd en toegewezen toohello gebruiker of een groep Hallo-gebruiker lid is van toepassing op Hallo toosee in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b0a66-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="b0a66-107">Hallo-type van een gebruiker ziet u mogelijk apps kunnen worden onderverdeeld in de volgende categorieën Hallo:</span><span class="sxs-lookup"><span data-stu-id="b0a66-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="b0a66-108">Office 365-toepassingen</span><span class="sxs-lookup"><span data-stu-id="b0a66-108">Office 365 Applications</span></span>

-   <span data-ttu-id="b0a66-109">Microsoft en derden toepassingen die zijn geconfigureerd op basis van een federatieve aanmelding bij</span><span class="sxs-lookup"><span data-stu-id="b0a66-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="b0a66-110">SSO-toepassingen op basis van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="b0a66-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="b0a66-111">Toepassingen met bestaande oplossingen voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0a66-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="b0a66-112">Algemene problemen toocheck eerst</span><span class="sxs-lookup"><span data-stu-id="b0a66-112">General issues toocheck first</span></span>

-   <span data-ttu-id="b0a66-113">Zorg ervoor dat uw met een **browser** die voldoet aan de minimale vereisten van de Hallo voor Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b0a66-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="b0a66-114">Zorg ervoor dat de browser van Hallo gebruiker is toegevoegd Hallo-URL van Hallo toepassing tooits **vertrouwde websites**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="b0a66-115">Zorg ervoor dat toocheck Hallo toepassing **geconfigureerd** correct.</span><span class="sxs-lookup"><span data-stu-id="b0a66-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="b0a66-116">Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="b0a66-117">Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="b0a66-118">Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="b0a66-119">Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="b0a66-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="b0a66-120">Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="b0a66-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="b0a66-121">Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="b0a66-122">Zorg ervoor dat tooalso probeer wissen van cookies in uw browser opnieuw te proberen toosign in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="b0a66-123">Vergadering Browservereisten voor Hallo Toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="b0a66-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="b0a66-124">Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b0a66-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="b0a66-125">toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b0a66-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="b0a66-126">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="b0a66-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="b0a66-127">Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:</span><span class="sxs-lookup"><span data-stu-id="b0a66-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="b0a66-128">Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="b0a66-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="b0a66-129">Rand verjaardagseditie van Windows 10 of hoger</span><span class="sxs-lookup"><span data-stu-id="b0a66-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="b0a66-130">Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="b0a66-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="b0a66-131">Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="b0a66-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="b0a66-132">Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo</span><span class="sxs-lookup"><span data-stu-id="b0a66-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="b0a66-133">tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b0a66-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-134">Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0a66-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="b0a66-135">Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b0a66-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="b0a66-136">Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="b0a66-137">Op basis van uw browser zijn u gerichte toohello downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="b0a66-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="b0a66-138">**Voeg** Hallo extensie tooyour browser.</span><span class="sxs-lookup"><span data-stu-id="b0a66-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="b0a66-139">Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.</span><span class="sxs-lookup"><span data-stu-id="b0a66-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="b0a66-140">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="b0a66-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="b0a66-141">Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="b0a66-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="b0a66-142">U kunt ook Hallo-extensie voor Chrome en de rand van Hallo rechtstreekse koppelingen hieronder downloaden:</span><span class="sxs-lookup"><span data-stu-id="b0a66-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="b0a66-143">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="b0a66-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="b0a66-144">Uitbreiding van de rand toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="b0a66-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b0a66-145">Hoe tooconfigure federatieve eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0a66-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="b0a66-146">Alle toepassing in de galerie van Azure AD Hallo ingeschakeld met Enterprise Single Sign-On-functionaliteit is een stapsgewijze zelfstudie beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b0a66-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="b0a66-147">U hebt toegang tot Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.</span><span class="sxs-lookup"><span data-stu-id="b0a66-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="b0a66-148">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="b0a66-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b0a66-149">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="b0a66-150">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="b0a66-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b0a66-151">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="b0a66-152">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="b0a66-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="b0a66-153">Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="b0a66-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b0a66-154">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="b0a66-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b0a66-155">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b0a66-156">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b0a66-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-157">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="b0a66-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b0a66-158">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-159">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-160">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-161">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="b0a66-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b0a66-162">In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b0a66-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="b0a66-163">Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="b0a66-164">Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="b0a66-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="b0a66-165">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="b0a66-166">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b0a66-167">Eenmalige aanmelding voor een toepassing van Hallo-galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b0a66-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b0a66-168">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="b0a66-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-170">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-171">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-172">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-173">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b0a66-174">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-175">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="b0a66-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="b0a66-176">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-177">Selecteer **op basis van SAML aanmelding** van Hallo **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="b0a66-178">Voer waarden in Hallo vereist **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="b0a66-179">U moet deze waarden ophalen van de leverancier van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b0a66-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="b0a66-180">tooconfigure hello toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="b0a66-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="b0a66-181">Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="b0a66-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="b0a66-182">tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding, Hallo antwoord-URL is een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="b0a66-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="b0a66-183">Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="b0a66-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="b0a66-184">**Optioneel:** klikt u op **weergeven geavanceerde instellingen voor URL** als u toosee Hallo niet vereist waarden wilt.</span><span class="sxs-lookup"><span data-stu-id="b0a66-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="b0a66-185">In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="b0a66-186">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b0a66-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b0a66-187">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="b0a66-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="b0a66-188">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-188">click **Add attribute**.</span></span> <span data-ttu-id="b0a66-189">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b0a66-190">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-190">Click **Save.**</span></span> <span data-ttu-id="b0a66-191">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b0a66-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="b0a66-192">Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="b0a66-193">U heeft ook Hallo metagegevens-URL's en vereiste certificaat toosetup eenmalige aanmelding met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="b0a66-194">Klik op **opslaan** toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="b0a66-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="b0a66-195">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="b0a66-196">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="b0a66-197">tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="b0a66-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-198">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-199">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-200">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-201">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-202">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b0a66-203">Als u Hallo-toepassing die u wilt dat tooshow hier niet ziet, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-204">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0a66-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b0a66-205">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-206">Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="b0a66-207">Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b0a66-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b0a66-208">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="b0a66-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b0a66-209">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="b0a66-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="b0a66-210">gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b0a66-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b0a66-211">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="b0a66-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="b0a66-212">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-212">click **Add attribute**.</span></span> <span data-ttu-id="b0a66-213">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b0a66-214">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-214">Click **Save.**</span></span> <span data-ttu-id="b0a66-215">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b0a66-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="b0a66-216">Azure AD-metagegevens hello of een certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="b0a66-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="b0a66-217">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b0a66-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-218">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-219">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-220">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-221">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-222">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b0a66-223">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-224">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0a66-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b0a66-225">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-226">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="b0a66-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b0a66-227">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="b0a66-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="b0a66-228">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="b0a66-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b0a66-229">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0a66-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b0a66-230">Hoe tooconfigure federatieve eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="b0a66-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b0a66-231">een toepassing niet galerie tooconfigure, moet u toohave Azure AD premium en toepassing hello SAML 2.0 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="b0a66-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="b0a66-232">Voor meer informatie over Azure AD-versies, gaat u naar [prijzen van Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="b0a66-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="b0a66-233">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="b0a66-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="b0a66-234">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="b0a66-235">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="b0a66-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="b0a66-236">Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="b0a66-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="b0a66-237">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="b0a66-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="b0a66-238">tooconfigure eenmalige aanmelding voor een toepassing die zich niet in de galerie van Azure AD hello, stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b0a66-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-239">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-240">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-241">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-242">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-243">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="b0a66-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b0a66-244">Klik op **Non-galerie toepassing** in Hallo **uw eigen app toevoegen** sectie</span><span class="sxs-lookup"><span data-stu-id="b0a66-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="b0a66-245">Voer de naam van de Hallo van de toepassing hello in Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="b0a66-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="b0a66-246">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="b0a66-247">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="b0a66-248">Selecteer **op basis van SAML aanmelding** in Hallo **modus** vervolgkeuzelijst</span><span class="sxs-lookup"><span data-stu-id="b0a66-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="b0a66-249">Voer waarden in Hallo vereist **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="b0a66-250">U moet deze waarden ophalen van de leverancier van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b0a66-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="b0a66-251">tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding Hallo antwoord-URL en Hallo ID invoeren.</span><span class="sxs-lookup"><span data-stu-id="b0a66-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="b0a66-252">**Optioneel:** tooconfigure Hallo toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="b0a66-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="b0a66-253">In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="b0a66-254">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b0a66-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b0a66-255">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="b0a66-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="b0a66-256">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-256">click **Add attribute**.</span></span> <span data-ttu-id="b0a66-257">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b0a66-258">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-258">Click **Save.**</span></span> <span data-ttu-id="b0a66-259">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b0a66-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="b0a66-260">Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="b0a66-261">Bovendien heeft u Azure AD-URL's en het certificaat dat is vereist voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b0a66-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="b0a66-262">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="b0a66-263">tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="b0a66-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-264">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-265">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-266">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-267">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-268">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b0a66-269">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-270">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0a66-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b0a66-271">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-272">Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="b0a66-273">Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b0a66-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b0a66-274">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="b0a66-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b0a66-275">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="b0a66-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="b0a66-276">gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b0a66-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b0a66-277">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="b0a66-277">tooadd an attribute:</span></span>

   <span data-ttu-id="b0a66-278">1. Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-278">1.click **Add attribute**.</span></span> <span data-ttu-id="b0a66-279">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="b0a66-280">2 Klik **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-280">2 Click **Save.**</span></span> <span data-ttu-id="b0a66-281">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b0a66-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="b0a66-282">Azure AD-metagegevens hello of een certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="b0a66-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="b0a66-283">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b0a66-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-284">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-285">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-286">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-287">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-288">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b0a66-289">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-290">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0a66-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b0a66-291">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-292">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="b0a66-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b0a66-293">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="b0a66-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="b0a66-294">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="b0a66-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b0a66-295">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0a66-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b0a66-296">Hoe tooconfigure wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0a66-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="b0a66-297">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="b0a66-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b0a66-298">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="b0a66-299">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="b0a66-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b0a66-300">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0a66-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b0a66-301">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b0a66-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-302">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="b0a66-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b0a66-303">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-304">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-305">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-306">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="b0a66-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b0a66-307">In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="b0a66-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="b0a66-308">Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="b0a66-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="b0a66-309">Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="b0a66-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="b0a66-310">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="b0a66-311">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="b0a66-312">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="b0a66-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="b0a66-313">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="b0a66-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-314">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-315">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-316">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-317">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-318">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="b0a66-319">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-320">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="b0a66-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="b0a66-321">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-322">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b0a66-323">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="b0a66-324">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b0a66-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="b0a66-325">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="b0a66-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b0a66-326">Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="b0a66-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b0a66-327">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="b0a66-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b0a66-328">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="b0a66-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="b0a66-329">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="b0a66-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="b0a66-330">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="b0a66-330">Add a non-gallery application</span></span>

<span data-ttu-id="b0a66-331">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b0a66-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-332">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="b0a66-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b0a66-333">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-334">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-335">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-336">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="b0a66-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b0a66-337">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="b0a66-338">Vul in Hallo Hallo-naam van uw toepassing **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="b0a66-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="b0a66-339">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-339">Select **Add.**</span></span>

<span data-ttu-id="b0a66-340">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="b0a66-341">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="b0a66-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="b0a66-342">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="b0a66-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-343">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b0a66-344">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-345">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-346">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-347">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="b0a66-348">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-349">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="b0a66-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="b0a66-350">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-351">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b0a66-352">Voer Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="b0a66-353">Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="b0a66-354">Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="b0a66-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="b0a66-355">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="b0a66-356">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b0a66-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="b0a66-357">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="b0a66-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="b0a66-358">Hoe een gebruiker tooan toepassing rechtstreeks tooassign</span><span class="sxs-lookup"><span data-stu-id="b0a66-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="b0a66-359">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b0a66-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="b0a66-360">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b0a66-361">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b0a66-362">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b0a66-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b0a66-363">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b0a66-364">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0a66-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b0a66-365">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b0a66-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b0a66-366">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="b0a66-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="b0a66-367">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b0a66-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b0a66-368">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="b0a66-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b0a66-369">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="b0a66-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b0a66-370">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="b0a66-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b0a66-371">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="b0a66-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="b0a66-372">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="b0a66-373">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="b0a66-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="b0a66-374">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0a66-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="b0a66-375">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="b0a66-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="b0a66-376">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="b0a66-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="b0a66-377">Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.</span><span class="sxs-lookup"><span data-stu-id="b0a66-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="b0a66-378">Als deze stappen voor probleemoplossing niet Hallo Hallo probleem oplossen</span><span class="sxs-lookup"><span data-stu-id="b0a66-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="b0a66-379">Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="b0a66-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="b0a66-380">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="b0a66-380">Correlation error ID</span></span>

-   <span data-ttu-id="b0a66-381">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="b0a66-381">UPN (user email address)</span></span>

-   <span data-ttu-id="b0a66-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="b0a66-382">TenantID</span></span>

-   <span data-ttu-id="b0a66-383">Browsertype</span><span class="sxs-lookup"><span data-stu-id="b0a66-383">Browser type</span></span>

-   <span data-ttu-id="b0a66-384">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="b0a66-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="b0a66-385">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="b0a66-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0a66-386">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0a66-386">Next steps</span></span>
[<span data-ttu-id="b0a66-387">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="b0a66-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

