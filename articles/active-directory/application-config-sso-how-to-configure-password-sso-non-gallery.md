---
title: aaaHow tooconfigure wachtwoord eenmalige aanmelding voor een niet-galerie applicationn | Microsoft Docs
description: Hoe tooconfigure voor een aangepaste toepassing niet galerie beveiligen op basis van wachtwoorden eenmalige aanmelding wanneer deze niet wordt weergegeven in hello Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="462a3-103">Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="462a3-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="462a3-104">Bovendien toohello keuzes gevonden binnen hello Azure AD-Toepassingsgalerie, hebt u ook Hallo optie tooadd een **niet galerie toepassing** wanneer Hallo-toepassing die u wilt dat er niet wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="462a3-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="462a3-105">Met deze mogelijkheid kunt u elke toepassing die al bestaat in uw organisatie of een toepassing van derden die u mogelijk toevoegen van een leverancier die nog geen deel uitmaakt van Hallo [Azure AD-Toepassingsgalerie](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="462a3-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="462a3-106">Als u een niet-galerie-toepassing toevoegt, kunt u configureren Hallo één aanmelding methode deze toepassing wordt gebruikt door het selecteren van Hallo **Single Sign-on** navigatie-item op een zakelijke toepassing in Hallo [Azure Portal ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="462a3-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="462a3-107">Een van de Hallo Single Sign-on methoden beschikbaar tooyou Hallo is [op basis van wachtwoorden Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) optie.</span><span class="sxs-lookup"><span data-stu-id="462a3-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="462a3-108">Hello **toevoegen van een toepassing niet galerie** ervaring, kunt u elke toepassing die een gebruikersnaam voor de HTML gebaseerde renders integreren en wachtwoord invoeren veld, zelfs als deze zich niet in de set vooraf geïntegreerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="462a3-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="462a3-109">Hallo manier dit werkt, is door een technologie die deel uitmaakt van Hallo slijmen pagina Toegangsvenster uitbreiding waarmee we tooauto-gebruikersnaam en wachtwoord invoervelden detecteren, veilig opslaan voor uw exemplaar van de specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="462a3-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="462a3-110">Vervolgens veilig replay-gebruikersnamen en wachtwoorden toothose velden wanneer een gebruiker navigeert toothat toepassing op Hallo toepassing Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="462a3-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="462a3-111">Dit is een uitstekende manier tooget gestart elk soort toepassing snel integreren met Azure AD en kunt u:</span><span class="sxs-lookup"><span data-stu-id="462a3-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="462a3-112">Integreren **elke toepassing in Hallo wereld** met uw Azure AD-tenant, zo lang zijn als een HTML-gebruikersnaam en wachtwoord invoerveld wordt</span><span class="sxs-lookup"><span data-stu-id="462a3-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="462a3-113">Schakel **eenmalige aanmelding voor uw gebruikers** door veilig opslaan en opnieuw wordt afgespeeld gebruikersnamen en wachtwoorden voor de toepassing hello die u hebt geïntegreerd met Azure AD</span><span class="sxs-lookup"><span data-stu-id="462a3-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="462a3-114">**Automatische detectie invoer** velden voor elke toepassing en kunt u toomanually detecteren die velden met Hallo toegang Configuratiescherm Browseruitbreiding, indien automatische detectie niet worden gevonden</span><span class="sxs-lookup"><span data-stu-id="462a3-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="462a3-115">**Ondersteuning voor toepassingen waarvoor meerdere velden aanmelden** voor toepassingen waarvoor meer dan alleen gebruikersnaam en wachtwoord velden toosign in</span><span class="sxs-lookup"><span data-stu-id="462a3-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="462a3-116">**Hallo labels aanpassen** Hallo gebruikersnaam en wachtwoord invoervelden uw gebruikers te zien op Hallo [toepassing Toegangsvenster](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) wanneer ze hun referenties invoeren</span><span class="sxs-lookup"><span data-stu-id="462a3-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="462a3-117">Toestaan dat uw **gebruikers** tooprovide hun eigen gebruikersnamen en wachtwoorden voor bestaande toepassing accounts ze handmatig te op Hallo typen zijn [Toegangsvenster toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="462a3-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="462a3-118">Toestaan dat een **lid is van een bedrijfsgroep Hallo** toospecify Hallo gebruikersnamen en wachtwoorden tooa gebruiker toegewezen met behulp van Hallo [Self-Service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) functie</span><span class="sxs-lookup"><span data-stu-id="462a3-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="462a3-119">Toestaan dat een **beheerder** toospecify Hallo gebruikersnamen en wachtwoorden tooa gebruiker zijn toegewezen met behulp van de referenties van de Update Hallo functie wanneer [toewijzen van een gebruiker tooan-toepassing](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="462a3-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="462a3-120">Toestaan dat een **beheerder** toospecify Hallo gedeelde gebruikersnaam of het wachtwoord dat wordt gebruikt door een groep personen met behulp van de referenties van de Update Hallo functie wanneer [toewijzen van een groep tooan-toepassing](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="462a3-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="462a3-121">Hieronder wordt beschreven hoe u kunt inschakelen [op basis van wachtwoorden Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany toepassing toe te voegen met behulp van Hallo **toevoegen van een toepassing niet galerie** optreden.</span><span class="sxs-lookup"><span data-stu-id="462a3-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="462a3-122">Overzicht van stappen vereist</span><span class="sxs-lookup"><span data-stu-id="462a3-122">Overview of steps required</span></span>

<span data-ttu-id="462a3-123">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="462a3-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="462a3-124">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="462a3-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="462a3-125">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="462a3-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="462a3-126">Hallo toepassing tooa gebruiker of een groep toewijzen</span><span class="sxs-lookup"><span data-stu-id="462a3-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="462a3-127">De toepassing van een gebruiker tooan rechtstreeks toewijzen</span><span class="sxs-lookup"><span data-stu-id="462a3-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="462a3-128">Een groep van toepassingen tooa rechtstreeks toewijzen</span><span class="sxs-lookup"><span data-stu-id="462a3-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="462a3-129">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="462a3-129">Add a non-gallery application</span></span>

<span data-ttu-id="462a3-130">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="462a3-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="462a3-131">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="462a3-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="462a3-132">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="462a3-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="462a3-133">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="462a3-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="462a3-134">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="462a3-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="462a3-135">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade</span><span class="sxs-lookup"><span data-stu-id="462a3-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="462a3-136">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="462a3-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="462a3-137">Vul in Hallo Hallo-naam van uw toepassing **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="462a3-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="462a3-138">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="462a3-138">Select **Add.**</span></span>

<span data-ttu-id="462a3-139">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="462a3-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="462a3-140">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="462a3-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="462a3-141">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="462a3-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="462a3-142">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="462a3-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="462a3-143">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="462a3-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="462a3-144">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="462a3-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="462a3-145">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="462a3-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="462a3-146">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="462a3-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="462a3-147">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="462a3-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="462a3-148">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="462a3-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="462a3-149">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="462a3-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="462a3-150">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="462a3-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="462a3-151">Voer Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="462a3-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="462a3-152">Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen.</span><span class="sxs-lookup"><span data-stu-id="462a3-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="462a3-153">Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="462a3-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="462a3-154">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="462a3-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="462a3-155">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="462a3-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="462a3-156">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="462a3-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="462a3-157">De toepassing van een gebruiker tooan rechtstreeks toewijzen</span><span class="sxs-lookup"><span data-stu-id="462a3-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="462a3-158">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="462a3-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="462a3-159">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="462a3-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="462a3-160">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="462a3-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="462a3-161">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="462a3-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="462a3-162">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="462a3-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="462a3-163">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="462a3-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="462a3-164">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="462a3-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="462a3-165">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="462a3-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="462a3-166">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="462a3-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="462a3-167">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="462a3-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="462a3-168">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="462a3-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="462a3-169">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="462a3-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="462a3-170">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="462a3-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="462a3-171">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="462a3-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="462a3-172">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="462a3-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="462a3-173">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="462a3-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="462a3-174">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="462a3-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="462a3-175">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="462a3-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="462a3-176">Een groep van toepassingen tooa rechtstreeks toewijzen</span><span class="sxs-lookup"><span data-stu-id="462a3-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="462a3-177">tooassign een of meer groepen tooan toepassing rechtstreeks Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="462a3-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="462a3-178">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="462a3-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="462a3-179">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="462a3-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="462a3-180">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="462a3-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="462a3-181">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="462a3-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="462a3-182">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="462a3-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="462a3-183">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="462a3-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="462a3-184">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="462a3-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="462a3-185">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="462a3-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="462a3-186">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="462a3-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="462a3-187">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="462a3-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="462a3-188">Type in Hallo **volledige groepsnaam** van Hallo groep u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="462a3-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="462a3-189">Beweeg de muisaanwijzer over Hallo **groep** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="462a3-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="462a3-190">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van de groep uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="462a3-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="462a3-191">**Optioneel:** indien te gewenst**toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd van deze groep toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="462a3-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="462a3-192">Wanneer u klaar bent met groepen te selecteren, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="462a3-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="462a3-193">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello groepen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="462a3-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="462a3-194">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello geselecteerde groepen.</span><span class="sxs-lookup"><span data-stu-id="462a3-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="462a3-195">Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.</span><span class="sxs-lookup"><span data-stu-id="462a3-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="462a3-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="462a3-196">Next steps</span></span>
[<span data-ttu-id="462a3-197">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="462a3-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
