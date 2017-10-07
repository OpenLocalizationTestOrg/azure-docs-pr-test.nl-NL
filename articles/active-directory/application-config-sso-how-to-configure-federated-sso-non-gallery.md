---
title: aaaHow tooconfigure federatieve eenmalige aanmelding voor een toepassing niet galerie | Microsoft Docs
description: Hoe tooconfigure federatieve eenmalige aanmelding voor een aangepaste niet-galerie-toepassing die u toointegrate met Azure AD wilt
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="dba3e-103">Hoe tooconfigure federatieve eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="dba3e-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="dba3e-104">een toepassing niet galerie tooconfigure, moet u toohave Azure AD premium en toepassing hello SAML 2.0 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="dba3e-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="dba3e-105">Voor meer informatie over Azure AD-versies, gaat u naar [prijzen van Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="dba3e-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="dba3e-106">Overzicht van stappen vereist</span><span class="sxs-lookup"><span data-stu-id="dba3e-106">Overview of steps required</span></span>
<span data-ttu-id="dba3e-107">Hieronder volgt een overzicht op hoog niveau van Hallo stappen vereist tooconfigure federatieve eenmalige aanmelding voor een niet-galerie (bijvoorbeeld aangepaste) toepassing.</span><span class="sxs-lookup"><span data-stu-id="dba3e-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="dba3e-108">Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="dba3e-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="dba3e-109">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="dba3e-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="dba3e-110">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="dba3e-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="dba3e-111">Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="dba3e-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="dba3e-112">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="dba3e-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="dba3e-113">Eenmalige aanmelding toonon-galerie toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="dba3e-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="dba3e-114">tooconfigure eenmalige aanmelding voor een toepassing die zich niet in de galerie van Azure AD hello, stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="dba3e-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="dba3e-115">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dba3e-116">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="dba3e-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dba3e-117">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="dba3e-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dba3e-118">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="dba3e-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dba3e-119">Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="dba3e-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="dba3e-120">Klik op **Non-galerie toepassing** in Hallo **uw eigen app toevoegen** sectie</span><span class="sxs-lookup"><span data-stu-id="dba3e-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="dba3e-121">Voer de naam van de Hallo van de toepassing hello in Hallo **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="dba3e-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="dba3e-122">Klik op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dba3e-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="dba3e-123">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="dba3e-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="dba3e-124">Selecteer **op basis van SAML aanmelding** in Hallo **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="dba3e-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="dba3e-125">Voer waarden in Hallo vereist **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="dba3e-126">U moet deze waarden ophalen van de leverancier van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="dba3e-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="dba3e-127">tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding Hallo antwoord-URL en Hallo ID invoeren.</span><span class="sxs-lookup"><span data-stu-id="dba3e-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="dba3e-128">**Optioneel:** tooconfigure Hallo toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="dba3e-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="dba3e-129">In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="dba3e-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="dba3e-130">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="dba3e-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="dba3e-131">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="dba3e-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="dba3e-132">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="dba3e-132">click **Add attribute**.</span></span> <span data-ttu-id="dba3e-133">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="dba3e-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="dba3e-134">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-134">Click **Save.**</span></span> <span data-ttu-id="dba3e-135">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="dba3e-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="dba3e-136">Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dba3e-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="dba3e-137">Bovendien heeft u Azure AD-URL's en het certificaat dat is vereist voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="dba3e-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="dba3e-138">Gebruikers toohello toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="dba3e-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="dba3e-139">Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="dba3e-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="dba3e-140">tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="dba3e-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="dba3e-141">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dba3e-142">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="dba3e-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dba3e-143">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="dba3e-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dba3e-144">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="dba3e-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dba3e-145">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="dba3e-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="dba3e-146">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="dba3e-147">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dba3e-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="dba3e-148">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="dba3e-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dba3e-149">Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="dba3e-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="dba3e-150">Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dba3e-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="dba3e-151">[! Opmerking} Azure AD selecteren Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="dba3e-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="dba3e-152">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="dba3e-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="dba3e-153">gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="dba3e-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="dba3e-154">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="dba3e-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="dba3e-155">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="dba3e-155">click **Add attribute**.</span></span> <span data-ttu-id="dba3e-156">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="dba3e-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="dba3e-157">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-157">Click **Save.**</span></span> <span data-ttu-id="dba3e-158">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="dba3e-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="dba3e-159">Azure AD-metagegevens hello of een certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="dba3e-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="dba3e-160">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="dba3e-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="dba3e-161">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dba3e-162">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="dba3e-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dba3e-163">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="dba3e-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dba3e-164">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="dba3e-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dba3e-165">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="dba3e-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="dba3e-166">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="dba3e-167">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dba3e-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="dba3e-168">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="dba3e-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dba3e-169">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="dba3e-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="dba3e-170">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="dba3e-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="dba3e-171">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="dba3e-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="dba3e-172">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="dba3e-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="dba3e-173">Toohello-toepassing voor gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="dba3e-173">Assign users toohello application</span></span>

<span data-ttu-id="dba3e-174">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="dba3e-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="dba3e-175">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="dba3e-176">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="dba3e-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dba3e-177">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="dba3e-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dba3e-178">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="dba3e-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dba3e-179">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="dba3e-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="dba3e-180">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="dba3e-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="dba3e-181">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="dba3e-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="dba3e-182">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="dba3e-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dba3e-183">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="dba3e-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="dba3e-184">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="dba3e-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="dba3e-185">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="dba3e-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="dba3e-186">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="dba3e-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="dba3e-187">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="dba3e-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="dba3e-188">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="dba3e-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="dba3e-189">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="dba3e-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="dba3e-190">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="dba3e-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="dba3e-191">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="dba3e-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="dba3e-192">Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="dba3e-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="dba3e-193">Tooan toepassing aanpassen Hallo SAML claims worden verzonden</span><span class="sxs-lookup"><span data-stu-id="dba3e-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="dba3e-194">toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dba3e-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dba3e-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dba3e-195">Next steps</span></span>
[<span data-ttu-id="dba3e-196">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="dba3e-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
