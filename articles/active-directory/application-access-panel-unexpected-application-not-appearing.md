---
title: aaaAn toegewezen toepassing wordt niet weergegeven op het toegangsvenster Hallo | Microsoft Docs
description: Waarom een toepassing wordt niet weergegeven in het deelvenster toegang Hallo
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
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="91940-103">Een toegewezen toepassing wordt niet weergegeven op het toegangsvenster Hallo</span><span class="sxs-lookup"><span data-stu-id="91940-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="91940-104">Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="91940-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="91940-105">Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="91940-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="91940-106">Hallo-toepassing moet correct worden geconfigureerd en toegewezen toohello gebruiker of een groep Hallo-gebruiker lid is van toepassing op Hallo toosee in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="91940-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="91940-107">Hallo-type van een gebruiker ziet u mogelijk apps kunnen worden onderverdeeld in de volgende categorieën Hallo:</span><span class="sxs-lookup"><span data-stu-id="91940-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="91940-108">Office 365-toepassingen</span><span class="sxs-lookup"><span data-stu-id="91940-108">Office 365 Applications</span></span>

-   <span data-ttu-id="91940-109">Microsoft en derden toepassingen die zijn geconfigureerd op basis van een federatieve aanmelding bij</span><span class="sxs-lookup"><span data-stu-id="91940-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="91940-110">SSO-toepassingen op basis van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="91940-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="91940-111">Toepassingen met bestaande oplossingen voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="91940-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="91940-112">Algemene problemen toocheck eerst</span><span class="sxs-lookup"><span data-stu-id="91940-112">General issues toocheck first</span></span>

-   <span data-ttu-id="91940-113">Als een toepassing NET tooa gebruiker werd toegevoegd, opnieuw toosign in en uit in het toegangsvenster Hallo van de gebruiker na een paar minuten toosee als toepassing hello wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="91940-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="91940-114">Als u een licentie is verwijderd uit een gebruiker of groep Hallo gebruiker is dat lid van deze kan lang duren, afhankelijk van Hallo omvang en complexiteit van de groep Hallo voor toobe van wijzigingen aangebracht.</span><span class="sxs-lookup"><span data-stu-id="91940-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="91940-115">Voor extra tijd voordat je je aanmeldt bij Hallo Toegangsvenster toestaan.</span><span class="sxs-lookup"><span data-stu-id="91940-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="91940-116">Problemen met gerelateerde tooapplication configuratie</span><span class="sxs-lookup"><span data-stu-id="91940-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="91940-117">Een toepassing kan niet worden weergegeven in het deelvenster voor een gebruiker toegang omdat deze niet correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="91940-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="91940-118">Hieronder volgen enkele manieren waarop die u gerelateerde tooapplication configuratie van problemen kunt oplossen:</span><span class="sxs-lookup"><span data-stu-id="91940-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="91940-119">Hoe tooconfigure federatieve eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="91940-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="91940-120">Hoe tooconfigure federatieve eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="91940-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="91940-121">Hoe tooconfigure een wachtwoord eenmalige aanmelding-toepassing voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="91940-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="91940-122">Hoe tooconfigure een wachtwoord eenmalige aanmelding-toepassing voor een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="91940-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="91940-123">Hoe tooconfigure federatieve eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="91940-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="91940-124">Alle toepassingen in de galerie van Azure AD Hallo ingeschakeld met Enterprise Single Sign-On-functionaliteit is een stapsgewijze zelfstudie beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="91940-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="91940-125">U hebt toegang tot Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.</span><span class="sxs-lookup"><span data-stu-id="91940-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="91940-126">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="91940-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="91940-127">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="91940-128">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="91940-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="91940-129">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="91940-130">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="91940-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="91940-131">Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="91940-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="91940-132">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="91940-133">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="91940-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-134">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="91940-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="91940-135">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-136">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-137">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-138">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="91940-139">In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="91940-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="91940-140">Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="91940-141">Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="91940-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="91940-142">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="91940-143">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="91940-144">Eenmalige aanmelding voor een toepassing van Hallo-galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="91940-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="91940-145">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="91940-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-146">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-147">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-148">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-149">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-150">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="91940-151">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-152">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="91940-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="91940-153">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-154">Selecteer **op basis van SAML aanmelding** van Hallo **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="91940-155">Voer waarden in Hallo vereist **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="91940-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="91940-156">U moet deze waarden ophalen van de leverancier van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="91940-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="91940-157">tooconfigure hello toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="91940-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="91940-158">Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="91940-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="91940-159">tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding, Hallo antwoord-URL is een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="91940-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="91940-160">Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="91940-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="91940-161">**Optioneel:** klikt u op **weergeven geavanceerde instellingen voor URL** als u toosee Hallo niet vereist waarden wilt.</span><span class="sxs-lookup"><span data-stu-id="91940-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="91940-162">In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="91940-163">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="91940-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="91940-164">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="91940-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="91940-165">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="91940-165">click **Add attribute**.</span></span> <span data-ttu-id="91940-166">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="91940-167">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="91940-167">click **Save.**</span></span> <span data-ttu-id="91940-168">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="91940-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="91940-169">Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="91940-170">U heeft ook Hallo metagegevens-URL's en vereiste certificaat toosetup eenmalige aanmelding met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="91940-171">Klik op **opslaan** toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="91940-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="91940-172">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="91940-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="91940-173">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="91940-174">tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="91940-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-175">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-176">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-177">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-178">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-179">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="91940-180">Als u Hallo-toepassing die u wilt dat tooshow hier niet ziet, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-181">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91940-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="91940-182">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-183">Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="91940-184">Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="91940-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="91940-185">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="91940-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="91940-186">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="91940-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="91940-187">gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="91940-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="91940-188">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="91940-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="91940-189">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="91940-189">click **Add attribute**.</span></span> <span data-ttu-id="91940-190">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="91940-191">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="91940-191">click **Save.**</span></span> <span data-ttu-id="91940-192">Hier ziet u nieuw kenmerk in de tabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="91940-193">Azure AD-metagegevens hello of een certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="91940-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="91940-194">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="91940-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-195">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-196">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-197">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-198">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-199">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="91940-200">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-201">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91940-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="91940-202">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-203">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="91940-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="91940-204">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="91940-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="91940-205">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="91940-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="91940-206">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="91940-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="91940-207">Hoe tooconfigure federatieve eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="91940-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="91940-208">een toepassing niet galerie tooconfigure, moet u toohave Azure AD premium en toepassing hello SAML 2.0 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="91940-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="91940-209">Voor meer informatie over Azure AD-versies, gaat u naar [prijzen van Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="91940-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="91940-210">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="91940-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="91940-211">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="91940-212">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="91940-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="91940-213">Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="91940-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="91940-214">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="91940-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="91940-215">tooconfigure eenmalige aanmelding voor een toepassing die zich niet in de galerie van Azure AD hello, stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="91940-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-216">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-217">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-218">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-219">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-220">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="91940-221">Klik op **Non-galerie toepassing** in Hallo **uw eigen app toevoegen** sectie.</span><span class="sxs-lookup"><span data-stu-id="91940-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="91940-222">Voer de naam van de Hallo van de toepassing hello in Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="91940-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="91940-223">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="91940-224">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="91940-225">Selecteer **op basis van SAML aanmelding** in Hallo **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="91940-226">Voer waarden in Hallo vereist **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="91940-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="91940-227">U moet deze waarden ophalen van de leverancier van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="91940-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="91940-228">tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding Hallo antwoord-URL en Hallo ID invoeren.</span><span class="sxs-lookup"><span data-stu-id="91940-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="91940-229">**Optioneel:** tooconfigure Hallo toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="91940-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="91940-230">In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="91940-231">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="91940-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="91940-232">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="91940-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="91940-233">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="91940-233">click **Add attribute**.</span></span> <span data-ttu-id="91940-234">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="91940-235">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="91940-235">Click **Save.**</span></span> <span data-ttu-id="91940-236">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="91940-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="91940-237">Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="91940-238">Bovendien heeft u Azure AD-URL's en het certificaat dat is vereist voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="91940-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="91940-239">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="91940-240">tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="91940-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-241">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-242">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-243">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-244">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-245">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="91940-246">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-247">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91940-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="91940-248">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-249">Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="91940-250">Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="91940-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="91940-251">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="91940-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="91940-252">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="91940-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="91940-253">gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="91940-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="91940-254">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="91940-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="91940-255">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="91940-255">click **Add attribute**.</span></span> <span data-ttu-id="91940-256">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="91940-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="91940-257">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="91940-257">Click **Save.**</span></span> <span data-ttu-id="91940-258">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="91940-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="91940-259">Azure AD-metagegevens hello of een certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="91940-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="91940-260">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="91940-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-261">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-262">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-263">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-264">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-265">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="91940-266">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-267">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91940-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="91940-268">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-269">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="91940-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="91940-270">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="91940-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="91940-271">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="91940-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="91940-272">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="91940-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="91940-273">Hoe tooconfigure wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="91940-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="91940-274">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="91940-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="91940-275">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="91940-276">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="91940-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="91940-277">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="91940-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="91940-278">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="91940-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-279">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="91940-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="91940-280">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-281">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-282">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-283">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="91940-284">In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="91940-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="91940-285">Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="91940-286">Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="91940-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="91940-287">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="91940-288">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="91940-289">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="91940-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="91940-290">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="91940-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-291">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-292">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-293">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-294">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-295">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="91940-296">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-297">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="91940-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="91940-298">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-299">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="91940-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="91940-300">[Gebruikers toewijzen toohello toepassing](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="91940-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="91940-301">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="91940-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="91940-302">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="91940-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="91940-303">Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="91940-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="91940-304">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="91940-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="91940-305">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="91940-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="91940-306">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="91940-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="91940-307">Toevoegen van een toepassing niet-galerie</span><span class="sxs-lookup"><span data-stu-id="91940-307">Add a non-gallery application</span></span>

<span data-ttu-id="91940-308">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="91940-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-309">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="91940-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="91940-310">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-311">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-312">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-313">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="91940-314">Klik op **Non-galerie-toepassing.**</span><span class="sxs-lookup"><span data-stu-id="91940-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="91940-315">Vul in Hallo Hallo-naam van uw toepassing **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="91940-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="91940-316">Selecteer **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="91940-316">Select **Add.**</span></span>

<span data-ttu-id="91940-317">Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="91940-318">Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren</span><span class="sxs-lookup"><span data-stu-id="91940-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="91940-319">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="91940-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-320">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="91940-321">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-322">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-323">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-324">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="91940-325">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-326">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="91940-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="91940-327">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-328">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="91940-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="91940-329">Voer Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="91940-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="91940-330">Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen.</span><span class="sxs-lookup"><span data-stu-id="91940-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="91940-331">Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="91940-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="91940-332">[Gebruikers toewijzen toohello toepassing](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="91940-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="91940-333">Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="91940-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="91940-334">Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.</span><span class="sxs-lookup"><span data-stu-id="91940-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="91940-335">Problemen met gerelateerde tooassigning toepassingen toousers</span><span class="sxs-lookup"><span data-stu-id="91940-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="91940-336">Een gebruiker mogelijk niet ziet u een toepassing op hun Toegangsvenster omdat ze toohello toepassing nog niet zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="91940-337">Hieronder vindt u enkele toocheck manieren:</span><span class="sxs-lookup"><span data-stu-id="91940-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="91940-338">Controleren of een gebruiker toohello toepassing is toegewezen</span><span class="sxs-lookup"><span data-stu-id="91940-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="91940-339">Hoe een gebruiker tooan toepassing rechtstreeks tooassign</span><span class="sxs-lookup"><span data-stu-id="91940-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="91940-340">Controleer of een gebruiker is toegewezen licentie tooa gerelateerde toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="91940-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="91940-341">Hoe tooassign een licentie tooa gebruiker</span><span class="sxs-lookup"><span data-stu-id="91940-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="91940-342">Controleren of een gebruiker toohello toepassing is toegewezen</span><span class="sxs-lookup"><span data-stu-id="91940-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="91940-343">toocheck als een gebruiker is toegewezen toohello-toepassing hello volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="91940-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-344">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="91940-345">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-346">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-347">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-348">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="91940-349">**Search** voor Hallo-naam van de betrokken Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="91940-350">Klik op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="91940-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="91940-351">Controleer toosee als de gebruiker toohello toepassing is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="91940-352">Als dat niet het Hallo-stappen in ' hoe tooassign een tooan Gebruikerstoepassing rechtstreeks ' toodo zodat.</span><span class="sxs-lookup"><span data-stu-id="91940-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="91940-353">Hoe een gebruiker tooan toepassing rechtstreeks tooassign</span><span class="sxs-lookup"><span data-stu-id="91940-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="91940-354">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="91940-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-355">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="91940-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="91940-356">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-357">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-358">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-359">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="91940-360">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-361">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="91940-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="91940-362">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-363">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="91940-364">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="91940-365">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="91940-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="91940-366">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="91940-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="91940-367">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="91940-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="91940-368">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="91940-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="91940-369">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="91940-370">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="91940-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="91940-371">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="91940-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="91940-372">Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.</span><span class="sxs-lookup"><span data-stu-id="91940-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="91940-373">Controleer of een gebruiker zich onder een licentie gerelateerde toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="91940-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="91940-374">toocheck een gebruiker de toegewezen licenties, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="91940-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-375">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="91940-376">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-377">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-378">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="91940-379">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="91940-379">click **All users**.</span></span>

6.  <span data-ttu-id="91940-380">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="91940-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="91940-381">Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="91940-382">Hallo Toegangsvenster van de gebruiker als Hallo gebruiker tooan dit eerste partij Office-toepassingen tooappear inschakelen op Office-licentie is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="91940-383">Hoe een gebruiker een licentie tooassign</span><span class="sxs-lookup"><span data-stu-id="91940-383">How tooassign a user a license</span></span> 

<span data-ttu-id="91940-384">een gebruiker van de tooa licentie tooassign Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="91940-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-385">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="91940-386">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-387">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-388">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="91940-389">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="91940-389">click **All users**.</span></span>

6.  <span data-ttu-id="91940-390">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="91940-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="91940-391">Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="91940-392">Klik op Hallo **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="91940-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="91940-393">Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="91940-394">**Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="91940-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="91940-395">Klik op **Ok** wanneer dit is voltooid.</span><span class="sxs-lookup"><span data-stu-id="91940-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="91940-396">Klik op Hallo **toewijzen** knop tooassign deze licenties toothis-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="91940-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="91940-397">Problemen met gerelateerde tooassigning toepassingen toogroups</span><span class="sxs-lookup"><span data-stu-id="91940-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="91940-398">Een gebruiker mogelijk ziet u een toepassing op hun Toegangsvenster omdat ze deel uitmaken van een groep die de toepassing hello is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="91940-399">Hieronder vindt u enkele toocheck manieren:</span><span class="sxs-lookup"><span data-stu-id="91940-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="91940-400">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="91940-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="91940-401">Hoe tooassign een toepassing tooa groepeert rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="91940-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="91940-402">Controleer of een gebruiker deel van de groep tooa licentie is toegewezen uitmaakt</span><span class="sxs-lookup"><span data-stu-id="91940-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="91940-403">Hoe een licentiegroep tooa tooassign</span><span class="sxs-lookup"><span data-stu-id="91940-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="91940-404">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="91940-404">Check a user’s group memberships</span></span>

<span data-ttu-id="91940-405">toocheck een groepslidmaatschap, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="91940-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-406">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="91940-407">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-408">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-409">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="91940-410">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="91940-410">click **All users**.</span></span>

6.  <span data-ttu-id="91940-411">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="91940-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="91940-412">Klik op **groepen**.</span><span class="sxs-lookup"><span data-stu-id="91940-412">click **Groups**.</span></span>

8.  <span data-ttu-id="91940-413">Controleer de toosee als de gebruiker deel uit van een groep die is toegewezen toohello-toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="91940-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="91940-414">Als u tooremove Hallo gebruiker uit groep Hallo wilt **klikt u op Hallo rij** van Hallo groep en selecteer verwijderen.</span><span class="sxs-lookup"><span data-stu-id="91940-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="91940-415">Hoe tooassign een toepassing tooa groepeert rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="91940-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="91940-416">tooassign een of meer groepen tooan toepassing rechtstreeks Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="91940-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-417">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="91940-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="91940-418">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-419">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-420">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="91940-421">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="91940-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="91940-422">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="91940-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="91940-423">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="91940-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="91940-424">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="91940-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="91940-425">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="91940-426">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="91940-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="91940-427">Type in Hallo **volledige groepsnaam** van Hallo groep u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="91940-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="91940-428">Beweeg de muisaanwijzer over Hallo **groep** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="91940-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="91940-429">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van de groep uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="91940-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="91940-430">**Optioneel:** indien te gewenst**toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd van deze groep toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="91940-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="91940-431">Wanneer u klaar bent met groepen te selecteren, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="91940-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="91940-432">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello groepen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="91940-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="91940-433">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello geselecteerde groepen.</span><span class="sxs-lookup"><span data-stu-id="91940-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="91940-434">Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.</span><span class="sxs-lookup"><span data-stu-id="91940-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="91940-435">Controleer of een gebruiker deel van de groep tooa licentie is toegewezen uitmaakt</span><span class="sxs-lookup"><span data-stu-id="91940-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="91940-436">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="91940-437">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-438">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-439">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="91940-440">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="91940-440">click **All users**.</span></span>

6.  <span data-ttu-id="91940-441">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="91940-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="91940-442">Klik op **groepen**.</span><span class="sxs-lookup"><span data-stu-id="91940-442">click **Groups**.</span></span>

8.  <span data-ttu-id="91940-443">Klik op Hallo rij van een bepaalde groep.</span><span class="sxs-lookup"><span data-stu-id="91940-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="91940-444">Klik op **licenties** toosee welke licenties Hallo groep tooit is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="91940-445">Hallo Toegangsvenster van de gebruiker als Hallo groep tooan dit mogelijk bepaalde tooappear eerste partij Office-toepassingen inschakelen op Office-licentie is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="91940-446">Hoe een licentiegroep tooa tooassign</span><span class="sxs-lookup"><span data-stu-id="91940-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="91940-447">een licentiegroep tooa tooassign Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="91940-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="91940-448">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="91940-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="91940-449">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="91940-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="91940-450">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="91940-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="91940-451">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="91940-452">Klik op **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="91940-452">click **All groups**.</span></span>

6.  <span data-ttu-id="91940-453">**Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="91940-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="91940-454">Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91940-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="91940-455">Klik op Hallo **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="91940-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="91940-456">Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.</span><span class="sxs-lookup"><span data-stu-id="91940-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="91940-457">**Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="91940-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="91940-458">Klik op **Ok** wanneer dit is voltooid.</span><span class="sxs-lookup"><span data-stu-id="91940-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="91940-459">Klik op Hallo **toewijzen** knop tooassign deze groep toothis-licenties.</span><span class="sxs-lookup"><span data-stu-id="91940-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="91940-460">Dit kan lang duren, afhankelijk van Hallo omvang en complexiteit van Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="91940-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="91940-461">toodo dit snellere en overweeg tijdelijk een licentie toohello gebruiker rechtstreeks toewijzen.</span><span class="sxs-lookup"><span data-stu-id="91940-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="91940-462">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91940-462">Next steps</span></span>
[<span data-ttu-id="91940-463">Toevoegen van nieuwe gebruikers tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91940-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

