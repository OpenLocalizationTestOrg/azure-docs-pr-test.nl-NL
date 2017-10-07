---
title: aaaProblems tooan toepassing met behulp van een deeplink aanmelden | Microsoft Docs
description: Hoe tootroubleshoot problemen met toegang tot een toepassing van een gebruikmaken van Azure AD-deeplink-URL
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="c9454-103">Problemen met aanmelden met een deeplink tooan-toepassing</span><span class="sxs-lookup"><span data-stu-id="c9454-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="c9454-104">Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="c9454-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="c9454-105">Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="c9454-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="c9454-106">Hallo-toepassing moet correct worden geconfigureerd en toegewezen toohello gebruiker of een groep Hallo-gebruiker lid is van toepassing op Hallo toosee in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c9454-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="c9454-107">Dieptekoppelingen of toegang voor gebruikers zijn URL's koppelingen die uw gebruikers hun wachtwoord SSO-toepassingen rechtstreeks vanuit hun browser-URL balken van tooaccess kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9454-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="c9454-108">Door te navigeren toothis koppeling, worden gebruikers automatisch aangemeld bij de toepassing hello zonder toogo toohello Toegangspaneel eerst.</span><span class="sxs-lookup"><span data-stu-id="c9454-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="c9454-109">Dit is Hallo dezelfde koppeling die gebruikers tooaccess deze toepassingen vanuit Office 365 Hallo toepassing starten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9454-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="c9454-110">Algemene problemen toocheck eerst</span><span class="sxs-lookup"><span data-stu-id="c9454-110">General issues toocheck first</span></span>

-   <span data-ttu-id="c9454-111">Zorg ervoor dat uw met een **browser** die voldoet aan de minimale vereisten van de Hallo voor Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c9454-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="c9454-112">Zorg ervoor dat de browser van Hallo gebruiker is toegevoegd Hallo-URL van Hallo toepassing tooits **vertrouwde websites**.</span><span class="sxs-lookup"><span data-stu-id="c9454-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="c9454-113">Zorg ervoor dat toocheck Hallo toepassing **geconfigureerd** correct.</span><span class="sxs-lookup"><span data-stu-id="c9454-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="c9454-114">Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="c9454-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="c9454-115">Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**</span><span class="sxs-lookup"><span data-stu-id="c9454-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="c9454-116">Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.**</span><span class="sxs-lookup"><span data-stu-id="c9454-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="c9454-117">Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="c9454-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="c9454-118">Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="c9454-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="c9454-119">Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="c9454-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="c9454-120">Zorg ervoor dat tooalso probeer wissen van cookies in uw browser opnieuw te proberen toosign in.</span><span class="sxs-lookup"><span data-stu-id="c9454-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="c9454-121">Hallo-deeplink-controle</span><span class="sxs-lookup"><span data-stu-id="c9454-121">Checking hello deeplink</span></span>

<span data-ttu-id="c9454-122">toocheck hebt u de juiste deeplink hello, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c9454-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="c9454-123">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c9454-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c9454-124">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c9454-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9454-125">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c9454-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9454-126">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9454-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9454-127">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9454-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c9454-128">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c9454-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c9454-129">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c9454-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="c9454-130">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c9454-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9454-131">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c9454-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="c9454-132">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9454-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="c9454-133">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9454-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c9454-134">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c9454-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="c9454-135">Selecteer gewenste Hallo selectievakje Hallo deeplink voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9454-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="c9454-136">Hallo-label vinden **toegangs-URL van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="c9454-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="c9454-137">U deeplink moet overeenkomen met deze URL.</span><span class="sxs-lookup"><span data-stu-id="c9454-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="c9454-138">Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo</span><span class="sxs-lookup"><span data-stu-id="c9454-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="c9454-139">tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c9454-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="c9454-140">Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9454-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="c9454-141">Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c9454-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="c9454-142">Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="c9454-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="c9454-143">Op basis van uw browser zijn u gerichte toohello downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="c9454-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="c9454-144">**Voeg** Hallo extensie tooyour browser.</span><span class="sxs-lookup"><span data-stu-id="c9454-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="c9454-145">Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.</span><span class="sxs-lookup"><span data-stu-id="c9454-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="c9454-146">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="c9454-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="c9454-147">Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="c9454-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="c9454-148">U kunt ook Hallo-extensie voor Chrome en Firefox van Hallo rechtstreekse koppelingen hieronder downloaden:</span><span class="sxs-lookup"><span data-stu-id="c9454-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="c9454-149">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="c9454-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="c9454-150">Uitbreiding van het Configuratiescherm Firefox toegang</span><span class="sxs-lookup"><span data-stu-id="c9454-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="c9454-151">Hoe tooconfigure wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9454-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="c9454-152">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="c9454-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="c9454-153">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="c9454-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="c9454-154">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="c9454-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="c9454-155">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="c9454-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="c9454-156">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c9454-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="c9454-157">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="c9454-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="c9454-158">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c9454-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9454-159">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c9454-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9454-160">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9454-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9454-161">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="c9454-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="c9454-162">In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="c9454-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="c9454-163">Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9454-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="c9454-164">Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="c9454-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="c9454-165">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9454-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="c9454-166">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9454-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="c9454-167">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="c9454-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="c9454-168">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="c9454-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c9454-169">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c9454-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c9454-170">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c9454-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9454-171">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c9454-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9454-172">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9454-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9454-173">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9454-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c9454-174">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c9454-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c9454-175">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c9454-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c9454-176">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="c9454-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9454-177">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="c9454-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c9454-178">[Gebruikers toewijzen toohello toepassing](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="c9454-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="c9454-179">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c9454-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="c9454-180">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="c9454-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="c9454-181">Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="c9454-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="c9454-182">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="c9454-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="c9454-183">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="c9454-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="c9454-184">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="c9454-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="c9454-185">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="c9454-185">Add a non-gallery application</span></span>

<span data-ttu-id="c9454-186">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c9454-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="c9454-187">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="c9454-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="c9454-188">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c9454-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9454-189">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c9454-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9454-190">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9454-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9454-191">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="c9454-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="c9454-192">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="c9454-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="c9454-193">Vul in Hallo Hallo-naam van uw toepassing **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="c9454-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="c9454-194">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="c9454-194">Select **Add.**</span></span>

<span data-ttu-id="c9454-195">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9454-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="c9454-196">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="c9454-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="c9454-197">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="c9454-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c9454-198">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c9454-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c9454-199">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c9454-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9454-200">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c9454-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9454-201">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9454-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9454-202">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9454-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="c9454-203">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c9454-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c9454-204">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c9454-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c9454-205">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="c9454-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9454-206">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="c9454-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c9454-207">Voer Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="c9454-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="c9454-208">Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen.</span><span class="sxs-lookup"><span data-stu-id="c9454-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="c9454-209">Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="c9454-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="c9454-210">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c9454-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="c9454-211">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c9454-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="c9454-212">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="c9454-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="c9454-213">Hoe een gebruiker tooan toepassing rechtstreeks tooassign</span><span class="sxs-lookup"><span data-stu-id="c9454-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="c9454-214">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c9454-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="c9454-215">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c9454-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c9454-216">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c9454-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9454-217">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c9454-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9454-218">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9454-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9454-219">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9454-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c9454-220">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c9454-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c9454-221">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="c9454-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="c9454-222">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="c9454-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9454-223">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="c9454-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="c9454-224">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="c9454-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="c9454-225">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="c9454-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="c9454-226">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="c9454-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="c9454-227">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="c9454-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="c9454-228">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="c9454-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="c9454-229">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9454-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="c9454-230">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c9454-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="c9454-231">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c9454-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="c9454-232">Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.</span><span class="sxs-lookup"><span data-stu-id="c9454-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="c9454-233">Als u deze stappen voor probleemoplossing niet Hallo Hallo probleem oplossen</span><span class="sxs-lookup"><span data-stu-id="c9454-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="c9454-234">Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="c9454-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="c9454-235">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="c9454-235">Correlation error ID</span></span>

-   <span data-ttu-id="c9454-236">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="c9454-236">UPN (user email address)</span></span>

-   <span data-ttu-id="c9454-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="c9454-237">TenantID</span></span>

-   <span data-ttu-id="c9454-238">Browsertype</span><span class="sxs-lookup"><span data-stu-id="c9454-238">Browser type</span></span>

-   <span data-ttu-id="c9454-239">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="c9454-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="c9454-240">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="c9454-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9454-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9454-241">Next steps</span></span>
[<span data-ttu-id="c9454-242">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="c9454-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
