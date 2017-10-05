---
title: 'Zelfstudie: Azure Active Directory-integratie met Evernote | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Evernote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="a61ce-103">Zelfstudie: Azure Active Directory-integratie met Evernote</span><span class="sxs-lookup"><span data-stu-id="a61ce-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="a61ce-104">In deze zelfstudie leert u hoe Evernote integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a61ce-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a61ce-105">Evernote integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a61ce-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a61ce-106">U kunt beheren in Azure AD die toegang tot Evernote heeft.</span><span class="sxs-lookup"><span data-stu-id="a61ce-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="a61ce-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Evernote (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a61ce-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a61ce-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="a61ce-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a61ce-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a61ce-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a61ce-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a61ce-110">Prerequisites</span></span>

<span data-ttu-id="a61ce-111">Voor het configureren van Azure AD-integratie met Evernote, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a61ce-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="a61ce-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a61ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a61ce-113">Een Evernote eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a61ce-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a61ce-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a61ce-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a61ce-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a61ce-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a61ce-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a61ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a61ce-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a61ce-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a61ce-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a61ce-118">Scenario description</span></span>
<span data-ttu-id="a61ce-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a61ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a61ce-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a61ce-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a61ce-121">Evernote uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a61ce-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="a61ce-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a61ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="a61ce-123">Evernote uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a61ce-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="a61ce-124">Voor het configureren van de integratie van Evernote in Azure AD, moet u Evernote uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a61ce-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a61ce-125">**Als u wilt toevoegen Evernote uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a61ce-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a61ce-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a61ce-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="a61ce-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a61ce-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="a61ce-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a61ce-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="a61ce-133">Typ in het zoekvak **Evernote**, selecteer **Evernote** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a61ce-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Evernote in de lijst met resultaten](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a61ce-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="a61ce-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a61ce-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Evernote op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a61ce-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a61ce-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Evernote is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a61ce-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="a61ce-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Evernote tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a61ce-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="a61ce-139">Wijs in Evernote, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a61ce-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a61ce-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Evernote, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a61ce-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a61ce-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a61ce-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a61ce-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a61ce-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a61ce-143">**[Maken van een testgebruiker Evernote](#create-an-evernote-test-user)**  - Evernote die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="a61ce-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a61ce-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a61ce-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a61ce-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a61ce-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a61ce-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a61ce-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a61ce-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Evernote configureren.</span><span class="sxs-lookup"><span data-stu-id="a61ce-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="a61ce-148">**Voor het configureren van Azure AD eenmalige aanmelding met Evernote, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a61ce-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="a61ce-149">In de Azure-portal op de **Evernote** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a61ce-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a61ce-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="a61ce-153">Op de **Evernote domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren van de toepassing in de IDP geïnitieerd modus:</span><span class="sxs-lookup"><span data-stu-id="a61ce-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![URL's en Evernote domein eenmalige aanmelding informatie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="a61ce-155">In de **id** textbox, typ de URL:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="a61ce-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="a61ce-156">Controleer **weergeven geavanceerde instellingen voor URL** en voer de volgende stap als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="a61ce-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![URL's en Evernote domein eenmalige aanmelding informatie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="a61ce-158">In de **aanmelden URL** textbox, typ de URL:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="a61ce-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="a61ce-159">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a61ce-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="a61ce-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a61ce-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a61ce-163">Op de **Evernote configuratie** sectie, klikt u op **configureren Evernote** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a61ce-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a61ce-164">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a61ce-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evernote configuratie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="a61ce-166">In een ander browservenster, meld u bij uw bedrijf Evernote site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a61ce-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="a61ce-167">Ga naar **Admin-Console**</span><span class="sxs-lookup"><span data-stu-id="a61ce-167">Go to **'Admin Console'**</span></span>

    ![-Beheerconsole](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="a61ce-169">Van de **Admin-Console**, gaat u naar **'Security'** en selecteer **' Single Sign-On'**</span><span class="sxs-lookup"><span data-stu-id="a61ce-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-instelling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="a61ce-171">Configureer de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="a61ce-171">Configure the following values:</span></span>

    ![Certificaat-instelling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="a61ce-173">a.</span><span class="sxs-lookup"><span data-stu-id="a61ce-173">a.</span></span>  <span data-ttu-id="a61ce-174">**Eenmalige aanmelding inschakelen:** eenmalige aanmelding is standaard ingeschakeld (Klik op **uitschakelen Single Sign-on** verwijderen van de vereiste SSO)</span><span class="sxs-lookup"><span data-stu-id="a61ce-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="a61ce-175">b.</span><span class="sxs-lookup"><span data-stu-id="a61ce-175">b.</span></span> <span data-ttu-id="a61ce-176">Plakken **SAML eenmalige aanmelding Service-URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **SAML HTTP-verzoek-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a61ce-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="a61ce-177">c.</span><span class="sxs-lookup"><span data-stu-id="a61ce-177">c.</span></span> <span data-ttu-id="a61ce-178">Het gedownloade certificaat openen vanuit Azure AD in Kladblok en kopieer de inhoud, met inbegrip van 'BEGIN CERTIFICATE' en 'END CERTIFICATE' en plak deze in de **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="a61ce-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="a61ce-179">d.Click **wijzigingen opslaan**</span><span class="sxs-lookup"><span data-stu-id="a61ce-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="a61ce-180">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a61ce-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a61ce-181">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a61ce-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a61ce-182">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a61ce-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a61ce-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a61ce-183">Create an Azure AD test user</span></span>

<span data-ttu-id="a61ce-184">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a61ce-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="a61ce-186">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a61ce-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a61ce-187">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="a61ce-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a61ce-189">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a61ce-191">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a61ce-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a61ce-193">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a61ce-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a61ce-195">a.</span><span class="sxs-lookup"><span data-stu-id="a61ce-195">a.</span></span> <span data-ttu-id="a61ce-196">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a61ce-197">b.</span><span class="sxs-lookup"><span data-stu-id="a61ce-197">b.</span></span> <span data-ttu-id="a61ce-198">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a61ce-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a61ce-199">c.</span><span class="sxs-lookup"><span data-stu-id="a61ce-199">c.</span></span> <span data-ttu-id="a61ce-200">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="a61ce-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a61ce-201">d.</span><span class="sxs-lookup"><span data-stu-id="a61ce-201">d.</span></span> <span data-ttu-id="a61ce-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="a61ce-203">Een testgebruiker Evernote maken</span><span class="sxs-lookup"><span data-stu-id="a61ce-203">Create an Evernote test user</span></span>

<span data-ttu-id="a61ce-204">Om in te schakelen gebruikers van Azure AD aan te melden bij Evernote, moeten ze worden ingericht in Evernote.</span><span class="sxs-lookup"><span data-stu-id="a61ce-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="a61ce-205">In het geval van Evernote is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a61ce-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="a61ce-206">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a61ce-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="a61ce-207">Meld u aan bij uw bedrijf Evernote site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a61ce-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="a61ce-208">Klik op de **Admin-Console**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-208">Click the **'Admin Console'**.</span></span>

    ![-Beheerconsole](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="a61ce-210">Van de **Admin-Console**, gaat u naar **toevoegen van gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Voeg testgebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="a61ce-212">**Teamleden toevoegen** in de **e** textbox, typ het e-mailadres van gebruikersaccount en klik op **uit te nodigen.**</span><span class="sxs-lookup"><span data-stu-id="a61ce-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Voeg testgebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="a61ce-214">Nadat de uitnodiging is verzonden, ontvangt de houder van Azure Active Directory-account een e-mail met de uitnodiging accepteren.</span><span class="sxs-lookup"><span data-stu-id="a61ce-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a61ce-215">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="a61ce-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="a61ce-216">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Evernote.</span><span class="sxs-lookup"><span data-stu-id="a61ce-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="a61ce-218">**Britta Simon om aan te wijzen Evernote, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a61ce-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="a61ce-219">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a61ce-221">Selecteer in de lijst met toepassingen **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-221">In the applications list, select **Evernote**.</span></span>

    ![De koppeling Evernote in de lijst met toepassingen](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="a61ce-223">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a61ce-223">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="a61ce-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a61ce-225">Click **Add** button.</span></span> <span data-ttu-id="a61ce-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a61ce-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="a61ce-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a61ce-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a61ce-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a61ce-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a61ce-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a61ce-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a61ce-231">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a61ce-231">Test single sign-on</span></span>

<span data-ttu-id="a61ce-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a61ce-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a61ce-233">Als u op de tegel Evernote in het deelvenster toegang, u moet ophalen aangemeld bij uw toepassing Evernote.</span><span class="sxs-lookup"><span data-stu-id="a61ce-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="a61ce-234">U zult logboekregistratie in als een organisatie account maar moet zich aanmelden met uw persoonlijke account.</span><span class="sxs-lookup"><span data-stu-id="a61ce-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a61ce-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a61ce-235">Additional resources</span></span>

* [<span data-ttu-id="a61ce-236">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a61ce-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a61ce-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a61ce-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

