---
title: Problemen met aanmelden bij een galerie van Azure AD-toepassing die is geconfigureerd voor wachtwoordherstel eenmalige aanmelding | Microsoft Docs
description: Probleemgebieden die richtlijnen bieden voor het oplossen van problemen met aanmelden bij de galerie van Azure AD-toepassingen die zijn geconfigureerd voor eenmalige aanmelding wachtwoord wordt beschreven
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
ms.openlocfilehash: c90b61812affb7e7af05cf3e302d045958da59be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="a3687-103">Problemen met aanmelden bij een galerie van Azure AD-toepassing die is geconfigureerd voor eenmalige aanmelding wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a3687-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="a3687-104">Het Toegangspaneel is een portal op Internet waarmee een gebruiker met een account voor werk of school in Azure Active Directory (Azure AD) voor weergave in en start cloud-gebaseerde toepassingen die de Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="a3687-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="a3687-105">Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en app-mogelijkheden voor beheer via het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a3687-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="a3687-106">Het Toegangspaneel is gescheiden van de Azure-portal en vereist geen gebruikers een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="a3687-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="a3687-107">Als u wilt gebruiken op basis van wachtwoorden eenmalige aanmelding (SSO) in het deelvenster toegang, moet de extensie Toegangspaneel worden geïnstalleerd in de browser van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a3687-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="a3687-108">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="a3687-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="a3687-109">Vergadering Browservereisten voor het toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="a3687-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="a3687-110">Het toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a3687-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="a3687-111">Als u wilt gebruiken op basis van wachtwoorden eenmalige aanmelding (SSO) in het deelvenster toegang, moet de extensie Toegangspaneel worden geïnstalleerd in de browser van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a3687-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="a3687-112">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="a3687-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="a3687-113">Voor eenmalige aanmelding op basis van wachtwoorden kunnen van de eindgebruiker browsers zijn:</span><span class="sxs-lookup"><span data-stu-id="a3687-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="a3687-114">Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="a3687-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="a3687-115">Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="a3687-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="a3687-116">Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="a3687-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="a3687-117">De extensie eenmalige aanmelding op basis van wachtwoorden komen beschikbaar voor de rand in de Windows 10 als browseruitbreidingen worden ondersteund voor de rand.</span><span class="sxs-lookup"><span data-stu-id="a3687-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="a3687-118">Het installeren van de Browseruitbreiding toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="a3687-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="a3687-119">Volg de onderstaande stappen voor het installeren van de Browseruitbreiding toegang Configuratiescherm:</span><span class="sxs-lookup"><span data-stu-id="a3687-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="a3687-120">Open de [Toegangspaneel](https://myapps.microsoft.com) in een van de ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3687-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="a3687-121">Klik op een **wachtwoord SSO toepassing** in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="a3687-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="a3687-122">Selecteer in het venster met de vraag om de software te installeren, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="a3687-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="a3687-123">Op basis van uw browser u omgeleid naar de downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="a3687-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="a3687-124">**Voeg** de uitbreiding van uw browser.</span><span class="sxs-lookup"><span data-stu-id="a3687-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="a3687-125">Als uw browser wordt gevraagd, selecteert u op een **inschakelen** of **toestaan** de extensie.</span><span class="sxs-lookup"><span data-stu-id="a3687-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="a3687-126">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="a3687-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="a3687-127">Meld u aan in het deelvenster toegang en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="a3687-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="a3687-128">U kunt ook de uitbreiding voor Chrome en Firefox downloaden uit de onderstaande directe koppelingen:</span><span class="sxs-lookup"><span data-stu-id="a3687-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="a3687-129">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="a3687-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="a3687-130">Uitbreiding van het Configuratiescherm Firefox toegang</span><span class="sxs-lookup"><span data-stu-id="a3687-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="a3687-131">Instellen van een groepsbeleid voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a3687-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="a3687-132">U kunt een groepsbeleid waarmee u op afstand installeren van de extensie Toegangspaneel voor Internet Explorer op computers van uw gebruikers instellen.</span><span class="sxs-lookup"><span data-stu-id="a3687-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="a3687-133">De vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="a3687-133">The prerequisites include:</span></span>

-   <span data-ttu-id="a3687-134">U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u hebt uw gebruikers machines toegevoegd aan uw domein.</span><span class="sxs-lookup"><span data-stu-id="a3687-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="a3687-135">U moet de machtiging 'Instellingen bewerken' voor het bewerken van het groepsbeleidsobject (GPO) hebben.</span><span class="sxs-lookup"><span data-stu-id="a3687-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="a3687-136">Standaard hebben leden van de volgende beveiligingsgroepen deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="a3687-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="a3687-137">[Meer informatie](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3687-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="a3687-138">Volg de zelfstudie [het implementeren van de uitbreiding van het Configuratiescherm toegang voor Internet Explorer met behulp van Groepsbeleid](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) voor stapsgewijze instructies voor het configureren van het Groepsbeleid en het implementeren voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a3687-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="a3687-139">Problemen met het toegangsvenster in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a3687-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="a3687-140">Ga als volgt de [oplossen met de extensie van het Configuratiescherm toegang voor Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) geleid voor toegang tot een diagnostische hulpprogramma's en stapsgewijze instructies over het configureren van de extensie voor IE.</span><span class="sxs-lookup"><span data-stu-id="a3687-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a3687-141">Het configureren van wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="a3687-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a3687-142">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="a3687-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a3687-143">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="a3687-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="a3687-144">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="a3687-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="a3687-145">Gebruikers toewijzen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="a3687-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="a3687-146">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="a3687-146">Add a non-gallery application</span></span>

<span data-ttu-id="a3687-147">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a3687-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a3687-148">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="a3687-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a3687-149">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="a3687-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a3687-150">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a3687-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a3687-151">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="a3687-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a3687-152">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="a3687-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="a3687-153">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="a3687-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="a3687-154">Voer de naam van uw toepassing in de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="a3687-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="a3687-155">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="a3687-155">Select **Add.**</span></span>

<span data-ttu-id="a3687-156">Na een korte periode is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="a3687-156">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="a3687-157">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="a3687-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="a3687-158">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="a3687-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="a3687-159">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="a3687-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a3687-160">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="a3687-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a3687-161">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a3687-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a3687-162">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="a3687-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a3687-163">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a3687-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a3687-164">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="a3687-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a3687-165">Selecteer de toepassing die u wilt configureren eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a3687-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="a3687-166">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3687-166">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a3687-167">Selecteer de modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="a3687-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a3687-168">Voer de **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="a3687-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="a3687-169">Dit is de URL waar gebruikers hun gebruikersnaam en wachtwoord aanmelden bij invoeren.</span><span class="sxs-lookup"><span data-stu-id="a3687-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="a3687-170">Zorg ervoor dat de aanmeldingspagina velden zijn zichtbaar in de URL.</span><span class="sxs-lookup"><span data-stu-id="a3687-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="a3687-171">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3687-171">Assign users to the application.</span></span>

11. <span data-ttu-id="a3687-172">Bovendien kunt u ook referenties opgeven namens de gebruiker door de rijen van de gebruikers te selecteren en te klikken op **updatereferenties** en de gebruikersnaam en wachtwoord in te voeren namens de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a3687-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="a3687-173">Anders wordt gebruikers gevraagd de referenties zich bij het starten in te voeren.</span><span class="sxs-lookup"><span data-stu-id="a3687-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="a3687-174">Gebruikers toewijzen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="a3687-174">Assign users to the application</span></span>

<span data-ttu-id="a3687-175">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a3687-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="a3687-176">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="a3687-176">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a3687-177">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="a3687-177">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a3687-178">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a3687-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a3687-179">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="a3687-179">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a3687-180">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a3687-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a3687-181">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="a3687-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a3687-182">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="a3687-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="a3687-183">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3687-183">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a3687-184">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="a3687-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a3687-185">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="a3687-185">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a3687-186">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="a3687-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a3687-187">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="a3687-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="a3687-188">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="a3687-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="a3687-189">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="a3687-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="a3687-190">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3687-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="a3687-191">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a3687-191">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="a3687-192">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a3687-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="a3687-193">Na een korte periode de geselecteerde gebruikers mogelijk om deze toepassingen in het deelvenster toegang te starten.</span><span class="sxs-lookup"><span data-stu-id="a3687-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="a3687-194">Als bovenstaande stappen voor probleemoplossing niet de los het probleem doet</span><span class="sxs-lookup"><span data-stu-id="a3687-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="a3687-195">een ondersteuningsticket opent met de volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="a3687-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="a3687-196">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="a3687-196">Correlation error ID</span></span>

-   <span data-ttu-id="a3687-197">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="a3687-197">UPN (user email address)</span></span>

-   <span data-ttu-id="a3687-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="a3687-198">TenantID</span></span>

-   <span data-ttu-id="a3687-199">Browsertype</span><span class="sxs-lookup"><span data-stu-id="a3687-199">Browser type</span></span>

-   <span data-ttu-id="a3687-200">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="a3687-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="a3687-201">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="a3687-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3687-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3687-202">Next steps</span></span>
[<span data-ttu-id="a3687-203">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="a3687-203">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

