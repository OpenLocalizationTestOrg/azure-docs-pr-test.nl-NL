---
title: 'Zelfstudie: Azure Active Directory-integratie met HPE SaaS | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en HPE SaaS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 5e6f0da531df85359aa47477248dd020a039e7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="fd5ef-103">Zelfstudie: Azure Active Directory-integratie met HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="fd5ef-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="fd5ef-104">In deze zelfstudie leert u hoe HPE SaaS integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd5ef-104">In this tutorial, you learn how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd5ef-105">HPE SaaS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fd5ef-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fd5ef-106">U kunt beheren in Azure AD die toegang tot HPE SaaS heeft</span><span class="sxs-lookup"><span data-stu-id="fd5ef-106">You can control in Azure AD who has access to HPE SaaS</span></span>
- <span data-ttu-id="fd5ef-107">U kunt uw gebruikers automatisch ophalen aangemeld bij HPE SaaS (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="fd5ef-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd5ef-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fd5ef-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fd5ef-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd5ef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd5ef-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fd5ef-110">Prerequisites</span></span>

<span data-ttu-id="fd5ef-111">Voor het configureren van Azure AD-integratie met HPE SaaS, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="fd5ef-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span></span>

- <span data-ttu-id="fd5ef-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fd5ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fd5ef-113">Een HPE SaaS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fd5ef-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd5ef-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd5ef-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fd5ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd5ef-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd5ef-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd5ef-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd5ef-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fd5ef-118">Scenario description</span></span>
<span data-ttu-id="fd5ef-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd5ef-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fd5ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd5ef-121">HPE SaaS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fd5ef-121">Adding HPE SaaS from the gallery</span></span>
2. <span data-ttu-id="fd5ef-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fd5ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-the-gallery"></a><span data-ttu-id="fd5ef-123">HPE SaaS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fd5ef-123">Adding HPE SaaS from the gallery</span></span>
<span data-ttu-id="fd5ef-124">Voor het configureren van de integratie van HPE SaaS in Azure AD, moet u HPE SaaS uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fd5ef-125">**Als u wilt toevoegen HPE SaaS uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fd5ef-125">**To add HPE SaaS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fd5ef-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd5ef-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fd5ef-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="fd5ef-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="fd5ef-133">Typ in het zoekvak **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-133">In the search box, type **HPE SaaS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_search.png)

5. <span data-ttu-id="fd5ef-135">Selecteer in het deelvenster resultaten **HPE SaaS**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-135">In the results panel, select **HPE SaaS**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd5ef-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fd5ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd5ef-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met HPE SaaS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fd5ef-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in HPE SaaS is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS is to a user in Azure AD.</span></span> <span data-ttu-id="fd5ef-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante HPE SaaS-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-140">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span></span>

<span data-ttu-id="fd5ef-141">Wijs in HPE SaaS moet de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-141">In HPE SaaS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fd5ef-142">Om te configureren en testen van Azure AD eenmalige aanmelding met HPE SaaS, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="fd5ef-142">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fd5ef-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fd5ef-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd5ef-145">**[Maken van een testgebruiker HPE SaaS](#creating-an-hpe-saas-test-user)**  - HPE SaaS die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fd5ef-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd5ef-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd5ef-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fd5ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd5ef-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw HPE SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="fd5ef-150">**Om eenmalige aanmelding Azure AD met HPE SaaS configureert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fd5ef-150">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="fd5ef-151">In de Azure-portal op de **HPE SaaS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-151">In the Azure portal, on the **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fd5ef-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

3. <span data-ttu-id="fd5ef-155">Op de **HPE SaaS-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fd5ef-155">On the **HPE SaaS Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="fd5ef-157">a.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-157">a.</span></span> <span data-ttu-id="fd5ef-158">In de **aanmeldings-URL** textbox, typ een URL als:`https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="fd5ef-158">In the **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="fd5ef-159">b.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-159">b.</span></span> <span data-ttu-id="fd5ef-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="fd5ef-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fd5ef-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-161">These values are not real.</span></span> <span data-ttu-id="fd5ef-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fd5ef-163">Neem contact op met [HPE SaaS Client ondersteuningsteam](https://saas.hpe.com/en-us/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="fd5ef-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

5. <span data-ttu-id="fd5ef-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fd5ef-168">Eenmalige aanmelding configureren op **HPE SaaS** zijde, moet u de gedownloade verzenden **Metadata XML** naar [HPE SaaS ondersteuningsteam](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="fd5ef-168">To configure single sign-on on **HPE SaaS** side, you need to send the downloaded **Metadata XML** to [HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="fd5ef-169">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fd5ef-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="fd5ef-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fd5ef-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fd5ef-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fd5ef-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd5ef-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fd5ef-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="fd5ef-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fd5ef-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fd5ef-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fd5ef-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd5ef-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd5ef-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd5ef-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fd5ef-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd5ef-185">a.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-185">a.</span></span> <span data-ttu-id="fd5ef-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd5ef-187">b.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-187">b.</span></span> <span data-ttu-id="fd5ef-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fd5ef-189">c.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-189">c.</span></span> <span data-ttu-id="fd5ef-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fd5ef-191">d.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-191">d.</span></span> <span data-ttu-id="fd5ef-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="fd5ef-193">De gebruiker van een HPE SaaS-test maken</span><span class="sxs-lookup"><span data-stu-id="fd5ef-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="fd5ef-194">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-194">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="fd5ef-195">Neem contact op met [HPE SaaS ondersteuningsteam](https://saas.hpe.com/en-us/contact) de gebruikers in het HPE SaaS-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) to add the users in the HPE SaaS account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fd5ef-196">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd5ef-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fd5ef-197">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HPE SaaS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fd5ef-199">**Britta Simon om aan te wijzen HPE SaaS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fd5ef-199">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="fd5ef-200">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fd5ef-202">Selecteer in de lijst met toepassingen **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-202">In the applications list, select **HPE SaaS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_app.png) 

3. <span data-ttu-id="fd5ef-204">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="fd5ef-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-206">Click **Add** button.</span></span> <span data-ttu-id="fd5ef-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="fd5ef-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fd5ef-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd5ef-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd5ef-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fd5ef-212">Testing single sign-on</span></span>

<span data-ttu-id="fd5ef-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fd5ef-214">Als u op de tegel HPE SaaS in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw HPE SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fd5ef-214">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span></span>
<span data-ttu-id="fd5ef-215">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fd5ef-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd5ef-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fd5ef-216">Additional resources</span></span>

* [<span data-ttu-id="fd5ef-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd5ef-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd5ef-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fd5ef-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png

