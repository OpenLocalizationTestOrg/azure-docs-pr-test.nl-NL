---
title: Het configureren van wachtwoord eenmalige aanmelding voor een niet-galerie applicationn | Microsoft Docs
description: Het configureren van een aangepaste niet-galerie-toepassing voor beveiligde op basis van wachtwoorden eenmalige aanmelding wanneer deze niet wordt weergegeven in de Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9c3e9-103">Het configureren van wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="9c3e9-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9c3e9-104">Naast de opties in de Azure AD-Toepassingsgalerie gevonden, hebt u ook de optie om toe te voegen een **niet galerie toepassing** wanneer de toepassing die u wilt dat er niet wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="9c3e9-105">Met deze mogelijkheid kunt u elke toepassing die al bestaat in uw organisatie of een toepassing van derden die u mogelijk toevoegen van een leverancier die niet al deel uit van de [Azure AD-Toepassingsgalerie](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="9c3e9-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="9c3e9-106">Als u een niet-galerie-toepassing toevoegt, kunt u configureren de methode voor eenmalige aanmelding deze toepassing worden gebruikt door het selecteren van de **Single Sign-on** navigatie-item op een zakelijke toepassing in de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c3e9-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="9c3e9-107">Een van de eenmalige aanmelding methoden beschikbaar voor u is de [op basis van wachtwoorden Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) optie.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="9c3e9-108">Met de **toevoegen van een toepassing niet galerie** ervaring, kunt u elke toepassing die een gebruikersnaam voor de HTML gebaseerde renders integreren en wachtwoord invoeren veld, zelfs als deze zich niet in de set vooraf geïntegreerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="9c3e9-109">De manier waarop die dit werkt, is door een pagina slijmen technologie die deel uitmaakt van de extensie Toegangspaneel waarmee we gebruikersnaam en wachtwoord invoervelden automatisch detecteren, veilig opslaan voor uw exemplaar van de specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="9c3e9-110">Vervolgens veilig replay-gebruikersnamen en wachtwoorden die velden wanneer een gebruiker naar deze toepassing op het toegangsvenster toepassing navigeert.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="9c3e9-111">Dit is een uitstekende manier om te beginnen met elk type toepassing snel integreren met Azure AD en kunt u:</span><span class="sxs-lookup"><span data-stu-id="9c3e9-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="9c3e9-112">Integreren **elke toepassing in de hele wereld** met uw Azure AD-tenant, zo lang zijn als een HTML-gebruikersnaam en wachtwoord invoerveld wordt</span><span class="sxs-lookup"><span data-stu-id="9c3e9-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="9c3e9-113">Schakel **eenmalige aanmelding voor uw gebruikers** door veilig opslaan en opnieuw wordt afgespeeld gebruikersnamen en wachtwoorden voor de toepassing die u hebt geïntegreerd met Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c3e9-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="9c3e9-114">**Automatische detectie invoer** velden voor elke toepassing en kunt u handmatig detecteren die met behulp van de Browseruitbreiding toegang deelvenster velden als automatische detectie niet worden gevonden</span><span class="sxs-lookup"><span data-stu-id="9c3e9-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="9c3e9-115">**Ondersteuning voor toepassingen waarvoor meerdere velden aanmelden** voor toepassingen waarvoor meer dan alleen velden gebruikersnaam en wachtwoord aanmelden</span><span class="sxs-lookup"><span data-stu-id="9c3e9-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="9c3e9-116">**De labels aanpassen** van de gebruikersnaam en wachtwoord invoervelden uw gebruikers te zien op de [toepassing Toegangsvenster](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) wanneer ze hun referenties invoeren</span><span class="sxs-lookup"><span data-stu-id="9c3e9-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="9c3e9-117">Toestaan dat uw **gebruikers** om te bieden hun eigen gebruikersnamen en wachtwoorden voor bestaande toepassing accounts het typen van in handmatig in op de [Toegangspaneel voor toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="9c3e9-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="9c3e9-118">Toestaan dat een **lid van de groep business** om op te geven van de gebruikersnamen en wachtwoorden die zijn toegewezen aan een gebruiker met behulp van de [Self-Service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) functie</span><span class="sxs-lookup"><span data-stu-id="9c3e9-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="9c3e9-119">Toestaan dat een **beheerder** om op te geven de gebruikersnamen en wachtwoorden die zijn toegewezen aan een gebruiker met de referenties bijwerken wanneer functie [een gebruiker aan een toepassing toewijzen](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="9c3e9-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="9c3e9-120">Toestaan dat een **beheerder** om op te geven de gedeelde gebruikersnaam of het wachtwoord dat wordt gebruikt door een groep personen met de referenties bijwerken wanneer functie [een groep toewijzen aan een toepassing](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="9c3e9-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="9c3e9-121">Hieronder wordt beschreven hoe u kunt inschakelen [op basis van wachtwoorden Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) voor elke toepassing die u toevoegt met behulp van de **toevoegen van een toepassing niet galerie** optreden.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="9c3e9-122">Overzicht van stappen vereist</span><span class="sxs-lookup"><span data-stu-id="9c3e9-122">Overview of steps required</span></span>

<span data-ttu-id="9c3e9-123">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="9c3e9-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9c3e9-124">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="9c3e9-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="9c3e9-125">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="9c3e9-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="9c3e9-126">De toepassing toewijzen aan een gebruiker of een groep</span><span class="sxs-lookup"><span data-stu-id="9c3e9-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="9c3e9-127">Een gebruiker rechtstreeks aan een toepassing toewijzen</span><span class="sxs-lookup"><span data-stu-id="9c3e9-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="9c3e9-128">Een toepassing toewijzen aan een groep rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="9c3e9-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="9c3e9-129">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="9c3e9-129">Add a non-gallery application</span></span>

<span data-ttu-id="9c3e9-130">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9c3e9-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9c3e9-131">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9c3e9-132">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c3e9-133">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c3e9-134">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c3e9-135">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="9c3e9-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="9c3e9-136">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="9c3e9-137">Voer de naam van uw toepassing in de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="9c3e9-138">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-138">Select **Add.**</span></span>

<span data-ttu-id="9c3e9-139">Na een korte periode is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="9c3e9-140">De toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="9c3e9-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="9c3e9-141">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="9c3e9-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9c3e9-142">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c3e9-143">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c3e9-144">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c3e9-145">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c3e9-146">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c3e9-147">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c3e9-148">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9c3e9-149">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c3e9-150">Selecteer de modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9c3e9-151">Voer de **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="9c3e9-152">Dit is de URL waar gebruikers hun gebruikersnaam en wachtwoord aanmelden bij invoeren.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="9c3e9-153">Zorg ervoor dat de aanmeldingspagina velden zijn zichtbaar in de URL.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="9c3e9-154">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-154">Assign users to the application.</span></span>

11. <span data-ttu-id="9c3e9-155">Bovendien kunt u ook referenties opgeven namens de gebruiker door de rijen van de gebruikers te selecteren en te klikken op **updatereferenties** en de gebruikersnaam en wachtwoord in te voeren namens de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="9c3e9-156">Anders wordt gebruikers gevraagd de referenties zich bij het starten in te voeren.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="9c3e9-157">Een gebruiker rechtstreeks aan een toepassing toewijzen</span><span class="sxs-lookup"><span data-stu-id="9c3e9-157">Assign a user to an application directly</span></span>

<span data-ttu-id="9c3e9-158">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9c3e9-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9c3e9-159">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c3e9-160">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c3e9-161">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c3e9-162">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c3e9-163">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c3e9-164">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c3e9-165">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9c3e9-166">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c3e9-167">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9c3e9-168">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9c3e9-169">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9c3e9-170">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9c3e9-171">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9c3e9-172">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9c3e9-173">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9c3e9-174">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9c3e9-175">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="9c3e9-176">Een toepassing toewijzen aan een groep rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="9c3e9-176">Assign an application to a group directly</span></span>

<span data-ttu-id="9c3e9-177">Als u wilt toewijzen een of meer groepen rechtstreeks aan een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9c3e9-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9c3e9-178">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c3e9-179">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c3e9-180">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c3e9-181">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c3e9-182">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c3e9-183">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9c3e9-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c3e9-184">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9c3e9-185">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c3e9-186">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9c3e9-187">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9c3e9-188">Typ in het **volledige groepsnaam** van de groep die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9c3e9-189">Beweeg de muisaanwijzer over de **groep** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9c3e9-190">Schakel het selectievakje in naast de profielfoto of het logo voor uw gebruiker toevoegen aan de groep de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9c3e9-191">**Optioneel:** als u wilt **toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje in om toe te voegen van deze groep de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="9c3e9-192">Wanneer u klaar bent met groepen te selecteren, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9c3e9-193">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de groepen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="9c3e9-194">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde groepen.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="9c3e9-195">Na een korte periode de geselecteerde gebruikers mogelijk om deze toepassingen in het deelvenster toegang te starten.</span><span class="sxs-lookup"><span data-stu-id="9c3e9-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c3e9-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c3e9-196">Next steps</span></span>
[<span data-ttu-id="9c3e9-197">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="9c3e9-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
