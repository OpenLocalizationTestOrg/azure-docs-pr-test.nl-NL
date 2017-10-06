---
title: aaaProblems tooan-galerie van Azure AD-toepassing die zijn geconfigureerd voor wachtwoord aanmelden eenmalige aanmelding | Microsoft Docs
description: Probleemgebieden die bieden richtlijnen tootroubleshoot problemen gerelateerde toosigning in tooAzure galerie AD-toepassingen die zijn geconfigureerd voor eenmalige aanmelding wachtwoord wordt beschreven
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="497c3-103">Problemen met aanmelden tooan-galerie van Azure AD-toepassing die zijn geconfigureerd voor eenmalige aanmelding wachtwoord</span><span class="sxs-lookup"><span data-stu-id="497c3-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="497c3-104">Hallo Toegangspaneel is een portal op Internet zodat een gebruiker met een werk- of school-account in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen of hello Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="497c3-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="497c3-105">Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en beheermogelijkheden van de app via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="497c3-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="497c3-106">Hallo Toegangspaneel is gescheiden van hello Azure-portal en vereist geen gebruikers toohave een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="497c3-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="497c3-107">toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="497c3-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="497c3-108">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="497c3-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="497c3-109">Vergadering Browservereisten voor Hallo Toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="497c3-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="497c3-110">Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="497c3-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="497c3-111">toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="497c3-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="497c3-112">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="497c3-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="497c3-113">Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:</span><span class="sxs-lookup"><span data-stu-id="497c3-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="497c3-114">Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="497c3-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="497c3-115">Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="497c3-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="497c3-116">Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="497c3-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="497c3-117">Hallo op basis van wachtwoorden SSO-extensie wordt beschikbaar voor de rand in de Windows 10 als browseruitbreidingen worden ondersteund voor de rand.</span><span class="sxs-lookup"><span data-stu-id="497c3-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="497c3-118">Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo</span><span class="sxs-lookup"><span data-stu-id="497c3-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="497c3-119">tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="497c3-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="497c3-120">Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="497c3-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="497c3-121">Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="497c3-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="497c3-122">Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="497c3-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="497c3-123">Op basis van uw browser zijn u gerichte toohello downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="497c3-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="497c3-124">**Voeg** Hallo extensie tooyour browser.</span><span class="sxs-lookup"><span data-stu-id="497c3-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="497c3-125">Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.</span><span class="sxs-lookup"><span data-stu-id="497c3-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="497c3-126">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="497c3-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="497c3-127">Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="497c3-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="497c3-128">U kunt ook Hallo-extensie voor Chrome en Firefox van Hallo rechtstreekse koppelingen hieronder downloaden:</span><span class="sxs-lookup"><span data-stu-id="497c3-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="497c3-129">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="497c3-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="497c3-130">Uitbreiding van het Configuratiescherm Firefox toegang</span><span class="sxs-lookup"><span data-stu-id="497c3-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="497c3-131">Instellen van een groepsbeleid voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="497c3-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="497c3-132">U kunt een groepsbeleid waarmee u tooremotely installeren Hallo Toegangsvenster extensie voor Internet Explorer op computers van uw gebruikers instellen.</span><span class="sxs-lookup"><span data-stu-id="497c3-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="497c3-133">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="497c3-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="497c3-134">U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u uw gebruikers machines tooyour domein hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="497c3-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="497c3-135">Hallo 'Instellingen bewerken' machtiging tooedit Hallo groepsbeleidsobject (GPO), moet u hebben.</span><span class="sxs-lookup"><span data-stu-id="497c3-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="497c3-136">Standaard hebben leden van beveiligingsgroepen na Hallo deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="497c3-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="497c3-137">[Meer informatie](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="497c3-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="497c3-138">Volg de zelfstudie Hallo [hoe tooDeploy Configuratiescherm-uitbreiding voor toegang voor Internet Explorer met behulp van Groepsbeleid Hallo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) voor stapsgewijze instructies over hoe tooconfigure Hallo Groepsbeleid en het toousers implementeren.</span><span class="sxs-lookup"><span data-stu-id="497c3-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="497c3-139">Hallo Toegangsvenster in Internet Explorer oplossen</span><span class="sxs-lookup"><span data-stu-id="497c3-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="497c3-140">Ga als volgt Hallo [oplossen Hallo Configuratiescherm-uitbreiding voor toegang voor Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) geleid voor toegang tot een diagnostische hulpprogramma's en stapsgewijze instructies over het configureren van Hallo-extensie voor IE.</span><span class="sxs-lookup"><span data-stu-id="497c3-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="497c3-141">Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="497c3-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="497c3-142">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="497c3-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="497c3-143">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="497c3-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="497c3-144">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="497c3-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="497c3-145">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="497c3-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="497c3-146">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="497c3-146">Add a non-gallery application</span></span>

<span data-ttu-id="497c3-147">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="497c3-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="497c3-148">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="497c3-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="497c3-149">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="497c3-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="497c3-150">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="497c3-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="497c3-151">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="497c3-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="497c3-152">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="497c3-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="497c3-153">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="497c3-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="497c3-154">Vul in Hallo Hallo-naam van uw toepassing **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="497c3-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="497c3-155">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="497c3-155">Select **Add.**</span></span>

<span data-ttu-id="497c3-156">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="497c3-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="497c3-157">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="497c3-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="497c3-158">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="497c3-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="497c3-159">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="497c3-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="497c3-160">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="497c3-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="497c3-161">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="497c3-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="497c3-162">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="497c3-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="497c3-163">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="497c3-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="497c3-164">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="497c3-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="497c3-165">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="497c3-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="497c3-166">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="497c3-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="497c3-167">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="497c3-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="497c3-168">Voer Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="497c3-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="497c3-169">Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen.</span><span class="sxs-lookup"><span data-stu-id="497c3-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="497c3-170">Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="497c3-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="497c3-171">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="497c3-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="497c3-172">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="497c3-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="497c3-173">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="497c3-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="497c3-174">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="497c3-174">Assign users toohello application</span></span>

<span data-ttu-id="497c3-175">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="497c3-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="497c3-176">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="497c3-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="497c3-177">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="497c3-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="497c3-178">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="497c3-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="497c3-179">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="497c3-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="497c3-180">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="497c3-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="497c3-181">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="497c3-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="497c3-182">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="497c3-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="497c3-183">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="497c3-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="497c3-184">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="497c3-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="497c3-185">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="497c3-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="497c3-186">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="497c3-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="497c3-187">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="497c3-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="497c3-188">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="497c3-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="497c3-189">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="497c3-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="497c3-190">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="497c3-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="497c3-191">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="497c3-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="497c3-192">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="497c3-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="497c3-193">Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.</span><span class="sxs-lookup"><span data-stu-id="497c3-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="497c3-194">Als deze stappen voor probleemoplossing niet Hallo Hallo probleem oplossen</span><span class="sxs-lookup"><span data-stu-id="497c3-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="497c3-195">Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="497c3-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="497c3-196">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="497c3-196">Correlation error ID</span></span>

-   <span data-ttu-id="497c3-197">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="497c3-197">UPN (user email address)</span></span>

-   <span data-ttu-id="497c3-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="497c3-198">TenantID</span></span>

-   <span data-ttu-id="497c3-199">Browsertype</span><span class="sxs-lookup"><span data-stu-id="497c3-199">Browser type</span></span>

-   <span data-ttu-id="497c3-200">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="497c3-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="497c3-201">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="497c3-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="497c3-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="497c3-202">Next steps</span></span>
[<span data-ttu-id="497c3-203">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="497c3-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

