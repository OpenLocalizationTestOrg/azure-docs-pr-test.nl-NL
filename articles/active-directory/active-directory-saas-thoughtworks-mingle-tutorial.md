---
title: 'Zelfstudie: Azure Active Directory-integratie met Thoughtworks Singleplayer | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Thoughtworks Singleplayer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="0ed21-103">Zelfstudie: Azure Active Directory-integratie met Thoughtworks Singleplayer</span><span class="sxs-lookup"><span data-stu-id="0ed21-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="0ed21-104">In deze zelfstudie leert u hoe Thoughtworks Singleplayer integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ed21-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ed21-105">Thoughtworks Singleplayer integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0ed21-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0ed21-106">U kunt beheren in Azure AD die toegang tot Thoughtworks Singleplayer heeft</span><span class="sxs-lookup"><span data-stu-id="0ed21-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="0ed21-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Thoughtworks Singleplayer (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="0ed21-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ed21-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0ed21-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0ed21-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ed21-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ed21-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0ed21-110">Prerequisites</span></span>

<span data-ttu-id="0ed21-111">Voor het configureren van Azure AD-integratie met Thoughtworks Singleplayer, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="0ed21-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="0ed21-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0ed21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ed21-113">Een Thoughtworks Singleplayer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0ed21-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ed21-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0ed21-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ed21-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0ed21-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ed21-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0ed21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ed21-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ed21-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ed21-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0ed21-118">Scenario description</span></span>
<span data-ttu-id="0ed21-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0ed21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ed21-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0ed21-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ed21-121">Toe te voegen Thoughtworks Singleplayer uit de galerie</span><span class="sxs-lookup"><span data-stu-id="0ed21-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="0ed21-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0ed21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="0ed21-123">Toe te voegen Thoughtworks Singleplayer uit de galerie</span><span class="sxs-lookup"><span data-stu-id="0ed21-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="0ed21-124">Voor het configureren van de integratie van Thoughtworks Singleplayer in Azure AD, moet u Thoughtworks Singleplayer toevoegen uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0ed21-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0ed21-125">**Als u wilt toevoegen Thoughtworks Singleplayer uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0ed21-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0ed21-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0ed21-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="0ed21-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0ed21-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="0ed21-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0ed21-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="0ed21-133">Typ in het zoekvak **Thoughtworks Singleplayer**, selecteer **Thoughtworks Singleplayer** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ed21-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![Thoughtworks Singleplayer in de lijst met resultaten](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0ed21-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ed21-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0ed21-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Thoughtworks Singleplayer op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0ed21-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ed21-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Thoughtworks Singleplayer is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ed21-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="0ed21-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Thoughtworks Singleplayer tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="0ed21-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="0ed21-139">Wijs in het Thoughtworks Singleplayer, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="0ed21-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0ed21-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Thoughtworks Singleplayer, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="0ed21-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0ed21-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ed21-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0ed21-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ed21-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ed21-143">**[Maak een testgebruiker Thoughtworks Singleplayer](#create-a-thoughtworks-mingle-test-user)**  - Thoughtworks Singleplayer die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="0ed21-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ed21-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0ed21-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ed21-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0ed21-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0ed21-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0ed21-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0ed21-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Thoughtworks Singleplayer configureren.</span><span class="sxs-lookup"><span data-stu-id="0ed21-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="0ed21-148">**Voor het configureren van Azure AD eenmalige aanmelding met Thoughtworks Singleplayer, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0ed21-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="0ed21-149">In de Azure-portal op de **Thoughtworks Singleplayer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0ed21-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0ed21-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="0ed21-153">Op de **Thoughtworks Singleplayer domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0ed21-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en Thoughtworks Singleplayer domein eenmalige aanmelding informatie](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="0ed21-155">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="0ed21-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ed21-156">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="0ed21-156">The value is not real.</span></span> <span data-ttu-id="0ed21-157">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0ed21-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="0ed21-158">Neem contact op met [Thoughtworks Singleplayer Client ondersteuningsteam](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="0ed21-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="0ed21-159">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0ed21-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="0ed21-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0ed21-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ed21-163">Meld u aan bij uw **Thoughtworks Singleplayer** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="0ed21-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="0ed21-164">Klik op de **Admin** tabblad en klik vervolgens op **SSO-Config**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="0ed21-165">![Tabblad beheer](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="0ed21-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="0ed21-166">In de **SSO-Config** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0ed21-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="0ed21-167">![SSO-Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="0ed21-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="0ed21-168">a.</span><span class="sxs-lookup"><span data-stu-id="0ed21-168">a.</span></span> <span data-ttu-id="0ed21-169">Als u wilt uploaden van het metagegevensbestand, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="0ed21-170">b.</span><span class="sxs-lookup"><span data-stu-id="0ed21-170">b.</span></span> <span data-ttu-id="0ed21-171">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0ed21-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="0ed21-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0ed21-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="0ed21-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0ed21-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ed21-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0ed21-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0ed21-175">Create an Azure AD test user</span></span>
<span data-ttu-id="0ed21-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0ed21-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="0ed21-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0ed21-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0ed21-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0ed21-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ed21-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ed21-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0ed21-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ed21-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0ed21-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ed21-187">a.</span><span class="sxs-lookup"><span data-stu-id="0ed21-187">a.</span></span> <span data-ttu-id="0ed21-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ed21-189">b.</span><span class="sxs-lookup"><span data-stu-id="0ed21-189">b.</span></span> <span data-ttu-id="0ed21-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0ed21-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ed21-191">c.</span><span class="sxs-lookup"><span data-stu-id="0ed21-191">c.</span></span> <span data-ttu-id="0ed21-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0ed21-193">d.</span><span class="sxs-lookup"><span data-stu-id="0ed21-193">d.</span></span> <span data-ttu-id="0ed21-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="0ed21-195">Een testgebruiker Thoughtworks Singleplayer maken</span><span class="sxs-lookup"><span data-stu-id="0ed21-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="0ed21-196">Azure AD-gebruikers moeten kunnen aanmelden, als ze worden ingericht voor de toepassing Thoughtworks Singleplayer met behulp van de namen van de Azure Active Directory-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0ed21-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="0ed21-197">In het geval van Thoughtworks Singleplayer is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="0ed21-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="0ed21-198">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0ed21-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0ed21-199">Meld u aan bij uw bedrijf Thoughtworks Singleplayer site als administrator.</span><span class="sxs-lookup"><span data-stu-id="0ed21-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="0ed21-200">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="0ed21-201">![Uw eerste Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "uw eerste Project")</span><span class="sxs-lookup"><span data-stu-id="0ed21-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="0ed21-202">Klik op de **Admin** tabblad en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="0ed21-203">![Gebruikers](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="0ed21-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="0ed21-204">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-204">Click **New User**.</span></span>
   
    <span data-ttu-id="0ed21-205">![Nieuwe gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="0ed21-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="0ed21-206">Op de **nieuwe gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0ed21-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="0ed21-207">![Dialoogvenster Nieuwe gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="0ed21-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="0ed21-208">a.</span><span class="sxs-lookup"><span data-stu-id="0ed21-208">a.</span></span> <span data-ttu-id="0ed21-209">Type de **aanmeldingsnaam**, **weergavenaam**, **Kies wachtwoord**, **wachtwoord bevestigen** van een geldig Azure AD-account die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="0ed21-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="0ed21-210">b.</span><span class="sxs-lookup"><span data-stu-id="0ed21-210">b.</span></span> <span data-ttu-id="0ed21-211">Als **gebruikerstype**, selecteer **volledige gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="0ed21-212">c.</span><span class="sxs-lookup"><span data-stu-id="0ed21-212">c.</span></span> <span data-ttu-id="0ed21-213">Klik op **maken van dit profiel**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="0ed21-214">U kunt andere Thoughtworks Singleplayer gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Thoughtworks Singleplayer aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="0ed21-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0ed21-215">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="0ed21-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="0ed21-216">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen Thoughtworks Singleplayer.</span><span class="sxs-lookup"><span data-stu-id="0ed21-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="0ed21-218">**Britta Simon om aan te wijzen Thoughtworks Singleplayer, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0ed21-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="0ed21-219">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0ed21-221">Selecteer in de lijst met toepassingen **Thoughtworks Singleplayer**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![De koppeling Thoughtworks Singleplayer in de lijst met toepassingen](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="0ed21-223">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0ed21-223">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202] 

4. <span data-ttu-id="0ed21-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0ed21-225">Click **Add** button.</span></span> <span data-ttu-id="0ed21-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0ed21-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="0ed21-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0ed21-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0ed21-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0ed21-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ed21-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0ed21-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0ed21-231">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0ed21-231">Test single sign-on</span></span>

<span data-ttu-id="0ed21-232">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="0ed21-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0ed21-233">Als u op de tegel Thoughtworks Singleplayer in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Thoughtworks Singleplayer.</span><span class="sxs-lookup"><span data-stu-id="0ed21-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ed21-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0ed21-234">Additional resources</span></span>

* [<span data-ttu-id="0ed21-235">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ed21-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ed21-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ed21-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

