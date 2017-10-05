---
title: 'Zelfstudie: Azure Active Directory-integratie met Land echte reus Client | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en echte reus Land.
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="acc6e-103">Zelfstudie: Azure Active Directory-integratie met Land echte reus Client</span><span class="sxs-lookup"><span data-stu-id="acc6e-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="acc6e-104">In deze zelfstudie leert u het Land echte reus Client integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acc6e-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acc6e-105">Land echte reus Client integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="acc6e-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="acc6e-106">U kunt beheren in Azure AD die toegang tot Land echte reus Client heeft</span><span class="sxs-lookup"><span data-stu-id="acc6e-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="acc6e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Land echte reus Client (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="acc6e-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="acc6e-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="acc6e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="acc6e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="acc6e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="acc6e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="acc6e-110">Prerequisites</span></span>

<span data-ttu-id="acc6e-111">Voor het configureren van Azure AD-integratie met Land echte reus Client, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="acc6e-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="acc6e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="acc6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acc6e-113">Een Land echte reus Client eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="acc6e-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="acc6e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="acc6e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="acc6e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="acc6e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acc6e-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="acc6e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="acc6e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acc6e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="acc6e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="acc6e-118">Scenario description</span></span>
<span data-ttu-id="acc6e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="acc6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acc6e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="acc6e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acc6e-121">Land echte reus Client uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="acc6e-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="acc6e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="acc6e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="acc6e-123">Land echte reus Client uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="acc6e-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="acc6e-124">Voor het configureren van de integratie van Land echte reus Client in Azure AD, moet u Land echte reus Client uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="acc6e-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="acc6e-125">**Als u wilt toevoegen Land echte reus Client uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="acc6e-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="acc6e-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="acc6e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="acc6e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="acc6e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="acc6e-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="acc6e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="acc6e-133">Typ in het zoekvak **Land echte reus Client**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="acc6e-135">Selecteer in het deelvenster resultaten **Land echte reus Client**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="acc6e-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="acc6e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="acc6e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="acc6e-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Land echte reus-Client op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="acc6e-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="acc6e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Land echte reus Client is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acc6e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="acc6e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in een Land echte reus Client tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="acc6e-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="acc6e-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Land echte reus-Client.</span><span class="sxs-lookup"><span data-stu-id="acc6e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="acc6e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Land echte reus Client, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="acc6e-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="acc6e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="acc6e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="acc6e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met beperkte groep.</span><span class="sxs-lookup"><span data-stu-id="acc6e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="acc6e-145">**[Maken van een testgebruiker Land echte reus](#creating-a-land-gorilla-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acc6e-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="acc6e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="acc6e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acc6e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="acc6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="acc6e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="acc6e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="acc6e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw Land echte reus Client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="acc6e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="acc6e-150">**Voor het configureren van Azure AD eenmalige aanmelding met Land echte reus Client, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="acc6e-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="acc6e-151">In de Azure-beheerportal op de **Land echte reus Client** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="acc6e-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="acc6e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="acc6e-155">Op de **Land echte reus clientdomein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="acc6e-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="acc6e-157">a.</span><span class="sxs-lookup"><span data-stu-id="acc6e-157">a.</span></span> <span data-ttu-id="acc6e-158">In de **id** textbox, typ de waarde met een van de volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="acc6e-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="acc6e-159">b.</span><span class="sxs-lookup"><span data-stu-id="acc6e-159">b.</span></span> <span data-ttu-id="acc6e-160">In de **antwoord-URL** textbox, typ een URL met een van de volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="acc6e-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="acc6e-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="acc6e-161">Please note that these are not the real values.</span></span> <span data-ttu-id="acc6e-162">U hebt deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="acc6e-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="acc6e-163">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="acc6e-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="acc6e-164">Neem contact op met [Land echte reus Client team](https://www.landgorilla.com/support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="acc6e-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="acc6e-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="acc6e-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="acc6e-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="acc6e-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="acc6e-169">Als u eenmalige aanmelding configuratie voltooid voor uw toepassing aan Land echte reus einde, neem contact op met [Land echte reus Client ondersteuningsteam](https://www.landgorilla.com/support/) en geeft u de gedownloade **' Metadata XML** bestand.</span><span class="sxs-lookup"><span data-stu-id="acc6e-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="acc6e-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="acc6e-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="acc6e-171">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="acc6e-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="acc6e-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="acc6e-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="acc6e-174">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="acc6e-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="acc6e-176">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="acc6e-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="acc6e-178">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="acc6e-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="acc6e-180">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="acc6e-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="acc6e-182">a.</span><span class="sxs-lookup"><span data-stu-id="acc6e-182">a.</span></span> <span data-ttu-id="acc6e-183">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acc6e-184">b.</span><span class="sxs-lookup"><span data-stu-id="acc6e-184">b.</span></span> <span data-ttu-id="acc6e-185">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="acc6e-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="acc6e-186">c.</span><span class="sxs-lookup"><span data-stu-id="acc6e-186">c.</span></span> <span data-ttu-id="acc6e-187">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="acc6e-188">d.</span><span class="sxs-lookup"><span data-stu-id="acc6e-188">d.</span></span> <span data-ttu-id="acc6e-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="acc6e-190">Maken van een echte reus Land testgebruiker</span><span class="sxs-lookup"><span data-stu-id="acc6e-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="acc6e-191">Neem contact op met [Land echte reus ondersteuningsteam](https://www.landgorilla.com/support/) toevoegen van de gebruikers in het Land echte reus-platform.</span><span class="sxs-lookup"><span data-stu-id="acc6e-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="acc6e-192">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="acc6e-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="acc6e-193">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Land echte reus Client.</span><span class="sxs-lookup"><span data-stu-id="acc6e-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="acc6e-195">**Britta Simon om aan te wijzen Land echte reus Client, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="acc6e-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="acc6e-196">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="acc6e-198">Selecteer in de lijst met toepassingen **Land echte reus Client**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="acc6e-200">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="acc6e-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="acc6e-202">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="acc6e-202">Click **Add** button.</span></span> <span data-ttu-id="acc6e-203">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="acc6e-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="acc6e-205">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="acc6e-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="acc6e-206">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="acc6e-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acc6e-207">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="acc6e-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="acc6e-208">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="acc6e-208">Testing single sign-on</span></span>

<span data-ttu-id="acc6e-209">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="acc6e-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="acc6e-210">Als u op de tegel Land echte reus Client in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Land echte reus Client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="acc6e-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="acc6e-211">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="acc6e-211">Additional resources</span></span>

* [<span data-ttu-id="acc6e-212">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acc6e-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acc6e-213">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="acc6e-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
