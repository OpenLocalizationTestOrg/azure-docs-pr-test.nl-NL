---
title: 'Zelfstudie: Azure Active Directory-integratie met Springer koppeling | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Springer koppeling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: b9aec6f8f293cdd31456a7f50e3efe792804c7c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="e68e4-103">Zelfstudie: Azure Active Directory-integratie met Springer koppeling</span><span class="sxs-lookup"><span data-stu-id="e68e4-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="e68e4-104">In deze zelfstudie leert u hoe Springer koppeling integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e68e4-104">In this tutorial, you learn how to integrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e68e4-105">Springer koppeling integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e68e4-105">Integrating Springer Link with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e68e4-106">U kunt beheren in Azure AD die toegang tot Springer koppeling heeft.</span><span class="sxs-lookup"><span data-stu-id="e68e4-106">You can control in Azure AD who has access to Springer Link.</span></span>
- <span data-ttu-id="e68e4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Springer-koppeling (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="e68e4-107">You can enable your users to automatically get signed-on to Springer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e68e4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="e68e4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e68e4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e68e4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e68e4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e68e4-110">Prerequisites</span></span>

<span data-ttu-id="e68e4-111">Voor het configureren van Azure AD-integratie met Springer koppeling, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e68e4-111">To configure Azure AD integration with Springer Link, you need the following items:</span></span>

- <span data-ttu-id="e68e4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e68e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e68e4-113">Een koppeling Springer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e68e4-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e68e4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e68e4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e68e4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e68e4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e68e4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e68e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e68e4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e68e4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e68e4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e68e4-118">Scenario description</span></span>
<span data-ttu-id="e68e4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e68e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e68e4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e68e4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e68e4-121">Springer koppeling toe te voegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="e68e4-121">Adding Springer Link from the gallery</span></span>
2. <span data-ttu-id="e68e4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e68e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-the-gallery"></a><span data-ttu-id="e68e4-123">Springer koppeling toe te voegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="e68e4-123">Adding Springer Link from the gallery</span></span>
<span data-ttu-id="e68e4-124">Voor het configureren van de integratie van Springer koppeling in Azure AD, moet u Springer koppeling uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e68e4-124">To configure the integration of Springer Link into Azure AD, you need to add Springer Link from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e68e4-125">**U kunt Springer koppeling uit de galerie toevoegen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e68e4-125">**To add Springer Link from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e68e4-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e68e4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="e68e4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e68e4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="e68e4-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e68e4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="e68e4-133">Typ in het zoekvak **Springer koppeling**, selecteer **Springer koppeling** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e68e4-133">In the search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button to add the application.</span></span>

    ![Springer koppeling in de lijst met resultaten](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e68e4-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="e68e4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e68e4-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Springer-koppeling die overeenkomt met een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e68e4-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e68e4-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Springer koppeling is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e68e4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Springer Link is to a user in Azure AD.</span></span> <span data-ttu-id="e68e4-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Springer koppeling tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e68e4-138">In other words, a link relationship between an Azure AD user and the related user in Springer Link needs to be established.</span></span>

<span data-ttu-id="e68e4-139">In de koppeling Springer, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="e68e4-139">In Springer Link, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e68e4-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Springer koppeling, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e68e4-140">To configure and test Azure AD single sign-on with Springer Link, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e68e4-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e68e4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e68e4-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e68e4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e68e4-143">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e68e4-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="e68e4-144">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e68e4-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e68e4-145">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e68e4-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e68e4-146">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Springer koppeling.</span><span class="sxs-lookup"><span data-stu-id="e68e4-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="e68e4-147">**Voor het configureren van Azure AD eenmalige aanmelding met Springer koppeling, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e68e4-147">**To configure Azure AD single sign-on with Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="e68e4-148">In de Azure-portal op de **Springer koppeling** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-148">In the Azure portal, on the **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e68e4-150">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e68e4-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="e68e4-152">Op de **Springer koppeling domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="e68e4-152">On the **Springer Link Domain and URLs** section,  If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![URL's en Springer koppeling domein eenmalige aanmelding informatie](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="e68e4-154">a.</span><span class="sxs-lookup"><span data-stu-id="e68e4-154">a.</span></span> <span data-ttu-id="e68e4-155">In de **id** textbox, typ de URL:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="e68e4-155">In the **Identifier** textbox, type the URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="e68e4-156">b.</span><span class="sxs-lookup"><span data-stu-id="e68e4-156">b.</span></span> <span data-ttu-id="e68e4-157">In de **antwoord-URL** textbox, typ de URL:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="e68e4-157">In the **Reply URL** textbox, type the URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="e68e4-158">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="e68e4-159">Als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="e68e4-159">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![URL's en Springer koppeling domein eenmalige aanmelding informatie](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="e68e4-161">In de **aanmeldings-URL** textbox, typ de URL:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="e68e4-161">In the **Sign-on URL** textbox, type the URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="e68e4-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e68e4-162">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e68e4-164">Voor het genereren van de **metagegevens** -url, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e68e4-164">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="e68e4-165">a.</span><span class="sxs-lookup"><span data-stu-id="e68e4-165">a.</span></span> <span data-ttu-id="e68e4-166">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-166">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="e68e4-168">b.</span><span class="sxs-lookup"><span data-stu-id="e68e4-168">b.</span></span> <span data-ttu-id="e68e4-169">Klik op **eindpunten** openen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e68e4-169">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="e68e4-171">c.</span><span class="sxs-lookup"><span data-stu-id="e68e4-171">c.</span></span> <span data-ttu-id="e68e4-172">Klik op de knop kopiëren om te kopiëren **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="e68e4-172">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="e68e4-174">d.</span><span class="sxs-lookup"><span data-stu-id="e68e4-174">d.</span></span> <span data-ttu-id="e68e4-175">Nu gaat u naar de eigenschappenpagina van **Springer koppeling** en kopieer de **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="e68e4-175">Now go to the property page of **Springer Link** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="e68e4-177">e.</span><span class="sxs-lookup"><span data-stu-id="e68e4-177">e.</span></span> <span data-ttu-id="e68e4-178">Genereren van de **metagegevens-URL** met het volgende patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="e68e4-178">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="e68e4-179">Eenmalige aanmelding configureren op **Springer koppeling** zijde, moet u de gegenereerde verzenden **metagegevens-URL** naar [Springer koppeling ondersteuningsteam](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="e68e4-179">To configure single sign-on on **Springer Link** side, you need to send the generated **Metadata URL** to [Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="e68e4-180">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e68e4-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e68e4-181">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e68e4-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e68e4-182">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e68e4-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e68e4-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e68e4-183">Create an Azure AD test user</span></span>

<span data-ttu-id="e68e4-184">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e68e4-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="e68e4-186">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e68e4-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e68e4-187">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="e68e4-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e68e4-189">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e68e4-191">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e68e4-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e68e4-193">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e68e4-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e68e4-195">a.</span><span class="sxs-lookup"><span data-stu-id="e68e4-195">a.</span></span> <span data-ttu-id="e68e4-196">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e68e4-197">b.</span><span class="sxs-lookup"><span data-stu-id="e68e4-197">b.</span></span> <span data-ttu-id="e68e4-198">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e68e4-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e68e4-199">c.</span><span class="sxs-lookup"><span data-stu-id="e68e4-199">c.</span></span> <span data-ttu-id="e68e4-200">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="e68e4-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e68e4-201">d.</span><span class="sxs-lookup"><span data-stu-id="e68e4-201">d.</span></span> <span data-ttu-id="e68e4-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-202">Click **Create**.</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e68e4-203">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="e68e4-203">Assign the Azure AD test user</span></span>

<span data-ttu-id="e68e4-204">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Springer koppeling.</span><span class="sxs-lookup"><span data-stu-id="e68e4-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Springer Link.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="e68e4-206">**Britta Simon om aan te wijzen Springer koppeling, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e68e4-206">**To assign Britta Simon to Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="e68e4-207">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e68e4-209">Selecteer in de lijst met toepassingen **Springer koppeling**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-209">In the applications list, select **Springer Link**.</span></span>

    ![De koppeling Springer koppeling in de lijst met toepassingen](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="e68e4-211">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e68e4-211">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="e68e4-213">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e68e4-213">Click **Add** button.</span></span> <span data-ttu-id="e68e4-214">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e68e4-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="e68e4-216">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e68e4-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e68e4-217">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e68e4-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e68e4-218">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e68e4-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e68e4-219">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e68e4-219">Test single sign-on</span></span>

<span data-ttu-id="e68e4-220">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e68e4-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e68e4-221">Als u op de tegel Springer koppeling in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Springer koppeling.</span><span class="sxs-lookup"><span data-stu-id="e68e4-221">When you click the Springer Link tile in the Access Panel, you should get automatically signed-on to your Springer Link application.</span></span>
<span data-ttu-id="e68e4-222">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e68e4-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e68e4-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e68e4-223">Additional resources</span></span>

* [<span data-ttu-id="e68e4-224">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e68e4-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e68e4-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e68e4-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

