---
title: Problemen met aanmelden bij een toepassing met een deeplink | Microsoft Docs
description: Het oplossen van problemen met toegang tot een toepassing van een gebruikmaken van Azure AD-deeplink-URL
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="40d6c-103">Problemen met aanmelden bij een toepassing met een deeplink</span><span class="sxs-lookup"><span data-stu-id="40d6c-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="40d6c-104">Het Toegangspaneel is een portal op Internet waarmee een gebruiker met een account voor werk of school in Azure Active Directory (Azure AD) weergeven en starten van cloud-gebaseerde toepassingen die de Azure AD-beheerder heeft deze toegang verleend.</span><span class="sxs-lookup"><span data-stu-id="40d6c-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="40d6c-105">Deze toepassingen zijn geconfigureerd namens de gebruiker in de Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="40d6c-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="40d6c-106">De toepassing moet worden geconfigureerd en toegewezen aan de gebruiker of een groep die de gebruiker is lid van de toepassing in het deelvenster toegang zien.</span><span class="sxs-lookup"><span data-stu-id="40d6c-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="40d6c-107">Dieptekoppelingen of toegang voor gebruikers zijn URL's koppelingen die uw gebruikers toegang krijgen tot hun wachtwoord SSO-toepassingen rechtstreeks vanuit hun browser-URL balken kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="40d6c-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="40d6c-108">Door te navigeren naar deze koppeling, worden gebruikers automatisch aangemeld bij de toepassing zonder eerst het toegangsvenster naar.</span><span class="sxs-lookup"><span data-stu-id="40d6c-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="40d6c-109">Dit is dezelfde koppeling waarmee gebruikers toegang tot deze toepassingen van startprogramma voor toepassingen van Office 365.</span><span class="sxs-lookup"><span data-stu-id="40d6c-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="40d6c-110">Algemene problemen om eerst te controleren</span><span class="sxs-lookup"><span data-stu-id="40d6c-110">General issues to check first</span></span>

-   <span data-ttu-id="40d6c-111">Zorg ervoor dat uw met een **browser** die voldoet aan de minimale vereisten voor het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="40d6c-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="40d6c-112">Zorg ervoor dat de URL van de toepassing is toegevoegd door de browser van de gebruiker de **vertrouwde websites**.</span><span class="sxs-lookup"><span data-stu-id="40d6c-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="40d6c-113">Controleer of de toepassing is **geconfigureerd** correct.</span><span class="sxs-lookup"><span data-stu-id="40d6c-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="40d6c-114">Zorg ervoor dat het gebruikersaccount **ingeschakeld** voor aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="40d6c-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="40d6c-115">Zorg ervoor dat het gebruikersaccount **niet is vergrendeld.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="40d6c-116">Zorg ervoor dat de gebruiker **wachtwoord niet is verlopen of is vergeten.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="40d6c-117">Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="40d6c-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="40d6c-118">Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="40d6c-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="40d6c-119">Zorg ervoor dat een gebruiker **verificatie contactgegevens** is up-to-date houden om toe te staan van multi-factor Authentication of voorwaardelijk beleid worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="40d6c-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="40d6c-120">Zorg ervoor dat ook moet worden geprobeerd wissen van cookies in uw browser en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="40d6c-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="40d6c-121">De deeplink controleren</span><span class="sxs-lookup"><span data-stu-id="40d6c-121">Checking the deeplink</span></span>

<span data-ttu-id="40d6c-122">Als u wilt controleren of u de juiste deeplink hebt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="40d6c-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="40d6c-123">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="40d6c-124">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="40d6c-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="40d6c-125">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="40d6c-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="40d6c-126">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="40d6c-127">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="40d6c-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="40d6c-128">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="40d6c-129">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="40d6c-130">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="40d6c-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="40d6c-131">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="40d6c-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="40d6c-132">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="40d6c-133">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="40d6c-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="40d6c-134">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="40d6c-135">Selecteer de toepassing die u wilt dat de controle van de deeplink voor.</span><span class="sxs-lookup"><span data-stu-id="40d6c-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="40d6c-136">Zoek het label **toegangs-URL van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="40d6c-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="40d6c-137">U deeplink moet overeenkomen met deze URL.</span><span class="sxs-lookup"><span data-stu-id="40d6c-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="40d6c-138">Het installeren van de Browseruitbreiding toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="40d6c-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="40d6c-139">Volg de onderstaande stappen voor het installeren van de Browseruitbreiding toegang Configuratiescherm:</span><span class="sxs-lookup"><span data-stu-id="40d6c-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="40d6c-140">Open de [Toegangspaneel](https://myapps.microsoft.com) in een van de ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40d6c-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="40d6c-141">Klik op een **wachtwoord SSO toepassing** in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="40d6c-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="40d6c-142">Selecteer in het venster met de vraag om de software te installeren, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="40d6c-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="40d6c-143">Op basis van uw browser u omgeleid naar de downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="40d6c-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="40d6c-144">**Voeg** de uitbreiding van uw browser.</span><span class="sxs-lookup"><span data-stu-id="40d6c-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="40d6c-145">Als uw browser wordt gevraagd, selecteert u op een **inschakelen** of **toestaan** de extensie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="40d6c-146">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="40d6c-147">Meld u aan in het deelvenster toegang en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="40d6c-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="40d6c-148">U kunt ook de uitbreiding voor Chrome en Firefox downloaden uit de onderstaande directe koppelingen:</span><span class="sxs-lookup"><span data-stu-id="40d6c-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="40d6c-149">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="40d6c-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="40d6c-150">Uitbreiding van het Configuratiescherm Firefox toegang</span><span class="sxs-lookup"><span data-stu-id="40d6c-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="40d6c-151">Het wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="40d6c-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="40d6c-152">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="40d6c-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="40d6c-153">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d6c-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="40d6c-154">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="40d6c-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="40d6c-155">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d6c-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="40d6c-156">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="40d6c-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="40d6c-157">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="40d6c-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="40d6c-158">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="40d6c-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="40d6c-159">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="40d6c-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="40d6c-160">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="40d6c-161">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="40d6c-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="40d6c-162">In de **Voer een naam** textbox uit de **toevoegen uit de galerie** sectie, typ de naam van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="40d6c-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="40d6c-163">Selecteer de toepassing die u wilt configureren voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="40d6c-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="40d6c-164">Voordat u de toepassing toevoegt, kunt u de naam van de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="40d6c-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="40d6c-165">Klik op **toevoegen** knop, de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="40d6c-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="40d6c-166">Na een korte periode is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="40d6c-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="40d6c-167">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="40d6c-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="40d6c-168">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="40d6c-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="40d6c-169">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="40d6c-170">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="40d6c-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="40d6c-171">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="40d6c-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="40d6c-172">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="40d6c-173">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="40d6c-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="40d6c-174">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="40d6c-175">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="40d6c-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="40d6c-176">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="40d6c-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="40d6c-177">Selecteer de modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="40d6c-178">[Gebruikers toewijzen aan de toepassing](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="40d6c-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="40d6c-179">Bovendien kunt u ook referenties opgeven namens de gebruiker door de rijen van de gebruikers te selecteren en te klikken op **updatereferenties** en de gebruikersnaam en wachtwoord in te voeren namens de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="40d6c-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="40d6c-180">Anders wordt gebruikers gevraagd de referenties zich bij het starten in te voeren.</span><span class="sxs-lookup"><span data-stu-id="40d6c-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="40d6c-181">Het configureren van wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="40d6c-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="40d6c-182">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="40d6c-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="40d6c-183">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="40d6c-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="40d6c-184">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="40d6c-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="40d6c-185">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="40d6c-185">Add a non-gallery application</span></span>

<span data-ttu-id="40d6c-186">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="40d6c-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="40d6c-187">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="40d6c-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="40d6c-188">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="40d6c-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="40d6c-189">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="40d6c-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="40d6c-190">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="40d6c-191">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="40d6c-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="40d6c-192">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="40d6c-193">Voer de naam van uw toepassing in de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="40d6c-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="40d6c-194">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-194">Select **Add.**</span></span>

<span data-ttu-id="40d6c-195">Na een korte periode is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="40d6c-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="40d6c-196">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="40d6c-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="40d6c-197">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="40d6c-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="40d6c-198">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="40d6c-199">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="40d6c-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="40d6c-200">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="40d6c-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="40d6c-201">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="40d6c-202">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="40d6c-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="40d6c-203">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="40d6c-204">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="40d6c-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="40d6c-205">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="40d6c-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="40d6c-206">Selecteer de modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="40d6c-207">Voer de **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="40d6c-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="40d6c-208">Dit is de URL waar gebruikers hun gebruikersnaam en wachtwoord aanmelden bij invoeren.</span><span class="sxs-lookup"><span data-stu-id="40d6c-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="40d6c-209">Zorg ervoor dat de aanmeldingspagina velden zijn zichtbaar in de URL.</span><span class="sxs-lookup"><span data-stu-id="40d6c-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="40d6c-210">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="40d6c-210">Assign users to the application.</span></span>

11. <span data-ttu-id="40d6c-211">Bovendien kunt u ook referenties opgeven namens de gebruiker door de rijen van de gebruikers te selecteren en te klikken op **updatereferenties** en de gebruikersnaam en wachtwoord in te voeren namens de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="40d6c-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="40d6c-212">Anders wordt gebruikers gevraagd de referenties zich bij het starten in te voeren.</span><span class="sxs-lookup"><span data-stu-id="40d6c-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="40d6c-213">Een gebruiker rechtstreeks naar een toepassing toewijzen</span><span class="sxs-lookup"><span data-stu-id="40d6c-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="40d6c-214">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="40d6c-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="40d6c-215">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="40d6c-216">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="40d6c-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="40d6c-217">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="40d6c-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="40d6c-218">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="40d6c-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="40d6c-219">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="40d6c-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="40d6c-220">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="40d6c-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="40d6c-221">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="40d6c-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="40d6c-222">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="40d6c-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="40d6c-223">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="40d6c-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="40d6c-224">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="40d6c-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="40d6c-225">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="40d6c-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="40d6c-226">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="40d6c-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="40d6c-227">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="40d6c-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="40d6c-228">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="40d6c-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="40d6c-229">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="40d6c-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="40d6c-230">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="40d6c-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="40d6c-231">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="40d6c-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="40d6c-232">Na een korte periode de geselecteerde gebruikers mogelijk om deze toepassingen in het deelvenster toegang te starten.</span><span class="sxs-lookup"><span data-stu-id="40d6c-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="40d6c-233">Als bovenstaande stappen voor probleemoplossing niet de los het probleem doet.</span><span class="sxs-lookup"><span data-stu-id="40d6c-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="40d6c-234">een ondersteuningsticket opent met de volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="40d6c-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="40d6c-235">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="40d6c-235">Correlation error ID</span></span>

-   <span data-ttu-id="40d6c-236">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="40d6c-236">UPN (user email address)</span></span>

-   <span data-ttu-id="40d6c-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="40d6c-237">TenantID</span></span>

-   <span data-ttu-id="40d6c-238">Browsertype</span><span class="sxs-lookup"><span data-stu-id="40d6c-238">Browser type</span></span>

-   <span data-ttu-id="40d6c-239">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="40d6c-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="40d6c-240">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="40d6c-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="40d6c-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40d6c-241">Next steps</span></span>
[<span data-ttu-id="40d6c-242">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="40d6c-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
