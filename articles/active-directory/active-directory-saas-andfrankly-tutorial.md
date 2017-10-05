---
title: 'Zelfstudie: Azure Active Directory-integratie met & eerlijk gezegd | Microsoft Docs'
description: Meer informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en & eerlijk gezegd.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: ea18a9f9bff258337a3de6d7703b4c548efa37df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="ec9ea-103">Zelfstudie: Azure Active Directory-integratie met & eerlijk gezegd</span><span class="sxs-lookup"><span data-stu-id="ec9ea-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="ec9ea-104">In deze zelfstudie leert u hoe integreren & eerlijk gezegd met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec9ea-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec9ea-105">Integratie van & eerlijk gezegd met Azure AD biedt u de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ec9ea-106">U kunt beheren in Azure AD die toegang tot & eerlijk gezegd heeft</span><span class="sxs-lookup"><span data-stu-id="ec9ea-106">You can control in Azure AD who has access to &frankly</span></span>
- <span data-ttu-id="ec9ea-107">U kunt uw gebruikers automatisch aangemelde op & eerlijk gezegd inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="ec9ea-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec9ea-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ec9ea-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ec9ea-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec9ea-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec9ea-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec9ea-110">Prerequisites</span></span>

<span data-ttu-id="ec9ea-111">Voor het configureren van Azure AD nodig-integratie met & eerlijk gezegd, u het volgende:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

- <span data-ttu-id="ec9ea-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ec9ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec9ea-113">A & eerlijk gezegd eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ec9ea-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec9ea-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec9ea-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec9ea-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec9ea-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec9ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec9ea-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ec9ea-118">Scenario description</span></span>
<span data-ttu-id="ec9ea-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec9ea-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec9ea-121">Toe te voegen & eerlijk gezegd uit de galerie</span><span class="sxs-lookup"><span data-stu-id="ec9ea-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="ec9ea-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec9ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="ec9ea-123">Toe te voegen & eerlijk gezegd uit de galerie</span><span class="sxs-lookup"><span data-stu-id="ec9ea-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="ec9ea-124">Voor het configureren van de integratie van & eerlijk gezegd met Azure AD, moet u toevoegen & eerlijk gezegd uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ec9ea-125">**Voeg & eerlijk gezegd uit de galerie, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ec9ea-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ec9ea-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec9ea-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ec9ea-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ec9ea-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ec9ea-133">Typ in het zoekvak **& eerlijk gezegd**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-133">In the search box, type **&frankly**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="ec9ea-135">Selecteer in het deelvenster resultaten **& eerlijk gezegd**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec9ea-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec9ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec9ea-138">In deze sectie u configureren en testen van Azure AD eenmalige aanmelding met & eerlijk gezegd op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ec9ea-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ec9ea-139">Voor eenmalige aanmelding werkt, Azure AD moet weten welke gebruiker de bijbehorende equivalent in & eerlijk gezegd is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span></span> <span data-ttu-id="ec9ea-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in & eerlijk gezegd tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="ec9ea-141">In & eerlijk gezegd, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ec9ea-142">Als u wilt configureren en testen van Azure AD moet eenmalige aanmelding met & eerlijk gezegd, u voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ec9ea-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ec9ea-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec9ea-145">**[Maken van een & eerlijk gezegd testgebruiker](#creating-a-frankly-test-user)**  - hebben een equivalent van Britta Simon in & eerlijk gezegd is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec9ea-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec9ea-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec9ea-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ec9ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec9ea-149">In deze sectie kunt u Azure AD eenmalige aanmelding in de Azure portal inschakelen en configureren eenmalige aanmelding in uw & eerlijk gezegd groep.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="ec9ea-150">**Voor het configureren van Azure AD één aanmelding met & eerlijk gezegd, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="ec9ea-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="ec9ea-151">In de Azure-portal op de **& eerlijk gezegd** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ec9ea-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="ec9ea-155">Op de **& eerlijk gezegd domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="ec9ea-157">a.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-157">a.</span></span> <span data-ttu-id="ec9ea-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="ec9ea-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="ec9ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-159">b.</span></span> <span data-ttu-id="ec9ea-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="ec9ea-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="ec9ea-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ec9ea-162">Als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="ec9ea-164">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="ec9ea-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="ec9ea-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-165">These values are not real.</span></span> <span data-ttu-id="ec9ea-166">Deze waarden bijwerken met de werkelijke-id en eenmalige aanmelding en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="ec9ea-167">Neem contact op met [andfrankly ondersteuningsteam](mailto:help@andfrankly.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span></span>

5. <span data-ttu-id="ec9ea-168">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="ec9ea-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ec9ea-172">Eenmalige aanmelding configureren op **& eerlijk gezegd** zijde, moet u de gedownloade verzenden **Metadata XML** naar [andfrankly ondersteuningsteam](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="ec9ea-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ec9ea-173">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ec9ea-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ec9ea-174">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ec9ea-175">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec9ea-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec9ea-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ec9ea-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec9ea-177">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ec9ea-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ec9ea-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ec9ea-180">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec9ea-182">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec9ea-184">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec9ea-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ec9ea-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec9ea-188">a.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-188">a.</span></span> <span data-ttu-id="ec9ea-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec9ea-190">b.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-190">b.</span></span> <span data-ttu-id="ec9ea-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec9ea-192">c.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-192">c.</span></span> <span data-ttu-id="ec9ea-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ec9ea-194">d.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-194">d.</span></span> <span data-ttu-id="ec9ea-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="ec9ea-196">Maken van een & eerlijk gezegd testgebruiker</span><span class="sxs-lookup"><span data-stu-id="ec9ea-196">Creating a &frankly test user</span></span>

<span data-ttu-id="ec9ea-197">In deze sectie maakt u een gebruiker met de naam Britta Simon in & eerlijk gezegd.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="ec9ea-198">Werken met [andfrankly ondersteuningsteam](mailto:help@andfrankly.com) om toe te voegen de gebruikers in de & eerlijk gezegd platform.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ec9ea-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec9ea-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ec9ea-200">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot & eerlijk gezegd.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ec9ea-202">**Als u wilt toewijzen Britta Simon op & eerlijk gezegd, kunt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ec9ea-202">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="ec9ea-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ec9ea-205">Selecteer in de lijst met toepassingen **& eerlijk gezegd**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-205">In the applications list, select **&frankly**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="ec9ea-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ec9ea-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-209">Click **Add** button.</span></span> <span data-ttu-id="ec9ea-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ec9ea-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ec9ea-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec9ea-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec9ea-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec9ea-215">Testing single sign-on</span></span>

<span data-ttu-id="ec9ea-216">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="ec9ea-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ec9ea-217">Wanneer u klikt op de & eerlijk gezegd tegel in het deelvenster toegang, krijgt u automatisch aangemeld bij uw & eerlijk gezegd groep</span><span class="sxs-lookup"><span data-stu-id="ec9ea-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec9ea-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ec9ea-218">Additional resources</span></span>

* [<span data-ttu-id="ec9ea-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec9ea-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec9ea-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec9ea-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

