---
title: Problemen met aanmelden bij een niet-galerie-toepassing is geconfigureerd voor federatieve eenmalige aanmelding | Microsoft Docs
description: Richtlijnen voor de specifieke problemen die u mee te maken mogelijk tijdens het aanmelden bij een toepassing die is geconfigureerd voor op basis van SAML federatieve eenmalige aanmelding met Azure AD
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
ms.openlocfilehash: 3afc7bca878caef424d3fa3c64aa17df0fda7de5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="9a31f-103">Problemen met aanmelden bij een niet-galerie-toepassing die is geconfigureerd voor federatieve eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a31f-103">Problems signing in to a non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="9a31f-104">Om het probleem kunt oplossen, moet u controleren of de configuratie van de toepassing in Azure AD als volgt:</span><span class="sxs-lookup"><span data-stu-id="9a31f-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="9a31f-105">U kunt de configuratiestappen voor de toepassing van de galerie van Azure AD hebt gevolgd.</span><span class="sxs-lookup"><span data-stu-id="9a31f-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="9a31f-106">De id en de antwoord-URL geconfigureerd in AAD overeen ze verwachte waarden in de toepassing</span><span class="sxs-lookup"><span data-stu-id="9a31f-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="9a31f-107">U hebt gebruikers toegewezen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="9a31f-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="9a31f-108">Toepassing is niet gevonden in map</span><span class="sxs-lookup"><span data-stu-id="9a31f-108">Application not found in directory</span></span>

<span data-ttu-id="9a31f-109">*Fout AADSTS70001: Toepassing met id 'https://contoso.com' is niet gevonden in de map*.</span><span class="sxs-lookup"><span data-stu-id="9a31f-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="9a31f-110">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="9a31f-110">**Possible cause**</span></span>

<span data-ttu-id="9a31f-111">De verlener kenmerk uit de toepassing naar Azure AD in de SAML-aanvraag verzendt komt niet overeen met de id-waarde die is geconfigureerd in de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="9a31f-112">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="9a31f-112">**Resolution**</span></span>

<span data-ttu-id="9a31f-113">Zorg ervoor dat het kenmerk uitgever in de SAML-aanvraag die deze komt overeen met de id die is geconfigureerd in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9a31f-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="9a31f-114">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9a31f-115">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9a31f-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9a31f-116">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9a31f-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9a31f-117">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9a31f-118">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9a31f-118">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9a31f-119">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9a31f-120">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a31f-120">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9a31f-121">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9a31f-122"><span id="_Hlk477190042" class="anchor"></span>Ga naar **domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-122"><span id="_Hlk477190042" class="anchor"></span>Go to **Domain and URLs** section.</span></span> <span data-ttu-id="9a31f-123">Controleer of dat wordt de waarde in het tekstvak voor de id die overeenkomt met de waarde voor de id-waarde in de volgende fout weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9a31f-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="9a31f-124">Nadat u de id-waarde hebben bijgewerkt in Azure AD en deze met de waarde verzendt door de toepassing in de SAML-aanvraag overeen komt, moet u mogelijk zijn aan te melden bij de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="9a31f-125">Het antwoordadres komt niet overeen met de antwoordadressen geconfigureerd voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-125">The reply address does not match the reply addresses configured for the application.</span></span> 

<span data-ttu-id="9a31f-126">*Fout AADSTS50011: Het antwoordadres 'https://contoso.com' komt niet overeen met de antwoordadressen geconfigureerd voor de toepassing*</span><span class="sxs-lookup"><span data-stu-id="9a31f-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span> 

<span data-ttu-id="9a31f-127">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="9a31f-127">**Possible cause**</span></span> 

<span data-ttu-id="9a31f-128">De waarde AssertionConsumerServiceURL in de SAML-aanvraag komt niet overeen met de antwoord-URL-waarde of patroon dat is geconfigureerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a31f-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="9a31f-129">De waarde AssertionConsumerServiceURL in de SAML-aanvraag is de URL die u in de fout ziet.</span><span class="sxs-lookup"><span data-stu-id="9a31f-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span> 

<span data-ttu-id="9a31f-130">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="9a31f-130">**Resolution**</span></span> 

<span data-ttu-id="9a31f-131">Zorg ervoor dat de waarde AssertionConsumerServiceURL in de SAML-aanvraag die deze komt overeen met de antwoord-URL die is geconfigureerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a31f-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="9a31f-132">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="9a31f-133">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9a31f-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="9a31f-134">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9a31f-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="9a31f-135">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="9a31f-136">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9a31f-136">click **All Applications** to view a list of all your applications.</span></span> 

  * <span data-ttu-id="9a31f-137">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and       set the **Show** option to **All Applications.**</span></span>
  
6.  <span data-ttu-id="9a31f-138">Selecteer de toepassing die u wilt configureren eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a31f-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="9a31f-139">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9a31f-140">Ga naar **domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="9a31f-141">Controleer of de waarde in het tekstvak voor de antwoord-URL overeenkomt met de waarde AssertionConsumerServiceURL in de SAML-aanvraag bijwerken.</span><span class="sxs-lookup"><span data-stu-id="9a31f-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>

  * <span data-ttu-id="9a31f-142">Als u het tekstvak voor de antwoord-URL niet ziet, selecteert u de **weergeven geavanceerde instellingen voor URL** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="9a31f-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="9a31f-143">Nadat u de antwoord-URL-waarde hebben bijgewerkt in Azure AD en deze met de waarde verzendt door de toepassing in de SAML-aanvraag overeen komt, moet u mogelijk zijn aan te melden bij de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="9a31f-144">Gebruiker met een niet toegewezen</span><span class="sxs-lookup"><span data-stu-id="9a31f-144">User not assigned a role</span></span>

<span data-ttu-id="9a31f-145">*Fout AADSTS50105: De aangemelde gebruiker 'brian@contoso.com' is niet toegewezen aan een rol voor de toepassing*</span><span class="sxs-lookup"><span data-stu-id="9a31f-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*</span></span>

<span data-ttu-id="9a31f-146">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="9a31f-146">**Possible cause**</span></span>

<span data-ttu-id="9a31f-147">De gebruiker heeft geen toegang gekregen tot de toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a31f-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="9a31f-148">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="9a31f-148">**Resolution**</span></span>

<span data-ttu-id="9a31f-149">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9a31f-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9a31f-150">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9a31f-151">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9a31f-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9a31f-152">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9a31f-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9a31f-153">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9a31f-154">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9a31f-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9a31f-155">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9a31f-156">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="9a31f-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9a31f-157">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9a31f-158">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="9a31f-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9a31f-159">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="9a31f-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9a31f-160">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="9a31f-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9a31f-161">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="9a31f-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9a31f-162">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="9a31f-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9a31f-163">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="9a31f-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9a31f-164">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9a31f-165">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9a31f-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9a31f-166">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9a31f-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9a31f-167">Na een korte periode, de gebruikers die u hebt geselecteerd mogelijk om deze toepassingen met behulp van de methoden die worden beschreven in de sectie oplossing beschrijving te starten.</span><span class="sxs-lookup"><span data-stu-id="9a31f-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="9a31f-168">Geen een geldige SAML aanvragen</span><span class="sxs-lookup"><span data-stu-id="9a31f-168">Not a valid SAML Request</span></span>

<span data-ttu-id="9a31f-169">*Fout AADSTS75005: De aanvraag is niet een geldig Saml2-protocolbericht.*</span><span class="sxs-lookup"><span data-stu-id="9a31f-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="9a31f-170">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="9a31f-170">**Possible cause**</span></span>

<span data-ttu-id="9a31f-171">Azure AD biedt geen ondersteuning voor SAML Request verzonden door de toepassing voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a31f-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="9a31f-172">Enkele veelvoorkomende problemen zijn:</span><span class="sxs-lookup"><span data-stu-id="9a31f-172">Some common issues are:</span></span>

-   <span data-ttu-id="9a31f-173">Ontbrekende vereiste velden in de SAML-aanvraag</span><span class="sxs-lookup"><span data-stu-id="9a31f-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="9a31f-174">SAML gecodeerd aanvraagmethode</span><span class="sxs-lookup"><span data-stu-id="9a31f-174">SAML request encoded method</span></span>

<span data-ttu-id="9a31f-175">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="9a31f-175">**Resolution**</span></span>

1.  <span data-ttu-id="9a31f-176">Vastleggen van SAML-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9a31f-176">Capture SAML request.</span></span> <span data-ttu-id="9a31f-177">Volg de zelfstudie op [fouten opsporen in op basis van SAML eenmalige aanmelding tot toepassingen in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) voor informatie over het vastleggen van de SAML-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9a31f-177">follow the tutorial on [how to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="9a31f-178">Neem contact op met de leverancier van toepassing en -share:</span><span class="sxs-lookup"><span data-stu-id="9a31f-178">Contact the application vendor and share:</span></span>

    -   <span data-ttu-id="9a31f-179">SAML-aanvraag</span><span class="sxs-lookup"><span data-stu-id="9a31f-179">SAML request</span></span>

    -   [<span data-ttu-id="9a31f-180">Vereisten voor Azure AD Single Sign-on SAML-protocol</span><span class="sxs-lookup"><span data-stu-id="9a31f-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="9a31f-181">Ze moeten valideren deze ondersteuning bieden voor de implementatie van de Azure AD SAML voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a31f-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="9a31f-182">Er is geen resource in de lijst requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="9a31f-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="9a31f-183">*Fout AADSTS65005: De clienttoepassing heeft aangevraagd toegang tot de resource ' 00000002-0000-0000-c000-000000000000'. Deze aanvraag is mislukt omdat de client niet voor deze bron in de lijst met requiredResourceAccess opgegeven is*.</span><span class="sxs-lookup"><span data-stu-id="9a31f-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="9a31f-184">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="9a31f-184">**Possible cause**</span></span>

<span data-ttu-id="9a31f-185">Het toepassingsobject is beschadigd.</span><span class="sxs-lookup"><span data-stu-id="9a31f-185">The application object is corrupted.</span></span>

<span data-ttu-id="9a31f-186">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="9a31f-186">**Resolution**</span></span>

<span data-ttu-id="9a31f-187">Verwijder de toepassing van de map om het probleem kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="9a31f-187">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="9a31f-188">Vervolgens toevoegen en configureren van de toepassing, volgt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9a31f-188">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="9a31f-189">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9a31f-190">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9a31f-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9a31f-191">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9a31f-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9a31f-192">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9a31f-193">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9a31f-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9a31f-194">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9a31f-195">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a31f-195">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9a31f-196">Klik op **verwijderen** op de linkerbovenhoek van de toepassing **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="9a31f-196">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="9a31f-197">Vernieuwen van Azure AD en voegt u de toepassing van de galerie van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a31f-197">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="9a31f-198">Configureer vervolgens de toepassing opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9a31f-198">Then, Configure the application again.</span></span>

<span data-ttu-id="9a31f-199">Na het opnieuw configureren van de toepassing, moet u het volgende kunnen aanmelden bij de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-199">After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="9a31f-200">Certificaat of de sleutel niet geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="9a31f-200">Certificate or key not configured</span></span>

<span data-ttu-id="9a31f-201">Fout AADSTS50003: Er is geen ondertekeningssleutel geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9a31f-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="9a31f-202">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="9a31f-202">**Possible cause**</span></span>

<span data-ttu-id="9a31f-203">Het toepassingsobject is beschadigd en Azure AD niet wordt herkend door het certificaat dat is geconfigureerd voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-203">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="9a31f-204">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="9a31f-204">**Resolution**</span></span>

<span data-ttu-id="9a31f-205">Als u wilt verwijderen en maak een nieuw certificaat, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9a31f-205">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="9a31f-206">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-206">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9a31f-207">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9a31f-207">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9a31f-208">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9a31f-208">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9a31f-209">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-209">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9a31f-210">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9a31f-210">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9a31f-211">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-211">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9a31f-212">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a31f-212">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9a31f-213">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a31f-213">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9a31f-214">Klik op **nieuw certificaat maken** onder de **SAML handtekeningcertificaat** sectie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-214">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="9a31f-215">Selecteer de vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="9a31f-215">Select Expiration date.</span></span> <span data-ttu-id="9a31f-216">Klik vervolgens op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="9a31f-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="9a31f-217">Controleer **nieuwe certificaat activeren** voor het onderdrukken van het actieve certificaat.</span><span class="sxs-lookup"><span data-stu-id="9a31f-217">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="9a31f-218">Klik vervolgens op **opslaan** boven aan de blade en voor het activeren van de rollovercertificaat accepteren.</span><span class="sxs-lookup"><span data-stu-id="9a31f-218">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="9a31f-219">Onder de **SAML-certificaat voor ondertekening van** sectie, klikt u op **verwijderen** verwijderen van de **ongebruikt** certificaat.</span><span class="sxs-lookup"><span data-stu-id="9a31f-219">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="9a31f-220">Probleem bij het aanpassen van de SAML-claims verzonden naar een toepassing</span><span class="sxs-lookup"><span data-stu-id="9a31f-220">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="9a31f-221">Zie voor meer informatie over het aanpassen van de SAML-kenmerk claims verzonden naar uw toepassing, [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9a31f-221">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a31f-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a31f-222">Next steps</span></span>
[<span data-ttu-id="9a31f-223">Vereisten voor Azure AD Single Sign-on SAML-protocol</span><span class="sxs-lookup"><span data-stu-id="9a31f-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
