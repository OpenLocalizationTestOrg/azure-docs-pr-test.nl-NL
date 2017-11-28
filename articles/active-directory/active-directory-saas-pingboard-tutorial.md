---
title: 'Zelfstudie: Azure Active Directory-integratie met Pingboard | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Pingboard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="65ad6-103">Zelfstudie: Azure Active Directory-integratie met Pingboard</span><span class="sxs-lookup"><span data-stu-id="65ad6-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="65ad6-104">In deze zelfstudie leert u hoe Pingboard integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65ad6-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65ad6-105">Pingboard integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="65ad6-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65ad6-106">U kunt beheren in Azure AD die toegang tot Pingboard heeft</span><span class="sxs-lookup"><span data-stu-id="65ad6-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="65ad6-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Pingboard (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="65ad6-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65ad6-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="65ad6-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="65ad6-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65ad6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65ad6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="65ad6-110">Prerequisites</span></span>

<span data-ttu-id="65ad6-111">Voor het configureren van Azure AD-integratie met Pingboard, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="65ad6-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="65ad6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="65ad6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65ad6-113">Een Pingboard eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="65ad6-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65ad6-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="65ad6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65ad6-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="65ad6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65ad6-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="65ad6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="65ad6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65ad6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65ad6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="65ad6-118">Scenario description</span></span>
<span data-ttu-id="65ad6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="65ad6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65ad6-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="65ad6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65ad6-121">Pingboard uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="65ad6-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="65ad6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65ad6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="65ad6-123">Pingboard uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="65ad6-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="65ad6-124">Voor het configureren van de integratie van Pingboard in Azure AD, moet u Pingboard uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="65ad6-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65ad6-125">**Als u wilt toevoegen Pingboard uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="65ad6-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65ad6-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="65ad6-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65ad6-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65ad6-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="65ad6-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65ad6-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="65ad6-133">Typ in het zoekvak **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-133">In the search box, type **Pingboard**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="65ad6-135">Selecteer in het deelvenster resultaten **Pingboard**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="65ad6-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65ad6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65ad6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65ad6-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Pingboard op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="65ad6-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65ad6-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Pingboard is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65ad6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="65ad6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Pingboard tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="65ad6-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="65ad6-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="65ad6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="65ad6-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Pingboard, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="65ad6-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65ad6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65ad6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65ad6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65ad6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65ad6-145">**[Maken van een testgebruiker Pingboard](#creating-a-pingboard-test-user)**  - Pingboard die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="65ad6-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="65ad6-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="65ad6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65ad6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="65ad6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65ad6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="65ad6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65ad6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing Pingboard configureren.</span><span class="sxs-lookup"><span data-stu-id="65ad6-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="65ad6-150">**Voor het configureren van Azure AD eenmalige aanmelding met Pingboard, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="65ad6-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="65ad6-151">In de Azure-beheerportal op de **Pingboard** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="65ad6-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="65ad6-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="65ad6-155">Op de **Pingboard domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="65ad6-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="65ad6-157">a.</span><span class="sxs-lookup"><span data-stu-id="65ad6-157">a.</span></span> <span data-ttu-id="65ad6-158">In de **id** textbox, typ de waarde als:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="65ad6-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="65ad6-159">b.</span><span class="sxs-lookup"><span data-stu-id="65ad6-159">b.</span></span> <span data-ttu-id="65ad6-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="65ad6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65ad6-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="65ad6-161">Please note that these are not the real values.</span></span> <span data-ttu-id="65ad6-162">U hebt deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="65ad6-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="65ad6-163">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="65ad6-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="65ad6-164">Neem contact op met [Pingboard Client ondersteuningsteam](https://support.pingboard.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="65ad6-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="65ad6-165">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="65ad6-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="65ad6-167">a.</span><span class="sxs-lookup"><span data-stu-id="65ad6-167">a.</span></span> <span data-ttu-id="65ad6-168">In de **aanmeldings-URL** textbox, typ de waarde als:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="65ad6-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="65ad6-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="65ad6-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="65ad6-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="65ad6-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="65ad6-173">Eenmalige aanmelding configureren Pingboard zijde, open een nieuw browservenster en meld u aan uw Pingboard Account bij.</span><span class="sxs-lookup"><span data-stu-id="65ad6-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="65ad6-174">U moet een beheerder Pingboard voor het instellen van eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="65ad6-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="65ad6-175">Selecteer in het bovenste menu **Apps > integraties**</span><span class="sxs-lookup"><span data-stu-id="65ad6-175">From the top menu select **Apps > Integrations**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="65ad6-177">Op de **integraties** pagina, zoek de **'Azure Active Directory'** tegel en klik erop.</span><span class="sxs-lookup"><span data-stu-id="65ad6-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="65ad6-179">In de modale klikt u op volgende **'Configureren'**</span><span class="sxs-lookup"><span data-stu-id="65ad6-179">In the modal that follows click **"Configure"**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="65ad6-181">Op de volgende pagina ziet u dat ' Azure SSO-integratie is ingeschakeld.'.</span><span class="sxs-lookup"><span data-stu-id="65ad6-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="65ad6-182">Open het gedownloade Metadata XML-bestand in Kladblok en plak de inhoud van **IDP metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="65ad6-184">Het bestand worden gevalideerd en wordt nu als alles juist en eenmalige aanmelding op ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="65ad6-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65ad6-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="65ad6-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="65ad6-186">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="65ad6-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="65ad6-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="65ad6-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65ad6-189">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="65ad6-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65ad6-191">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="65ad6-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65ad6-193">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65ad6-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65ad6-195">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="65ad6-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65ad6-197">a.</span><span class="sxs-lookup"><span data-stu-id="65ad6-197">a.</span></span> <span data-ttu-id="65ad6-198">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65ad6-199">b.</span><span class="sxs-lookup"><span data-stu-id="65ad6-199">b.</span></span> <span data-ttu-id="65ad6-200">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65ad6-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65ad6-201">c.</span><span class="sxs-lookup"><span data-stu-id="65ad6-201">c.</span></span> <span data-ttu-id="65ad6-202">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65ad6-203">d.</span><span class="sxs-lookup"><span data-stu-id="65ad6-203">d.</span></span> <span data-ttu-id="65ad6-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="65ad6-205">Een testgebruiker Pingboard maken</span><span class="sxs-lookup"><span data-stu-id="65ad6-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="65ad6-206">Om in te schakelen gebruikers van Azure AD aan te melden bij Pingboard, moeten ze worden ingericht in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="65ad6-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="65ad6-207">In het geval van Pingboard is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="65ad6-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="65ad6-208">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="65ad6-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="65ad6-209">Meld u aan bij uw bedrijf Pingboard site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="65ad6-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="65ad6-210">Klik op **'Werknemer toevoegen'** knop op **Directory** pagina.</span><span class="sxs-lookup"><span data-stu-id="65ad6-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="65ad6-212">Op de **'Werknemer toevoegen'** dialoogvenster pagina, de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="65ad6-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="65ad6-214">a.</span><span class="sxs-lookup"><span data-stu-id="65ad6-214">a.</span></span> <span data-ttu-id="65ad6-215">In de **volledige naam** textbox, typt u de volledige naam van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65ad6-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="65ad6-216">b.</span><span class="sxs-lookup"><span data-stu-id="65ad6-216">b.</span></span> <span data-ttu-id="65ad6-217">In de **e** textbox, typ de e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="65ad6-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="65ad6-218">c.</span><span class="sxs-lookup"><span data-stu-id="65ad6-218">c.</span></span> <span data-ttu-id="65ad6-219">In de **taaktitel** textbox, typt u de functie van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65ad6-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="65ad6-220">d.</span><span class="sxs-lookup"><span data-stu-id="65ad6-220">d.</span></span> <span data-ttu-id="65ad6-221">In de **locatie** vervolgkeuzelijst, selecteer de locatie van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65ad6-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="65ad6-222">e.</span><span class="sxs-lookup"><span data-stu-id="65ad6-222">e.</span></span> <span data-ttu-id="65ad6-223">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-223">Click **Add**.</span></span>   

4. <span data-ttu-id="65ad6-224">Een bevestigingsvenster terug om te bevestigen dat het toevoegen van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="65ad6-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![Bevestigen](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="65ad6-226">De accounthouder Azure Active Directory wordt een e-mailbericht ontvangen en Ga als volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="65ad6-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65ad6-227">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="65ad6-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65ad6-228">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Pingboard.</span><span class="sxs-lookup"><span data-stu-id="65ad6-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="65ad6-230">**Britta Simon om aan te wijzen Pingboard, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="65ad6-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="65ad6-231">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="65ad6-233">Selecteer in de lijst met toepassingen **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-233">In the applications list, select **Pingboard**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="65ad6-235">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="65ad6-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="65ad6-237">Click **Add** button.</span></span> <span data-ttu-id="65ad6-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65ad6-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="65ad6-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="65ad6-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65ad6-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65ad6-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65ad6-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65ad6-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65ad6-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65ad6-243">Testing single sign-on</span></span>

<span data-ttu-id="65ad6-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="65ad6-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65ad6-245">Als u op de tegel Pingboard in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Pingboard.</span><span class="sxs-lookup"><span data-stu-id="65ad6-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65ad6-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="65ad6-246">Additional resources</span></span>

* [<span data-ttu-id="65ad6-247">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65ad6-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65ad6-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65ad6-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
