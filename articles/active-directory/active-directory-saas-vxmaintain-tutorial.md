---
title: 'Zelfstudie: Azure Active Directory integreren met vxMaintain | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en vxMaintain.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="743c3-103">Zelfstudie: Azure Active Directory integreren met vxMaintain</span><span class="sxs-lookup"><span data-stu-id="743c3-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="743c3-104">In deze zelfstudie leert u hoe toointegrate vxMaintain met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="743c3-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="743c3-105">Deze integratie biedt een aantal belangrijke voordelen.</span><span class="sxs-lookup"><span data-stu-id="743c3-105">This integration provides several important benefits.</span></span> <span data-ttu-id="743c3-106">U kunt:</span><span class="sxs-lookup"><span data-stu-id="743c3-106">You can:</span></span>

- <span data-ttu-id="743c3-107">Besturingselement in Azure AD wie heeft toegang tot toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="743c3-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="743c3-108">Uw gebruikers tooautomatically aanmelding toovxMaintain met eenmalige aanmelding (SSO) inschakelen met behulp van hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="743c3-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="743c3-109">Uw accounts beheren via één centrale locatie: hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="743c3-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="743c3-110">Zie toolearn meer over de integratie met Azure AD SaaS [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="743c3-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="743c3-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="743c3-111">Prerequisites</span></span>

<span data-ttu-id="743c3-112">Azure AD-integratie met vxMaintain tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="743c3-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="743c3-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="743c3-113">An Azure AD subscription</span></span>
- <span data-ttu-id="743c3-114">Een vxMaintain abonnement SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="743c3-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="743c3-115">Wanneer u Hallo stappen in deze zelfstudie test, wordt u aangeraden een productie-omgeving niet te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="743c3-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="743c3-116">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="743c3-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="743c3-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="743c3-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="743c3-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="743c3-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="743c3-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="743c3-119">Scenario description</span></span>
<span data-ttu-id="743c3-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="743c3-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="743c3-121">Hallo-scenario dat geeft een overzicht van deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="743c3-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="743c3-122">Het toevoegen van vxMaintain van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="743c3-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="743c3-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="743c3-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="743c3-124">VxMaintain van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="743c3-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="743c3-125">tooconfigure hello integratie van vxMaintain met Azure AD, moet u tooadd vxMaintain uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="743c3-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="743c3-126">tooadd vxMaintain via Hallo gallery Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="743c3-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="743c3-127">In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="743c3-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="743c3-129">Selecteer **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="743c3-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Hallo 'Bedrijfstoepassingen' deelvenster][2]
    
3. <span data-ttu-id="743c3-131">een toepassing, in Hallo tooadd **alle toepassingen** dialoogvenster, **nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="743c3-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    !['Nieuwe application' Hallo knop][3]

4. <span data-ttu-id="743c3-133">Typ in het zoekvak Hallo **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="743c3-133">In hello search box, type **vxMaintain**.</span></span>

    ![Hallo 'Single Sign-on modus' vervolgkeuzelijst](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="743c3-135">Selecteer in de lijst met resultaten Hallo **vxMaintain**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="743c3-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![Hallo vxMaintain koppeling](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="743c3-137">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="743c3-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="743c3-138">In deze sectie u configureren en testen van Azure AD-SSO met behulp van vxMaintain, op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="743c3-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="743c3-139">Voor eenmalige aanmelding toowork moet Azure AD tooknow hello vxMaintain equivalent toohello Azure AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="743c3-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="743c3-140">Dat wil zeggen, moet u een koppeling bestaat tussen hello Azure AD-gebruiker en Hallo bijbehorende vxMaintain gebruiker instellen.</span><span class="sxs-lookup"><span data-stu-id="743c3-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="743c3-141">tooestablish hello koppeling relatie toewijzen Hallo vxMaintain **gebruikersnaam** waarde als hello Azure AD **gebruikersnaam** waarde.</span><span class="sxs-lookup"><span data-stu-id="743c3-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="743c3-142">tooconfigure en test Azure AD-SSO met behulp van vxMaintain, volledige Hallo bouwstenen te volgen.</span><span class="sxs-lookup"><span data-stu-id="743c3-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="743c3-143">Azure AD-eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="743c3-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="743c3-144">In deze sectie maakt kunt u zowel Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing vxMaintain door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="743c3-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="743c3-145">In de Azure-portal op Hallo Hallo **vxMaintain** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="743c3-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![opdracht 'Single sign-on' Hallo][4]

2. <span data-ttu-id="743c3-147">tooenable SSO in Hallo **modus voor één aanmelding** vervolgkeuzelijst, selecteer **op basis van SAML aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="743c3-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![de opdracht 'op basis van SAML aanmelding' Hallo](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="743c3-149">Onder **vxMaintain domein en de URL's**, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="743c3-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Hallo vxMaintain sectie domein en URL 's](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="743c3-151">a.</span><span class="sxs-lookup"><span data-stu-id="743c3-151">a.</span></span> <span data-ttu-id="743c3-152">In Hallo **id** vak een URL die is Hallo de volgende syntaxis:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="743c3-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="743c3-153">b.</span><span class="sxs-lookup"><span data-stu-id="743c3-153">b.</span></span> <span data-ttu-id="743c3-154">In Hallo **antwoord-URL** vak een URL die is Hallo de volgende syntaxis:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="743c3-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="743c3-155">Hallo voorgaande waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="743c3-155">hello preceding values are not real.</span></span> <span data-ttu-id="743c3-156">Deze bijwerken met de werkelijke Hallo-id en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="743c3-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="743c3-157">tooobtain hello waarden, neem contact op met Hallo [vxMaintain ondersteuningsteam](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="743c3-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="743c3-158">Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**, en sla Hallo metagegevens bestand tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="743c3-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![de sectie 'SAML handtekeningcertificaat' Hallo](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="743c3-160">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="743c3-160">Select **Save**.</span></span>

    ![de knop Opslaan Hallo](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="743c3-162">tooconfigure **vxMaintain** SSO, verzenden Hallo gedownload **Metadata XML** bestand toohello [vxMaintain ondersteuningsteam](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="743c3-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="743c3-163">Bij het instellen van de app hello, vindt u een beknopte versie van de voorgaande instructies in Hallo Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="743c3-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="743c3-164">Nadat u Hallo app toegevoegd uit Hallo **Active Directory** > **bedrijfstoepassingen** sectie, selecteer Hallo **Single Sign-On** tabblad en toegang Hallo documentatie van Hallo ingesloten **configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="743c3-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="743c3-165">toolearn meer informatie over de functie voor Hallo embedded-documentatie, Zie [het beheren van eenmalige aanmelding voor zakelijke apps](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="743c3-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="743c3-166">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="743c3-166">Create an Azure AD test user</span></span>
<span data-ttu-id="743c3-167">In deze sectie kunt u testgebruiker Britta Simon in hello Azure-portal maken door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="743c3-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![testgebruiker Hello Azure AD][100]

1. <span data-ttu-id="743c3-169">In Hallo **Azure-portal**, in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="743c3-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![Hallo 'Azure Active Directory' knop](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="743c3-171">een lijst met gebruikers, toodisplay te gaan**gebruikers en groepen** > **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="743c3-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="743c3-172">![Hallo 'Alle gebruikers' koppelen](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="743c3-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="743c3-173">Hallo **alle gebruikers** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="743c3-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="743c3-174">Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="743c3-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="743c3-176">In Hallo **gebruiker** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="743c3-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="743c3-178">a.</span><span class="sxs-lookup"><span data-stu-id="743c3-178">a.</span></span> <span data-ttu-id="743c3-179">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="743c3-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="743c3-180">b.</span><span class="sxs-lookup"><span data-stu-id="743c3-180">b.</span></span> <span data-ttu-id="743c3-181">In Hallo **gebruikersnaam** type Hallo e-mailadres van de testgebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="743c3-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="743c3-182">c.</span><span class="sxs-lookup"><span data-stu-id="743c3-182">c.</span></span> <span data-ttu-id="743c3-183">Selecteer Hallo **wachtwoord weergeven** selectievakje en Opmerking Hallo waarde die is gegenereerd in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="743c3-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="743c3-184">d.</span><span class="sxs-lookup"><span data-stu-id="743c3-184">d.</span></span> <span data-ttu-id="743c3-185">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="743c3-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="743c3-186">Een testgebruiker vxMaintain maken</span><span class="sxs-lookup"><span data-stu-id="743c3-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="743c3-187">In deze sectie maakt u testgebruiker Britta Simon in vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="743c3-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="743c3-188">tooadd gebruikers in Hallo vxMaintain platform, werken met de [vxMaintain ondersteuningsteam](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="743c3-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="743c3-189">Voordat u eenmalige aanmelding gebruiken, maken en activeren Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="743c3-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="743c3-190">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="743c3-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="743c3-191">In deze sectie kunt u testgebruiker Britta Simon toouse Azure eenmalige aanmelding inschakelen toovxMaintain toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="743c3-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="743c3-192">toodo dus Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="743c3-192">toodo so, do hello following:</span></span>

![Testgebruiker in Hallo weergavenaam lijst][200] 

1. <span data-ttu-id="743c3-194">In de Azure-portal Hallo **toepassingen** weergeven, gaat u te**Directory** weergave > **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="743c3-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Hallo 'Alle toepassingen' koppelen][201] 

2. <span data-ttu-id="743c3-196">In Hallo **toepassingen** selecteert **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="743c3-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![Hallo vxMaintain koppeling](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="743c3-198">Selecteer in het linkerdeelvenster Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="743c3-198">In hello left pane, select **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="743c3-200">Selecteer **toevoegen** en klikt u op Hallo **toevoegen toewijzing** deelvenster **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="743c3-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][203]

5. <span data-ttu-id="743c3-202">In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**, en selecteer vervolgens Hallo **selecteren** knop.</span><span class="sxs-lookup"><span data-stu-id="743c3-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="743c3-203">In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="743c3-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="743c3-204">Test uw Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="743c3-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="743c3-205">In deze sectie kunt u de configuratie van uw Azure AD SSO testen met behulp van Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="743c3-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="743c3-206">Selecteren Hallo **vxMaintain** tegel in Hallo Toegangsvenster moet u tooyour vxMaintain toepassing automatisch aanmelden.</span><span class="sxs-lookup"><span data-stu-id="743c3-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="743c3-207">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="743c3-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="743c3-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="743c3-208">Next steps</span></span>

* [<span data-ttu-id="743c3-209">Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="743c3-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="743c3-210">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="743c3-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

