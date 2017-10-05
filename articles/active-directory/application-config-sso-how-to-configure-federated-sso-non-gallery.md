---
title: Het configureren van federatieve eenmalige aanmelding voor een toepassing niet galerie | Microsoft Docs
description: Het configureren van federatieve eenmalige aanmelding voor een aangepaste niet-galerie-toepassing die u wilt integreren met Azure AD
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
ms.openlocfilehash: da7bc05c6452cde4d0236806f249559f178dd4e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="7de11-103">Het configureren van federatieve eenmalige aanmelding voor de toepassing van een niet-galerie</span><span class="sxs-lookup"><span data-stu-id="7de11-103">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="7de11-104">Als u een toepassing niet galerie configureren, moet u beschikken over Azure AD premium en de toepassing SAML 2.0 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="7de11-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="7de11-105">Voor meer informatie over Azure AD-versies, gaat u naar [prijzen van Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="7de11-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="7de11-106">Overzicht van stappen vereist</span><span class="sxs-lookup"><span data-stu-id="7de11-106">Overview of steps required</span></span>
<span data-ttu-id="7de11-107">Hieronder volgt een overzicht van hoog niveau van de stappen die nodig zijn voor het configureren van federatieve eenmalige aanmelding voor een niet-galerie (bijvoorbeeld aangepaste) toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="7de11-108">Waarden voor metagegevens van de toepassing configureren in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="7de11-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="7de11-109">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="7de11-109">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="7de11-110">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="7de11-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="7de11-111">Azure AD metagegevenswaarden configureren in de toepassing (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="7de11-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="7de11-112">Gebruikers toewijzen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="7de11-112">Assign users to the application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-to-non-gallery-applications"></a><span data-ttu-id="7de11-113">Eenmalige aanmelding niet galerie toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="7de11-113">Configuring single sign-on to non-gallery applications</span></span>

<span data-ttu-id="7de11-114">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing die zich niet in de galerie van Azure AD:</span><span class="sxs-lookup"><span data-stu-id="7de11-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="7de11-115">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7de11-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7de11-116">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="7de11-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7de11-117">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7de11-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7de11-118">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="7de11-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7de11-119">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="7de11-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="7de11-120">Klik op **Non-galerie toepassing** in de **uw eigen app toevoegen** sectie</span><span class="sxs-lookup"><span data-stu-id="7de11-120">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="7de11-121">Voer de naam van de toepassing in de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="7de11-121">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="7de11-122">Klik op **toevoegen** knop, de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7de11-122">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="7de11-123">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="7de11-124">Selecteer **op basis van SAML aanmelding** in de **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="7de11-125">Voer de vereiste waarden in **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="7de11-125">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="7de11-126">U moet deze waarden ophalen van de leverancier van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-126">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="7de11-127">Voer de antwoord-URL en de id voor het configureren van de toepassing als IdP geïnitieerde eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7de11-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2. <span data-ttu-id="7de11-128">**Optioneel:** voor het configureren van de toepassing als Serviceprovider geïnitieerde eenmalige aanmelding, het teken op de URL voor deze waarde is vereist.</span><span class="sxs-lookup"><span data-stu-id="7de11-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="7de11-129">In de **gebruikerskenmerken**, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="7de11-130">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7de11-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7de11-131">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7de11-131">To add an attribute:</span></span>

   1. <span data-ttu-id="7de11-132">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="7de11-132">click **Add attribute**.</span></span> <span data-ttu-id="7de11-133">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-133">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="7de11-134">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="7de11-134">Click **Save.**</span></span> <span data-ttu-id="7de11-135">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="7de11-135">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="7de11-136">Klik op **configureren &lt;toepassingsnaam&gt;**  toegang tot documentatie over het configureren van eenmalige aanmelding in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="7de11-137">Bovendien heeft u Azure AD-URL's en het certificaat dat is vereist voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-137">Also, you has Azure AD URLs and certificate required for the application.</span></span>

15. [<span data-ttu-id="7de11-138">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-138">Assign users to the application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="7de11-139">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="7de11-139">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="7de11-140">Als u de gebruikers-ID selecteren of gebruikerskenmerken toevoegen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7de11-140">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="7de11-141">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7de11-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7de11-142">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="7de11-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7de11-143">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7de11-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7de11-144">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="7de11-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7de11-145">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7de11-145">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7de11-146">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="7de11-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7de11-147">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7de11-147">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7de11-148">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7de11-149">Onder de **gebruikerskenmerken** sectie, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="7de11-150">De geselecteerde optie moet overeenkomen met de verwachte waarde in de toepassing om de gebruiker te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="7de11-150">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

 ><span data-ttu-id="7de11-151">[! Opmerking} Azure AD de indeling voor het kenmerk NameID (gebruikers-id) op basis van de geselecteerde waarde of de indeling die is aangevraagd door de toepassing in de SAML-AuthRequest selecteren.</span><span class="sxs-lookup"><span data-stu-id="7de11-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="7de11-152">Raadpleeg voor meer informatie het artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder de sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="7de11-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="7de11-153">Gebruikerskenmerken toevoegen: klik op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7de11-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7de11-154">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7de11-154">To add an attribute:</span></span>

   1. <span data-ttu-id="7de11-155">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="7de11-155">click **Add attribute**.</span></span> <span data-ttu-id="7de11-156">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-156">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="7de11-157">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="7de11-157">Click **Save.**</span></span> <span data-ttu-id="7de11-158">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="7de11-158">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="7de11-159">De metagegevens van de Azure AD of het certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="7de11-159">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="7de11-160">Voor het downloaden van de metagegevens van de toepassing of het certificaat van Azure AD, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7de11-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="7de11-161">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7de11-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7de11-162">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="7de11-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7de11-163">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7de11-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7de11-164">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="7de11-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7de11-165">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7de11-165">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7de11-166">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="7de11-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7de11-167">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7de11-167">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7de11-168">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7de11-169">Ga naar **SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="7de11-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="7de11-170">Afhankelijk van wat de toepassing configureren van eenmalige aanmelding vereist, ziet u ofwel de optie voor het downloaden van de Metadata XML of het certificaat.</span><span class="sxs-lookup"><span data-stu-id="7de11-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="7de11-171">Azure AD biedt een URL als u de metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="7de11-171">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="7de11-172">De metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="7de11-172">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="7de11-173">Gebruikers toewijzen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="7de11-173">Assign users to the application</span></span>

<span data-ttu-id="7de11-174">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7de11-174">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="7de11-175">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7de11-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7de11-176">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="7de11-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7de11-177">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7de11-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7de11-178">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="7de11-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7de11-179">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7de11-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7de11-180">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="7de11-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7de11-181">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-181">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="7de11-182">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7de11-183">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="7de11-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7de11-184">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="7de11-184">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7de11-185">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="7de11-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7de11-186">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="7de11-186">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="7de11-187">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="7de11-188">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="7de11-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="7de11-189">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7de11-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="7de11-190">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7de11-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="7de11-191">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7de11-191">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="7de11-192">Na een korte periode, de gebruikers die u hebt geselecteerd mogelijk om deze toepassingen met behulp van de methoden die worden beschreven in de sectie oplossing beschrijving te starten.</span><span class="sxs-lookup"><span data-stu-id="7de11-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="7de11-193">De SAML-claims verzonden naar een toepassing aanpassen</span><span class="sxs-lookup"><span data-stu-id="7de11-193">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="7de11-194">Zie voor meer informatie over het aanpassen van de SAML-kenmerk claims verzonden naar uw toepassing, [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7de11-194">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7de11-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7de11-195">Next steps</span></span>
[<span data-ttu-id="7de11-196">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="7de11-196">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
