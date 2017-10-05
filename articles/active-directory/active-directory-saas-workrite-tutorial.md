---
title: 'Zelfstudie: Azure Active Directory-integratie met Workrite | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Workrite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4358c4c621634c17cbbd7fa1c72f12746b8e4a2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="b6d48-103">Zelfstudie: Azure Active Directory-integratie met Workrite</span><span class="sxs-lookup"><span data-stu-id="b6d48-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="b6d48-104">In deze zelfstudie leert u hoe Workrite integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6d48-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6d48-105">Workrite integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b6d48-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6d48-106">U kunt beheren in Azure AD die toegang tot Workrite heeft.</span><span class="sxs-lookup"><span data-stu-id="b6d48-106">You can control in Azure AD who has access to Workrite.</span></span>
- <span data-ttu-id="b6d48-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Workrite (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b6d48-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b6d48-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="b6d48-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b6d48-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6d48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6d48-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b6d48-110">Prerequisites</span></span>

<span data-ttu-id="b6d48-111">Voor het configureren van Azure AD-integratie met Workrite, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b6d48-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

- <span data-ttu-id="b6d48-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b6d48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6d48-113">Een Workrite eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b6d48-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6d48-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b6d48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6d48-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b6d48-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6d48-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b6d48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6d48-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6d48-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6d48-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b6d48-118">Scenario description</span></span>
<span data-ttu-id="b6d48-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b6d48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6d48-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b6d48-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6d48-121">Workrite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b6d48-121">Adding Workrite from the gallery</span></span>
2. <span data-ttu-id="b6d48-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b6d48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="b6d48-123">Workrite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b6d48-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="b6d48-124">Voor het configureren van de integratie van Workrite in Azure AD, moet u Workrite uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b6d48-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6d48-125">**Als u wilt toevoegen Workrite uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6d48-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6d48-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b6d48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="b6d48-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6d48-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="b6d48-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b6d48-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="b6d48-133">Typ in het zoekvak **Workrite**, selecteer **Workrite** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b6d48-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span></span>

    ![Workrite in de lijst met resultaten](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b6d48-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6d48-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b6d48-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Workrite op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b6d48-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b6d48-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Workrite is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6d48-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span></span> <span data-ttu-id="b6d48-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Workrite tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b6d48-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>

<span data-ttu-id="b6d48-139">Wijs in Workrite, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b6d48-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6d48-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Workrite, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b6d48-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6d48-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b6d48-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6d48-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6d48-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6d48-143">**[Maak een testgebruiker Workrite](#create-a-workrite-test-user)**  - Workrite die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b6d48-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6d48-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b6d48-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6d48-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b6d48-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b6d48-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b6d48-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b6d48-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Workrite configureren.</span><span class="sxs-lookup"><span data-stu-id="b6d48-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="b6d48-148">**Voor het configureren van Azure AD eenmalige aanmelding met Workrite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6d48-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="b6d48-149">In de Azure-portal op de **Workrite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b6d48-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b6d48-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="b6d48-153">Op de **Workrite domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b6d48-153">On the **Workrite Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en Workrite domein eenmalige aanmelding informatie](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="b6d48-155">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="b6d48-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6d48-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="b6d48-156">This value is not real.</span></span> <span data-ttu-id="b6d48-157">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b6d48-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b6d48-158">Neem contact op met [Workrite Client ondersteuningsteam](mailto:support@workrite.co.uk) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="b6d48-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span></span>

4. <span data-ttu-id="b6d48-159">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b6d48-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="b6d48-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b6d48-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b6d48-163">Op de **Workrite configuratie** sectie, klikt u op **configureren Workrite** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b6d48-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b6d48-164">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b6d48-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Workrite configuratie](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="b6d48-166">Eenmalige aanmelding configureren op **Workrite** zijde, moet u de gedownloade verzenden **Certificate(Base64), Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [Workrite ondersteuningsteam](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="b6d48-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="b6d48-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b6d48-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6d48-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b6d48-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6d48-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b6d48-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b6d48-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b6d48-170">Create an Azure AD test user</span></span>

<span data-ttu-id="b6d48-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b6d48-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b6d48-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6d48-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6d48-174">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="b6d48-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b6d48-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b6d48-178">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b6d48-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b6d48-180">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b6d48-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b6d48-182">a.</span><span class="sxs-lookup"><span data-stu-id="b6d48-182">a.</span></span> <span data-ttu-id="b6d48-183">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6d48-184">b.</span><span class="sxs-lookup"><span data-stu-id="b6d48-184">b.</span></span> <span data-ttu-id="b6d48-185">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6d48-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b6d48-186">c.</span><span class="sxs-lookup"><span data-stu-id="b6d48-186">c.</span></span> <span data-ttu-id="b6d48-187">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="b6d48-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b6d48-188">d.</span><span class="sxs-lookup"><span data-stu-id="b6d48-188">d.</span></span> <span data-ttu-id="b6d48-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="b6d48-190">Een testgebruiker Workrite maken</span><span class="sxs-lookup"><span data-stu-id="b6d48-190">Create a Workrite test user</span></span>

<span data-ttu-id="b6d48-191">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Workrite genoemd.</span><span class="sxs-lookup"><span data-stu-id="b6d48-191">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="b6d48-192">**Als u wilt een gebruiker Britta Simon aangeroepen in Workrite maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6d48-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="b6d48-193">Meld u op met uw bedrijf workrite site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b6d48-193">Sign on to your workrite company site as administrator.</span></span>

2. <span data-ttu-id="b6d48-194">Klik in het navigatievenster op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-194">In the navigation pane, click **Admin**.</span></span>
   
    ![Controle van de beheerder][400]

3. <span data-ttu-id="b6d48-196">Ga naar snelkoppelingen en klik vervolgens op **maken van een gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-196">Go to Quick Links, and then click **Create a User**.</span></span>
   
    ![Sectie van de gebruiker maken][401]

4. <span data-ttu-id="b6d48-198">Op de **gebruiker maken** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b6d48-198">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Gebruiker Dailog maken][402]
    
    <span data-ttu-id="b6d48-200">a.</span><span class="sxs-lookup"><span data-stu-id="b6d48-200">a.</span></span> <span data-ttu-id="b6d48-201">In de **e** textbox, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b6d48-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="b6d48-202">b.</span><span class="sxs-lookup"><span data-stu-id="b6d48-202">b.</span></span> <span data-ttu-id="b6d48-203">In de **voornaam** textbox, typt u de voornaam van de gebruiker zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="b6d48-203">In the **First Name** textbox, type the firstname of user like Britta.</span></span>

    <span data-ttu-id="b6d48-204">c.</span><span class="sxs-lookup"><span data-stu-id="b6d48-204">c.</span></span> <span data-ttu-id="b6d48-205">In de **achternaam** textbox, typt u de achternaam van de gebruiker zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="b6d48-205">In the **Surname** textbox, type the surname of user like Simon.</span></span>
    
    <span data-ttu-id="b6d48-206">d.</span><span class="sxs-lookup"><span data-stu-id="b6d48-206">d.</span></span> <span data-ttu-id="b6d48-207">Selecteer **Client Administrator** als **Kies rol**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="b6d48-208">e.</span><span class="sxs-lookup"><span data-stu-id="b6d48-208">e.</span></span> <span data-ttu-id="b6d48-209">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-209">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b6d48-210">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="b6d48-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="b6d48-211">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Workrite.</span><span class="sxs-lookup"><span data-stu-id="b6d48-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="b6d48-213">**Britta Simon om aan te wijzen Workrite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6d48-213">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="b6d48-214">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b6d48-216">Selecteer in de lijst met toepassingen **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-216">In the applications list, select **Workrite**.</span></span>

    ![De koppeling Workrite in de lijst met toepassingen](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="b6d48-218">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b6d48-218">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="b6d48-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b6d48-220">Click **Add** button.</span></span> <span data-ttu-id="b6d48-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b6d48-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="b6d48-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b6d48-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6d48-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b6d48-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6d48-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b6d48-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b6d48-226">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b6d48-226">Test single sign-on</span></span>

<span data-ttu-id="b6d48-227">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b6d48-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b6d48-228">Als u op de tegel Workrite in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Workrite.</span><span class="sxs-lookup"><span data-stu-id="b6d48-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6d48-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b6d48-229">Additional resources</span></span>

* [<span data-ttu-id="b6d48-230">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6d48-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6d48-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6d48-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

