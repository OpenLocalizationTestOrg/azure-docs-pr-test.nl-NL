---
title: 'Zelfstudie: Azure Active Directory-integratie met Brightspace door Desire2Learn | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Brightspace door Desire2Learn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7076b476ba71c5d94ae4728e5f6032b0d7e047ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="cf978-103">Zelfstudie: Azure Active Directory-integratie met Brightspace door Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="cf978-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="cf978-104">In deze zelfstudie leert u hoe Brightspace door Desire2Learn integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf978-104">In this tutorial, you learn how to integrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf978-105">Brightspace door Desire2Learn integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="cf978-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cf978-106">U kunt beheren in Azure AD die toegang tot Brightspace door Desire2Learn heeft</span><span class="sxs-lookup"><span data-stu-id="cf978-106">You can control in Azure AD who has access to Brightspace by Desire2Learn</span></span>
- <span data-ttu-id="cf978-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Brightspace door Desire2Learn inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="cf978-107">You can enable your users to automatically get signed-on to Brightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf978-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="cf978-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cf978-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf978-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf978-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cf978-110">Prerequisites</span></span>

<span data-ttu-id="cf978-111">Voor het configureren van Azure AD-integratie met Brightspace door Desire2Learn, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="cf978-111">To configure Azure AD integration with Brightspace by Desire2Learn, you need the following items:</span></span>

- <span data-ttu-id="cf978-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="cf978-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf978-113">Een Brightspace door eenmalige aanmelding Desire2Learn abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="cf978-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf978-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cf978-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf978-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="cf978-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf978-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="cf978-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf978-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf978-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf978-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cf978-118">Scenario description</span></span>
<span data-ttu-id="cf978-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="cf978-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf978-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="cf978-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf978-121">Brightspace door Desire2Learn uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="cf978-121">Adding Brightspace by Desire2Learn from the gallery</span></span>
2. <span data-ttu-id="cf978-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf978-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-the-gallery"></a><span data-ttu-id="cf978-123">Brightspace door Desire2Learn uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="cf978-123">Adding Brightspace by Desire2Learn from the gallery</span></span>
<span data-ttu-id="cf978-124">Voor het configureren van de integratie van Brightspace door Desire2Learn in Azure AD, moet u Brightspace door Desire2Learn uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="cf978-124">To configure the integration of Brightspace by Desire2Learn into Azure AD, you need to add Brightspace by Desire2Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cf978-125">**Als u wilt toevoegen Brightspace door Desire2Learn uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf978-125">**To add Brightspace by Desire2Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cf978-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cf978-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf978-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf978-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cf978-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf978-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="cf978-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf978-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="cf978-133">Typ in het zoekvak **Brightspace door Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="cf978-133">In the search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="cf978-135">Selecteer in het deelvenster resultaten **Brightspace door Desire2Learn**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="cf978-135">In the results panel, select **Brightspace by Desire2Learn**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf978-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf978-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf978-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Brightspace door Desire2Learn op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="cf978-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf978-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Brightspace door Desire2Learn is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf978-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Brightspace by Desire2Learn is to a user in Azure AD.</span></span> <span data-ttu-id="cf978-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Brightspace door Desire2Learn tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="cf978-140">In other words, a link relationship between an Azure AD user and the related user in Brightspace by Desire2Learn needs to be established.</span></span>

<span data-ttu-id="cf978-141">Wijs in Brightspace door Desire2Learn de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="cf978-141">In Brightspace by Desire2Learn, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cf978-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Brightspace door Desire2Learn, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="cf978-142">To configure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cf978-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cf978-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cf978-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf978-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf978-145">**[Maken van een Brightspace door Desire2Learn testgebruiker](#creating-a-brightspace-by-desire2learn-test-user)**  - Brightspace door Desire2Learn die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="cf978-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - to have a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf978-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cf978-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf978-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="cf978-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf978-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="cf978-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf978-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Brightspace door Desire2Learn toepassing.</span><span class="sxs-lookup"><span data-stu-id="cf978-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="cf978-150">**Voor het configureren van Azure AD eenmalige aanmelding met Brightspace door Desire2Learn, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf978-150">**To configure Azure AD single sign-on with Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="cf978-151">In de Azure-portal op de **Brightspace door Desire2Learn** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="cf978-151">In the Azure portal, on the **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="cf978-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cf978-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="cf978-155">Op de **Brightspace Desire2Learn domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cf978-155">On the **Brightspace by Desire2Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="cf978-157">a.</span><span class="sxs-lookup"><span data-stu-id="cf978-157">a.</span></span> <span data-ttu-id="cf978-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="cf978-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="cf978-159">b.</span><span class="sxs-lookup"><span data-stu-id="cf978-159">b.</span></span> <span data-ttu-id="cf978-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="cf978-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cf978-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="cf978-161">These values are not real.</span></span> <span data-ttu-id="cf978-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="cf978-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="cf978-163">Neem contact op met [Brightspace door Desire2Learn ondersteuningsteam](https://www.d2l.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="cf978-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) to get these values.</span></span>
 


4. <span data-ttu-id="cf978-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cf978-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="cf978-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="cf978-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cf978-168">Eenmalige aanmelding configureren op **Brightspace door Desire2Learn** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Brightspace door Desire2Learn ondersteuningsteam](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cf978-168">To configure single sign-on on **Brightspace by Desire2Learn** side, you need to send the downloaded **Metadata XML** to [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="cf978-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="cf978-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cf978-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="cf978-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cf978-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf978-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf978-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cf978-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf978-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cf978-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="cf978-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf978-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cf978-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cf978-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf978-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cf978-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf978-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf978-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf978-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cf978-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf978-184">a.</span><span class="sxs-lookup"><span data-stu-id="cf978-184">a.</span></span> <span data-ttu-id="cf978-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf978-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf978-186">b.</span><span class="sxs-lookup"><span data-stu-id="cf978-186">b.</span></span> <span data-ttu-id="cf978-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf978-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf978-188">c.</span><span class="sxs-lookup"><span data-stu-id="cf978-188">c.</span></span> <span data-ttu-id="cf978-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="cf978-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cf978-190">d.</span><span class="sxs-lookup"><span data-stu-id="cf978-190">d.</span></span> <span data-ttu-id="cf978-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cf978-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="cf978-192">Een Brightspace door Desire2Learn testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cf978-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="cf978-193">Om in te schakelen gebruikers van Azure AD aan te melden bij Brightspace door Desire2Learn, moeten ze in Brightspace worden ingericht met behulp van Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="cf978-193">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="cf978-194">In het geval van Brightspace door Desire2Learn de gebruikersaccounts moeten worden gemaakt door uw [Brightspace door Desire2Learn ondersteuningsteam](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cf978-194">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="cf978-195">Kunt u andere Brightspace door Desire2Learn gebruiker-account maken's of API's geleverd door Brightspace door Desire2Learn om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="cf978-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cf978-196">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf978-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cf978-197">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Brightspace door Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="cf978-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Brightspace by Desire2Learn.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="cf978-199">**Britta Simon om aan te wijzen Brightspace door Desire2Learn, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf978-199">**To assign Britta Simon to Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="cf978-200">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf978-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="cf978-202">Selecteer in de lijst met toepassingen **Brightspace door Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="cf978-202">In the applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="cf978-204">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="cf978-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="cf978-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="cf978-206">Click **Add** button.</span></span> <span data-ttu-id="cf978-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf978-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="cf978-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cf978-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cf978-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf978-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf978-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf978-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf978-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf978-212">Testing single sign-on</span></span>

<span data-ttu-id="cf978-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="cf978-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cf978-214">Als u op de Brightspace door Desire2Learn-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Brightspace door Desire2Learn toepassing.</span><span class="sxs-lookup"><span data-stu-id="cf978-214">When you click the Brightspace by Desire2Learn tile in the Access Panel, you should get automatically signed-on to your Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="cf978-215">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cf978-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf978-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cf978-216">Additional resources</span></span>

* [<span data-ttu-id="cf978-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf978-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf978-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf978-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

