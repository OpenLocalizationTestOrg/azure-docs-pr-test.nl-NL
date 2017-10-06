---
title: aaaProblem toohello toegang Configuratiescherm website aanmelden | Microsoft Docs
description: Richtlijnen tootroubleshoot problemen die optreden kunnen tijdens een poging toosign in toouse Hallo Toegangsvenster
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="f85e7-103">Probleem bij aanmelden toohello toegang Configuratiescherm website</span><span class="sxs-lookup"><span data-stu-id="f85e7-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="f85e7-104">Hallo Toegangspaneel is een portal op Internet zodat een gebruiker met een werk- of school-account in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen of hello Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="f85e7-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="f85e7-105">Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en beheermogelijkheden van de app via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f85e7-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="f85e7-106">Hallo Toegangspaneel is gescheiden van hello Azure-portal en vereist geen gebruikers toohave een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f85e7-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="f85e7-107">In het deelvenster toegang toohello kunnen gebruikers zich aanmelden als ze een account voor werk of school in Azure AD hebben.</span><span class="sxs-lookup"><span data-stu-id="f85e7-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="f85e7-108">Gebruikers kunnen worden geverifieerd door Azure AD rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="f85e7-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="f85e7-109">Gebruikers kunnen worden geverifieerd met behulp van Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="f85e7-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="f85e7-110">Gebruikers kunnen worden geverifieerd door Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f85e7-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="f85e7-111">Als een gebruiker een abonnement voor Azure of Office 365 heeft en de hello Azure-portal of een Office 365-toepassing gebruikt, moet ze kunnen toouse Hallo Toegangsvenster naadloos opnieuw zonder toosign in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="f85e7-112">Gebruikers die niet worden geverifieerd worden na vragen aan gebruiker toosign in met behulp van Hallo gebruikersnaam en wachtwoord voor hun account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f85e7-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="f85e7-113">Als de organisatie Hallo heeft federation geconfigureerd, is te typen Hallo gebruikersnaam voldoende.</span><span class="sxs-lookup"><span data-stu-id="f85e7-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="f85e7-114">Algemene problemen toocheck eerst</span><span class="sxs-lookup"><span data-stu-id="f85e7-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="f85e7-115">Zorg ervoor dat het Hallo-gebruiker zich aanmeldt toohello **Corrigeer URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="f85e7-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="f85e7-116">Zorg ervoor dat de browser van de gebruiker Hallo Hallo URL tooits is toegevoegd **vertrouwde sites**</span><span class="sxs-lookup"><span data-stu-id="f85e7-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="f85e7-117">Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="f85e7-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="f85e7-118">Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="f85e7-119">Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="f85e7-120">Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="f85e7-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="f85e7-121">Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="f85e7-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="f85e7-122">Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="f85e7-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="f85e7-123">Zorg ervoor dat tooalso probeer wissen van cookies in uw browser opnieuw te proberen toosign in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="f85e7-124">Vergadering Browservereisten voor Hallo Toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="f85e7-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="f85e7-125">Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f85e7-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="f85e7-126">toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f85e7-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="f85e7-127">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="f85e7-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="f85e7-128">Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:</span><span class="sxs-lookup"><span data-stu-id="f85e7-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="f85e7-129">Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="f85e7-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="f85e7-130">Rand verjaardagseditie van Windows 10 of hoger</span><span class="sxs-lookup"><span data-stu-id="f85e7-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="f85e7-131">Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="f85e7-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="f85e7-132">Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="f85e7-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="f85e7-133">Problemen met Hallo gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="f85e7-133">Problems with hello user’s account</span></span>

<span data-ttu-id="f85e7-134">Toegang tot toohello die toegangspaneel vanwege een probleem met Hallo gebruikersaccount tooa kunnen worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="f85e7-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="f85e7-135">Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met gebruikers en hun Accountinstellingen:</span><span class="sxs-lookup"><span data-stu-id="f85e7-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="f85e7-136">Controleer of er een gebruikersaccount in Azure Active Directory bestaat</span><span class="sxs-lookup"><span data-stu-id="f85e7-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="f85e7-137">Controleer de status van de account van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="f85e7-138">Een gebruiker-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="f85e7-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="f85e7-139">Selfservice voor wachtwoordherstel inschakelen</span><span class="sxs-lookup"><span data-stu-id="f85e7-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="f85e7-140">Controleer de status van een gebruiker multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="f85e7-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="f85e7-141">Controleer de contactgegevens van de verificatie van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="f85e7-142">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="f85e7-143">Controleer de toegewezen licenties van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="f85e7-144">Een gebruiker een licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="f85e7-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="f85e7-145">Controleer of er een gebruikersaccount in Azure Active Directory bestaat</span><span class="sxs-lookup"><span data-stu-id="f85e7-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="f85e7-146">toocheck als aanwezig is, is van een gebruikersaccount Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="f85e7-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-147">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-148">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-149">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-150">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-151">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-151">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-152">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f85e7-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f85e7-153">Controleer de eigenschappen Hallo van Hallo gebruiker object toobe zeker van te zijn dat ze zo uitzien als u verwacht en er worden geen gegevens ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="f85e7-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="f85e7-154">Controleer de status van de account van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-154">Check a user’s account status</span></span>

<span data-ttu-id="f85e7-155">toocheck een gebruiker van account status, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="f85e7-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-156">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-157">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-158">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-159">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-160">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-160">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-161">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f85e7-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f85e7-162">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-162">click **Profile**.</span></span>

8.  <span data-ttu-id="f85e7-163">Onder **instellingen** ervoor te zorgen dat **blok aanmelden** te is ingesteld,**Nee**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="f85e7-164">Een gebruiker-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="f85e7-164">Reset a user’s password</span></span>

<span data-ttu-id="f85e7-165">tooreset het gebruikerswachtwoord Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="f85e7-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-166">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-167">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-168">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-169">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-170">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-170">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-171">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f85e7-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f85e7-172">Klik op Hallo **wachtwoord opnieuw instellen** knop bovenaan Hallo Hallo gebruiker blade.</span><span class="sxs-lookup"><span data-stu-id="f85e7-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="f85e7-173">Klik op Hallo **wachtwoord opnieuw instellen** knop op Hallo **wachtwoord opnieuw instellen** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f85e7-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="f85e7-174">Kopiëren Hallo **tijdelijk wachtwoord** of **een nieuw wachtwoord invoeren** voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f85e7-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="f85e7-175">Deze nieuwe gebruiker met wachtwoord toohello communiceren, kunnen ze vereist toochange dit wachtwoord tijdens de volgende aanmelden tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f85e7-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="f85e7-176">Selfservice voor wachtwoordherstel inschakelen</span><span class="sxs-lookup"><span data-stu-id="f85e7-176">Enable self-service password reset</span></span>

<span data-ttu-id="f85e7-177">tooenable zelf uw wachtwoord opnieuw instellen, Hallo implementatie volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="f85e7-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="f85e7-178">Tooreset gebruikers hun wachtwoorden met Azure Active Directory inschakelen</span><span class="sxs-lookup"><span data-stu-id="f85e7-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="f85e7-179">Inschakelen van gebruikers tooreset of hun on-premises Active Directory wachtwoorden wijzigen</span><span class="sxs-lookup"><span data-stu-id="f85e7-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="f85e7-180">Controleer de status van een gebruiker multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="f85e7-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="f85e7-181">toocheck een gebruiker de multi-factor authentication status, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="f85e7-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-182">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-183">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-184">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-185">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-186">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-186">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-187">Klik op Hallo **multi-Factor Authentication** knop Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="f85e7-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="f85e7-188">Eenmaal Hallo **multi-factor Authentication-beheerportal** laadt, zorg ervoor dat u op Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f85e7-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="f85e7-189">Hallo-gebruiker in de lijst met gebruikers Hallo vinden door te zoeken, filteren of sorteren.</span><span class="sxs-lookup"><span data-stu-id="f85e7-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="f85e7-190">Selecteer Hallo gebruiker uit Hallo lijst met gebruikers en **inschakelen**, **uitschakelen**, of **afdwingen** multi-factor authentication-server naar wens.</span><span class="sxs-lookup"><span data-stu-id="f85e7-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f85e7-191">Als een gebruiker zich in een **afgedwongen** staat, kunt u ze te instellen**uitgeschakelde** tijdelijk toolet deze terug te zetten bij hun account.</span><span class="sxs-lookup"><span data-stu-id="f85e7-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="f85e7-192">Wanneer ze terug in bent, kunt u wijzigen hun status te**ingeschakeld** opnieuw toorequire ze hun contactgegevens tijdens de volgende Meld u aan de toore registratie.</span><span class="sxs-lookup"><span data-stu-id="f85e7-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="f85e7-193">U kunt ook u kunt stappen Hallo in Hallo [controleren van de contactgegevens van de verificatie van een gebruiker](#check-a-users-authentication-contact-info) tooverify of instellen van deze gegevens voor deze.</span><span class="sxs-lookup"><span data-stu-id="f85e7-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="f85e7-194">Controleer de contactgegevens van de verificatie van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="f85e7-195">verificatie van een gebruiker contactgegevens gebruikt voor multi-factor authentication, voorwaardelijke toegang, Identity Protection en het wachtwoord opnieuw instellen, toocheck Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="f85e7-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-196">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-197">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-198">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-199">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-200">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-200">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-201">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f85e7-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f85e7-202">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-202">click **Profile**.</span></span>

8.  <span data-ttu-id="f85e7-203">Schuif naar beneden te**verificatie contactgegevens**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="f85e7-204">**Bekijk** Hallo gegevens geregistreerd voor Hallo gebruiker en de update zo nodig.</span><span class="sxs-lookup"><span data-stu-id="f85e7-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="f85e7-205">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-205">Check a user’s group memberships</span></span>

<span data-ttu-id="f85e7-206">toocheck een gebruiker van groepslidmaatschappen, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="f85e7-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-207">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-208">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-209">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-210">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-211">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-211">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-212">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f85e7-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f85e7-213">Klik op **groepen** toosee die Hallo gebruiker groepen lid van is.</span><span class="sxs-lookup"><span data-stu-id="f85e7-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="f85e7-214">Controleer de toegewezen licenties van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f85e7-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="f85e7-215">toocheck een gebruiker de toegewezen licenties, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="f85e7-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-216">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-217">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-218">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-219">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-220">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-220">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-221">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f85e7-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f85e7-222">Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f85e7-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="f85e7-223">Een gebruiker een licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="f85e7-223">Assign a user a license</span></span> 

<span data-ttu-id="f85e7-224">een gebruiker van de tooa licentie tooassign Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="f85e7-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="f85e7-225">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="f85e7-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f85e7-226">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f85e7-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f85e7-227">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f85e7-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f85e7-228">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f85e7-229">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f85e7-229">click **All users**.</span></span>

6.  <span data-ttu-id="f85e7-230">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f85e7-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f85e7-231">Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f85e7-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="f85e7-232">Klik op Hallo **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="f85e7-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="f85e7-233">Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.</span><span class="sxs-lookup"><span data-stu-id="f85e7-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="f85e7-234">**Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f85e7-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="f85e7-235">Klik op **Ok** wanneer dit is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f85e7-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="f85e7-236">Klik op Hallo **toewijzen** knop tooassign deze licenties toothis-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f85e7-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="f85e7-237">Als u deze stappen voor probleemoplossing Hallo probleem niet verhelpen</span><span class="sxs-lookup"><span data-stu-id="f85e7-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="f85e7-238">Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="f85e7-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="f85e7-239">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="f85e7-239">Correlation error ID</span></span>

-   <span data-ttu-id="f85e7-240">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="f85e7-240">UPN (user email address)</span></span>

-   <span data-ttu-id="f85e7-241">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="f85e7-241">Tenant ID</span></span>

-   <span data-ttu-id="f85e7-242">Browsertype</span><span class="sxs-lookup"><span data-stu-id="f85e7-242">Browser type</span></span>

-   <span data-ttu-id="f85e7-243">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="f85e7-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="f85e7-244">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="f85e7-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="f85e7-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f85e7-245">Next steps</span></span>
[<span data-ttu-id="f85e7-246">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="f85e7-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
