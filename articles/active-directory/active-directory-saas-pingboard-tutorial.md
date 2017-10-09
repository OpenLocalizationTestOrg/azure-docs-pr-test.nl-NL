---
title: 'Zelfstudie: Azure Active Directory-integratie met Pingboard | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Pingboard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="f89cc-103">Zelfstudie: Azure Active Directory-integratie met Pingboard</span><span class="sxs-lookup"><span data-stu-id="f89cc-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="f89cc-104">In deze zelfstudie leert u hoe toointegrate Pingboard met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f89cc-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f89cc-105">Pingboard integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f89cc-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f89cc-106">U kunt beheren in Azure AD die tooPingboard toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f89cc-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="f89cc-107">U kunt uw gebruikers tooautomatically get aangemelde tooPingboard (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f89cc-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f89cc-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="f89cc-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="f89cc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f89cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f89cc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f89cc-110">Prerequisites</span></span>

<span data-ttu-id="f89cc-111">Azure AD-integratie met Pingboard tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f89cc-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="f89cc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f89cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f89cc-113">Een Pingboard eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f89cc-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f89cc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f89cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f89cc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f89cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f89cc-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f89cc-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f89cc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f89cc-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f89cc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f89cc-118">Scenario description</span></span>
<span data-ttu-id="f89cc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f89cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f89cc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f89cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f89cc-121">Het toevoegen van Pingboard van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f89cc-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="f89cc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f89cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="f89cc-123">Het toevoegen van Pingboard van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f89cc-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="f89cc-124">tooconfigure hello integratie van Pingboard in Azure AD, moet u tooadd Pingboard uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f89cc-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f89cc-125">**tooadd Pingboard via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f89cc-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89cc-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f89cc-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f89cc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f89cc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f89cc-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f89cc-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f89cc-133">Typ in het zoekvak Hallo **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-133">In hello search box, type **Pingboard**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="f89cc-135">Selecteer in het deelvenster resultaten hello, **Pingboard**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f89cc-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f89cc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f89cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f89cc-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Pingboard op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f89cc-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f89cc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Pingboard is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f89cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="f89cc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Pingboard toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f89cc-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="f89cc-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="f89cc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="f89cc-142">tooconfigure en eenmalige aanmelding Azure AD-test met Pingboard, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f89cc-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f89cc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f89cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f89cc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f89cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f89cc-145">**[Maken van een testgebruiker Pingboard](#creating-a-pingboard-test-user)**  -toohave een equivalent van Britta Simon in Pingboard die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="f89cc-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f89cc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f89cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f89cc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f89cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f89cc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f89cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f89cc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing Pingboard configureren.</span><span class="sxs-lookup"><span data-stu-id="f89cc-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="f89cc-150">**Azure AD tooconfigure eenmalige aanmelding met Pingboard, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f89cc-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89cc-151">In hello Azure Management portal op Hallo **Pingboard** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f89cc-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f89cc-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="f89cc-155">Op Hallo **Pingboard domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f89cc-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="f89cc-157">a.</span><span class="sxs-lookup"><span data-stu-id="f89cc-157">a.</span></span> <span data-ttu-id="f89cc-158">In Hallo **id** textbox Hallo typewaarde als:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="f89cc-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="f89cc-159">b.</span><span class="sxs-lookup"><span data-stu-id="f89cc-159">b.</span></span> <span data-ttu-id="f89cc-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="f89cc-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f89cc-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="f89cc-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="f89cc-162">U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="f89cc-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f89cc-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="f89cc-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="f89cc-164">Neem contact op met [Pingboard Client ondersteuningsteam](https://support.pingboard.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f89cc-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="f89cc-165">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f89cc-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="f89cc-167">a.</span><span class="sxs-lookup"><span data-stu-id="f89cc-167">a.</span></span> <span data-ttu-id="f89cc-168">In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="f89cc-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="f89cc-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f89cc-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="f89cc-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f89cc-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f89cc-173">tooconfigure SSO Pingboard zijde, open een nieuw browservenster en meld u tooyour Pingboard-Account.</span><span class="sxs-lookup"><span data-stu-id="f89cc-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="f89cc-174">U moet een Pingboard admin tooset van eenmalige aanmelding op.</span><span class="sxs-lookup"><span data-stu-id="f89cc-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="f89cc-175">Selecteer in het bovenste menu Hallo **Apps > integraties**</span><span class="sxs-lookup"><span data-stu-id="f89cc-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="f89cc-177">Op Hallo **integraties** pagina, Hallo zoeken **'Azure Active Directory'** tegel en klik erop.</span><span class="sxs-lookup"><span data-stu-id="f89cc-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="f89cc-179">In de modale Hallo klikt u op volgende **'Configureren'**</span><span class="sxs-lookup"><span data-stu-id="f89cc-179">In hello modal that follows click **"Configure"**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="f89cc-181">Op Hallo na pagina, zult u merken dat ' Azure SSO-integratie is ingeschakeld.'.</span><span class="sxs-lookup"><span data-stu-id="f89cc-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="f89cc-182">Open Hallo gedownload Metadata XML-bestand in een Hallo Kladblok en plak de inhoud van **IDP metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="f89cc-184">Hallo-bestand worden gevalideerd en als alles juist is eenmalige aanmelding nu worden ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="f89cc-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f89cc-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f89cc-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="f89cc-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f89cc-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f89cc-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f89cc-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89cc-189">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f89cc-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f89cc-191">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f89cc-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f89cc-193">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f89cc-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f89cc-195">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f89cc-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f89cc-197">a.</span><span class="sxs-lookup"><span data-stu-id="f89cc-197">a.</span></span> <span data-ttu-id="f89cc-198">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f89cc-199">b.</span><span class="sxs-lookup"><span data-stu-id="f89cc-199">b.</span></span> <span data-ttu-id="f89cc-200">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f89cc-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f89cc-201">c.</span><span class="sxs-lookup"><span data-stu-id="f89cc-201">c.</span></span> <span data-ttu-id="f89cc-202">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f89cc-203">d.</span><span class="sxs-lookup"><span data-stu-id="f89cc-203">d.</span></span> <span data-ttu-id="f89cc-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="f89cc-205">Een testgebruiker Pingboard maken</span><span class="sxs-lookup"><span data-stu-id="f89cc-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="f89cc-206">In de volgorde tooenable Azure AD gebruikers toolog in Pingboard, moeten ze worden ingericht in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="f89cc-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="f89cc-207">In geval van Pingboard Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="f89cc-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="f89cc-208">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="f89cc-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89cc-209">Aanmelden tooyour Pingboard bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f89cc-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="f89cc-210">Klik op **'Werknemer toevoegen'** knop op **Directory** pagina.</span><span class="sxs-lookup"><span data-stu-id="f89cc-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="f89cc-212">Op Hallo **'Werknemer toevoegen'** dialoogvenster pagina, voert u Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="f89cc-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="f89cc-214">a.</span><span class="sxs-lookup"><span data-stu-id="f89cc-214">a.</span></span> <span data-ttu-id="f89cc-215">In Hallo **volledige naam** textbox Hallo volledige typenaam van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f89cc-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="f89cc-216">b.</span><span class="sxs-lookup"><span data-stu-id="f89cc-216">b.</span></span> <span data-ttu-id="f89cc-217">In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="f89cc-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="f89cc-218">c.</span><span class="sxs-lookup"><span data-stu-id="f89cc-218">c.</span></span> <span data-ttu-id="f89cc-219">In Hallo **taaktitel** textbox type Hallo-functie van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f89cc-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="f89cc-220">d.</span><span class="sxs-lookup"><span data-stu-id="f89cc-220">d.</span></span> <span data-ttu-id="f89cc-221">In Hallo **locatie** vervolgkeuzelijst, selecteer Hallo-locatie van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f89cc-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="f89cc-222">e.</span><span class="sxs-lookup"><span data-stu-id="f89cc-222">e.</span></span> <span data-ttu-id="f89cc-223">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-223">Click **Add**.</span></span>   

4. <span data-ttu-id="f89cc-224">Tooconfirm hello toevoeging van de gebruiker wordt een bevestigingsvenster komen.</span><span class="sxs-lookup"><span data-stu-id="f89cc-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![Bevestigen](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="f89cc-226">Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="f89cc-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f89cc-227">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f89cc-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f89cc-228">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooPingboard toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="f89cc-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f89cc-230">**tooassign Britta Simon tooPingboard, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f89cc-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="f89cc-231">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f89cc-233">Selecteer in de lijst met de toepassingen van Hallo **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-233">In hello applications list, select **Pingboard**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="f89cc-235">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f89cc-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f89cc-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f89cc-237">Click **Add** button.</span></span> <span data-ttu-id="f89cc-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f89cc-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f89cc-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f89cc-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f89cc-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f89cc-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f89cc-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f89cc-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f89cc-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f89cc-243">Testing single sign-on</span></span>

<span data-ttu-id="f89cc-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f89cc-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f89cc-245">Als u op Hallo Pingboard tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Pingboard toepassing.</span><span class="sxs-lookup"><span data-stu-id="f89cc-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f89cc-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f89cc-246">Additional resources</span></span>

* [<span data-ttu-id="f89cc-247">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f89cc-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f89cc-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f89cc-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
