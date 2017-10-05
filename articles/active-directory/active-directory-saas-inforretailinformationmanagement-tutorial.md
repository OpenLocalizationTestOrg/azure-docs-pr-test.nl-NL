---
title: "Zelfstudie: Azure Active Directory-integratie met informatie Retail – informatiebeheer | Microsoft Docs"
description: "Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en informatie Retail – informatiebeheer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 1ab8b7e98324ba4f4ae95775f89df0461058fe4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="26ba0-103">Zelfstudie: Azure Active Directory-integratie met informatie Retail – informatiebeheer</span><span class="sxs-lookup"><span data-stu-id="26ba0-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="26ba0-104">In deze zelfstudie leert u het integreren van informatie Retail – informatiebeheer met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26ba0-104">In this tutorial, you learn how to integrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26ba0-105">Integratie van informatie Retail – informatiebeheer met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="26ba0-105">Integrating Infor Retail – Information Management with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26ba0-106">U kunt beheren in Azure AD die toegang tot informatie Retail – informatiebeheer heeft.</span><span class="sxs-lookup"><span data-stu-id="26ba0-106">You can control in Azure AD who has access to Infor Retail – Information Management.</span></span>
- <span data-ttu-id="26ba0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij informatie Retail – informatiebeheer (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="26ba0-107">You can enable your users to automatically get signed-on to Infor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="26ba0-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="26ba0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="26ba0-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26ba0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26ba0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="26ba0-110">Prerequisites</span></span>

<span data-ttu-id="26ba0-111">Voor het configureren van Azure AD-integratie met informatie Retail – informatiebeheer, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="26ba0-111">To configure Azure AD integration with Infor Retail – Information Management, you need the following items:</span></span>

- <span data-ttu-id="26ba0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="26ba0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26ba0-113">Een handelsversie informatie – informatiebeheer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="26ba0-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26ba0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="26ba0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26ba0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="26ba0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26ba0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="26ba0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26ba0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26ba0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26ba0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="26ba0-118">Scenario description</span></span>
<span data-ttu-id="26ba0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="26ba0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26ba0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="26ba0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26ba0-121">Informatie Retail – informatiebeheer uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="26ba0-121">Adding Infor Retail – Information Management from the gallery</span></span>
2. <span data-ttu-id="26ba0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="26ba0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-the-gallery"></a><span data-ttu-id="26ba0-123">Informatie Retail – informatiebeheer uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="26ba0-123">Adding Infor Retail – Information Management from the gallery</span></span>
<span data-ttu-id="26ba0-124">Voor het configureren van de integratie van informatie Retail – Information Management in Azure AD, moet u informatie Retail – informatiebeheer aan de lijst met beheerde SaaS-apps uit de galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="26ba0-124">To configure the integration of Infor Retail – Information Management into Azure AD, you need to add Infor Retail – Information Management from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26ba0-125">**Als u wilt toevoegen, informatie Retail – informatiebeheer uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="26ba0-125">**To add Infor Retail – Information Management from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26ba0-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="26ba0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="26ba0-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26ba0-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="26ba0-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="26ba0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="26ba0-133">Typ in het zoekvak **informatie Retail – informatiebeheer**, selecteer **informatie Retail – informatiebeheer** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen de de toepassing.</span><span class="sxs-lookup"><span data-stu-id="26ba0-133">In the search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button to add the application.</span></span>

    ![Informatie Retail: beheer van de informatie in de lijst met resultaten](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="26ba0-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="26ba0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="26ba0-136">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met informatie Retail – informatiebeheer op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="26ba0-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26ba0-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de detailhandel informatie – Information Management in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="26ba0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Infor Retail – Information Management is to a user in Azure AD.</span></span> <span data-ttu-id="26ba0-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de detailhandel informatie – informatiebeheer tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="26ba0-138">In other words, a link relationship between an Azure AD user and the related user in Infor Retail – Information Management needs to be established.</span></span>

<span data-ttu-id="26ba0-139">In de detailhandel informatie – informatiebeheer, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="26ba0-139">In Infor Retail – Information Management, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="26ba0-140">Als u wilt configureren en testen Azure AD eenmalige aanmelding met informatie Retail – informatiebeheer, moet u voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="26ba0-140">To configure and test Azure AD single sign-on with Infor Retail – Information Management, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26ba0-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="26ba0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26ba0-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26ba0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26ba0-143">**[Maken van een handelsversie informatie – informatiebeheer testgebruiker](#create-an-infor-retail--information-management-test-user)**  - informatie Retail – informatiebeheer die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="26ba0-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - to have a counterpart of Britta Simon in Infor Retail – Information Management that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="26ba0-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="26ba0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26ba0-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="26ba0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="26ba0-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="26ba0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="26ba0-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in de detailhandel van uw informatie – informatie Management-toepassing.</span><span class="sxs-lookup"><span data-stu-id="26ba0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="26ba0-148">**Voor het configureren van Azure AD eenmalige aanmelding met informatie Retail – Information Management, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="26ba0-148">**To configure Azure AD single sign-on with Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="26ba0-149">In de Azure-portal op de **informatie Retail – informatiebeheer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-149">In the Azure portal, on the **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="26ba0-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="26ba0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="26ba0-153">Op de **informatie Retail-URL's en informatie beheerdomein** sectie, voert u de volgende stappen uit als u wilt configureren van de toepassing in de IDP geïnitieerd modus:</span><span class="sxs-lookup"><span data-stu-id="26ba0-153">On the **Infor Retail – Information Management Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Informatie Retail-URL's en informatie beheerdomein eenmalige aanmelding informatie IDP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="26ba0-155">a.</span><span class="sxs-lookup"><span data-stu-id="26ba0-155">a.</span></span> <span data-ttu-id="26ba0-156">In de **id** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="26ba0-156">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="26ba0-157">b.</span><span class="sxs-lookup"><span data-stu-id="26ba0-157">b.</span></span> <span data-ttu-id="26ba0-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="26ba0-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="26ba0-159">Controleer **weergeven geavanceerde instellingen voor URL** en voer de volgende stap als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="26ba0-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informatie Retail – informatie beheerdomein en URL's eenmalige aanmelding informatie SP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="26ba0-161">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="26ba0-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="26ba0-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="26ba0-162">These values are not real.</span></span> <span data-ttu-id="26ba0-163">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="26ba0-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="26ba0-164">Neem contact op met [informatie Retail – informatie Beheerclient ondersteuningsteam](mailto:innovate@infor.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="26ba0-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) to get these values.</span></span> 

5. <span data-ttu-id="26ba0-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="26ba0-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="26ba0-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="26ba0-167">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="26ba0-169">Eenmalige aanmelding configureren op **informatie Retail – informatiebeheer** zijde, moet u de gedownloade verzenden **Metadata XML** naar [informatie Retail – informatiebeheer ondersteuningsteam](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="26ba0-169">To configure single sign-on on **Infor Retail – Information Management** side, you need to send the downloaded **Metadata XML** to [Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="26ba0-170">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="26ba0-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="26ba0-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="26ba0-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26ba0-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="26ba0-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26ba0-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26ba0-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="26ba0-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="26ba0-174">Create an Azure AD test user</span></span>

<span data-ttu-id="26ba0-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="26ba0-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="26ba0-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="26ba0-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26ba0-178">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="26ba0-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="26ba0-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="26ba0-182">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="26ba0-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="26ba0-184">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="26ba0-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="26ba0-186">a.</span><span class="sxs-lookup"><span data-stu-id="26ba0-186">a.</span></span> <span data-ttu-id="26ba0-187">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26ba0-188">b.</span><span class="sxs-lookup"><span data-stu-id="26ba0-188">b.</span></span> <span data-ttu-id="26ba0-189">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26ba0-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="26ba0-190">c.</span><span class="sxs-lookup"><span data-stu-id="26ba0-190">c.</span></span> <span data-ttu-id="26ba0-191">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="26ba0-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="26ba0-192">d.</span><span class="sxs-lookup"><span data-stu-id="26ba0-192">d.</span></span> <span data-ttu-id="26ba0-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="26ba0-194">Maken van een handelsversie informatie – informatiebeheer testgebruiker</span><span class="sxs-lookup"><span data-stu-id="26ba0-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="26ba0-195">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in de detailhandel informatie – informatiebeheer maken.</span><span class="sxs-lookup"><span data-stu-id="26ba0-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="26ba0-196">Neem contact op met [informatie Retail – informatiebeheer ondersteuningsteam](mailto:innovate@infor.com) toevoegen van de gebruikers in de detailhandel informatie – platform voor het beheer van informatie.</span><span class="sxs-lookup"><span data-stu-id="26ba0-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) to add the users in the Infor Retail – Information Management platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="26ba0-197">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="26ba0-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="26ba0-198">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan informatie Retail – informatiebeheer.</span><span class="sxs-lookup"><span data-stu-id="26ba0-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Infor Retail – Information Management.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="26ba0-200">**Britta Simon om aan te wijzen informatie Retail – Information Management, kunt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="26ba0-200">**To assign Britta Simon to Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="26ba0-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="26ba0-203">Selecteer in de lijst met toepassingen **informatie Retail – informatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-203">In the applications list, select **Infor Retail – Information Management**.</span></span>

    ![De informatie handelsversie – informatiebeheer koppeling in de lijst met toepassingen](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="26ba0-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="26ba0-205">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="26ba0-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="26ba0-207">Click **Add** button.</span></span> <span data-ttu-id="26ba0-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="26ba0-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="26ba0-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="26ba0-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26ba0-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="26ba0-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26ba0-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="26ba0-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="26ba0-213">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="26ba0-213">Test single sign-on</span></span>

<span data-ttu-id="26ba0-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="26ba0-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="26ba0-215">Wanneer u klikt op de informatie handelsversie – informatiebeheer tegel in het deelvenster toegang u moet ophalen automatisch aangemeld bij uw informatie Retail – informatie Management-toepassing.</span><span class="sxs-lookup"><span data-stu-id="26ba0-215">When you click the Infor Retail – Information Management tile in the Access Panel, you should get automatically signed-on to your Infor Retail – Information Management application.</span></span>
<span data-ttu-id="26ba0-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26ba0-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26ba0-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="26ba0-217">Additional resources</span></span>

* [<span data-ttu-id="26ba0-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26ba0-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26ba0-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26ba0-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png

