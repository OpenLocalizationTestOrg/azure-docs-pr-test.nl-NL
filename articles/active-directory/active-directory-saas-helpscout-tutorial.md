---
title: 'Zelfstudie: Azure Active Directory-integratie met Help Scout | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Scout Help.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="35ace-103">Zelfstudie: Azure Active Directory-integratie met Scout Help</span><span class="sxs-lookup"><span data-stu-id="35ace-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="35ace-104">In deze zelfstudie leert u hoe Scout te integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35ace-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35ace-105">Bij het ophalen van de volgende voordelen van Scout te integreren met Azure AD:</span><span class="sxs-lookup"><span data-stu-id="35ace-105">You get the following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="35ace-106">In Azure AD kunt u bepalen wie toegang heeft tot Scout Help.</span><span class="sxs-lookup"><span data-stu-id="35ace-106">In Azure AD, you can control who has access to Help Scout.</span></span>
- <span data-ttu-id="35ace-107">U kunt uw gebruikers helpen Scout automatisch aanmelden met behulp van eenmalige aanmelding en Azure AD-account van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="35ace-107">You can automatically sign in your users to Help Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="35ace-108">U kunt uw accounts op één centrale locatie, de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="35ace-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="35ace-109">Zie voor meer informatie over software als een dienst (SaaS)-app-integratie met Azure AD, [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35ace-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35ace-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="35ace-110">Prerequisites</span></span>

<span data-ttu-id="35ace-111">Als u Azure AD-integratie met Help Scout instelt, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="35ace-111">To set up Azure AD integration with Help Scout, you need the following items:</span></span>

- <span data-ttu-id="35ace-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="35ace-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35ace-113">Een abonnement te Scout met eenmalige aanmelding ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="35ace-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="35ace-114">Als u de stappen in deze zelfstudie hebt getest, wordt u aangeraden dat u deze niet in een productieomgeving testen.</span><span class="sxs-lookup"><span data-stu-id="35ace-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="35ace-115">Aanbevelingen voor het testen van de stappen in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="35ace-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="35ace-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="35ace-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="35ace-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35ace-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35ace-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="35ace-118">Scenario description</span></span>
<span data-ttu-id="35ace-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="35ace-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="35ace-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="35ace-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35ace-121">Help Scout uit de galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="35ace-121">Add Help Scout from the gallery.</span></span>
2. <span data-ttu-id="35ace-122">Instellen en testen van eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35ace-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-the-gallery"></a><span data-ttu-id="35ace-123">Help Scout uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="35ace-123">Add Help Scout from the gallery</span></span>
<span data-ttu-id="35ace-124">Om in te stellen de integratie van Help Scout met Azure AD in de galerie toevoegen Scout helpen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="35ace-124">To set up the integration of Help Scout with Azure AD, in the gallery, add Help Scout to your list of managed SaaS apps.</span></span>

<span data-ttu-id="35ace-125">Help Scout uit de galerie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="35ace-125">To add Help Scout from the gallery:</span></span>

1. <span data-ttu-id="35ace-126">In de [Azure-portal](https://portal.azure.com), selecteer in het menu links **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35ace-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="35ace-128">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![De pagina met Enterprise-toepassingen][2]
    
3. <span data-ttu-id="35ace-130">Selecteer om een nieuwe toepassing toe **nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="35ace-130">To add a new application, select **New application**.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="35ace-132">Voer in het zoekvak **helpen Scout**.</span><span class="sxs-lookup"><span data-stu-id="35ace-132">In the search box, enter **Help Scout**.</span></span> <span data-ttu-id="35ace-133">Selecteer in de lijst met zoekresultaten **helpen Scout**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-133">In the search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Help Scout in de lijst met resultaten](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="35ace-135">Instellen en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="35ace-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="35ace-136">In deze sectie kunt u instellen en eenmalige aanmelding Azure AD-test met Scout Help op basis van een testgebruiker met de naam *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="35ace-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="35ace-137">Voor eenmalige aanmelding werkt, moet Azure AD de equivalente Azure AD-gebruiker in de Help Scout bekend.</span><span class="sxs-lookup"><span data-stu-id="35ace-137">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="35ace-138">Een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Help Scout moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="35ace-138">A link relationship between an Azure AD user and the related user in Help Scout must be established.</span></span>

<span data-ttu-id="35ace-139">Om te bepalen van de relatie koppeling in de Help Scout voor **gebruikersnaam**, wijs de waarde van de **gebruikersnaam** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35ace-139">To establish the link relationship, in Help Scout, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="35ace-140">Als u wilt configureren en Azure AD eenmalige aanmelding met Scout te testen, moet u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="35ace-140">To configure and test Azure AD single sign-on with Help Scout, complete the following tasks:</span></span>

1. <span data-ttu-id="35ace-141">[Instellen van eenmalige aanmelding Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="35ace-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="35ace-142">Hiermee stelt u een gebruiker deze functie wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="35ace-142">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="35ace-143">[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="35ace-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="35ace-144">Azure AD tests eenmalige aanmelding met de gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35ace-144">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="35ace-145">[Maak een testgebruiker Scout Help](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="35ace-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="35ace-146">Maakt een equivalent van Britta Simon in Help Scout, dat is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="35ace-146">Creates a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="35ace-147">[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="35ace-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="35ace-148">Ingesteld Britta Simon naar Azure AD gebruikt eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="35ace-148">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35ace-149">[Test eenmalige aanmelding](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="35ace-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="35ace-150">Verifieert dat de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="35ace-150">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="35ace-151">Instellen van eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="35ace-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="35ace-152">In deze sectie kunt instellen u Azure AD eenmalige aanmelding in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="35ace-152">In this section, you set up Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="35ace-153">Vervolgens instellen u eenmalige aanmelding in uw toepassing Scout Help.</span><span class="sxs-lookup"><span data-stu-id="35ace-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="35ace-154">Voor het instellen van Azure AD eenmalige aanmelding met Scout helpen:</span><span class="sxs-lookup"><span data-stu-id="35ace-154">To set up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="35ace-155">In de Azure-portal op de **helpen Scout** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="35ace-155">In the Azure portal, on the **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Koppeling voor eenmalige aanmelding instellen][4]

2. <span data-ttu-id="35ace-157">Op de **eenmalige aanmelding** pagina voor **modus**, selecteer **op basis van SAML aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="35ace-157">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="35ace-159">Onder **helpen Scout domein en URL's**, als u wilt dat voor het instellen van de toepassing in de IDP geïnitieerde modus voltooid de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="35ace-159">Under **Help Scout Domain and URLs**, if you want to set up the application in IDP-initiated mode, complete the following steps:</span></span>

    1. <span data-ttu-id="35ace-160">In de **id** Voer een URL die het volgende patroon volgen is:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="35ace-160">In the **Identifier** box, enter a URL that has the following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="35ace-161">In de **antwoord-URL** Voer een URL die het volgende patroon volgen is:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="35ace-161">In the **Reply URL** box, enter a URL that has the following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="35ace-163">Als u wilt dat de toepassing in de modus Serviceprovider geïnitieerde ingesteld, selecteert u de **weergeven geavanceerde instellingen voor URL** uit en doe vervolgens het volgende:</span><span class="sxs-lookup"><span data-stu-id="35ace-163">If you want to set up the application in SP-initiated mode, select the **Show advanced URL settings** check box, and then do the following:</span></span>

    * <span data-ttu-id="35ace-164">In de **aanmelden URL** Voer een URL die de volgende indeling heeft:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="35ace-164">In the **Sign on URL** box, enter a URL that has the following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="35ace-166">De waarden in deze URL's zijn voor de demonstratie alleen.</span><span class="sxs-lookup"><span data-stu-id="35ace-166">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="35ace-167">Werk de waarden op met de werkelijke identificatie-URL en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="35ace-167">Update the values with the actual identifier URL and reply URL.</span></span> <span data-ttu-id="35ace-168">Als u deze waarden, neem contact op met [helpen Scout ondersteuningsteam](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="35ace-168">To get these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="35ace-169">Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**, en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="35ace-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="35ace-171">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="35ace-171">Select **Save**.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="35ace-173">Als u eenmalige aanmelding aan de kant van de Help Scout instelt, verzendt het gedownloade metagegevens-XML-bestand naar de [helpen Scout ondersteuningsteam](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="35ace-173">To set up single sign-on on the Help Scout side, send the downloaded metadata XML file to the [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="35ace-174">Het ondersteuningsteam Scout Help is deze instelling zodat de SAML eenmalige aanmelding verbinding juist is ingesteld op beide zijden van toepassing.</span><span class="sxs-lookup"><span data-stu-id="35ace-174">The Help Scout support team applies this setting so that the SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="35ace-175">Vindt u een beknopte versie van deze instructies in de [Azure-portal](https://portal.azure.com), terwijl u uw app instelt.</span><span class="sxs-lookup"><span data-stu-id="35ace-175">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="35ace-176">Nadat u de app door te selecteren toevoegen **Active Directory** > **bedrijfstoepassingen**, selecteer de **Single Sign-On** tabblad. U hebt toegang tot het embedded-documentatie in de **configuratie** sectie aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="35ace-176">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="35ace-177">Zie voor meer informatie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="35ace-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="35ace-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="35ace-178">Create an Azure AD test user</span></span>

<span data-ttu-id="35ace-179">In deze sectie in de Azure portal maakt u een testgebruiker Britta Simon met de naam.</span><span class="sxs-lookup"><span data-stu-id="35ace-179">In this section, in the Azure portal, you create a test user named Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="35ace-181">Een testgebruiker maken in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="35ace-181">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="35ace-182">Selecteer in de Azure-portal in het menu links **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35ace-182">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="35ace-184">Als u wilt weergeven in de lijst met gebruikers, selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="35ace-184">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Gebruikers en groepen selecteren en selecteer alle gebruikers](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="35ace-186">Openen van de **gebruiker** in het dialoogvenster aan de bovenkant van de **alle gebruikers** pagina **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-186">To open the **User** dialog box, at the top of the **All Users** page, select **Add**.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="35ace-188">In de **gebruiker** dialoogvenster Vervolledig de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="35ace-188">In the **User** dialog box, complete the following steps:</span></span>

    1. <span data-ttu-id="35ace-189">In de **naam** Voer **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35ace-189">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="35ace-190">In de **gebruikersnaam** Voer het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35ace-190">In the **User name** box, enter the email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="35ace-191">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="35ace-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="35ace-192">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="35ace-192">Select **Create**.</span></span>

        ![Het dialoogvenster gebruiker](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="35ace-194">Een testgebruiker Scout te maken</span><span class="sxs-lookup"><span data-stu-id="35ace-194">Create a Help Scout test user</span></span>

<span data-ttu-id="35ace-195">Het object van deze sectie is het maken van een gebruiker met de naam Britta Simon in Scout Help.</span><span class="sxs-lookup"><span data-stu-id="35ace-195">The object of this section is to create a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="35ace-196">Help Scout ondersteunt just in time (Just in time) inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="35ace-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="35ace-197">In deze sectie vindt er geen actie of de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="35ace-197">In this section, there's no action or task to complete.</span></span> <span data-ttu-id="35ace-198">Als een gebruiker niet al in de Help Scout bestaat, wordt een nieuw wordt gemaakt wanneer u probeert te openen Scout Help.</span><span class="sxs-lookup"><span data-stu-id="35ace-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="35ace-199">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="35ace-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="35ace-200">In deze sectie kunt u de gebruiker Britta Simon Azure AD eenmalige aanmelding gebruiken door de gebruikerstoegang verlenen aan Help Scout toestaan.</span><span class="sxs-lookup"><span data-stu-id="35ace-200">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to Help Scout.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="35ace-202">Britta Simon toewijzen aan Scout helpen:</span><span class="sxs-lookup"><span data-stu-id="35ace-202">To assign Britta Simon to Help Scout:</span></span>

1. <span data-ttu-id="35ace-203">Open de toepassingen in de Azure portal en gaat u naar de directoryweergave.</span><span class="sxs-lookup"><span data-stu-id="35ace-203">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="35ace-204">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="35ace-206">Selecteer in de lijst met toepassingen **helpen Scout**.</span><span class="sxs-lookup"><span data-stu-id="35ace-206">In the applications list, select **Help Scout**.</span></span>

    ![De Scout Help-koppeling in de lijst met toepassingen](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="35ace-208">Selecteer in het menu links **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-208">In the left menu, select **Users and groups**.</span></span>

    ![De koppeling gebruikers en groepen][202]

4. <span data-ttu-id="35ace-210">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-210">Select **Add**.</span></span> <span data-ttu-id="35ace-211">Klik op de **toevoegen toewijzing** pagina **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-211">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="35ace-213">Op de **gebruikers en groepen** pagina in de lijst met gebruikers, selecteer **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="35ace-213">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="35ace-214">Op de **gebruikers en groepen** pagina **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="35ace-214">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="35ace-215">Op de **toevoegen toewijzing** pagina **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="35ace-215">On the **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="35ace-216">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="35ace-216">Test single sign-on</span></span>

<span data-ttu-id="35ace-217">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="35ace-217">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="35ace-218">Wanneer u de tegel Help Scout in het deelvenster toegang selecteert, moet u worden automatisch aangemeld bij uw toepassing Scout Help.</span><span class="sxs-lookup"><span data-stu-id="35ace-218">When you select the Help Scout tile in the access panel, you should be automatically signed in to your Help Scout application.</span></span>

<span data-ttu-id="35ace-219">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35ace-219">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="35ace-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="35ace-220">Additional resources</span></span>

* [<span data-ttu-id="35ace-221">Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35ace-221">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35ace-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35ace-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

