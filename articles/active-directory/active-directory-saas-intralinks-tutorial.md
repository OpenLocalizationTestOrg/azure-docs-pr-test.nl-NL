---
title: 'Zelfstudie: Azure Active Directory-integratie met Intralinks | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Intralinks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="50901-103">Zelfstudie: Azure Active Directory-integratie met Intralinks</span><span class="sxs-lookup"><span data-stu-id="50901-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="50901-104">In deze zelfstudie leert u hoe Intralinks integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50901-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50901-105">Intralinks integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="50901-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="50901-106">U kunt beheren in Azure AD die toegang tot Intralinks heeft</span><span class="sxs-lookup"><span data-stu-id="50901-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="50901-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Intralinks (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="50901-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="50901-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="50901-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="50901-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50901-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50901-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="50901-110">Prerequisites</span></span>

<span data-ttu-id="50901-111">Voor het configureren van Azure AD-integratie met Intralinks, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="50901-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="50901-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="50901-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50901-113">Een Intralinks eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="50901-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50901-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="50901-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50901-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="50901-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50901-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="50901-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50901-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50901-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50901-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="50901-118">Scenario description</span></span>
<span data-ttu-id="50901-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="50901-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50901-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="50901-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50901-121">Intralinks uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="50901-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="50901-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="50901-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="50901-123">Intralinks uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="50901-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="50901-124">Voor het configureren van de integratie van Intralinks in Azure AD, moet u Intralinks uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="50901-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50901-125">**Als u wilt toevoegen Intralinks uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50901-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50901-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="50901-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="50901-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50901-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50901-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50901-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="50901-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50901-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="50901-133">Typ in het zoekvak **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="50901-133">In the search box, type **Intralinks**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="50901-135">Selecteer in het deelvenster resultaten **Intralinks**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="50901-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="50901-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="50901-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="50901-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Intralinks op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="50901-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50901-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Intralinks is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50901-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="50901-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Intralinks tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="50901-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="50901-141">Wijs in Intralinks, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="50901-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="50901-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Intralinks, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="50901-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50901-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50901-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="50901-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50901-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50901-145">**[Maken van een testgebruiker Intralinks](#creating-an-intralinks-test-user)**  - Intralinks die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="50901-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="50901-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="50901-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50901-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="50901-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="50901-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="50901-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="50901-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Intralinks configureren.</span><span class="sxs-lookup"><span data-stu-id="50901-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="50901-150">**Voor het configureren van Azure AD eenmalige aanmelding met Intralinks, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50901-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="50901-151">In de Azure-portal op de **Intralinks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="50901-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="50901-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="50901-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="50901-155">Op de **Intralinks domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="50901-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="50901-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="50901-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="50901-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="50901-158">This value is not real.</span></span> <span data-ttu-id="50901-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="50901-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="50901-160">Neem contact op met [Intralinks Client ondersteuningsteam](https://www.intralinks.com/contact-1) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="50901-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="50901-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="50901-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="50901-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="50901-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="50901-165">Eenmalige aanmelding configureren op **Intralinks** zijde, moet u de gedownloade verzenden **Metadata XML** [Intralinks ondersteuningsteam](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="50901-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="50901-166">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="50901-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="50901-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="50901-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="50901-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="50901-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="50901-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50901-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="50901-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="50901-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="50901-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="50901-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="50901-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50901-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50901-174">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="50901-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="50901-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="50901-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="50901-178">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50901-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="50901-180">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="50901-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="50901-182">a.</span><span class="sxs-lookup"><span data-stu-id="50901-182">a.</span></span> <span data-ttu-id="50901-183">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50901-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50901-184">b.</span><span class="sxs-lookup"><span data-stu-id="50901-184">b.</span></span> <span data-ttu-id="50901-185">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="50901-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="50901-186">c.</span><span class="sxs-lookup"><span data-stu-id="50901-186">c.</span></span> <span data-ttu-id="50901-187">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="50901-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="50901-188">d.</span><span class="sxs-lookup"><span data-stu-id="50901-188">d.</span></span> <span data-ttu-id="50901-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="50901-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="50901-190">Een testgebruiker Intralinks maken</span><span class="sxs-lookup"><span data-stu-id="50901-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="50901-191">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Intralinks maken.</span><span class="sxs-lookup"><span data-stu-id="50901-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="50901-192">Neem contact op met [Intralinks ondersteuningsteam](https://www.intralinks.com/contact-1) de gebruikers van het platform Intralinks toevoegen.</span><span class="sxs-lookup"><span data-stu-id="50901-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="50901-193">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="50901-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="50901-194">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Intralinks.</span><span class="sxs-lookup"><span data-stu-id="50901-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="50901-196">**Britta Simon om aan te wijzen Intralinks, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50901-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="50901-197">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50901-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="50901-199">Selecteer in de lijst met toepassingen **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="50901-199">In the applications list, select **Intralinks**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="50901-201">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="50901-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="50901-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="50901-203">Click **Add** button.</span></span> <span data-ttu-id="50901-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50901-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="50901-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="50901-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="50901-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50901-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50901-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50901-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="50901-209">Intralinks VIA of Elite toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="50901-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="50901-210">Intralinks gebruikt hetzelfde SSO identiteitsplatform voor alle andere Intralinks toepassingen met uitzondering van de Deal Nexus toepassing.</span><span class="sxs-lookup"><span data-stu-id="50901-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="50901-211">Dus als u van plan bent gebruik van andere Intralinks-toepassing hebt eerst u eenmalige aanmelding configureren voor één primaire Intralinks toepassing met de procedure die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="50901-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="50901-212">Daarna kunt u de onderstaande procedure voor het toevoegen van een andere Intralinks toepassing in uw tenant die u van deze primaire toepassing voor eenmalige aanmelding gebruikmaken kunt.</span><span class="sxs-lookup"><span data-stu-id="50901-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="50901-213">Deze functie is alleen beschikbaar voor Azure AD Premium-SKU-klanten en niet beschikbaar voor klanten Free of basis-SKU.</span><span class="sxs-lookup"><span data-stu-id="50901-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="50901-214">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="50901-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="50901-216">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50901-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50901-217">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50901-217">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="50901-219">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50901-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="50901-221">Typ in het zoekvak **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="50901-221">In the search box, type **Intralinks**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="50901-223">Op **app Intralinks toevoegen** de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="50901-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Intralinks VIA of Elite toepassing toe te voegen](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="50901-225">a.</span><span class="sxs-lookup"><span data-stu-id="50901-225">a.</span></span> <span data-ttu-id="50901-226">In **naam** textbox geschikte naam van de toepassing bijvoorbeeld Voer **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="50901-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="50901-227">b.</span><span class="sxs-lookup"><span data-stu-id="50901-227">b.</span></span> <span data-ttu-id="50901-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="50901-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="50901-229">In de Azure-portal op de **Intralinks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="50901-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

7. <span data-ttu-id="50901-231">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **gekoppelde aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="50901-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="50901-233">Ophalen van de SP geïnitieerd SSO-URL van [Intralinks team](https://www.intralinks.com/contact-1) voor de andere Intralinks-toepassing en voer deze in **configureren aanmeldings-URL** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50901-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="50901-235">Typ in het tekstvak voor aanmelding op URL de URL die wordt gebruikt door uw gebruikers eenmalige aanmelding voor uw toepassing Intralinks is met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="50901-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="50901-236">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="50901-236">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="50901-238">De toepassing toewijzen aan gebruikers of groepen zoals weergegeven in de sectie  **[toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="50901-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="50901-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="50901-239">Testing single sign-on</span></span>

<span data-ttu-id="50901-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="50901-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="50901-241">Als u op de tegel Intralinks in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Intralinks.</span><span class="sxs-lookup"><span data-stu-id="50901-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="50901-242">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50901-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50901-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="50901-243">Additional resources</span></span>

* [<span data-ttu-id="50901-244">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50901-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50901-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50901-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

