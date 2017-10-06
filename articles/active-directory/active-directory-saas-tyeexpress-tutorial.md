---
title: 'Zelfstudie: Azure Active Directory-integratie met T & E Express | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en T & E Express.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="140e7-103">Zelfstudie: Azure Active Directory-integratie met T & E Express</span><span class="sxs-lookup"><span data-stu-id="140e7-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="140e7-104">In deze zelfstudie leert u hoe toointegrate d & E Express met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="140e7-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="140e7-105">D & E Express integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="140e7-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="140e7-106">U kunt beheren in Azure AD wie toegang tot tooT heeft & E Express</span><span class="sxs-lookup"><span data-stu-id="140e7-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="140e7-107">U kunt uw gebruikers tooautomatically get aangemelde tooT & E Express (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="140e7-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="140e7-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="140e7-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="140e7-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="140e7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="140e7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="140e7-110">Prerequisites</span></span>

<span data-ttu-id="140e7-111">Azure AD-integratie met T & E Express tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="140e7-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="140e7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="140e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="140e7-113">Een d & E Express eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="140e7-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="140e7-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="140e7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="140e7-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="140e7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="140e7-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="140e7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="140e7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="140e7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="140e7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="140e7-118">Scenario description</span></span>
<span data-ttu-id="140e7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="140e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="140e7-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="140e7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="140e7-121">D & E Express uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="140e7-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="140e7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="140e7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="140e7-123">D & E Express uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="140e7-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="140e7-124">tooconfigure hello integratie van d & E Express in Azure AD, moet u tooadd T & E Express uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="140e7-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="140e7-125">**tooadd T & E Express uit de galerie hello, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="140e7-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="140e7-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="140e7-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="140e7-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="140e7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="140e7-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="140e7-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="140e7-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="140e7-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="140e7-133">Typ in het zoekvak Hallo **d & E Express**.</span><span class="sxs-lookup"><span data-stu-id="140e7-133">In hello search box, type **T&E Express**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="140e7-135">Selecteer in het deelvenster resultaten hello, **d & E Express**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="140e7-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="140e7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="140e7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="140e7-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met T & E Express op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="140e7-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="140e7-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de T & E Express is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="140e7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="140e7-140">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in d & E Express behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="140e7-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="140e7-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in d & E Express.</span><span class="sxs-lookup"><span data-stu-id="140e7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="140e7-142">tooconfigure en test eenmalige aanmelding Azure AD met behulp van d & E Express, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="140e7-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="140e7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="140e7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="140e7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="140e7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="140e7-145">**[Maken van een testgebruiker d & E Express](#creating-a-te-express-test-user)**  -toohave een equivalent van Britta Simon in d & E Express die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="140e7-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="140e7-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="140e7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="140e7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="140e7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="140e7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="140e7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="140e7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing d & E Express.</span><span class="sxs-lookup"><span data-stu-id="140e7-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="140e7-150">**tooconfigure eenmalige aanmelding Azure AD met T & E Express, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="140e7-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="140e7-151">In hello Azure Management portal op Hallo **d & E Express** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="140e7-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="140e7-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="140e7-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="140e7-155">Op Hallo **T & E Express domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="140e7-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="140e7-157">a.</span><span class="sxs-lookup"><span data-stu-id="140e7-157">a.</span></span> <span data-ttu-id="140e7-158">In Hallo **id** textbox Hallo typewaarde als:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="140e7-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="140e7-159">b.</span><span class="sxs-lookup"><span data-stu-id="140e7-159">b.</span></span> <span data-ttu-id="140e7-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="140e7-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="140e7-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="140e7-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="140e7-162">U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="140e7-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="140e7-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="140e7-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="140e7-164">Neem contact op met [d & E Express ondersteuningsteam](http://www.tyeexpress.com/contacto.aspx) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="140e7-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="140e7-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="140e7-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="140e7-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="140e7-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="140e7-169">tooconfigure eenmalige aanmelding op **d & E snelle** aan clientzijde, aanmelding toohello T & E snelle toepassing zonder SAML eenmalige over het gebruik van beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="140e7-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="140e7-170">Onder Hallo **Admin** tabblad, klikt u op **SAML domein** tooOpen Hallo SAML instellingenpagina.</span><span class="sxs-lookup"><span data-stu-id="140e7-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="140e7-172">Selecteer Hallo **Activar(Activate)** optie van **Nee** te**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="140e7-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="140e7-173">In Hallo **identiteit Provider metagegevens** textbox plakken Hallo metagegevens XML, die u hebt donwloaded vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="140e7-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="140e7-175">Klik op Hallo **Guardar(Save)** knop toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="140e7-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="140e7-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="140e7-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="140e7-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="140e7-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="140e7-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="140e7-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="140e7-180">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="140e7-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="140e7-182">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="140e7-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="140e7-184">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="140e7-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="140e7-186">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="140e7-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="140e7-188">a.</span><span class="sxs-lookup"><span data-stu-id="140e7-188">a.</span></span> <span data-ttu-id="140e7-189">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="140e7-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="140e7-190">b.</span><span class="sxs-lookup"><span data-stu-id="140e7-190">b.</span></span> <span data-ttu-id="140e7-191">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="140e7-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="140e7-192">c.</span><span class="sxs-lookup"><span data-stu-id="140e7-192">c.</span></span> <span data-ttu-id="140e7-193">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="140e7-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="140e7-194">d.</span><span class="sxs-lookup"><span data-stu-id="140e7-194">d.</span></span> <span data-ttu-id="140e7-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="140e7-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="140e7-196">Maken van een testgebruiker d & E Express</span><span class="sxs-lookup"><span data-stu-id="140e7-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="140e7-197">In volgorde tooenable Azure AD gebruikers toolog in d & E Express, moeten ze worden ingericht in d & E Express.</span><span class="sxs-lookup"><span data-stu-id="140e7-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="140e7-198">In geval van een T & E Express is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="140e7-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="140e7-199">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="140e7-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="140e7-200">Meld u in de tooyour T & E Express bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="140e7-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="140e7-201">Klik op gebruikers tooopen Hallo gebruikers basispagina onder Admin-tag.</span><span class="sxs-lookup"><span data-stu-id="140e7-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="140e7-203">Klik op de startpagina van Hallo op  **+**  tooadd Hallo gebruikers.</span><span class="sxs-lookup"><span data-stu-id="140e7-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="140e7-205">Alle verplichte Hallo-details in Hallo vorm gevraagd en klik op Hallo opslaan knop toosave Hallo details.</span><span class="sxs-lookup"><span data-stu-id="140e7-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="140e7-208">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="140e7-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="140e7-209">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooT & E Express verlenen.</span><span class="sxs-lookup"><span data-stu-id="140e7-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="140e7-211">**tooassign Britta Simon tooT & E Express, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="140e7-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="140e7-212">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="140e7-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="140e7-214">Selecteer in de lijst met de toepassingen van Hallo **d & E Express**.</span><span class="sxs-lookup"><span data-stu-id="140e7-214">In hello applications list, select **T&E Express**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="140e7-216">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="140e7-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="140e7-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="140e7-218">Click **Add** button.</span></span> <span data-ttu-id="140e7-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="140e7-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="140e7-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="140e7-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="140e7-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="140e7-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="140e7-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="140e7-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="140e7-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="140e7-224">Testing single sign-on</span></span>

<span data-ttu-id="140e7-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="140e7-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="140e7-226">Als u klikt op Hallo T & E Express-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour T & E Express-toepassing.</span><span class="sxs-lookup"><span data-stu-id="140e7-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="140e7-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="140e7-227">Additional resources</span></span>

* [<span data-ttu-id="140e7-228">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="140e7-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="140e7-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="140e7-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

