---
title: 'Zelfstudie: Azure Active Directory-integratie met Land echte reus Client | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en echte reus Land.
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="801cc-103">Zelfstudie: Azure Active Directory-integratie met Land echte reus Client</span><span class="sxs-lookup"><span data-stu-id="801cc-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="801cc-104">In deze zelfstudie leert u hoe toointegrate Land echte reus Client met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="801cc-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="801cc-105">Land echte reus Client integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="801cc-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="801cc-106">U kunt beheren in Azure AD wie toegang tot tooLand echte reus Client heeft</span><span class="sxs-lookup"><span data-stu-id="801cc-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="801cc-107">U kunt uw gebruikers tooautomatically get aangemelde tooLand echte reus Client (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="801cc-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="801cc-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="801cc-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="801cc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="801cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="801cc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="801cc-110">Prerequisites</span></span>

<span data-ttu-id="801cc-111">Azure AD-integratie met Land echte reus Client tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="801cc-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="801cc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="801cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="801cc-113">Een Land echte reus Client eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="801cc-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="801cc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="801cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="801cc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="801cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="801cc-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="801cc-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="801cc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="801cc-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="801cc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="801cc-118">Scenario description</span></span>
<span data-ttu-id="801cc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="801cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="801cc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="801cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="801cc-121">Toevoegen van Land echte reus Client vanuit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="801cc-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="801cc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="801cc-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="801cc-123">Toevoegen van Land echte reus Client vanuit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="801cc-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="801cc-124">tooconfigure hello integratie van Land echte reus Client in Azure AD, moet u tooadd Land echte reus Client Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="801cc-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="801cc-125">**tooadd Land echte reus Client via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="801cc-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="801cc-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="801cc-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="801cc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="801cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="801cc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="801cc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="801cc-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="801cc-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="801cc-133">Typ in het zoekvak Hallo **Land echte reus Client**.</span><span class="sxs-lookup"><span data-stu-id="801cc-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="801cc-135">Selecteer in het deelvenster resultaten hello, **Land echte reus Client**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="801cc-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="801cc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="801cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="801cc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Land echte reus-Client op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="801cc-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="801cc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Land echte reus-Client is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="801cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="801cc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Land echte reus Client toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="801cc-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="801cc-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Land echte reus-Client.</span><span class="sxs-lookup"><span data-stu-id="801cc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="801cc-142">tooconfigure en test eenmalige aanmelding Azure AD met Land echte reus Client, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="801cc-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="801cc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="801cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="801cc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met beperkte groep.</span><span class="sxs-lookup"><span data-stu-id="801cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="801cc-145">**[Maken van een testgebruiker Land echte reus](#creating-a-land-gorilla-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="801cc-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="801cc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="801cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="801cc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="801cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="801cc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="801cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="801cc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw Land echte reus Client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="801cc-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="801cc-150">**tooconfigure eenmalige aanmelding Azure AD met Land echte reus Client, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="801cc-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="801cc-151">In hello Azure Management portal op Hallo **Land echte reus Client** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="801cc-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="801cc-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="801cc-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="801cc-155">Op Hallo **Land echte reus clientdomein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="801cc-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="801cc-157">a.</span><span class="sxs-lookup"><span data-stu-id="801cc-157">a.</span></span> <span data-ttu-id="801cc-158">In Hallo **id** textbox Hallo typewaarde met behulp van een Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="801cc-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="801cc-159">b.</span><span class="sxs-lookup"><span data-stu-id="801cc-159">b.</span></span> <span data-ttu-id="801cc-160">In Hallo **antwoord-URL** textbox, typ een URL met een Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="801cc-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="801cc-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="801cc-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="801cc-162">U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="801cc-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="801cc-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="801cc-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="801cc-164">Neem contact op met [Land echte reus Client team](https://www.landgorilla.com/support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="801cc-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="801cc-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="801cc-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="801cc-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="801cc-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="801cc-169">tooget SSO configuratie voltooid voor uw toepassing aan het einde van Land echte reus Contact [Land echte reus Client ondersteuningsteam](https://www.landgorilla.com/support/) en voorzien Hallo gedownload **' Metadata XML** bestand.</span><span class="sxs-lookup"><span data-stu-id="801cc-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="801cc-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="801cc-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="801cc-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="801cc-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="801cc-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="801cc-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="801cc-174">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="801cc-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="801cc-176">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="801cc-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="801cc-178">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="801cc-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="801cc-180">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="801cc-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="801cc-182">a.</span><span class="sxs-lookup"><span data-stu-id="801cc-182">a.</span></span> <span data-ttu-id="801cc-183">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="801cc-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="801cc-184">b.</span><span class="sxs-lookup"><span data-stu-id="801cc-184">b.</span></span> <span data-ttu-id="801cc-185">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="801cc-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="801cc-186">c.</span><span class="sxs-lookup"><span data-stu-id="801cc-186">c.</span></span> <span data-ttu-id="801cc-187">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="801cc-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="801cc-188">d.</span><span class="sxs-lookup"><span data-stu-id="801cc-188">d.</span></span> <span data-ttu-id="801cc-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="801cc-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="801cc-190">Maken van een echte reus Land testgebruiker</span><span class="sxs-lookup"><span data-stu-id="801cc-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="801cc-191">Neem contact op met [Land echte reus ondersteuningsteam](https://www.landgorilla.com/support/) tooadd Hallo gebruikers in Hallo Land echte reus platform.</span><span class="sxs-lookup"><span data-stu-id="801cc-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="801cc-192">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="801cc-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="801cc-193">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooLand echte reus Client verlenen.</span><span class="sxs-lookup"><span data-stu-id="801cc-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="801cc-195">**tooassign Britta Simon tooLand echte reus Client, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="801cc-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="801cc-196">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="801cc-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="801cc-198">Selecteer in de lijst met de toepassingen van Hallo **Land echte reus Client**.</span><span class="sxs-lookup"><span data-stu-id="801cc-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="801cc-200">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="801cc-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="801cc-202">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="801cc-202">Click **Add** button.</span></span> <span data-ttu-id="801cc-203">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="801cc-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="801cc-205">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="801cc-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="801cc-206">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="801cc-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="801cc-207">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="801cc-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="801cc-208">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="801cc-208">Testing single sign-on</span></span>

<span data-ttu-id="801cc-209">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="801cc-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="801cc-210">Als u op Hallo Land echte reus Client tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Land echte reus Client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="801cc-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="801cc-211">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="801cc-211">Additional resources</span></span>

* [<span data-ttu-id="801cc-212">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="801cc-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="801cc-213">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="801cc-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
