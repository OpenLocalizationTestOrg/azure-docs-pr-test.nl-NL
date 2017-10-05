---
title: 'Zelfstudie: Azure Active Directory-integratie met contracten ASC | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ASC contracten.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="6d634-103">Zelfstudie: Azure Active Directory-integratie met ASC contracten</span><span class="sxs-lookup"><span data-stu-id="6d634-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="6d634-104">In deze zelfstudie leert u hoe ASC contracten integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d634-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d634-105">ASC contracten integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6d634-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d634-106">U kunt beheren in Azure AD die toegang tot ASC contracten heeft</span><span class="sxs-lookup"><span data-stu-id="6d634-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="6d634-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ASC contracten (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="6d634-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d634-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6d634-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6d634-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d634-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d634-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6d634-110">Prerequisites</span></span>

<span data-ttu-id="6d634-111">Voor het configureren van Azure AD-integratie met ASC contracten, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6d634-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="6d634-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6d634-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d634-113">Een ASC contracten eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6d634-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d634-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d634-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d634-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6d634-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d634-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6d634-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d634-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d634-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d634-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6d634-118">Scenario description</span></span>
<span data-ttu-id="6d634-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d634-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d634-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6d634-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d634-121">ASC contracten uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d634-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="6d634-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d634-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="6d634-123">ASC contracten uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d634-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="6d634-124">Voor het configureren van de integratie van ASC contracten in Azure AD, moet u ASC contracten uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6d634-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d634-125">**Als u wilt toevoegen ASC contracten uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d634-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d634-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d634-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d634-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d634-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d634-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d634-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6d634-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d634-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6d634-133">Typ in het zoekvak **ASC contracten**.</span><span class="sxs-lookup"><span data-stu-id="6d634-133">In the search box, type **ASC Contracts**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="6d634-135">Selecteer in het deelvenster resultaten **ASC contracten**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d634-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d634-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d634-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d634-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ASC contracten op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6d634-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6d634-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ASC contracten in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="6d634-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="6d634-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ASC contracten tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6d634-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="6d634-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in ASC contracten.</span><span class="sxs-lookup"><span data-stu-id="6d634-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="6d634-142">Om te configureren en testen van Azure AD eenmalige aanmelding met ASC contracten, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6d634-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d634-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d634-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d634-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d634-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d634-145">**[Maken van een testgebruiker ASC contracten](#creating-an-asc-contracts-test-user)**  - ASC contracten die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6d634-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d634-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6d634-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d634-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6d634-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d634-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6d634-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d634-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing ASC contracten.</span><span class="sxs-lookup"><span data-stu-id="6d634-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="6d634-150">**Voor het configureren van Azure AD eenmalige aanmelding met ASC contracten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d634-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="6d634-151">In de Azure-portal op de **ASC contracten** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6d634-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6d634-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6d634-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="6d634-155">Op de **ASC contracten domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d634-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="6d634-157">a.</span><span class="sxs-lookup"><span data-stu-id="6d634-157">a.</span></span> <span data-ttu-id="6d634-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="6d634-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="6d634-159">b.</span><span class="sxs-lookup"><span data-stu-id="6d634-159">b.</span></span> <span data-ttu-id="6d634-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="6d634-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d634-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6d634-161">These values are not real.</span></span> <span data-ttu-id="6d634-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="6d634-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6d634-163">Neem contact op met ASC netwerken Inc. (ASC)-team via **613.599.6178** ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6d634-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="6d634-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6d634-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="6d634-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6d634-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6d634-168">Eenmalige aanmelding configureren op **ASC contracten** zijde, contact op met ondersteuning op ASC netwerken Inc. (ASC) **613.599.6178** en geeft u de gedownloade **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="6d634-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="6d634-169">Ze hebben de SAML SSO-verbinding juist ingesteld voor beide zijden van deze toepassing ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6d634-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6d634-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6d634-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6d634-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6d634-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6d634-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d634-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d634-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6d634-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d634-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6d634-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6d634-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d634-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d634-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d634-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d634-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6d634-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d634-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d634-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d634-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d634-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d634-185">a.</span><span class="sxs-lookup"><span data-stu-id="6d634-185">a.</span></span> <span data-ttu-id="6d634-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d634-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d634-187">b.</span><span class="sxs-lookup"><span data-stu-id="6d634-187">b.</span></span> <span data-ttu-id="6d634-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6d634-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d634-189">c.</span><span class="sxs-lookup"><span data-stu-id="6d634-189">c.</span></span> <span data-ttu-id="6d634-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6d634-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d634-191">d.</span><span class="sxs-lookup"><span data-stu-id="6d634-191">d.</span></span> <span data-ttu-id="6d634-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6d634-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="6d634-193">Een testgebruiker ASC contracten maken</span><span class="sxs-lookup"><span data-stu-id="6d634-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="6d634-194">Werken met het ondersteuningsteam ASC netwerken Inc. (ASC) op **613.599.6178** ophalen van de gebruikers van het platform ASC contracten toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6d634-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d634-195">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d634-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d634-196">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ASC contracten.</span><span class="sxs-lookup"><span data-stu-id="6d634-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6d634-198">**Britta Simon om aan te wijzen ASC contracten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d634-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="6d634-199">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d634-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6d634-201">Selecteer in de lijst met toepassingen **ASC contracten**.</span><span class="sxs-lookup"><span data-stu-id="6d634-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="6d634-203">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6d634-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6d634-205">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6d634-205">Click **Add** button.</span></span> <span data-ttu-id="6d634-206">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d634-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6d634-208">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6d634-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d634-209">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d634-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d634-210">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d634-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d634-211">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d634-211">Testing single sign-on</span></span>

<span data-ttu-id="6d634-212">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6d634-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6d634-213">Als u op de tegel ASC contracten in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ASC contracten.</span><span class="sxs-lookup"><span data-stu-id="6d634-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="6d634-214">Zie voor meer informatie over het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6d634-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="6d634-215">[Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="6d634-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d634-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6d634-216">Additional resources</span></span>

* [<span data-ttu-id="6d634-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d634-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d634-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d634-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

