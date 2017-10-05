---
title: 'Zelfstudie: Azure Active Directory-integratie met Nomadic | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Nomadic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 1817a1395c2ffa7268abfff268d9d041f7f21a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="21e66-103">Zelfstudie: Azure Active Directory-integratie met Nomadic</span><span class="sxs-lookup"><span data-stu-id="21e66-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="21e66-104">In deze zelfstudie leert u hoe Nomadic integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21e66-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21e66-105">Nomadic integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="21e66-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="21e66-106">U kunt beheren in Azure AD die toegang tot Nomadic heeft.</span><span class="sxs-lookup"><span data-stu-id="21e66-106">You can control in Azure AD who has access to Nomadic.</span></span>
- <span data-ttu-id="21e66-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Nomadic (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="21e66-107">You can enable your users to automatically get signed-on to Nomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="21e66-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="21e66-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="21e66-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21e66-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21e66-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="21e66-110">Prerequisites</span></span>

<span data-ttu-id="21e66-111">Voor het configureren van Azure AD-integratie met Nomadic, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="21e66-111">To configure Azure AD integration with Nomadic, you need the following items:</span></span>

- <span data-ttu-id="21e66-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="21e66-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21e66-113">Een Nomadic eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="21e66-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21e66-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="21e66-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21e66-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="21e66-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21e66-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="21e66-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21e66-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21e66-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21e66-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="21e66-118">Scenario description</span></span>
<span data-ttu-id="21e66-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="21e66-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21e66-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="21e66-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21e66-121">Nomadic uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="21e66-121">Add Nomadic from the gallery</span></span>
2. <span data-ttu-id="21e66-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="21e66-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-the-gallery"></a><span data-ttu-id="21e66-123">Nomadic uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="21e66-123">Add Nomadic from the gallery</span></span>
<span data-ttu-id="21e66-124">Voor het configureren van de integratie van Nomadic in Azure AD, moet u Nomadic uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="21e66-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="21e66-125">**Als u wilt toevoegen Nomadic uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="21e66-125">**To add Nomadic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="21e66-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="21e66-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="21e66-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="21e66-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="21e66-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="21e66-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="21e66-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="21e66-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="21e66-133">Typ in het zoekvak **Nomadic**, selecteer **Nomadic** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="21e66-133">In the search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button to add the application.</span></span>

    ![Nomadic in de lijst met resultaten](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="21e66-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="21e66-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="21e66-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Nomadic op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="21e66-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="21e66-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Nomadic is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21e66-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span></span> <span data-ttu-id="21e66-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Nomadic tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="21e66-138">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span></span>

<span data-ttu-id="21e66-139">Wijs in Nomadic, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="21e66-139">In Nomadic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="21e66-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Nomadic, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="21e66-140">To configure and test Azure AD single sign-on with Nomadic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="21e66-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="21e66-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="21e66-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21e66-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21e66-143">**[Maak een Nomadic testgebruiker](#create-a-nomadic-test-user)**  - Nomadic die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="21e66-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="21e66-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="21e66-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21e66-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="21e66-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="21e66-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="21e66-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="21e66-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Nomadic configureren.</span><span class="sxs-lookup"><span data-stu-id="21e66-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="21e66-148">**Voor het configureren van Azure AD eenmalige aanmelding met Nomadic, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="21e66-148">**To configure Azure AD single sign-on with Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="21e66-149">In de Azure-portal op de **Nomadic** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="21e66-149">In the Azure portal, on the **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="21e66-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="21e66-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="21e66-153">Op de **Nomadic domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="21e66-153">On the **Nomadic Domain and URLs** section, perform the following steps:</span></span>

    ![Nomadic domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="21e66-155">a.</span><span class="sxs-lookup"><span data-stu-id="21e66-155">a.</span></span> <span data-ttu-id="21e66-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="21e66-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="21e66-157">b.</span><span class="sxs-lookup"><span data-stu-id="21e66-157">b.</span></span> <span data-ttu-id="21e66-158">In de **id** textbox, typ een URL met het volgende patroon volgen: `https://<company name>.nomadic.fm/auth/saml2/sp`,`https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="21e66-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21e66-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="21e66-159">These values are not real.</span></span> <span data-ttu-id="21e66-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="21e66-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="21e66-161">Neem contact op met [Nomadic Client ondersteuningsteam](mailto:help@nomadic.fm) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="21e66-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) to get these values.</span></span> 
 


4. <span data-ttu-id="21e66-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="21e66-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="21e66-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="21e66-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="21e66-166">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [Nomadic ondersteuningsteam](mailto:help@nomadic.fm) en geeft u de gedownloade **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="21e66-166">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="21e66-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="21e66-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="21e66-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="21e66-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="21e66-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="21e66-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="21e66-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="21e66-170">Create an Azure AD test user</span></span>

<span data-ttu-id="21e66-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="21e66-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="21e66-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="21e66-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="21e66-174">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="21e66-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="21e66-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="21e66-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="21e66-178">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="21e66-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="21e66-180">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="21e66-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="21e66-182">a.</span><span class="sxs-lookup"><span data-stu-id="21e66-182">a.</span></span> <span data-ttu-id="21e66-183">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="21e66-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21e66-184">b.</span><span class="sxs-lookup"><span data-stu-id="21e66-184">b.</span></span> <span data-ttu-id="21e66-185">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21e66-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="21e66-186">c.</span><span class="sxs-lookup"><span data-stu-id="21e66-186">c.</span></span> <span data-ttu-id="21e66-187">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="21e66-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="21e66-188">d.</span><span class="sxs-lookup"><span data-stu-id="21e66-188">d.</span></span> <span data-ttu-id="21e66-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="21e66-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="21e66-190">Een Nomadic testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="21e66-190">Create a Nomadic test user</span></span>

<span data-ttu-id="21e66-191">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Nomadic maken.</span><span class="sxs-lookup"><span data-stu-id="21e66-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="21e66-192">Neem contact op met [Nomadic ondersteuningsteam](mailto:help@nomadic.fm) toevoegen van de gebruikers in het Nomadic platform.</span><span class="sxs-lookup"><span data-stu-id="21e66-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="21e66-193">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="21e66-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="21e66-194">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Nomadic.</span><span class="sxs-lookup"><span data-stu-id="21e66-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadic.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="21e66-196">**Britta Simon om aan te wijzen Nomadic, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="21e66-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="21e66-197">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="21e66-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="21e66-199">Selecteer in de lijst met toepassingen **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="21e66-199">In the applications list, select **Nomadic**.</span></span>

    ![De Nomadic koppelen in de lijst met toepassingen](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="21e66-201">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="21e66-201">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="21e66-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="21e66-203">Click **Add** button.</span></span> <span data-ttu-id="21e66-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="21e66-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="21e66-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="21e66-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="21e66-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="21e66-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21e66-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="21e66-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="21e66-209">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="21e66-209">Test single sign-on</span></span>

<span data-ttu-id="21e66-210">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="21e66-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="21e66-211">Wanneer u klikt op de tegel Nomadic in het deelvenster toegang u moet ophalen automatisch aangemeld bij uw Nomadic toepassing.</span><span class="sxs-lookup"><span data-stu-id="21e66-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span></span>
<span data-ttu-id="21e66-212">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="21e66-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="21e66-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="21e66-213">Additional resources</span></span>

* [<span data-ttu-id="21e66-214">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21e66-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21e66-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="21e66-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

