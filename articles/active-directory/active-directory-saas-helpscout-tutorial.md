---
title: 'Zelfstudie: Azure Active Directory-integratie met Help Scout | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Scout Help.
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
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="1c4f9-103">Zelfstudie: Azure Active Directory-integratie met Scout Help</span><span class="sxs-lookup"><span data-stu-id="1c4f9-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="1c4f9-104">In deze zelfstudie leert u hoe toointegrate helpen gids met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c4f9-105">U de volgende voordelen van Scout te integreren met Azure AD Hallo krijgen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="1c4f9-106">In Azure AD, kunt u bepalen wie toegang tooHelp Scout heeft.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="1c4f9-107">U kunt uw gebruikers tooHelp Scout automatisch aanmelden met behulp van eenmalige aanmelding en Azure AD-account van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="1c4f9-108">U kunt uw accounts op één centrale locatie hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="1c4f9-109">Zie toolearn meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c4f9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1c4f9-110">Prerequisites</span></span>

<span data-ttu-id="1c4f9-111">tooset van Azure AD-integratie met Help Scout, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="1c4f9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1c4f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c4f9-113">Een abonnement te Scout met eenmalige aanmelding ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="1c4f9-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="1c4f9-114">Als u Hallo stappen in deze zelfstudie hebt getest, wordt u aangeraden dat u deze niet in een productieomgeving testen.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="1c4f9-115">Aanbevelingen voor het testen van Hallo stappen in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="1c4f9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="1c4f9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c4f9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1c4f9-118">Scenario description</span></span>
<span data-ttu-id="1c4f9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="1c4f9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c4f9-121">Help Scout uit Hallo galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="1c4f9-122">Instellen en testen van eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="1c4f9-123">Help Scout van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c4f9-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="1c4f9-124">tooset van integratie van Help Scout met Azure AD in de galerie Hallo Hallo Scout Help tooyour lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c4f9-125">tooadd Scout uit de galerie Hallo helpen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="1c4f9-126">In Hallo [Azure-portal](https://portal.azure.com), Hallo linkermenu in, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="1c4f9-128">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![pagina met toepassingen Hallo Enterprise][2]
    
3. <span data-ttu-id="1c4f9-130">Selecteer een nieuwe toepassing tooadd **nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-130">tooadd a new application, select **New application**.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="1c4f9-132">Voer in het zoekvak Hallo **helpen Scout**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="1c4f9-133">Selecteer in de zoekresultaten hello, **helpen Scout**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Scout Help in de lijst met resultaten Hallo](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1c4f9-135">Instellen en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4f9-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="1c4f9-136">In deze sectie kunt u instellen en eenmalige aanmelding Azure AD-test met Scout Help op basis van een testgebruiker met de naam *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="1c4f9-137">Voor één aanmelding toowork moet Azure AD tooknow hello Azure AD-equivalent gebruiker in Scout Help.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="1c4f9-138">Een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Help Scout moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="1c4f9-139">Hallo tooestablish relatie in Scout te koppelen voor **gebruikersnaam**, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="1c4f9-140">tooconfigure en eenmalige aanmelding Azure AD-test met Help Scout, volledige Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="1c4f9-141">[Instellen van eenmalige aanmelding Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="1c4f9-142">Een gebruiker toouse ingesteld met deze functie.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="1c4f9-143">[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="1c4f9-144">Azure AD tests eenmalige aanmelding met Hallo gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="1c4f9-145">[Maak een testgebruiker Scout Help](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="1c4f9-146">Een exemplaar van Britta Simon in Help Scout gekoppelde toohello Azure AD-weergave van Hallo gebruiker is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="1c4f9-147">[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="1c4f9-148">Stelt Britta Simon toouse eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c4f9-149">[Test eenmalige aanmelding](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="1c4f9-150">Controleert of dat die Hallo configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="1c4f9-151">Instellen van eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4f9-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="1c4f9-152">In deze sectie kunt instellen u Azure AD eenmalige aanmelding in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="1c4f9-153">Vervolgens instellen u eenmalige aanmelding in uw toepassing Scout Help.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="1c4f9-154">tooset van Azure AD eenmalige aanmelding met Scout helpen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="1c4f9-155">In de Azure-portal op Hallo Hallo **helpen Scout** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Koppeling voor eenmalige aanmelding instellen][4]

2. <span data-ttu-id="1c4f9-157">Op Hallo **eenmalige aanmelding** pagina voor **modus**, selecteer **op basis van SAML aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="1c4f9-159">Onder **helpen Scout domein en URL's**, als u wilt dat tooset Hallo-toepassing in de IDP geïnitieerde modus volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="1c4f9-160">In Hallo **id** Voer een URL Hallo patroon volgen:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1c4f9-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="1c4f9-161">In Hallo **antwoord-URL** Voer een URL Hallo patroon volgen:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1c4f9-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="1c4f9-163">Als u in de modus Serviceprovider geïnitieerde tooset toepassing hello, selecteert u Hallo **weergeven geavanceerde instellingen voor URL** selectievakje en vervolgens Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="1c4f9-164">In Hallo **aanmelden URL** Voer een URL Hallo volgende indeling:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="1c4f9-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="1c4f9-166">Hallo-waarden in deze URL's zijn voor alleen demonstratie.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="1c4f9-167">Hallo-waarden bijwerken met Hallo werkelijke identificatie-URL en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="1c4f9-168">Neem contact op met tooget deze waarden [helpen Scout ondersteuningsteam](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="1c4f9-169">Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**, en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="1c4f9-171">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-171">Select **Save**.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1c4f9-173">tooset van één aanmelding Hallo Scout Help-zijde, verzenden Hallo gedownload metagegevens XML-bestand toohello [helpen Scout ondersteuningsteam](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="1c4f9-174">Deze instelling is van toepassing Hello Help Scout ondersteuningsteam zodat Hallo SAML één aanmelding verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1c4f9-175">U kunt een beknopte versie van deze instructies in Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u uw app instelt!</span><span class="sxs-lookup"><span data-stu-id="1c4f9-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="1c4f9-176">Nadat u Hallo app door te selecteren toevoegen **Active Directory** > **bedrijfstoepassingen**, selecteer Hallo **Single Sign-On** tabblad. U hebt toegang tot documentatie in Hallo Hallo ingesloten **configuratie** sectie Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="1c4f9-177">Zie voor meer informatie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1c4f9-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1c4f9-178">Create an Azure AD test user</span></span>

<span data-ttu-id="1c4f9-179">In deze sectie in hello Azure-portal, maakt u een testgebruiker Britta Simon met de naam.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="1c4f9-181">toocreate een testgebruiker in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="1c4f9-182">Selecteer in de Azure-portal in het linkermenu Hallo Hallo **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1c4f9-184">toodisplay hello lijst met gebruikers, selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Gebruikers en groepen selecteren en selecteer alle gebruikers](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1c4f9-186">Hallo tooopen **gebruiker** in het dialoogvenster bovenaan Hallo Hallo **alle gebruikers** pagina **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1c4f9-188">In Hallo **gebruiker** dialoogvenster, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="1c4f9-189">In Hallo **naam** Voer **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="1c4f9-190">In Hallo **gebruikersnaam** Voer Hallo e-mailadres van de gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="1c4f9-191">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="1c4f9-192">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-192">Select **Create**.</span></span>

        ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="1c4f9-194">Een testgebruiker Scout te maken</span><span class="sxs-lookup"><span data-stu-id="1c4f9-194">Create a Help Scout test user</span></span>

<span data-ttu-id="1c4f9-195">Hallo-doel van deze sectie is toocreate Britta Simon in Scout helpen met de naam van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="1c4f9-196">Help Scout ondersteunt just in time (Just in time) inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="1c4f9-197">In deze sectie is er geen actie of een taak toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="1c4f9-198">Als een gebruiker nog niet in de Help Scout bestaat, wordt een nieuwe gemaakt wanneer u tooaccess Scout Help probeert.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1c4f9-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c4f9-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1c4f9-200">In deze sectie maakt toestaan u Hallo gebruiker Britta Simon eenmalige aanmelding toouse Azure AD Hallo gebruiker account toegang tooHelp Scout verleent.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="1c4f9-202">tooassign Britta Simon tooHelp Scout:</span><span class="sxs-lookup"><span data-stu-id="1c4f9-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="1c4f9-203">Hallo toepassingen weergave opent in hello Azure-portal, en gaat u toohello directory weergeven.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="1c4f9-204">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1c4f9-206">Selecteer in de lijst met de toepassingen van Hallo **helpen Scout**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-206">In hello applications list, select **Help Scout**.</span></span>

    ![Hallo Scout Help-koppeling in lijst met toepassingen Hallo](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="1c4f9-208">Selecteer in het linkermenu Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-208">In hello left menu, select **Users and groups**.</span></span>

    ![Hallo gebruikers en groepen koppelen][202]

4. <span data-ttu-id="1c4f9-210">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-210">Select **Add**.</span></span> <span data-ttu-id="1c4f9-211">Klik vervolgens op Hallo **toevoegen toewijzing** pagina **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="1c4f9-213">Op Hallo **gebruikers en groepen** pagina in de lijst Hallo van gebruikers, selecteer **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="1c4f9-214">Op Hallo **gebruikers en groepen** pagina **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="1c4f9-215">Op Hallo **toevoegen toewijzing** pagina **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1c4f9-216">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c4f9-216">Test single sign-on</span></span>

<span data-ttu-id="1c4f9-217">In deze sectie kunt u uw configuratie Azure AD eenmalige aanmelding met behulp van het toegangsvenster Hallo testen.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="1c4f9-218">Wanneer u Hallo Scout Help-tegel in het toegangsvenster Hallo selecteert, moet u tooyour Scout Help-toepassing automatisch worden aangemeld.</span><span class="sxs-lookup"><span data-stu-id="1c4f9-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="1c4f9-219">Zie voor meer informatie over het toegangsvenster [inleiding toohello toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c4f9-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1c4f9-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1c4f9-220">Additional resources</span></span>

* [<span data-ttu-id="1c4f9-221">Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c4f9-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c4f9-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c4f9-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

