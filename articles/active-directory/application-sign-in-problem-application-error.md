---
title: Fout op de pagina voor een toepassing na het aanmelden | Microsoft Docs
description: Het oplossen van problemen met Azure AD aanmelden wanneer de toepassing zelf een fout opgetreden genereert
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="3581e-103">Fout op de pagina voor een toepassing na het aanmelden</span><span class="sxs-lookup"><span data-stu-id="3581e-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="3581e-104">In dit scenario, Azure AD heeft de gebruiker in ondertekend, maar de toepassing is een fout opgetreden waardoor de gebruiker te kunnen voltooien van de aanmeldingspagina stroom niet kan weergeven.</span><span class="sxs-lookup"><span data-stu-id="3581e-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="3581e-105">In dit scenario is de toepassing niet het probleem antwoord accepteert door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3581e-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="3581e-106">Er zijn enkele mogelijke redenen waarom de reactie van Azure AD is de toepassing niet geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="3581e-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="3581e-107">Als de fout in de toepassing niet duidelijk is weten wat ontbreekt in het antwoord vervolgens:</span><span class="sxs-lookup"><span data-stu-id="3581e-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="3581e-108">Als de toepassing de galerie van Azure AD wordt, controleert u of u alle stappen in het artikel hebt gevolgd [fouten opsporen in op basis van SAML eenmalige aanmelding tot toepassingen in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="3581e-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="3581e-109">Gebruik een hulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) voor het vastleggen van SAML-aanvraag, SAML-reactie en SAML-token.</span><span class="sxs-lookup"><span data-stu-id="3581e-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="3581e-110">De SAML-reactie delen met de leverancier van de toepassing te weten wat ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="3581e-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="3581e-111">Ontbrekende kenmerken in de SAML-reactie</span><span class="sxs-lookup"><span data-stu-id="3581e-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="3581e-112">Volg de onderstaande stappen voor het toevoegen van een kenmerk in de configuratie van Azure AD worden verzonden in de Azure AD-antwoord:</span><span class="sxs-lookup"><span data-stu-id="3581e-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="3581e-113">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="3581e-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3581e-114">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="3581e-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3581e-115">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3581e-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3581e-116">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="3581e-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3581e-117">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3581e-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="3581e-118">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="3581e-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3581e-119">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3581e-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="3581e-120">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3581e-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3581e-121">Klik op **weergeven en alle andere gebruiker onder kenmerken bewerken** de **gebruikerskenmerken** sectie voor het bewerken van de kenmerken worden verzonden naar de toepassing in het SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="3581e-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="3581e-122">Een kenmerk toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3581e-122">To add an attribute:</span></span>

   * <span data-ttu-id="3581e-123">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="3581e-123">click **Add attribute**.</span></span> <span data-ttu-id="3581e-124">Voer de **naam** en selecteer de **waarde** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="3581e-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="3581e-125">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="3581e-125">Click **Save.**</span></span> <span data-ttu-id="3581e-126">Ziet u het nieuwe kenmerk in de tabel.</span><span class="sxs-lookup"><span data-stu-id="3581e-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="3581e-127">De configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="3581e-127">Save the configuration.</span></span>

<span data-ttu-id="3581e-128">Zodra de gebruiker zich aanmeldt bij de toepassing Azure AD verzenden het nieuwe kenmerk in de SAML-reactie.</span><span class="sxs-lookup"><span data-stu-id="3581e-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="3581e-129">De toepassing verwacht een andere gebruikers-id-waarde of de indeling</span><span class="sxs-lookup"><span data-stu-id="3581e-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="3581e-130">De aanmelding bij de toepassing is mislukt omdat de SAML-reactie kenmerken, zoals rollen ontbreekt of omdat de toepassing een andere indeling voor het kenmerk id van de entiteit wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="3581e-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="3581e-131">Een kenmerk in de configuratie van de Azure AD-toepassing toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3581e-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="3581e-132">De waarde van de gebruikers-id wilt wijzigen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3581e-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="3581e-133">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="3581e-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3581e-134">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="3581e-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3581e-135">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3581e-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3581e-136">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="3581e-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3581e-137">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3581e-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="3581e-138">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="3581e-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3581e-139">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3581e-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="3581e-140">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3581e-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3581e-141">Onder de **gebruikerskenmerken**, selecteert u de unieke id voor uw gebruikers in de **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="3581e-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="3581e-142">Wijzigen van de id van de entiteit (gebruikers-id)</span><span class="sxs-lookup"><span data-stu-id="3581e-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="3581e-143">Als de toepassing een andere indeling voor het kenmerk id van de entiteit verwacht.</span><span class="sxs-lookup"><span data-stu-id="3581e-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="3581e-144">Vervolgens het niet mogelijk om de id van de entiteit (gebruikers-id)-indeling die Azure AD naar de toepassing in het antwoord na verificatie van gebruikers verzendt te selecteren.</span><span class="sxs-lookup"><span data-stu-id="3581e-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="3581e-145">Azure AD selecteren de indeling voor het kenmerk NameID (gebruikers-id) op basis van de waarde geselecteerd of de indeling die is aangevraagd door de toepassing in de SAML-AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="3581e-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="3581e-146">Raadpleeg voor meer informatie het artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder de sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="3581e-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="3581e-147">De toepassing verwacht een ander handtekeningmethode voor de SAML-reactie</span><span class="sxs-lookup"><span data-stu-id="3581e-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="3581e-148">Om te wijzigen welke onderdelen van het SAML-token digitaal zijn ondertekend door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3581e-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="3581e-149">Volg de onderstaande stappen:</span><span class="sxs-lookup"><span data-stu-id="3581e-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="3581e-150">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="3581e-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3581e-151">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="3581e-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3581e-152">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3581e-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3581e-153">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="3581e-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3581e-154">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3581e-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="3581e-155">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="3581e-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3581e-156">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3581e-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="3581e-157">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3581e-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3581e-158">Klik op **weergeven geavanceerde instellingen voor het ondertekenen van certificaat** onder de **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="3581e-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="3581e-159">Selecteer de relevante **ondertekening optie** werd verwacht door de toepassing:</span><span class="sxs-lookup"><span data-stu-id="3581e-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="3581e-160">Meld u SAML-reactie</span><span class="sxs-lookup"><span data-stu-id="3581e-160">Sign SAML response</span></span>

  * <span data-ttu-id="3581e-161">Meld u aan de SAML-reactie en verklaring</span><span class="sxs-lookup"><span data-stu-id="3581e-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="3581e-162">Aanmelding van SAML-verklaring</span><span class="sxs-lookup"><span data-stu-id="3581e-162">Sign SAML assertion</span></span>

<span data-ttu-id="3581e-163">Zodra de gebruiker zich aanmeldt bij de toepassing Azure AD Meld u aan het deel van de SAML-reactie die is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3581e-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="3581e-164">De toepassing verwacht de ondertekeningsalgoritme SHA-1</span><span class="sxs-lookup"><span data-stu-id="3581e-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="3581e-165">Standaard wordt in Azure AD het SAML-token met de meeste beveiligingsalgoritme ondertekent.</span><span class="sxs-lookup"><span data-stu-id="3581e-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="3581e-166">Wijzigen van het teken-algoritme in SHA-1 wordt niet aanbevolen, tenzij de toepassing vereist.</span><span class="sxs-lookup"><span data-stu-id="3581e-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="3581e-167">Als u wilt de ondertekeningsalgoritme wijzigen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3581e-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="3581e-168">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="3581e-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3581e-169">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="3581e-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3581e-170">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3581e-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3581e-171">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="3581e-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3581e-172">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3581e-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="3581e-173">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="3581e-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3581e-174">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3581e-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="3581e-175">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3581e-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3581e-176">Klik op **weergeven geavanceerde instellingen voor het ondertekenen van certificaat** onder de **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="3581e-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="3581e-177">SHA-1, selecteert u in de **handtekeningalgoritme**.</span><span class="sxs-lookup"><span data-stu-id="3581e-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="3581e-178">Zodra de gebruiker zich aanmeldt bij de toepassing Azure AD Meld u aan het SAML-token met behulp van algoritme SHA-1.</span><span class="sxs-lookup"><span data-stu-id="3581e-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3581e-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3581e-179">Next steps</span></span>
[<span data-ttu-id="3581e-180">Fouten opsporen in op basis van SAML eenmalige aanmelding tot toepassingen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3581e-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
