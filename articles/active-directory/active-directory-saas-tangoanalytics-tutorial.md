---
title: 'Zelfstudie: Azure Active Directory-integratie met Tango Analytics | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Tango Analytics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 46f6facc3c86630a9252340b2e89634368c0263d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="54f7d-103">Zelfstudie: Azure Active Directory-integratie met Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="54f7d-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="54f7d-104">In deze zelfstudie leert u hoe Tango Analytics integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54f7d-104">In this tutorial, you learn how to integrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54f7d-105">Tango Analytics integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="54f7d-105">Integrating Tango Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54f7d-106">U kunt beheren in Azure AD die toegang tot Tango Analytics heeft</span><span class="sxs-lookup"><span data-stu-id="54f7d-106">You can control in Azure AD who has access to Tango Analytics</span></span>
- <span data-ttu-id="54f7d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Tango Analytics (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="54f7d-107">You can enable your users to automatically get signed-on to Tango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54f7d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="54f7d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54f7d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54f7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54f7d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="54f7d-110">Prerequisites</span></span>

<span data-ttu-id="54f7d-111">Voor het configureren van Azure AD-integratie met Tango Analytics, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="54f7d-111">To configure Azure AD integration with Tango Analytics, you need the following items:</span></span>

- <span data-ttu-id="54f7d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="54f7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54f7d-113">Een Tango Analytics eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="54f7d-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54f7d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="54f7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54f7d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="54f7d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54f7d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="54f7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54f7d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54f7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54f7d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="54f7d-118">Scenario description</span></span>
<span data-ttu-id="54f7d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="54f7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54f7d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="54f7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54f7d-121">Tango Analytics uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="54f7d-121">Adding Tango Analytics from the gallery</span></span>
2. <span data-ttu-id="54f7d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="54f7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-the-gallery"></a><span data-ttu-id="54f7d-123">Tango Analytics uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="54f7d-123">Adding Tango Analytics from the gallery</span></span>
<span data-ttu-id="54f7d-124">Voor het configureren van de integratie van Tango Analytics met Azure AD, moet u Tango Analytics uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="54f7d-124">To configure the integration of Tango Analytics into Azure AD, you need to add Tango Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54f7d-125">**Als u wilt toevoegen Tango Analytics uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="54f7d-125">**To add Tango Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54f7d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="54f7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="54f7d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54f7d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="54f7d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="54f7d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="54f7d-133">Typ in het zoekvak **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-133">In the search box, type **Tango Analytics**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

5. <span data-ttu-id="54f7d-135">Selecteer in het deelvenster resultaten **Tango Analytics**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="54f7d-135">In the results panel, select **Tango Analytics**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54f7d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="54f7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54f7d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tango Analytics op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="54f7d-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54f7d-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Tango Analytics is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54f7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tango Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="54f7d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Tango Analytics tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="54f7d-140">In other words, a link relationship between an Azure AD user and the related user in Tango Analytics needs to be established.</span></span>

<span data-ttu-id="54f7d-141">Wijs in Tango Analytics, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="54f7d-141">In Tango Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54f7d-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Tango Analytics, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="54f7d-142">To configure and test Azure AD single sign-on with Tango Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54f7d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="54f7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54f7d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54f7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54f7d-145">**[Maken van een testgebruiker Tango Analytics](#creating-a-tango-analytics-test-user)**  - Tango Analytics die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="54f7d-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - to have a counterpart of Britta Simon in Tango Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54f7d-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="54f7d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54f7d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="54f7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54f7d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="54f7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54f7d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="54f7d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="54f7d-150">**Voor het configureren van Azure AD eenmalige aanmelding met Tango Analytics, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="54f7d-150">**To configure Azure AD single sign-on with Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="54f7d-151">In de Azure-portal op de **Tango Analytics** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-151">In the Azure portal, on the **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="54f7d-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="54f7d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

3. <span data-ttu-id="54f7d-155">Op de **Tango Analytics domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="54f7d-155">On the **Tango Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="54f7d-157">a.</span><span class="sxs-lookup"><span data-stu-id="54f7d-157">a.</span></span> <span data-ttu-id="54f7d-158">In de **id** textbox, typ de waarde`TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="54f7d-158">In the **Identifier** textbox, type the value `TACORE_SSO`</span></span>

    <span data-ttu-id="54f7d-159">b.</span><span class="sxs-lookup"><span data-stu-id="54f7d-159">b.</span></span> <span data-ttu-id="54f7d-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="54f7d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54f7d-161">De antwoord-URL-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="54f7d-161">The Reply URL value is not real.</span></span> <span data-ttu-id="54f7d-162">Dit bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="54f7d-162">Update this with the actual Reply URL.</span></span> <span data-ttu-id="54f7d-163">Neem contact op met [Tango Analytics ondersteuningsteam](mailto:support@tangoanalytics.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="54f7d-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) to get this value.</span></span>

4. <span data-ttu-id="54f7d-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="54f7d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

5. <span data-ttu-id="54f7d-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="54f7d-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="54f7d-168">Eenmalige aanmelding configureren op **Tango Analytics** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Tango Analytics ondersteuningsteam](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="54f7d-168">To configure single sign-on on **Tango Analytics** side, you need to send the downloaded **Metadata XML** to [Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="54f7d-169">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="54f7d-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="54f7d-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="54f7d-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54f7d-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="54f7d-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54f7d-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54f7d-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54f7d-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="54f7d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="54f7d-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="54f7d-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="54f7d-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="54f7d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54f7d-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="54f7d-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54f7d-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54f7d-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="54f7d-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54f7d-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="54f7d-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54f7d-185">a.</span><span class="sxs-lookup"><span data-stu-id="54f7d-185">a.</span></span> <span data-ttu-id="54f7d-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54f7d-187">b.</span><span class="sxs-lookup"><span data-stu-id="54f7d-187">b.</span></span> <span data-ttu-id="54f7d-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="54f7d-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54f7d-189">c.</span><span class="sxs-lookup"><span data-stu-id="54f7d-189">c.</span></span> <span data-ttu-id="54f7d-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54f7d-191">d.</span><span class="sxs-lookup"><span data-stu-id="54f7d-191">d.</span></span> <span data-ttu-id="54f7d-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="54f7d-193">Maken van een testgebruiker Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="54f7d-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="54f7d-194">In deze sectie maakt maakt u een gebruiker die Britta Simon aangeroepen in Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="54f7d-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="54f7d-195">Werken met [Tango Analytics ondersteuningsteam](mailto:support@tangoanalytics.com) om toe te voegen de gebruikers van het platform Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="54f7d-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add the users in the Tango Analytics platform.</span></span> <span data-ttu-id="54f7d-196">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="54f7d-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54f7d-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="54f7d-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="54f7d-198">In deze sectie maakt inschakelen u Britta Simon toegang verlenen aan Tango Analytics gebruikt Azure eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="54f7d-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tango Analytics.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="54f7d-200">**Britta Simon om aan te wijzen Tango Analytics, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="54f7d-200">**To assign Britta Simon to Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="54f7d-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="54f7d-203">Selecteer in de lijst met toepassingen **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-203">In the applications list, select **Tango Analytics**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

3. <span data-ttu-id="54f7d-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="54f7d-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="54f7d-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="54f7d-207">Click **Add** button.</span></span> <span data-ttu-id="54f7d-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="54f7d-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="54f7d-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="54f7d-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54f7d-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="54f7d-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54f7d-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="54f7d-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54f7d-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="54f7d-213">Testing single sign-on</span></span>

<span data-ttu-id="54f7d-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="54f7d-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54f7d-215">Als u op de tegel Tango Analytics in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="54f7d-215">When you click the Tango Analytics tile in the Access Panel, you should get automatically signed-on to your Tango Analytics application.</span></span>
<span data-ttu-id="54f7d-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54f7d-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54f7d-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="54f7d-217">Additional resources</span></span>

* [<span data-ttu-id="54f7d-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54f7d-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54f7d-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54f7d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_203.png

