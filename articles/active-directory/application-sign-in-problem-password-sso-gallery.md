---
title: aaaProblems aanmelden tooan-galerie van Azure AD-toepassing is geconfigureerd voor federatieve eenmalige aanmelding | Microsoft Docs
description: Hoe tootroubleshoot problemen met de galerie van Azure AD-toepassing die zijn geconfigureerd voor eenmalige aanmelding wachtwoord
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="51725-103">Problemen met aanmelden tooan-galerie van Azure AD-toepassing die zijn geconfigureerd voor federatieve eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="51725-103">Problems signing in tooan Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="51725-104">Hallo Toegangspaneel is een portal op Internet zodat een gebruiker met een werk- of school-account in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen of hello Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="51725-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="51725-105">Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en beheermogelijkheden van de app via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="51725-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="51725-106">Hallo Toegangspaneel is gescheiden van hello Azure-portal en vereist geen gebruikers toohave een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="51725-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="51725-107">toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="51725-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="51725-108">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="51725-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="51725-109">Vergadering Browservereisten voor Hallo Toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="51725-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="51725-110">Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="51725-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="51725-111">toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="51725-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="51725-112">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="51725-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="51725-113">Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:</span><span class="sxs-lookup"><span data-stu-id="51725-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="51725-114">Internet Explorer 8, 9, 10, 11 - in Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="51725-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="51725-115">Chrome - in Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="51725-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="51725-116">Firefox 26,0 of later - op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="51725-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="51725-117">Hallo op basis van wachtwoorden SSO-extensie wordt beschikbaar voor de rand in de Windows 10 als browseruitbreidingen worden ondersteund voor de rand.</span><span class="sxs-lookup"><span data-stu-id="51725-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="51725-118">Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo</span><span class="sxs-lookup"><span data-stu-id="51725-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="51725-119">tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="51725-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="51725-120">Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51725-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="51725-121">Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="51725-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="51725-122">Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="51725-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="51725-123">Op basis van uw browser zijn u gerichte toohello downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="51725-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="51725-124">**Voeg** Hallo extensie tooyour browser.</span><span class="sxs-lookup"><span data-stu-id="51725-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="51725-125">Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.</span><span class="sxs-lookup"><span data-stu-id="51725-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="51725-126">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="51725-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="51725-127">Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="51725-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="51725-128">U kunt ook Hallo-extensie voor Chrome en Firefox van Hallo rechtstreekse koppelingen hieronder downloaden:</span><span class="sxs-lookup"><span data-stu-id="51725-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="51725-129">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="51725-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="51725-130">Uitbreiding van het Configuratiescherm Firefox toegang</span><span class="sxs-lookup"><span data-stu-id="51725-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="51725-131">Instellen van een groepsbeleid voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="51725-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="51725-132">U kunt een groepsbeleid waarmee u tooremotely installeren Hallo Toegangsvenster extensie voor Internet Explorer op computers van uw gebruikers instellen.</span><span class="sxs-lookup"><span data-stu-id="51725-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="51725-133">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="51725-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="51725-134">U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u uw gebruikers machines tooyour domein hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="51725-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="51725-135">Hallo 'Instellingen bewerken' machtiging tooedit Hallo groepsbeleidsobject (GPO), moet u hebben.</span><span class="sxs-lookup"><span data-stu-id="51725-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="51725-136">Standaard hebben leden van beveiligingsgroepen na Hallo deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="51725-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="51725-137">[Meer informatie](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="51725-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="51725-138">Volg de zelfstudie Hallo [hoe tooDeploy Configuratiescherm-uitbreiding voor toegang voor Internet Explorer met behulp van Groepsbeleid Hallo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) voor stapsgewijze instructies over hoe tooconfigure Hallo Groepsbeleid en het toousers implementeren.</span><span class="sxs-lookup"><span data-stu-id="51725-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="51725-139">Hallo Toegangsvenster in Internet Explorer oplossen</span><span class="sxs-lookup"><span data-stu-id="51725-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="51725-140">Ga als volgt Hallo [oplossen Hallo Configuratiescherm-uitbreiding voor toegang voor Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) geleid voor toegang tot een diagnostische hulpprogramma's en stapsgewijze instructies over het configureren van Hallo-extensie voor IE.</span><span class="sxs-lookup"><span data-stu-id="51725-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="51725-141">Hoe tooconfigure wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="51725-141">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="51725-142">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="51725-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="51725-143">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="51725-143">Add an application from hello Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="51725-144">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="51725-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="51725-145">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="51725-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="51725-146">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="51725-146">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="51725-147">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="51725-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="51725-148">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="51725-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="51725-149">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="51725-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="51725-150">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="51725-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="51725-151">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="51725-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="51725-152">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="51725-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="51725-153">In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="51725-153">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="51725-154">Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="51725-154">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="51725-155">Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="51725-155">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="51725-156">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="51725-156">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="51725-157">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="51725-157">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="51725-158">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="51725-158">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="51725-159">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="51725-159">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="51725-160">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="51725-160">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="51725-161">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="51725-161">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="51725-162">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="51725-162">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="51725-163">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="51725-163">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="51725-164">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="51725-164">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="51725-165">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="51725-165">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="51725-166">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="51725-166">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="51725-167">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="51725-167">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="51725-168">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="51725-168">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="51725-169">[Gebruikers toewijzen toohello toepassing](#_How_to_assign).</span><span class="sxs-lookup"><span data-stu-id="51725-169">[Assign users toohello application](#_How_to_assign).</span></span>

10. <span data-ttu-id="51725-170">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="51725-170">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="51725-171">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="51725-171">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="51725-172">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="51725-172">Assign users toohello application</span></span>

<span data-ttu-id="51725-173">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="51725-173">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="51725-174">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="51725-174">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="51725-175">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="51725-175">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="51725-176">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="51725-176">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="51725-177">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="51725-177">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="51725-178">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="51725-178">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="51725-179">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="51725-179">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="51725-180">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="51725-180">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="51725-181">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="51725-181">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="51725-182">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="51725-182">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="51725-183">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="51725-183">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="51725-184">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="51725-184">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="51725-185">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="51725-185">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="51725-186">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="51725-186">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="51725-187">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="51725-187">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="51725-188">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="51725-188">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="51725-189">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="51725-189">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="51725-190">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="51725-190">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="51725-191">Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.</span><span class="sxs-lookup"><span data-stu-id="51725-191">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a><span data-ttu-id="51725-192">Als deze fout opsporen oplossen stappen Hallo probleem niet</span><span class="sxs-lookup"><span data-stu-id="51725-192">If these troubleshoot steps don't resolve hello issue</span></span> 
<span data-ttu-id="51725-193">Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="51725-193">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="51725-194">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="51725-194">Correlation error ID</span></span>

-   <span data-ttu-id="51725-195">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="51725-195">UPN (user email address)</span></span>

-   <span data-ttu-id="51725-196">TenantID</span><span class="sxs-lookup"><span data-stu-id="51725-196">TenantID</span></span>

-   <span data-ttu-id="51725-197">Browsertype</span><span class="sxs-lookup"><span data-stu-id="51725-197">Browser type</span></span>

-   <span data-ttu-id="51725-198">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="51725-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="51725-199">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="51725-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="51725-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51725-200">Next steps</span></span>
[<span data-ttu-id="51725-201">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="51725-201">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
