---
title: Aanmelden bij de website van het deelvenster toegang probleem | Microsoft Docs
description: Richtlijnen voor het oplossen van problemen die optreden kunnen tijdens het aanmelden voor gebruik van het toegangsvenster
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
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="df47d-103">Aanmelden bij de website van het deelvenster toegang probleem</span><span class="sxs-lookup"><span data-stu-id="df47d-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="df47d-104">Het Toegangspaneel is een portal op Internet waarmee een gebruiker met een account voor werk of school in Azure Active Directory (Azure AD) voor weergave in en start cloud-gebaseerde toepassingen die de Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="df47d-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="df47d-105">Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en app-mogelijkheden voor beheer via het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="df47d-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="df47d-106">Het Toegangspaneel is gescheiden van de Azure-portal en vereist geen gebruikers een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="df47d-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="df47d-107">Gebruikers kunnen aanmelden bij het toegangsvenster als ze een account voor werk of school in Azure AD hebben.</span><span class="sxs-lookup"><span data-stu-id="df47d-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="df47d-108">Gebruikers kunnen worden geverifieerd door Azure AD rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="df47d-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="df47d-109">Gebruikers kunnen worden geverifieerd met behulp van Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="df47d-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="df47d-110">Gebruikers kunnen worden geverifieerd door Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df47d-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="df47d-111">Als een gebruiker een abonnement voor Azure of Office 365 heeft en de Azure portal of een Office 365-toepassing heeft gebruikt, is het waarschijnlijk dat ze gebruikmaken van het toegangsvenster naadloos zonder opnieuw aanmelden.</span><span class="sxs-lookup"><span data-stu-id="df47d-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="df47d-112">Gebruikers die niet worden geverifieerd gevraagd aan te melden met behulp van de gebruikersnaam en het wachtwoord voor hun account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df47d-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="df47d-113">Als de organisatie heeft federation geconfigureerd, is typt de gebruikersnaam voldoende.</span><span class="sxs-lookup"><span data-stu-id="df47d-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="df47d-114">Algemene problemen om eerst te controleren</span><span class="sxs-lookup"><span data-stu-id="df47d-114">General issues to check first</span></span> 

-   <span data-ttu-id="df47d-115">Zorg ervoor dat de gebruiker is aangemeld bij de **Corrigeer URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="df47d-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="df47d-116">Zorg ervoor dat de browser van de gebruiker is toegevoegd de URL van de **vertrouwde sites**</span><span class="sxs-lookup"><span data-stu-id="df47d-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="df47d-117">Zorg ervoor dat het gebruikersaccount **ingeschakeld** voor aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="df47d-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="df47d-118">Zorg ervoor dat het gebruikersaccount **niet is vergrendeld.**</span><span class="sxs-lookup"><span data-stu-id="df47d-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="df47d-119">Zorg ervoor dat de gebruiker **wachtwoord niet is verlopen of is vergeten.**</span><span class="sxs-lookup"><span data-stu-id="df47d-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="df47d-120">Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="df47d-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="df47d-121">Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="df47d-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="df47d-122">Zorg ervoor dat een gebruiker **verificatie contactgegevens** is up-to-date houden om toe te staan van multi-factor Authentication of voorwaardelijk beleid worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="df47d-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="df47d-123">Zorg ervoor dat ook moet worden geprobeerd wissen van cookies in uw browser en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="df47d-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="df47d-124">Vergadering Browservereisten voor het toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="df47d-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="df47d-125">Het toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="df47d-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="df47d-126">Als u wilt gebruiken op basis van wachtwoorden eenmalige aanmelding (SSO) in het deelvenster toegang, moet de extensie Toegangspaneel worden geïnstalleerd in de browser van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="df47d-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="df47d-127">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="df47d-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="df47d-128">Voor eenmalige aanmelding op basis van wachtwoorden kunnen van de eindgebruiker browsers zijn:</span><span class="sxs-lookup"><span data-stu-id="df47d-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="df47d-129">Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="df47d-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="df47d-130">Rand verjaardagseditie van Windows 10 of hoger</span><span class="sxs-lookup"><span data-stu-id="df47d-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="df47d-131">Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="df47d-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="df47d-132">Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="df47d-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="df47d-133">Problemen met het gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="df47d-133">Problems with the user’s account</span></span>

<span data-ttu-id="df47d-134">Toegang tot het toegangsvenster kan worden geblokkeerd door een probleem met het gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="df47d-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="df47d-135">Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met gebruikers en hun Accountinstellingen:</span><span class="sxs-lookup"><span data-stu-id="df47d-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="df47d-136">Controleer of er een gebruikersaccount in Azure Active Directory bestaat</span><span class="sxs-lookup"><span data-stu-id="df47d-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="df47d-137">Controleer de status van de account van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="df47d-138">Een gebruiker-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="df47d-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="df47d-139">Selfservice voor wachtwoordherstel inschakelen</span><span class="sxs-lookup"><span data-stu-id="df47d-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="df47d-140">Controleer de status van een gebruiker multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="df47d-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="df47d-141">Controleer de contactgegevens van de verificatie van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="df47d-142">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="df47d-143">Controleer de toegewezen licenties van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="df47d-144">Een gebruiker een licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="df47d-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="df47d-145">Controleer of er een gebruikersaccount in Azure Active Directory bestaat</span><span class="sxs-lookup"><span data-stu-id="df47d-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="df47d-146">Als u wilt controleren of de account van een gebruiker aanwezig is, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-147">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-148">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-149">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-150">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-151">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-151">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-152">**Search** voor de gebruiker die u geïnteresseerd bent in en **klikt u op de rij** om te selecteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="df47d-153">Controleer de eigenschappen van het gebruikersobject om ervoor te zorgen dat ze zo uitzien als u verwacht en er worden geen gegevens ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="df47d-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="df47d-154">Controleer de status van de account van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-154">Check a user’s account status</span></span>

<span data-ttu-id="df47d-155">Als u wilt controleren accountstatus van een gebruiker, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-156">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-157">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-158">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-159">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-160">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-160">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-161">**Search** voor de gebruiker die u geïnteresseerd bent in en **klikt u op de rij** om te selecteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="df47d-162">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="df47d-162">click **Profile**.</span></span>

8.  <span data-ttu-id="df47d-163">Onder **instellingen** ervoor te zorgen dat **blok aanmelden** is ingesteld op **Nee**.</span><span class="sxs-lookup"><span data-stu-id="df47d-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="df47d-164">Een gebruiker-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="df47d-164">Reset a user’s password</span></span>

<span data-ttu-id="df47d-165">Als u het wachtwoord van een gebruiker herstellen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-166">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-167">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-168">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-169">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-170">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-170">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-171">**Search** voor de gebruiker die u geïnteresseerd bent in en **klikt u op de rij** om te selecteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="df47d-172">Klik op de **wachtwoord opnieuw instellen** knop aan de bovenkant van de gebruiker-blade.</span><span class="sxs-lookup"><span data-stu-id="df47d-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="df47d-173">Klik op de **wachtwoord opnieuw instellen** knop op de **wachtwoord opnieuw instellen** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="df47d-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="df47d-174">Kopieer de **tijdelijk wachtwoord** of **een nieuw wachtwoord invoeren** voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="df47d-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="df47d-175">Het nieuwe wachtwoord voor de gebruiker te communiceren, ze moeten dit wachtwoord wijzigen tijdens de volgende aanmelding in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df47d-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="df47d-176">Selfservice voor wachtwoordherstel inschakelen</span><span class="sxs-lookup"><span data-stu-id="df47d-176">Enable self-service password reset</span></span>

<span data-ttu-id="df47d-177">Voer de volgende stappen uit de implementatie zodat selfservice voor wachtwoordherstel:</span><span class="sxs-lookup"><span data-stu-id="df47d-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="df47d-178">Kunnen gebruikers hun Azure Active Directory-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="df47d-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="df47d-179">Kunnen gebruikers opnieuw instellen of hun on-premises Active Directory wachtwoorden wijzigen</span><span class="sxs-lookup"><span data-stu-id="df47d-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="df47d-180">Controleer de status van een gebruiker multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="df47d-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="df47d-181">Een gebruiker multi-factor authentication-server om status te controleren, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-182">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-183">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-184">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-185">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-186">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-186">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-187">Klik op de **multi-Factor Authentication** knop aan de bovenkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="df47d-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="df47d-188">Eenmaal de **multi-factor Authentication-beheerportal** laadt, zorg ervoor dat u op de **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="df47d-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="df47d-189">Zoek de gebruiker in de lijst met gebruikers door te zoeken, filteren of sorteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="df47d-190">Selecteer de gebruiker in de lijst met gebruikers en **inschakelen**, **uitschakelen**, of **afdwingen** multi-factor authentication-server naar wens.</span><span class="sxs-lookup"><span data-stu-id="df47d-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="df47d-191">Als een gebruiker zich in een **afgedwongen** staat, kunt u ze ingesteld op **uitgeschakelde** tijdelijk wilt laten terug bij hun account.</span><span class="sxs-lookup"><span data-stu-id="df47d-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="df47d-192">Wanneer ze terug in bent, kunt u vervolgens hun status te wijzigen **ingeschakeld** opnieuw naar de moet de gebruiker opnieuw registreren hun contactgegevens tijdens de volgende aanmelding in.</span><span class="sxs-lookup"><span data-stu-id="df47d-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="df47d-193">U kunt ook kunt u de stappen in de [controleren van de contactgegevens van de verificatie van een gebruiker](#check-a-users-authentication-contact-info) om te controleren of deze gegevens voor deze instellen.</span><span class="sxs-lookup"><span data-stu-id="df47d-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="df47d-194">Controleer de contactgegevens van de verificatie van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="df47d-195">Als u wilt controleren van een gebruiker verificatie contactgegevens die zijn gebruikt voor multi-factor authentication, voorwaardelijke toegang, Identity Protection en het wachtwoord opnieuw instellen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-196">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-197">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-198">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-199">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-200">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-200">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-201">**Search** voor de gebruiker die u geïnteresseerd bent in en **klikt u op de rij** om te selecteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="df47d-202">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="df47d-202">click **Profile**.</span></span>

8.  <span data-ttu-id="df47d-203">Schuif omlaag naar **verificatie contactgegevens**.</span><span class="sxs-lookup"><span data-stu-id="df47d-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="df47d-204">**Bekijk** de gegevens die zijn geregistreerd voor de gebruiker en de update zo nodig.</span><span class="sxs-lookup"><span data-stu-id="df47d-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="df47d-205">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-205">Check a user’s group memberships</span></span>

<span data-ttu-id="df47d-206">Als u wilt controleren groepslidmaatschappen van een gebruiker, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-207">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-208">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-209">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-210">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-211">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-211">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-212">**Search** voor de gebruiker die u geïnteresseerd bent in en **klikt u op de rij** om te selecteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="df47d-213">Klik op **groepen** om te zien die groepen de gebruiker lid van is.</span><span class="sxs-lookup"><span data-stu-id="df47d-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="df47d-214">Controleer de toegewezen licenties van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="df47d-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="df47d-215">Als u wilt controleren toegewezen licenties van een gebruiker, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-216">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-217">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-218">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-219">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-220">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-220">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-221">**Search** voor de gebruiker die u geïnteresseerd bent in en **klikt u op de rij** om te selecteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="df47d-222">Klik op **licenties** om te zien die verleent aan de gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="df47d-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="df47d-223">Een gebruiker een licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="df47d-223">Assign a user a license</span></span> 

<span data-ttu-id="df47d-224">Als u wilt een licentie toewijzen aan een gebruiker, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="df47d-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="df47d-225">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="df47d-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="df47d-226">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="df47d-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df47d-227">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="df47d-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df47d-228">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="df47d-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="df47d-229">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df47d-229">click **All users**.</span></span>

6.  <span data-ttu-id="df47d-230">**Search** voor de gebruiker die u geïnteresseerd bent in en **klikt u op de rij** om te selecteren.</span><span class="sxs-lookup"><span data-stu-id="df47d-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="df47d-231">Klik op **licenties** om te zien die verleent aan de gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="df47d-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="df47d-232">Klik op de **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="df47d-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="df47d-233">Selecteer **een of meer producten** uit de lijst met beschikbare producten.</span><span class="sxs-lookup"><span data-stu-id="df47d-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="df47d-234">**Optionele** klikt u op de **toewijzingsopties** item granulair toewijzen producten.</span><span class="sxs-lookup"><span data-stu-id="df47d-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="df47d-235">Klik op **Ok** wanneer dit is voltooid.</span><span class="sxs-lookup"><span data-stu-id="df47d-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="df47d-236">Klik op de **toewijzen** knop deze licenties toewijzen aan deze gebruiker.</span><span class="sxs-lookup"><span data-stu-id="df47d-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="df47d-237">Als bovenstaande stappen voor probleemoplossing het probleem niet oplossen</span><span class="sxs-lookup"><span data-stu-id="df47d-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="df47d-238">een ondersteuningsticket opent met de volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="df47d-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="df47d-239">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="df47d-239">Correlation error ID</span></span>

-   <span data-ttu-id="df47d-240">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="df47d-240">UPN (user email address)</span></span>

-   <span data-ttu-id="df47d-241">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="df47d-241">Tenant ID</span></span>

-   <span data-ttu-id="df47d-242">Browsertype</span><span class="sxs-lookup"><span data-stu-id="df47d-242">Browser type</span></span>

-   <span data-ttu-id="df47d-243">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="df47d-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="df47d-244">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="df47d-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="df47d-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df47d-245">Next steps</span></span>
[<span data-ttu-id="df47d-246">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="df47d-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
