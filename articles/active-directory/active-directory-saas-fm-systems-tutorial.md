---
title: 'Zelfstudie: Azure Active Directory-integratie met FM:Systems | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en FM:Systems.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3a597d228f6c9234ec2fd2644ec3ac50b98f3b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="922a1-103">Zelfstudie: Azure Active Directory-integratie met FM:Systems</span><span class="sxs-lookup"><span data-stu-id="922a1-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="922a1-104">In deze zelfstudie leert u hoe FM:Systems integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="922a1-104">In this tutorial, you learn how to integrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="922a1-105">FM:Systems integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="922a1-105">Integrating FM:Systems with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="922a1-106">U kunt beheren in Azure AD die toegang tot FM:Systems heeft</span><span class="sxs-lookup"><span data-stu-id="922a1-106">You can control in Azure AD who has access to FM:Systems</span></span>
- <span data-ttu-id="922a1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij FM:Systems (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="922a1-107">You can enable your users to automatically get signed-on to FM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="922a1-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="922a1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="922a1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="922a1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="922a1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="922a1-110">Prerequisites</span></span>

<span data-ttu-id="922a1-111">Voor het configureren van Azure AD-integratie met FM:Systems, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="922a1-111">To configure Azure AD integration with FM:Systems, you need the following items:</span></span>

- <span data-ttu-id="922a1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="922a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="922a1-113">Een FM:Systems eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="922a1-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="922a1-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="922a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="922a1-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="922a1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="922a1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="922a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="922a1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="922a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="922a1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="922a1-118">Scenario description</span></span>
<span data-ttu-id="922a1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="922a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="922a1-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="922a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="922a1-121">FM:Systems uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="922a1-121">Adding FM:Systems from the gallery</span></span>
2. <span data-ttu-id="922a1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="922a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-the-gallery"></a><span data-ttu-id="922a1-123">FM:Systems uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="922a1-123">Adding FM:Systems from the gallery</span></span>
<span data-ttu-id="922a1-124">Voor het configureren van de integratie van FM:Systems in Azure AD, moet u FM:Systems uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="922a1-124">To configure the integration of FM:Systems into Azure AD, you need to add FM:Systems from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="922a1-125">**Als u wilt toevoegen FM:Systems uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="922a1-125">**To add FM:Systems from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="922a1-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="922a1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="922a1-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="922a1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="922a1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="922a1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="922a1-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="922a1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="922a1-133">Typ in het zoekvak **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="922a1-133">In the search box, type **FM:Systems**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="922a1-135">Selecteer in het deelvenster resultaten **FM:Systems**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="922a1-135">In the results panel, select **FM:Systems**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="922a1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="922a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="922a1-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met FM:Systems op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="922a1-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="922a1-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in FM:Systems is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="922a1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FM:Systems is to a user in Azure AD.</span></span> <span data-ttu-id="922a1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in FM:Systems tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="922a1-140">In other words, a link relationship between an Azure AD user and the related user in FM:Systems needs to be established.</span></span>

<span data-ttu-id="922a1-141">Wijs in FM:Systems, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="922a1-141">In FM:Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="922a1-142">Om te configureren en testen van Azure AD eenmalige aanmelding met FM:Systems, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="922a1-142">To configure and test Azure AD single sign-on with FM:Systems, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="922a1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="922a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="922a1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="922a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="922a1-145">**[Maken van een testgebruiker FM:Systems](#creating-an-fmsystems-test-user)**  - hebben een equivalent van Britta Simon in FM:Systems die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="922a1-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - to have a counterpart of Britta Simon in FM:Systems that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="922a1-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="922a1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="922a1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="922a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="922a1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="922a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="922a1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing FM:Systems configureren.</span><span class="sxs-lookup"><span data-stu-id="922a1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="922a1-150">**Voor het configureren van Azure AD eenmalige aanmelding met FM:Systems, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="922a1-150">**To configure Azure AD single sign-on with FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="922a1-151">In de Azure-portal op de **FM:Systems** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="922a1-151">In the Azure portal, on the **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="922a1-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="922a1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="922a1-155">Op de **FM:Systems domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="922a1-155">On the **FM:Systems Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="922a1-157">In de **antwoord-URL** textbox, typt u uw FM:Systems **antwoord-URL**, typ de URL die met het volgende patroon volgen:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="922a1-157">In the **Reply URL** textbox, type your FM:Systems **Reply URL**, type the URL using the following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="922a1-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="922a1-158">This value is not real.</span></span> <span data-ttu-id="922a1-159">Deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="922a1-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="922a1-160">Neem contact op met [FM:Systems ondersteuningsteam](https://fmsystems.com/ask-us/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="922a1-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) to get this value.</span></span>
 
4. <span data-ttu-id="922a1-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="922a1-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="922a1-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="922a1-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="922a1-165">Eenmalige aanmelding configureren op **FM:Systems** zijde, moet u de gedownloade verzenden **Metadata XML** naar [FM:Systems ondersteuningsteam](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="922a1-165">To configure single sign-on on **FM:Systems** side, you need to send the downloaded **Metadata XML** to [FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="922a1-166">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="922a1-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="922a1-167">U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="922a1-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="922a1-168">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="922a1-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="922a1-169">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="922a1-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="922a1-170">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="922a1-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="922a1-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="922a1-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="922a1-172">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="922a1-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="922a1-174">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="922a1-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="922a1-175">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="922a1-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="922a1-177">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="922a1-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="922a1-179">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="922a1-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="922a1-181">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="922a1-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="922a1-183">a.</span><span class="sxs-lookup"><span data-stu-id="922a1-183">a.</span></span> <span data-ttu-id="922a1-184">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="922a1-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="922a1-185">b.</span><span class="sxs-lookup"><span data-stu-id="922a1-185">b.</span></span> <span data-ttu-id="922a1-186">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="922a1-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="922a1-187">c.</span><span class="sxs-lookup"><span data-stu-id="922a1-187">c.</span></span> <span data-ttu-id="922a1-188">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="922a1-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="922a1-189">d.</span><span class="sxs-lookup"><span data-stu-id="922a1-189">d.</span></span> <span data-ttu-id="922a1-190">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="922a1-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="922a1-191">Een testgebruiker FM:Systems maken</span><span class="sxs-lookup"><span data-stu-id="922a1-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="922a1-192">In een browservenster geopend, meld u bij uw bedrijf FM:Systems site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="922a1-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="922a1-193">Ga naar **Systeembeheer \> beveiliging beheren \> gebruikers \> gebruikerslijst**.</span><span class="sxs-lookup"><span data-stu-id="922a1-193">Go to **System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="922a1-194">![Systeembeheer](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="922a1-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="922a1-195">Klik op **nieuwe gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="922a1-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="922a1-196">![Nieuwe gebruiker maken](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "nieuwe gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="922a1-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="922a1-197">In de **gebruiker maken** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="922a1-197">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="922a1-198">![Gebruiker maken](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="922a1-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="922a1-199">a.</span><span class="sxs-lookup"><span data-stu-id="922a1-199">a.</span></span> <span data-ttu-id="922a1-200">Type de **gebruikersnaam**, wordt de **wachtwoord**, **wachtwoord bevestigen**, **e** en de **werknemer-ID** van een geldige Azure Active Directory-account die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="922a1-200">Type the **UserName**, the **Password**, **Confirm Password**, **E-mail** and the **Employee ID** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="922a1-201">b.</span><span class="sxs-lookup"><span data-stu-id="922a1-201">b.</span></span> <span data-ttu-id="922a1-202">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="922a1-202">Click **Next**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="922a1-203">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="922a1-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="922a1-204">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="922a1-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FM:Systems.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="922a1-206">**Britta Simon om aan te wijzen FM:Systems, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="922a1-206">**To assign Britta Simon to FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="922a1-207">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="922a1-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="922a1-209">Selecteer in de lijst met toepassingen **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="922a1-209">In the applications list, select **FM:Systems**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="922a1-211">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="922a1-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="922a1-213">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="922a1-213">Click **Add** button.</span></span> <span data-ttu-id="922a1-214">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="922a1-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="922a1-216">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="922a1-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="922a1-217">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="922a1-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="922a1-218">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="922a1-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="922a1-219">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="922a1-219">Testing single sign-on</span></span>

<span data-ttu-id="922a1-220">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="922a1-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="922a1-221">Als u op de tegel FM:Systems in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="922a1-221">When you click the FM:Systems tile in the Access Panel, you should get automatically signed-on to your FM:Systems application.</span></span>
<span data-ttu-id="922a1-222">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="922a1-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="922a1-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="922a1-223">Additional resources</span></span>

* [<span data-ttu-id="922a1-224">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="922a1-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="922a1-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="922a1-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

