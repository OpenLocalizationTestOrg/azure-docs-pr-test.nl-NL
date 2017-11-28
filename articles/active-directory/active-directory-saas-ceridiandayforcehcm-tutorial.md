---
title: 'Zelfstudie: Azure Active Directory-integratie met Ceridian Dayforce HCM | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Ceridian Dayforce HCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="f7f3b-103">Zelfstudie: Azure Active Directory-integratie met Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="f7f3b-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="f7f3b-104">In deze zelfstudie leert u hoe Ceridian Dayforce HCM integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7f3b-105">Ceridian Dayforce HCM integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7f3b-106">U kunt beheren in Azure AD die toegang tot Ceridian Dayforce HCM heeft.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="f7f3b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Ceridian Dayforce HCM (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f7f3b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f7f3b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7f3b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f7f3b-110">Prerequisites</span></span>

<span data-ttu-id="f7f3b-111">Voor het configureren van Azure AD-integratie met Ceridian Dayforce HCM, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="f7f3b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f7f3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7f3b-113">Een Ceridian Dayforce HCM eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f7f3b-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7f3b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7f3b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7f3b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7f3b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7f3b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f7f3b-118">Scenario description</span></span>
<span data-ttu-id="f7f3b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7f3b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7f3b-121">Ceridian Dayforce HCM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7f3b-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="f7f3b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f7f3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="f7f3b-123">Ceridian Dayforce HCM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7f3b-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="f7f3b-124">Voor het configureren van de integratie van Ceridian Dayforce HCM in Azure AD, moet u Ceridian Dayforce HCM uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7f3b-125">**Als u wilt toevoegen Ceridian Dayforce HCM uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7f3b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="f7f3b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7f3b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="f7f3b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="f7f3b-133">Typ in het zoekvak **Ceridian Dayforce HCM**, selecteer **Ceridian Dayforce HCM** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![Ceridian Dayforce HCM in de lijst met resultaten](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f7f3b-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7f3b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f7f3b-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Ceridian Dayforce HCM op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7f3b-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Ceridian Dayforce HCM is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="f7f3b-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Ceridian Dayforce HCM tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="f7f3b-139">Wijs in Ceridian Dayforce HCM, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7f3b-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Ceridian Dayforce HCM, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7f3b-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7f3b-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7f3b-143">**[Maak een testgebruiker Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  - Ceridian Dayforce HCM die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7f3b-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7f3b-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f7f3b-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f7f3b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f7f3b-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Ceridian Dayforce HCM configureren.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="f7f3b-148">**Voor het configureren van Azure AD eenmalige aanmelding met Ceridian Dayforce HCM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="f7f3b-149">In de Azure-portal op de **Ceridian Dayforce HCM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f7f3b-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="f7f3b-153">Op de **Ceridian Dayforce HCM domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="f7f3b-155">a.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-155">a.</span></span> <span data-ttu-id="f7f3b-156">In de **aanmelding op URL** textbox, typ de URL moet worden gebruikt door uw gebruikers aan te melden bij uw toepassing Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="f7f3b-157">Omgeving</span><span class="sxs-lookup"><span data-stu-id="f7f3b-157">Environment</span></span> | <span data-ttu-id="f7f3b-158">URL</span><span class="sxs-lookup"><span data-stu-id="f7f3b-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="f7f3b-159">Voor productie</span><span class="sxs-lookup"><span data-stu-id="f7f3b-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="f7f3b-160">Voor de tests voor</span><span class="sxs-lookup"><span data-stu-id="f7f3b-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="f7f3b-161">b.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-161">b.</span></span> <span data-ttu-id="f7f3b-162">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="f7f3b-163">Omgeving</span><span class="sxs-lookup"><span data-stu-id="f7f3b-163">Environment</span></span> | <span data-ttu-id="f7f3b-164">URL</span><span class="sxs-lookup"><span data-stu-id="f7f3b-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="f7f3b-165">Voor productie</span><span class="sxs-lookup"><span data-stu-id="f7f3b-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="f7f3b-166">Voor de tests voor</span><span class="sxs-lookup"><span data-stu-id="f7f3b-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="f7f3b-167">c.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-167">c.</span></span> <span data-ttu-id="f7f3b-168">In de **antwoord-URL** textbox, typ de URL waarnaar het antwoord door Azure AD gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="f7f3b-169">Omgeving</span><span class="sxs-lookup"><span data-stu-id="f7f3b-169">Environment</span></span> | <span data-ttu-id="f7f3b-170">URL</span><span class="sxs-lookup"><span data-stu-id="f7f3b-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="f7f3b-171">Voor productie</span><span class="sxs-lookup"><span data-stu-id="f7f3b-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="f7f3b-172">Voor de tests voor</span><span class="sxs-lookup"><span data-stu-id="f7f3b-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="f7f3b-173">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-173">These values are not real.</span></span> <span data-ttu-id="f7f3b-174">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="f7f3b-175">Neem contact op met [Ceridian Dayforce HCM Client ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="f7f3b-176">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="f7f3b-178">Uw toepassing Ceridian Dayforce HCM verwacht de SAML-asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f7f3b-179">Werken met [Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) eerst naar de juiste gebruikers-id te identificeren.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="f7f3b-180">Microsoft raadt u aan met behulp van de **'name'** kenmerk als gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="f7f3b-181">U kunt de waarden van deze kenmerken van beheren de **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="f7f3b-182">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-182">The following screenshot shows an example for this.</span></span>  

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="f7f3b-184">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="f7f3b-185">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f7f3b-185">Attribute Name</span></span>  | <span data-ttu-id="f7f3b-186">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f7f3b-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="f7f3b-187">naam</span><span class="sxs-lookup"><span data-stu-id="f7f3b-187">name</span></span>  | <span data-ttu-id="f7f3b-188">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="f7f3b-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="f7f3b-189">a.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-189">a.</span></span> <span data-ttu-id="f7f3b-190">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="f7f3b-193">b.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-193">b.</span></span> <span data-ttu-id="f7f3b-194">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="f7f3b-195">c.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-195">c.</span></span> <span data-ttu-id="f7f3b-196">In de **waarde** , selecteert u het gebruikerskenmerk die u wilt gebruiken voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="f7f3b-197">Bijvoorbeeld als u wilt gebruiken van de werknemer-id als unieke gebruikers-id en u hebt opgeslagen waarde van het kenmerk in de ExtensionAttribute2, selecteer vervolgens **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="f7f3b-198">d.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-198">d.</span></span> <span data-ttu-id="f7f3b-199">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-199">Click **Ok**.</span></span>

7. <span data-ttu-id="f7f3b-200">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-200">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="f7f3b-202">Op de **Ceridian Dayforce HCM configuratie** sectie, klikt u op **configureren Ceridian Dayforce HCM** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f7f3b-203">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM configuratie](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="f7f3b-205">Eenmalige aanmelding configureren op **Ceridian Dayforce HCM** zijde, moet u de gedownloade verzenden **Metadata XML** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="f7f3b-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="f7f3b-206">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f7f3b-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7f3b-207">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7f3b-208">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7f3b-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f7f3b-209">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f7f3b-209">Create an Azure AD test user</span></span>

<span data-ttu-id="f7f3b-210">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="f7f3b-212">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7f3b-213">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f7f3b-215">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f7f3b-217">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f7f3b-219">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f7f3b-219">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f7f3b-221">a.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-221">a.</span></span> <span data-ttu-id="f7f3b-222">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7f3b-223">b.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-223">b.</span></span> <span data-ttu-id="f7f3b-224">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f7f3b-225">c.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-225">c.</span></span> <span data-ttu-id="f7f3b-226">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f7f3b-227">d.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-227">d.</span></span> <span data-ttu-id="f7f3b-228">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="f7f3b-229">Een testgebruiker Ceridian Dayforce HCM maken</span><span class="sxs-lookup"><span data-stu-id="f7f3b-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="f7f3b-230">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Ceridian Dayforce HCM genoemd.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="f7f3b-231">Werken met de [Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) gebruikers die zijn toegevoegd in de toepassing Ceridian Dayforce HCM ophalen.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f7f3b-232">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7f3b-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f7f3b-233">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f7f3b-235">**Britta Simon om aan te wijzen Ceridian Dayforce HCM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="f7f3b-236">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f7f3b-238">Selecteer in de lijst met toepassingen **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="f7f3b-240">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f7f3b-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-242">Click **Add** button.</span></span> <span data-ttu-id="f7f3b-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f7f3b-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7f3b-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7f3b-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f7f3b-248">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="f7f3b-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="f7f3b-249">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="f7f3b-251">**Britta Simon om aan te wijzen Ceridian Dayforce HCM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f7f3b-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="f7f3b-252">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f7f3b-254">Selecteer in de lijst met toepassingen **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![De koppeling Ceridian Dayforce HCM in de lijst met toepassingen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="f7f3b-256">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-256">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="f7f3b-258">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-258">Click **Add** button.</span></span> <span data-ttu-id="f7f3b-259">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="f7f3b-261">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7f3b-262">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7f3b-263">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f7f3b-264">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f7f3b-264">Test single sign-on</span></span>

<span data-ttu-id="f7f3b-265">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f7f3b-266">Als u op de tegel Ceridian Dayforce HCM in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="f7f3b-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f7f3b-267">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f7f3b-267">Additional resources</span></span>

* [<span data-ttu-id="f7f3b-268">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7f3b-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7f3b-269">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7f3b-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

