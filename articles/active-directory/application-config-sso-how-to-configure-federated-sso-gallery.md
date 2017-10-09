---
title: aaaHow tooconfigure federatieve eenmalige aanmelding voor een galerie van Azure AD-toepassing | Microsoft Docs
description: Hoe tooconfigure federatieve eenmalige aanmelding voor een bestaande-galerie van Azure AD-toepassing en het gebruik zelfstudies tooget snel gaan
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="54ce1-103">Hoe tooconfigure federatieve eenmalige aanmelding voor een galerie van Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="54ce1-103">How tooconfigure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="54ce1-104">Alle toepassingen in hello Azure AD-galerie ingeschakeld met Enterprise single sign-on-functionaliteit is een stapsgewijze zelfstudie beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="54ce1-104">All applications in hello Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="54ce1-105">U hebt toegang tot Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor gedetailleerde stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="54ce1-105">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="54ce1-106">Overzicht van stappen vereist</span><span class="sxs-lookup"><span data-stu-id="54ce1-106">Overview of steps required</span></span>
<span data-ttu-id="54ce1-107">een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:</span><span class="sxs-lookup"><span data-stu-id="54ce1-107">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="54ce1-108">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="54ce1-108">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="54ce1-109">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="54ce1-109">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="54ce1-110">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="54ce1-110">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="54ce1-111">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="54ce1-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="54ce1-112">Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="54ce1-112">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="54ce1-113">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="54ce1-113">Assign users toohello application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="54ce1-114">Een toepassing uit de galerie van Azure AD Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="54ce1-114">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="54ce1-115">een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="54ce1-115">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="54ce1-116">Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="54ce1-116">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="54ce1-117">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="54ce1-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="54ce1-118">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="54ce1-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="54ce1-119">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="54ce1-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="54ce1-120">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="54ce1-120">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="54ce1-121">In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="54ce1-121">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="54ce1-122">Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="54ce1-122">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="54ce1-123">Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="54ce1-123">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="54ce1-124">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="54ce1-124">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="54ce1-125">Na een korte periode, moet u kunnen toosee Hallo van de toepassing configuration blade zijn.</span><span class="sxs-lookup"><span data-stu-id="54ce1-125">After a short period of time, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="54ce1-126">Eenmalige aanmelding voor een toepassing van Hallo-galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="54ce1-126">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="54ce1-127">Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="54ce1-127">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="54ce1-128">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="54ce1-128">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="54ce1-129">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="54ce1-129">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="54ce1-130">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="54ce1-130">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="54ce1-131">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="54ce1-131">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="54ce1-132">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="54ce1-132">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="54ce1-133">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-133">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="54ce1-134">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="54ce1-134">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="54ce1-135">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="54ce1-135">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="54ce1-136">Selecteer **op basis van SAML aanmelding** van Hallo **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="54ce1-136">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="54ce1-137">Voer waarden in Hallo vereist **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-137">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="54ce1-138">U moet deze waarden ophalen van de leverancier van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="54ce1-138">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="54ce1-139">tooconfigure hello toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="54ce1-139">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="54ce1-140">Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="54ce1-140">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="54ce1-141">tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding, Hallo antwoord-URL is een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="54ce1-141">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="54ce1-142">Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="54ce1-142">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="54ce1-143">**Optioneel:** klikt u op **weergeven geavanceerde instellingen voor URL** als u toosee Hallo niet vereist waarden wilt.</span><span class="sxs-lookup"><span data-stu-id="54ce1-143">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="54ce1-144">In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="54ce1-144">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="54ce1-145">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="54ce1-145">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

  <span data-ttu-id="54ce1-146">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="54ce1-146">tooadd an attribute:</span></span>
   
   1. <span data-ttu-id="54ce1-147">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="54ce1-147">click **Add attribute**.</span></span> <span data-ttu-id="54ce1-148">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="54ce1-148">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   1. <span data-ttu-id="54ce1-149">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-149">Click **Save.**</span></span> <span data-ttu-id="54ce1-150">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="54ce1-150">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="54ce1-151">Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="54ce1-151">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="54ce1-152">U heeft ook Hallo metagegevens-URL's en vereiste certificaat toosetup eenmalige aanmelding met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="54ce1-152">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="54ce1-153">Klik op **opslaan** toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="54ce1-153">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="54ce1-154">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="54ce1-154">Assign users toohello application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="54ce1-155">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="54ce1-155">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="54ce1-156">tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="54ce1-156">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="54ce1-157">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-157">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="54ce1-158">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="54ce1-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="54ce1-159">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="54ce1-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="54ce1-160">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="54ce1-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="54ce1-161">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="54ce1-161">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="54ce1-162">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-162">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="54ce1-163">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="54ce1-163">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="54ce1-164">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="54ce1-164">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="54ce1-165">Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="54ce1-165">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="54ce1-166">Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="54ce1-166">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="54ce1-167">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="54ce1-167">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="54ce1-168">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="54ce1-168">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="54ce1-169">gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="54ce1-169">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="54ce1-170">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="54ce1-170">tooadd an attribute:</span></span>
  
   1. <span data-ttu-id="54ce1-171">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="54ce1-171">click **Add attribute**.</span></span> <span data-ttu-id="54ce1-172">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="54ce1-172">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="54ce1-173">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="54ce1-173">Click **Save**.</span></span> <span data-ttu-id="54ce1-174">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="54ce1-174">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="54ce1-175">Azure AD-metagegevens hello of een certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="54ce1-175">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="54ce1-176">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="54ce1-176">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="54ce1-177">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-177">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="54ce1-178">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="54ce1-178">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="54ce1-179">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="54ce1-179">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="54ce1-180">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="54ce1-180">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="54ce1-181">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="54ce1-181">click **All Applications** tooview a list of all your applications.</span></span>

  *  <span data-ttu-id="54ce1-182">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="54ce1-182">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications**.</span></span>

6.  <span data-ttu-id="54ce1-183">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="54ce1-183">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="54ce1-184">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="54ce1-184">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="54ce1-185">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="54ce1-185">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="54ce1-186">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="54ce1-186">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="54ce1-187">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="54ce1-187">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="54ce1-188">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="54ce1-188">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="54ce1-189">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="54ce1-189">Assign users toohello application</span></span>

<span data-ttu-id="54ce1-190">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="54ce1-190">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="54ce1-191">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-191">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="54ce1-192">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="54ce1-192">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="54ce1-193">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="54ce1-193">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="54ce1-194">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="54ce1-194">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="54ce1-195">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="54ce1-195">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="54ce1-196">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="54ce1-196">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="54ce1-197">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="54ce1-197">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="54ce1-198">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="54ce1-198">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="54ce1-199">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="54ce1-199">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="54ce1-200">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="54ce1-200">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="54ce1-201">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="54ce1-201">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="54ce1-202">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="54ce1-202">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="54ce1-203">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="54ce1-203">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="54ce1-204">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="54ce1-204">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="54ce1-205">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="54ce1-205">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="54ce1-206">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="54ce1-206">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="54ce1-207">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="54ce1-207">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="54ce1-208">Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="54ce1-208">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="54ce1-209">Tooan toepassing aanpassen Hallo SAML claims worden verzonden</span><span class="sxs-lookup"><span data-stu-id="54ce1-209">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="54ce1-210">toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="54ce1-210">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54ce1-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54ce1-211">Next steps</span></span>
[<span data-ttu-id="54ce1-212">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="54ce1-212">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



