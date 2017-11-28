---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="f02f2-103">Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="f02f2-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="f02f2-104">In deze zelfstudie leert u hoe Salesforce Sandbox integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f02f2-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f02f2-105">Salesforce Sandbox integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f02f2-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f02f2-106">U kunt beheren in Azure AD die toegang tot de Salesforce-Sandbox heeft</span><span class="sxs-lookup"><span data-stu-id="f02f2-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="f02f2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Salesforce Sandbox (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f02f2-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f02f2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f02f2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f02f2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f02f2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f02f2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f02f2-110">Prerequisites</span></span>

<span data-ttu-id="f02f2-111">Voor het configureren van Azure AD-integratie met Salesforce Sandbox, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f02f2-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="f02f2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f02f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f02f2-113">Een Salesforce Sandbox eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f02f2-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f02f2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f02f2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f02f2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f02f2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f02f2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f02f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f02f2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f02f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f02f2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f02f2-118">Scenario description</span></span>
<span data-ttu-id="f02f2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f02f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f02f2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f02f2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f02f2-121">Salesforce Sandbox uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f02f2-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="f02f2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f02f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="f02f2-123">Salesforce Sandbox uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f02f2-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="f02f2-124">Voor het configureren van de integratie van Salesforce Sandbox in Azure AD, moet u Salesforce Sandbox uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f02f2-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f02f2-125">**Als u wilt toevoegen Salesforce Sandbox uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f02f2-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f02f2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f02f2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f02f2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f02f2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f02f2-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f02f2-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f02f2-133">Typ in het zoekvak **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="f02f2-135">Selecteer in het deelvenster resultaten **Salesforce Sandbox**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f02f2-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f02f2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f02f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f02f2-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Salesforce-Sandbox op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f02f2-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f02f2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Salesforce Sandbox is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f02f2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="f02f2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Salesforce Sandbox tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f02f2-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="f02f2-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="f02f2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="f02f2-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Salesforce Sandbox, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f02f2-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f02f2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f02f2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f02f2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f02f2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f02f2-145">**[Maken van een testgebruiker Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  - Salesforce Sandbox die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f02f2-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f02f2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f02f2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f02f2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f02f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f02f2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f02f2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f02f2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Salesforce-Sandbox-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f02f2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="f02f2-150">**Voor het configureren van Azure AD eenmalige aanmelding met Salesforce Sandbox, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f02f2-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="f02f2-151">In de Azure-portal op de **Salesforce Sandbox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f02f2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f02f2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="f02f2-155">Op de **Salesforce sandbox-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f02f2-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="f02f2-157">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f02f2-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f02f2-158">Deze waarde is niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="f02f2-158">This value is not the real.</span></span> <span data-ttu-id="f02f2-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding. Neem contact op met [Salesforce Sandbox Client ondersteuningsteam](https://help.salesforce.com/support) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="f02f2-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="f02f2-160">Als u al eenmalige aanmelding voor een ander exemplaar van Salesforce Sandbox hebt geconfigureerd in uw directory, dan moet u ook configureren de **id** hebben dezelfde waarde als de **aanmelden URL**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="f02f2-161">De **id** veld kan worden gevonden door het controleren van de **weergeven geavanceerde instellingen** selectievakje op het **App-URL configureren** pagina van het dialoogvenster</span><span class="sxs-lookup"><span data-stu-id="f02f2-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="f02f2-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f02f2-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="f02f2-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f02f2-164">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f02f2-166">Op de **Salesforce Sandbox configuratie** sectie, klikt u op **Salesforce Sandbox configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f02f2-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f02f2-167">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f02f2-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="f02f2-168">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="f02f2-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="f02f2-169">Een nieuw tabblad openen in uw browser en meld u aan uw Salesforce-Sandbox-beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="f02f2-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="f02f2-170">Klik in het menu bovenaan op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-170">In the menu on the top, click **Setup**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="f02f2-172">Klik in het navigatievenster aan de linkerkant op **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="f02f2-174">De volgende stappen uitvoeren in de sectie instellingen voor eenmalige aanmelding: ![configureren eenmalige aanmelding](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="f02f2-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="f02f2-175">a.</span><span class="sxs-lookup"><span data-stu-id="f02f2-175">a.</span></span>  <span data-ttu-id="f02f2-176">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="f02f2-177">b.</span><span class="sxs-lookup"><span data-stu-id="f02f2-177">b.</span></span>  <span data-ttu-id="f02f2-178">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-178">Click **New**.</span></span>

12. <span data-ttu-id="f02f2-179">Voer de volgende stappen uit in de sectie SAML Single Sign-On-instellingen:</span><span class="sxs-lookup"><span data-stu-id="f02f2-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="f02f2-181">a.In het tekstvak voor de naam, typ de naam van de configuratie (bijvoorbeeld: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="f02f2-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="f02f2-182">b.</span><span class="sxs-lookup"><span data-stu-id="f02f2-182">b.</span></span> <span data-ttu-id="f02f2-183">Plakken **SMAL entiteit-ID** waarde in de **verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="f02f2-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="f02f2-184">c.</span><span class="sxs-lookup"><span data-stu-id="f02f2-184">c.</span></span> <span data-ttu-id="f02f2-185">In de **entiteit-Id** textbox type **https://test.salesforce.com** als dit het eerste exemplaar van Salesforce Sandbox die u aan uw directory toevoegen wilt.</span><span class="sxs-lookup"><span data-stu-id="f02f2-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="f02f2-186">Als u al hebt toegevoegd een exemplaar van Salesforce-Sandbox vervolgens voor de **entiteit-ID** typt u in de **aanmelding op URL**, die moet worden in deze indeling:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f02f2-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="f02f2-187">d.</span><span class="sxs-lookup"><span data-stu-id="f02f2-187">d.</span></span> <span data-ttu-id="f02f2-188">Klik op **Bladeren** om de gedownloade certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="f02f2-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="f02f2-189">e.</span><span class="sxs-lookup"><span data-stu-id="f02f2-189">e.</span></span> <span data-ttu-id="f02f2-190">Als **SAML identiteitstype**, selecteer **Assertion bevat de Federation-ID van het gebruikersobject**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="f02f2-191">f.</span><span class="sxs-lookup"><span data-stu-id="f02f2-191">f.</span></span> <span data-ttu-id="f02f2-192">Als **SAML identiteit locatie**, selecteer **identiteit is in het element NameIdentifier van het onderwerp overzicht**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="f02f2-193">g.</span><span class="sxs-lookup"><span data-stu-id="f02f2-193">g.</span></span> <span data-ttu-id="f02f2-194">Plakken **Single Sign-On Service-URL** in de **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f02f2-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="f02f2-195">h.</span><span class="sxs-lookup"><span data-stu-id="f02f2-195">h.</span></span> <span data-ttu-id="f02f2-196">SFDC biedt geen ondersteuning voor SAML-afmelden.</span><span class="sxs-lookup"><span data-stu-id="f02f2-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="f02f2-197">Als een tijdelijke oplossing 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' te plakken in de **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f02f2-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="f02f2-198">ik.</span><span class="sxs-lookup"><span data-stu-id="f02f2-198">i.</span></span> <span data-ttu-id="f02f2-199">Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="f02f2-200">j.</span><span class="sxs-lookup"><span data-stu-id="f02f2-200">j.</span></span> <span data-ttu-id="f02f2-201">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="f02f2-202">Uw domein inschakelen</span><span class="sxs-lookup"><span data-stu-id="f02f2-202">Enable your domain</span></span>
<span data-ttu-id="f02f2-203">Deze sectie wordt ervan uitgegaan dat u al hebt gemaakt een domein.</span><span class="sxs-lookup"><span data-stu-id="f02f2-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="f02f2-204">Zie voor meer informatie [definiëren van uw domeinnaam](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="f02f2-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="f02f2-205">**Als u wilt maken voor uw domein, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f02f2-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="f02f2-206">Klik in het navigatiedeelvenster links op **domeinbeheer**, en klik vervolgens op **mijn domein.**</span><span class="sxs-lookup"><span data-stu-id="f02f2-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="f02f2-208">Zorg dat uw domein correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f02f2-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="f02f2-209">In de **pagina aanmeldingsinstellingen** sectie, klikt u op **bewerken**, naarmate **verificatieservice**, selecteert u de naam van de SAML Single Sign-On-instelling van de vorige sectie en klik tot slot **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="f02f2-211">Als u een domein geconfigureerd hebt, moeten uw gebruikers de domein-URL voor aanmelding bij de sandbox Salesforce gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f02f2-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="f02f2-212">Als u de waarde van de URL, klikt u op de SSO-profiel dat u hebt gemaakt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="f02f2-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="f02f2-213">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f02f2-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f02f2-214">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f02f2-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f02f2-215">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f02f2-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f02f2-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f02f2-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="f02f2-217">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f02f2-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f02f2-219">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f02f2-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f02f2-220">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f02f2-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f02f2-222">Om weer te geven naar de lijst met gebruikers gaan **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f02f2-224">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f02f2-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f02f2-226">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f02f2-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f02f2-228">a.</span><span class="sxs-lookup"><span data-stu-id="f02f2-228">a.</span></span> <span data-ttu-id="f02f2-229">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f02f2-230">b.</span><span class="sxs-lookup"><span data-stu-id="f02f2-230">b.</span></span> <span data-ttu-id="f02f2-231">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f02f2-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f02f2-232">c.</span><span class="sxs-lookup"><span data-stu-id="f02f2-232">c.</span></span> <span data-ttu-id="f02f2-233">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f02f2-234">d.</span><span class="sxs-lookup"><span data-stu-id="f02f2-234">d.</span></span> <span data-ttu-id="f02f2-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="f02f2-236">Maken van een testgebruiker Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="f02f2-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="f02f2-237">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="f02f2-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="f02f2-238">SalesForce Sandbox ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f02f2-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="f02f2-239">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f02f2-239">There is no action item for you in this section.</span></span> <span data-ttu-id="f02f2-240">Als een gebruiker in Salesforce Sandbox nog niet bestaat, wordt een nieuw gemaakt wanneer u probeert te krijgen tot de Salesforce-Sandbox.</span><span class="sxs-lookup"><span data-stu-id="f02f2-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f02f2-241">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f02f2-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f02f2-242">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen aan de Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="f02f2-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f02f2-244">**Britta Simon om aan te wijzen Salesforce Sandbox, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f02f2-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="f02f2-245">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f02f2-247">Selecteer in de lijst met toepassingen **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="f02f2-249">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f02f2-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f02f2-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f02f2-251">Click **Add** button.</span></span> <span data-ttu-id="f02f2-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f02f2-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f02f2-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f02f2-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f02f2-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f02f2-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f02f2-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f02f2-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f02f2-257">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f02f2-257">Testing single sign-on</span></span>

<span data-ttu-id="f02f2-258">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f02f2-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="f02f2-259">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f02f2-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f02f2-260">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f02f2-260">Additional resources</span></span>

* [<span data-ttu-id="f02f2-261">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f02f2-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f02f2-262">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f02f2-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f02f2-263">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="f02f2-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

