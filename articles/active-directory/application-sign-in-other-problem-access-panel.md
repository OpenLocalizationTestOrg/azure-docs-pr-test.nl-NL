---
title: Problemen met aanmelden bij een toepassing in het deelvenster toegang | Microsoft Docs
description: Het oplossen van problemen met toegang tot een toepassing van de Microsoft Azure AD-Toegangsvenster op myapps.microsoft.com
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
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="5e1e0-103">Problemen met aanmelden bij een toepassing van het toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="5e1e0-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="5e1e0-104">Het Toegangspaneel is een portal op Internet waarmee een gebruiker met een account voor werk of school in Azure Active Directory (Azure AD) weergeven en starten van cloud-gebaseerde toepassingen die de Azure AD-beheerder heeft deze toegang verleend.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="5e1e0-105">Deze toepassingen zijn geconfigureerd namens de gebruiker in de Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="5e1e0-106">De toepassing moet worden geconfigureerd en toegewezen aan de gebruiker of een groep die de gebruiker is lid van de toepassing in het deelvenster toegang zien.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="5e1e0-107">Het type van een gebruiker ziet u mogelijk apps kunnen worden onderverdeeld in de volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="5e1e0-108">Office 365-toepassingen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-108">Office 365 Applications</span></span>

-   <span data-ttu-id="5e1e0-109">Microsoft en derden toepassingen die zijn geconfigureerd op basis van een federatieve aanmelding bij</span><span class="sxs-lookup"><span data-stu-id="5e1e0-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="5e1e0-110">SSO-toepassingen op basis van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="5e1e0-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="5e1e0-111">Toepassingen met bestaande oplossingen voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5e1e0-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="5e1e0-112">Algemene problemen om eerst te controleren</span><span class="sxs-lookup"><span data-stu-id="5e1e0-112">General issues to check first</span></span>

-   <span data-ttu-id="5e1e0-113">Zorg ervoor dat uw met een **browser** die voldoet aan de minimale vereisten voor het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="5e1e0-114">Zorg ervoor dat de URL van de toepassing is toegevoegd door de browser van de gebruiker de **vertrouwde websites**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="5e1e0-115">Controleer of de toepassing is **geconfigureerd** correct.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="5e1e0-116">Zorg ervoor dat het gebruikersaccount **ingeschakeld** voor aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="5e1e0-117">Zorg ervoor dat het gebruikersaccount **niet is vergrendeld.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="5e1e0-118">Zorg ervoor dat de gebruiker **wachtwoord niet is verlopen of is vergeten.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="5e1e0-119">Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="5e1e0-120">Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="5e1e0-121">Zorg ervoor dat een gebruiker **verificatie contactgegevens** is up-to-date houden om toe te staan van multi-factor Authentication of voorwaardelijk beleid worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="5e1e0-122">Zorg ervoor dat ook moet worden geprobeerd wissen van cookies in uw browser en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="5e1e0-123">Vergadering Browservereisten voor het toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="5e1e0-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="5e1e0-124">Het toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="5e1e0-125">Als u wilt gebruiken op basis van wachtwoorden eenmalige aanmelding (SSO) in het deelvenster toegang, moet de extensie Toegangspaneel worden geïnstalleerd in de browser van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="5e1e0-126">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="5e1e0-127">Voor eenmalige aanmelding op basis van wachtwoorden kunnen van de eindgebruiker browsers zijn:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="5e1e0-128">Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="5e1e0-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="5e1e0-129">Rand verjaardagseditie van Windows 10 of hoger</span><span class="sxs-lookup"><span data-stu-id="5e1e0-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="5e1e0-130">Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="5e1e0-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="5e1e0-131">Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="5e1e0-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="5e1e0-132">Het installeren van de Browseruitbreiding toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="5e1e0-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="5e1e0-133">Volg de onderstaande stappen voor het installeren van de Browseruitbreiding toegang Configuratiescherm:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-134">Open de [Toegangspaneel](https://myapps.microsoft.com) in een van de ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="5e1e0-135">Klik op een **wachtwoord SSO toepassing** in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="5e1e0-136">Selecteer in het venster met de vraag om de software te installeren, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="5e1e0-137">Op basis van uw browser u omgeleid naar de downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="5e1e0-138">**Voeg** de uitbreiding van uw browser.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="5e1e0-139">Als uw browser wordt gevraagd, selecteert u op een **inschakelen** of **toestaan** de extensie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="5e1e0-140">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="5e1e0-141">Meld u aan in het deelvenster toegang en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="5e1e0-142">U kunt ook de uitbreiding voor Chrome en rand van de onderstaande directe koppelingen downloaden:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="5e1e0-143">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="5e1e0-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="5e1e0-144">Uitbreiding van de rand toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="5e1e0-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5e1e0-145">Het configureren van federatieve eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1e0-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="5e1e0-146">Alle toepassing in de galerie van Azure AD ingeschakeld met Enterprise Single Sign-On-functionaliteit is een stapsgewijze zelfstudie beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="5e1e0-147">U hebt toegang tot de [lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="5e1e0-148">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5e1e0-149">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1e0-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="5e1e0-150">Waarden voor metagegevens van de toepassing configureren in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="5e1e0-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="5e1e0-151">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="5e1e0-152">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="5e1e0-153">Azure AD metagegevenswaarden configureren in de toepassing (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="5e1e0-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="5e1e0-154">Gebruikers toewijzen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="5e1e0-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="5e1e0-155">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1e0-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="5e1e0-156">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-157">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5e1e0-158">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-159">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-160">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-161">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="5e1e0-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5e1e0-162">In de **Voer een naam** textbox uit de **toevoegen uit de galerie** sectie, typ de naam van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="5e1e0-163">Selecteer de toepassing die u wilt configureren voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="5e1e0-164">Voordat u de toepassing toevoegt, kunt u de naam van de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="5e1e0-165">Klik op **toevoegen** knop, de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="5e1e0-166">Na een korte periode is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="5e1e0-167">Eenmalige aanmelding voor een toepassing uit de galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5e1e0-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="5e1e0-168">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-170">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-171">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-172">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-173">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5e1e0-174">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-175">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5e1e0-176">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-177">Selecteer **op basis van SAML aanmelding** van de **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="5e1e0-178">Voer de vereiste waarden in **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="5e1e0-179">U moet deze waarden ophalen van de leverancier van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="5e1e0-180">Als u de toepassing configureren als Serviceprovider geïnitieerde eenmalige aanmelding, het teken op de URL voor is deze waarde vereist.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="5e1e0-181">Voor sommige toepassingen is de id ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="5e1e0-182">Het is een vereiste waarde voor het configureren van de toepassing als IdP geïnitieerde eenmalige aanmelding, de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="5e1e0-183">Voor sommige toepassingen is de id ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="5e1e0-184">**Optioneel:** klikt u op **weergeven geavanceerde instellingen voor URL** als u wilt zien van de waarden niet vereist.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="5e1e0-185">In de **gebruikerskenmerken**, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="5e1e0-186">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="5e1e0-187">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-187">To add an attribute:</span></span>

   1. <span data-ttu-id="5e1e0-188">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-188">click **Add attribute**.</span></span> <span data-ttu-id="5e1e0-189">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="5e1e0-190">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-190">Click **Save.**</span></span> <span data-ttu-id="5e1e0-191">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="5e1e0-192">Klik op **configureren &lt;toepassingsnaam&gt;**  toegang tot documentatie over het configureren van eenmalige aanmelding in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="5e1e0-193">Bovendien heeft u de metagegevens-URL's en het certificaat dat is vereist voor het instellen van eenmalige aanmelding met de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="5e1e0-194">Klik op **opslaan** aan de configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="5e1e0-195">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="5e1e0-196">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="5e1e0-197">Als u de gebruikers-ID selecteren of gebruikerskenmerken toevoegen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-198">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-199">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-200">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-201">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-202">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5e1e0-203">Als u de toepassing niet ziet u wilt het hier weergegeven, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar  **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-204">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5e1e0-205">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-206">Onder de **gebruikerskenmerken** sectie, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="5e1e0-207">De geselecteerde optie moet overeenkomen met de verwachte waarde in de toepassing om de gebruiker te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5e1e0-208">Azure AD selecteren de indeling voor het kenmerk NameID (gebruikers-id) op basis van de waarde geselecteerd of de indeling die is aangevraagd door de toepassing in de SAML-AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="5e1e0-209">Raadpleeg voor meer informatie het artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder de sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="5e1e0-210">Gebruikerskenmerken toevoegen: klik op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="5e1e0-211">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-211">To add an attribute:</span></span>

   1. <span data-ttu-id="5e1e0-212">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-212">click **Add attribute**.</span></span> <span data-ttu-id="5e1e0-213">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="5e1e0-214">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-214">Click **Save.**</span></span> <span data-ttu-id="5e1e0-215">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="5e1e0-216">De metagegevens van de Azure AD of het certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="5e1e0-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="5e1e0-217">Voor het downloaden van de metagegevens van de toepassing of het certificaat van Azure AD, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-218">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-219">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-220">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-221">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-222">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5e1e0-223">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-224">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5e1e0-225">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-226">Ga naar **SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="5e1e0-227">Afhankelijk van wat de toepassing configureren van eenmalige aanmelding vereist, ziet u ofwel de optie voor het downloaden van de Metadata XML of het certificaat.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="5e1e0-228">Azure AD biedt een URL als u de metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="5e1e0-229">De metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="5e1e0-230">Het configureren van federatieve eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="5e1e0-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="5e1e0-231">Als u een toepassing niet galerie configureren, moet u beschikken over Azure AD premium en de toepassing SAML 2.0 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="5e1e0-232">Voor meer informatie over Azure AD-versies, gaat u naar [prijzen van Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="5e1e0-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="5e1e0-233">Waarden voor metagegevens van de toepassing configureren in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="5e1e0-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="5e1e0-234">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="5e1e0-235">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="5e1e0-236">Azure AD metagegevenswaarden configureren in de toepassing (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="5e1e0-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="5e1e0-237">Waarden voor metagegevens van de toepassing configureren in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="5e1e0-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="5e1e0-238">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing die zich niet in de galerie van Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-239">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-240">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-241">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-242">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-243">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="5e1e0-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5e1e0-244">Klik op **Non-galerie toepassing** in de **uw eigen app toevoegen** sectie</span><span class="sxs-lookup"><span data-stu-id="5e1e0-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="5e1e0-245">Voer de naam van de toepassing in de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="5e1e0-246">Klik op **toevoegen** knop, de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="5e1e0-247">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="5e1e0-248">Selecteer **op basis van SAML aanmelding** in de **modus** vervolgkeuzelijst</span><span class="sxs-lookup"><span data-stu-id="5e1e0-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="5e1e0-249">Voer de vereiste waarden in **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="5e1e0-250">U moet deze waarden ophalen van de leverancier van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="5e1e0-251">Voer de antwoord-URL en de id voor het configureren van de toepassing als IdP geïnitieerde eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="5e1e0-252">**Optioneel:** voor het configureren van de toepassing als Serviceprovider geïnitieerde eenmalige aanmelding, het teken op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="5e1e0-253">In de **gebruikerskenmerken**, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="5e1e0-254">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="5e1e0-255">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-255">To add an attribute:</span></span>

   1. <span data-ttu-id="5e1e0-256">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-256">click **Add attribute**.</span></span> <span data-ttu-id="5e1e0-257">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="5e1e0-258">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-258">Click **Save.**</span></span> <span data-ttu-id="5e1e0-259">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="5e1e0-260">Klik op **configureren &lt;toepassingsnaam&gt;**  toegang tot documentatie over het configureren van eenmalige aanmelding in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="5e1e0-261">Bovendien heeft u Azure AD-URL's en het certificaat dat is vereist voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="5e1e0-262">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="5e1e0-263">Als u de gebruikers-ID selecteren of gebruikerskenmerken toevoegen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-264">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-265">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-266">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-267">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-268">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5e1e0-269">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-270">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5e1e0-271">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-272">Onder de **gebruikerskenmerken** sectie, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="5e1e0-273">De geselecteerde optie moet overeenkomen met de verwachte waarde in de toepassing om de gebruiker te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5e1e0-274">Azure AD selecteren de indeling voor het kenmerk NameID (gebruikers-id) op basis van de waarde geselecteerd of de indeling die is aangevraagd door de toepassing in de SAML-AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="5e1e0-275">Raadpleeg voor meer informatie het artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder de sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="5e1e0-276">Gebruikerskenmerken toevoegen: klik op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="5e1e0-277">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-277">To add an attribute:</span></span>

   <span data-ttu-id="5e1e0-278">1. Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-278">1.click **Add attribute**.</span></span> <span data-ttu-id="5e1e0-279">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="5e1e0-280">2 Klik **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-280">2 Click **Save.**</span></span> <span data-ttu-id="5e1e0-281">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="5e1e0-282">De metagegevens van de Azure AD of het certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="5e1e0-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="5e1e0-283">Voor het downloaden van de metagegevens van de toepassing of het certificaat van Azure AD, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-284">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-285">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-286">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-287">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-288">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="5e1e0-289">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-290">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5e1e0-291">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-292">Ga naar **SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="5e1e0-293">Afhankelijk van wat de toepassing configureren van eenmalige aanmelding vereist, ziet u ofwel de optie voor het downloaden van de Metadata XML of het certificaat.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="5e1e0-294">Azure AD biedt een URL als u de metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="5e1e0-295">De metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5e1e0-296">Het wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5e1e0-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="5e1e0-297">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5e1e0-298">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1e0-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="5e1e0-299">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="5e1e0-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="5e1e0-300">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1e0-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="5e1e0-301">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-302">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5e1e0-303">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-304">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-305">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-306">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="5e1e0-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5e1e0-307">In de **Voer een naam** textbox uit de **toevoegen uit de galerie** sectie, typ de naam van de toepassing</span><span class="sxs-lookup"><span data-stu-id="5e1e0-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="5e1e0-308">Selecteer de toepassing die u wilt configureren voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5e1e0-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="5e1e0-309">Voordat u de toepassing toevoegt, kunt u de naam van de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="5e1e0-310">Klik op **toevoegen** knop, de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="5e1e0-311">Na een korte periode is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="5e1e0-312">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="5e1e0-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="5e1e0-313">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-314">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-315">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-316">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-317">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-318">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="5e1e0-319">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-320">Selecteer de toepassing die u wilt configureren eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5e1e0-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="5e1e0-321">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-322">Selecteer de modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5e1e0-323">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-323">Assign users to the application.</span></span>

10. <span data-ttu-id="5e1e0-324">Bovendien kunt u ook referenties opgeven namens de gebruiker door de rijen van de gebruikers te selecteren en te klikken op **updatereferenties** en de gebruikersnaam en wachtwoord in te voeren namens de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="5e1e0-325">Anders wordt gebruikers gevraagd de referenties zich bij het starten in te voeren.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="5e1e0-326">Het configureren van wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="5e1e0-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="5e1e0-327">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5e1e0-328">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="5e1e0-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="5e1e0-329">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="5e1e0-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="5e1e0-330">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="5e1e0-330">Add a non-gallery application</span></span>

<span data-ttu-id="5e1e0-331">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-332">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5e1e0-333">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-334">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-335">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-336">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="5e1e0-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5e1e0-337">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="5e1e0-338">Voer de naam van uw toepassing in de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="5e1e0-339">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-339">Select **Add.**</span></span>

<span data-ttu-id="5e1e0-340">Na een korte periode is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="5e1e0-341">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="5e1e0-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="5e1e0-342">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-343">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e1e0-344">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-345">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-346">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-347">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="5e1e0-348">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-349">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5e1e0-350">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-351">Selecteer de modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5e1e0-352">Voer de **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="5e1e0-353">Dit is de URL waar gebruikers hun gebruikersnaam en wachtwoord aanmelden bij invoeren.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="5e1e0-354">Zorg ervoor dat de aanmeldingspagina velden zijn zichtbaar in de URL.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="5e1e0-355">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-355">Assign users to the application.</span></span>

11. <span data-ttu-id="5e1e0-356">Bovendien kunt u ook referenties opgeven namens de gebruiker door de rijen van de gebruikers te selecteren en te klikken op **updatereferenties** en de gebruikersnaam en wachtwoord in te voeren namens de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="5e1e0-357">Anders wordt gebruikers gevraagd de referenties zich bij het starten in te voeren.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="5e1e0-358">Een gebruiker rechtstreeks naar een toepassing toewijzen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="5e1e0-359">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="5e1e0-360">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5e1e0-361">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e1e0-362">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e1e0-363">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e1e0-364">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5e1e0-365">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="5e1e0-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e1e0-366">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="5e1e0-367">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e1e0-368">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5e1e0-369">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5e1e0-370">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5e1e0-371">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="5e1e0-372">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="5e1e0-373">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="5e1e0-374">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="5e1e0-375">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="5e1e0-376">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="5e1e0-377">Na een korte periode de geselecteerde gebruikers mogelijk om deze toepassingen in het deelvenster toegang te starten.</span><span class="sxs-lookup"><span data-stu-id="5e1e0-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="5e1e0-378">Als bovenstaande stappen voor probleemoplossing niet de los het probleem doet</span><span class="sxs-lookup"><span data-stu-id="5e1e0-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="5e1e0-379">een ondersteuningsticket opent met de volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="5e1e0-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="5e1e0-380">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="5e1e0-380">Correlation error ID</span></span>

-   <span data-ttu-id="5e1e0-381">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="5e1e0-381">UPN (user email address)</span></span>

-   <span data-ttu-id="5e1e0-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="5e1e0-382">TenantID</span></span>

-   <span data-ttu-id="5e1e0-383">Browsertype</span><span class="sxs-lookup"><span data-stu-id="5e1e0-383">Browser type</span></span>

-   <span data-ttu-id="5e1e0-384">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="5e1e0-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5e1e0-385">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e1e0-386">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e1e0-386">Next steps</span></span>
[<span data-ttu-id="5e1e0-387">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="5e1e0-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

