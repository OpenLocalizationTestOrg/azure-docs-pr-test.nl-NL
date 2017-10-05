---
title: Het configureren van federatieve eenmalige aanmelding voor een galerie van Azure AD-toepassing | Microsoft Docs
description: Het configureren van federatieve eenmalige aanmelding voor een bestaande-galerie van Azure AD-toepassing en het gebruik zelfstudies snel aan de slag
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
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="aab22-103">Het configureren van federatieve eenmalige aanmelding voor een galerie van Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="aab22-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="aab22-104">Alle toepassingen in de galerie van Azure AD ingeschakeld met Enterprise single sign-on-functionaliteit is een stapsgewijze zelfstudie beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="aab22-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="aab22-105">U hebt toegang tot de [lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor gedetailleerde stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="aab22-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="aab22-106">Overzicht van stappen vereist</span><span class="sxs-lookup"><span data-stu-id="aab22-106">Overview of steps required</span></span>
<span data-ttu-id="aab22-107">Een toepassing uit de galerie van Azure AD te hoeft configureren:</span><span class="sxs-lookup"><span data-stu-id="aab22-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="aab22-108">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="aab22-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="aab22-109">Waarden voor metagegevens van de toepassing configureren in Azure AD (URL,-id en antwoord-URL van de aanmelding)</span><span class="sxs-lookup"><span data-stu-id="aab22-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="aab22-110">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="aab22-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="aab22-111">Azure AD-metagegevens en certificaat ophalen</span><span class="sxs-lookup"><span data-stu-id="aab22-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="aab22-112">Azure AD metagegevenswaarden configureren in de toepassing (aanmelding URL, uitgever, afmelding URL en certificaat)</span><span class="sxs-lookup"><span data-stu-id="aab22-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="aab22-113">Gebruikers toewijzen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="aab22-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="aab22-114">Een toepassing toevoegen uit de galerie van Azure AD</span><span class="sxs-lookup"><span data-stu-id="aab22-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="aab22-115">Als u wilt een toepassing uit de galerie van Azure AD toevoegt, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="aab22-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="aab22-116">Open de [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**</span><span class="sxs-lookup"><span data-stu-id="aab22-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="aab22-117">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="aab22-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aab22-118">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="aab22-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aab22-119">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="aab22-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aab22-120">Klik op de **toevoegen** middenonder in de rechterbovenhoek op het **bedrijfstoepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="aab22-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="aab22-121">In de **Voer een naam** textbox uit de **toevoegen uit de galerie** sectie, typ de naam van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="aab22-122">Selecteer de toepassing die u wilt configureren voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aab22-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="aab22-123">Voordat u de toepassing toevoegt, kunt u de naam van de **naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="aab22-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="aab22-124">Klik op **toevoegen** knop, de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aab22-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="aab22-125">Na een korte periode, is het mogelijk om te zien van de toepassing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="aab22-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="aab22-126">Eenmalige aanmelding voor een toepassing uit de galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="aab22-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="aab22-127">Volg de onderstaande stappen voor het configureren van eenmalige aanmelding voor een toepassing:</span><span class="sxs-lookup"><span data-stu-id="aab22-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="aab22-128">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="aab22-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="aab22-129">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="aab22-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aab22-130">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="aab22-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aab22-131">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="aab22-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aab22-132">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aab22-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="aab22-133">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="aab22-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="aab22-134">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aab22-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="aab22-135">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aab22-136">Selecteer **op basis van SAML aanmelding** van de **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="aab22-137">Voer de vereiste waarden in **domein en de URL's.**</span><span class="sxs-lookup"><span data-stu-id="aab22-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="aab22-138">U moet deze waarden ophalen van de leverancier van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="aab22-139">Als u de toepassing configureren als Serviceprovider geïnitieerde eenmalige aanmelding, het teken op de URL voor is deze waarde vereist.</span><span class="sxs-lookup"><span data-stu-id="aab22-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="aab22-140">Voor sommige toepassingen is de id ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="aab22-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="aab22-141">Het is een vereiste waarde voor het configureren van de toepassing als IdP geïnitieerde eenmalige aanmelding, de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="aab22-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="aab22-142">Voor sommige toepassingen is de id ook een vereiste waarde.</span><span class="sxs-lookup"><span data-stu-id="aab22-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="aab22-143">**Optioneel:** klikt u op **weergeven geavanceerde instellingen voor URL** als u wilt zien van de waarden niet vereist.</span><span class="sxs-lookup"><span data-stu-id="aab22-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="aab22-144">In de **gebruikerskenmerken**, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="aab22-145">**Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="aab22-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="aab22-146">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="aab22-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="aab22-147">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="aab22-147">click **Add attribute**.</span></span> <span data-ttu-id="aab22-148">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="aab22-149">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="aab22-149">Click **Save.**</span></span> <span data-ttu-id="aab22-150">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="aab22-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="aab22-151">Klik op **configureren &lt;toepassingsnaam&gt;**  toegang tot documentatie over het configureren van eenmalige aanmelding in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="aab22-152">Bovendien heeft u de metagegevens-URL's en het certificaat dat is vereist voor het instellen van eenmalige aanmelding met de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="aab22-153">Klik op **opslaan** aan de configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="aab22-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="aab22-154">Gebruikers toewijzen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="aab22-155">Selecteer gebruikers-id en gebruikerskenmerken worden verzonden naar de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="aab22-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="aab22-156">Als u de gebruikers-ID selecteren of gebruikerskenmerken toevoegen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="aab22-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="aab22-157">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="aab22-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="aab22-158">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="aab22-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aab22-159">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="aab22-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aab22-160">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="aab22-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aab22-161">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aab22-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="aab22-162">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="aab22-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="aab22-163">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aab22-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="aab22-164">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aab22-165">Onder de **gebruikerskenmerken** sectie, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="aab22-166">De geselecteerde optie moet overeenkomen met de verwachte waarde in de toepassing om de gebruiker te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="aab22-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="aab22-167">Azure AD selecteren de indeling voor het kenmerk NameID (gebruikers-id) op basis van de waarde geselecteerd of de indeling die is aangevraagd door de toepassing in de SAML-AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="aab22-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="aab22-168">Raadpleeg voor meer informatie het artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder de sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="aab22-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="aab22-169">Gebruikerskenmerken toevoegen: klik op **weergeven en bewerken van alle andere gebruikerskenmerken** bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="aab22-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="aab22-170">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="aab22-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="aab22-171">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="aab22-171">click **Add attribute**.</span></span> <span data-ttu-id="aab22-172">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="aab22-173">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="aab22-173">Click **Save**.</span></span> <span data-ttu-id="aab22-174">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="aab22-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="aab22-175">De metagegevens van de Azure AD of het certificaat downloaden</span><span class="sxs-lookup"><span data-stu-id="aab22-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="aab22-176">Voor het downloaden van de metagegevens van de toepassing of het certificaat van Azure AD, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="aab22-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="aab22-177">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="aab22-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="aab22-178">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="aab22-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aab22-179">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="aab22-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aab22-180">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="aab22-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aab22-181">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aab22-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="aab22-182">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle Toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aab22-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="aab22-183">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aab22-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="aab22-184">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aab22-185">Ga naar **SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="aab22-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="aab22-186">Afhankelijk van wat de toepassing configureren van eenmalige aanmelding vereist, ziet u ofwel de optie voor het downloaden van de Metadata XML of het certificaat.</span><span class="sxs-lookup"><span data-stu-id="aab22-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="aab22-187">Azure AD biedt een URL als u de metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="aab22-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="aab22-188">De metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="aab22-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="aab22-189">Gebruikers toewijzen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="aab22-189">Assign users to the application</span></span>

<span data-ttu-id="aab22-190">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="aab22-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="aab22-191">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="aab22-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aab22-192">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="aab22-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aab22-193">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="aab22-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aab22-194">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="aab22-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aab22-195">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aab22-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="aab22-196">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="aab22-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="aab22-197">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="aab22-198">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aab22-199">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="aab22-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="aab22-200">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="aab22-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="aab22-201">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="aab22-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="aab22-202">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="aab22-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="aab22-203">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="aab22-204">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="aab22-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="aab22-205">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aab22-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="aab22-206">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="aab22-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="aab22-207">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="aab22-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="aab22-208">Na een korte periode, de gebruikers die u hebt geselecteerd mogelijk om deze toepassingen met behulp van de methoden die worden beschreven in de sectie oplossing beschrijving te starten.</span><span class="sxs-lookup"><span data-stu-id="aab22-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="aab22-209">De SAML-claims verzonden naar een toepassing aanpassen</span><span class="sxs-lookup"><span data-stu-id="aab22-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="aab22-210">Zie voor meer informatie over het aanpassen van de SAML-kenmerk claims verzonden naar uw toepassing, [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aab22-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aab22-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aab22-211">Next steps</span></span>
[<span data-ttu-id="aab22-212">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="aab22-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



