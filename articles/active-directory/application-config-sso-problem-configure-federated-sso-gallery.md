---
title: Probleem federatieve eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren | Microsoft Docs
description: Adres van een aantal veelvoorkomende problemen optreden kunnen bij het configureren van federatieve eenmalige aanmelding via SAML voor toepassingen die worden vermeld in de Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="d1188-103">Probleem federatieve eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d1188-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="d1188-104">Als u een probleem ondervindt bij het configureren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1188-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="d1188-105">Controleer of dat u alle stappen hebt gevolgd in de zelfstudie voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1188-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="d1188-106">In de configuratie van de toepassing hebt u inline-documentatie over het configureren van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1188-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="d1188-107">U hebt ook toegang tot de [lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.</span><span class="sxs-lookup"><span data-stu-id="d1188-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="d1188-108">Een ander exemplaar van de toepassing toevoegen niet</span><span class="sxs-lookup"><span data-stu-id="d1188-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="d1188-109">Als u wilt een tweede exemplaar van een toepassing toevoegt, moet u mogelijk:</span><span class="sxs-lookup"><span data-stu-id="d1188-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="d1188-110">Configureer een unieke id voor de tweede instantie.</span><span class="sxs-lookup"><span data-stu-id="d1188-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="d1188-111">Het niet mogelijk om te configureren voor het eerste exemplaar gebruikt dezelfde id.</span><span class="sxs-lookup"><span data-stu-id="d1188-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="d1188-112">Configureer een ander certificaat dan de versie die wordt gebruikt voor het eerste exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d1188-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="d1188-113">Als de toepassing biedt geen ondersteuning voor een van de bovenstaande.</span><span class="sxs-lookup"><span data-stu-id="d1188-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="d1188-114">Vervolgens het niet mogelijk voor het configureren van een tweede exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d1188-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="d1188-115">De id of de antwoord-URL toevoegen niet</span><span class="sxs-lookup"><span data-stu-id="d1188-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="d1188-116">Als je niet kan worden geconfigureerd voor de id of de antwoord-URL, controleert u de id en de antwoord-URL waarden overeenkomen met de patronen die vooraf is geconfigureerd voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1188-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="d1188-117">De patronen die vooraf is geconfigureerd voor de toepassing weten:</span><span class="sxs-lookup"><span data-stu-id="d1188-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="d1188-118">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="d1188-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="d1188-119">Ga naar stap 7.</span><span class="sxs-lookup"><span data-stu-id="d1188-119">Go to step 7.</span></span> <span data-ttu-id="d1188-120">Als u zich al in de blade van de configuratie van toepassing op Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1188-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="d1188-121">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="d1188-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1188-122">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d1188-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1188-123">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="d1188-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d1188-124">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="d1188-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="d1188-125">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="d1188-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d1188-126">Selecteer de toepassing die u wilt configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d1188-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="d1188-127">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1188-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d1188-128">Selecteer **op basis van SAML aanmelding** van de **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="d1188-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="d1188-129">Ga naar de **id** of **antwoord-URL** tekstvak onder de **sectie domein en URL's.**</span><span class="sxs-lookup"><span data-stu-id="d1188-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="d1188-130">Er zijn drie manieren om te weten van de ondersteunde patronen voor de toepassing:</span><span class="sxs-lookup"><span data-stu-id="d1188-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="d1188-131">In het tekstvak, ziet u de ondersteunde patroon of patronen als tijdelijke aanduiding *voorbeeld:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="d1188-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="d1188-132">Als het patroon wordt niet ondersteund, ziet u een rood uitroepteken wanneer u de waarde invoeren in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="d1188-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="d1188-133">Als u de muisaanwijzer op de rood uitroepteken, ziet u de ondersteunde patronen.</span><span class="sxs-lookup"><span data-stu-id="d1188-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="d1188-134">In de zelfstudie voor de toepassing, kunt u ook informatie over de ondersteunde patronen opvragen.</span><span class="sxs-lookup"><span data-stu-id="d1188-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="d1188-135">Onder de **eenmalige aanmelding configureren Azure AD** sectie.</span><span class="sxs-lookup"><span data-stu-id="d1188-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="d1188-136">Ga naar de stap voor configureren van de waarden onder de **domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="d1188-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="d1188-137">Als de waarden niet met de patronen die vooraf is geconfigureerd op Azure AD overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="d1188-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="d1188-138">U kunt:</span><span class="sxs-lookup"><span data-stu-id="d1188-138">You can:</span></span>

-   <span data-ttu-id="d1188-139">Werken met de leverancier van de toepassing ophalen van waarden die overeenkomen met het patroon dat vooraf is geconfigureerd op Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1188-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="d1188-140">U kunt ook contact opnemen met Azure AD-team via < aadapprequest@microsoft.com > of laat een opmerking in de zelfstudie om aan te vragen van de update van de ondersteunde patronen voor de toepassing</span><span class="sxs-lookup"><span data-stu-id="d1188-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="d1188-141">Waar kan ik de id van de entiteit (gebruikers-id)-indeling instellen</span><span class="sxs-lookup"><span data-stu-id="d1188-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="d1188-142">Het niet mogelijk om de id van de entiteit (gebruikers-id)-indeling die Azure AD naar de toepassing in het antwoord na verificatie van gebruikers verzendt te selecteren.</span><span class="sxs-lookup"><span data-stu-id="d1188-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="d1188-143">Azure AD selecteren de indeling voor het kenmerk NameID (gebruikers-id) op basis van de waarde geselecteerd of de indeling die is aangevraagd door de toepassing in de SAML-AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="d1188-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="d1188-144">Raadpleeg voor meer informatie het artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder de sectie NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="d1188-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="d1188-145">De Azure AD-metagegevens voor het voltooien van de configuratie met de toepassing niet gevonden</span><span class="sxs-lookup"><span data-stu-id="d1188-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="d1188-146">Voor het downloaden van de metagegevens van de toepassing of het certificaat van Azure AD, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="d1188-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="d1188-147">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="d1188-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d1188-148">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="d1188-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1188-149">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d1188-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1188-150">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="d1188-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d1188-151">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="d1188-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="d1188-152">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="d1188-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d1188-153">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d1188-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d1188-154">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1188-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d1188-155">Ga naar **SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="d1188-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="d1188-156">Afhankelijk van wat de toepassing configureren van eenmalige aanmelding vereist, ziet u ofwel de optie voor het downloaden van de Metadata XML of het certificaat.</span><span class="sxs-lookup"><span data-stu-id="d1188-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="d1188-157">Azure AD biedt een URL als u de metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="d1188-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="d1188-158">De metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="d1188-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="d1188-159">Weet u niet het aanpassen van SAML-claims verzonden naar een toepassing</span><span class="sxs-lookup"><span data-stu-id="d1188-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="d1188-160">Zie voor meer informatie over het aanpassen van de SAML-kenmerk claims verzonden naar uw toepassing, [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d1188-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1188-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1188-161">Next steps</span></span>
[<span data-ttu-id="d1188-162">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1188-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
