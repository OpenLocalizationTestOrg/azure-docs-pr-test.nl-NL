---
title: 'Zelfstudie: Azure Active Directory-integratie met Springer koppeling | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Springer koppeling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="0a768-103">Zelfstudie: Azure Active Directory-integratie met Springer koppeling</span><span class="sxs-lookup"><span data-stu-id="0a768-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="0a768-104">In deze zelfstudie leert u hoe toointegrate Springer koppelen aan Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a768-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a768-105">Springer koppeling integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0a768-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a768-106">U kunt beheren in Azure AD die toegang tooSpringer koppeling heeft.</span><span class="sxs-lookup"><span data-stu-id="0a768-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="0a768-107">U kunt uw gebruikers tooautomatically get aangemelde tooSpringer koppeling (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0a768-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0a768-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="0a768-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0a768-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a768-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a768-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0a768-110">Prerequisites</span></span>

<span data-ttu-id="0a768-111">Azure AD-integratie met Springer koppeling tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0a768-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="0a768-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0a768-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a768-113">Een koppeling Springer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0a768-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a768-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0a768-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a768-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0a768-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a768-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0a768-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a768-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a768-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a768-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0a768-118">Scenario description</span></span>
<span data-ttu-id="0a768-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0a768-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a768-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0a768-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a768-121">Springer koppeling toe te voegen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0a768-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="0a768-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0a768-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="0a768-123">Springer koppeling toe te voegen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0a768-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="0a768-124">tooconfigure hello integratie van Springer koppeling met Azure AD, moet u tooadd Springer koppeling uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0a768-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a768-125">**tooadd Springer koppeling via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a768-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a768-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0a768-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="0a768-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0a768-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a768-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0a768-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="0a768-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a768-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="0a768-133">Typ in het zoekvak Hallo **Springer koppeling**, selecteer **Springer koppeling** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a768-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Springer koppeling in de lijst met resultaten Hallo](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0a768-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a768-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0a768-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Springer-koppeling die overeenkomt met een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0a768-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a768-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Springer koppeling is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a768-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="0a768-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Springer koppeling toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0a768-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="0a768-139">In Springer koppeling, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="0a768-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0a768-140">tooconfigure en test eenmalige aanmelding Azure AD met Springer koppeling, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a768-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a768-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0a768-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a768-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a768-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a768-143">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0a768-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="0a768-144">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0a768-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0a768-145">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0a768-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0a768-146">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Springer koppeling.</span><span class="sxs-lookup"><span data-stu-id="0a768-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="0a768-147">**Voer tooconfigure Azure AD eenmalige aanmelding met Springer-koppeling Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a768-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a768-148">In de Azure-portal op Hallo Hallo **Springer koppeling** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0a768-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0a768-150">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0a768-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="0a768-152">Op Hallo **Springer koppeling domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="0a768-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![URL's en Springer koppeling domein eenmalige aanmelding informatie](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="0a768-154">a.</span><span class="sxs-lookup"><span data-stu-id="0a768-154">a.</span></span> <span data-ttu-id="0a768-155">In Hallo **id** textbox type Hallo URL:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="0a768-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="0a768-156">b.</span><span class="sxs-lookup"><span data-stu-id="0a768-156">b.</span></span> <span data-ttu-id="0a768-157">In Hallo **antwoord-URL** textbox type Hallo URL:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="0a768-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="0a768-158">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="0a768-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="0a768-159">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="0a768-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![URL's en Springer koppeling domein eenmalige aanmelding informatie](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="0a768-161">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="0a768-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="0a768-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0a768-162">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a768-164">Hallo toogenerate **metagegevens** -url, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="0a768-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="0a768-165">a.</span><span class="sxs-lookup"><span data-stu-id="0a768-165">a.</span></span> <span data-ttu-id="0a768-166">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="0a768-166">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="0a768-168">b.</span><span class="sxs-lookup"><span data-stu-id="0a768-168">b.</span></span> <span data-ttu-id="0a768-169">Klik op **eindpunten** tooopen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a768-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="0a768-171">c.</span><span class="sxs-lookup"><span data-stu-id="0a768-171">c.</span></span> <span data-ttu-id="0a768-172">Klik op Hallo kopie knop toocopy **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="0a768-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="0a768-174">d.</span><span class="sxs-lookup"><span data-stu-id="0a768-174">d.</span></span> <span data-ttu-id="0a768-175">Ga nu toohello eigenschappenpagina van **Springer koppeling** en kopiëren Hallo **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="0a768-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="0a768-177">e.</span><span class="sxs-lookup"><span data-stu-id="0a768-177">e.</span></span> <span data-ttu-id="0a768-178">Hallo genereren **metagegevens-URL** met Hallo patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="0a768-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="0a768-179">tooconfigure eenmalige aanmelding op **Springer koppeling** zijde, moet u toosend Hallo gegenereerd **metagegevens-URL** te[Springer koppeling ondersteuningsteam](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="0a768-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="0a768-180">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="0a768-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a768-181">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="0a768-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a768-182">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a768-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0a768-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0a768-183">Create an Azure AD test user</span></span>

<span data-ttu-id="0a768-184">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0a768-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="0a768-186">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a768-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a768-187">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="0a768-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0a768-189">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0a768-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0a768-191">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a768-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0a768-193">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a768-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0a768-195">a.</span><span class="sxs-lookup"><span data-stu-id="0a768-195">a.</span></span> <span data-ttu-id="0a768-196">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a768-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a768-197">b.</span><span class="sxs-lookup"><span data-stu-id="0a768-197">b.</span></span> <span data-ttu-id="0a768-198">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="0a768-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0a768-199">c.</span><span class="sxs-lookup"><span data-stu-id="0a768-199">c.</span></span> <span data-ttu-id="0a768-200">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="0a768-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0a768-201">d.</span><span class="sxs-lookup"><span data-stu-id="0a768-201">d.</span></span> <span data-ttu-id="0a768-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0a768-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0a768-203">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a768-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0a768-204">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSpringer koppeling.</span><span class="sxs-lookup"><span data-stu-id="0a768-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="0a768-206">**tooassign Britta Simon tooSpringer koppeling Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0a768-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a768-207">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0a768-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0a768-209">Selecteer in de lijst met de toepassingen van Hallo **Springer koppeling**.</span><span class="sxs-lookup"><span data-stu-id="0a768-209">In hello applications list, select **Springer Link**.</span></span>

    ![Hallo Springer koppeling koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="0a768-211">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0a768-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="0a768-213">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0a768-213">Click **Add** button.</span></span> <span data-ttu-id="0a768-214">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a768-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="0a768-216">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a768-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a768-217">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a768-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a768-218">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a768-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0a768-219">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0a768-219">Test single sign-on</span></span>

<span data-ttu-id="0a768-220">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0a768-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a768-221">Als u op Hallo Springer koppeling tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Springer koppeling toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a768-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="0a768-222">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a768-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a768-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0a768-223">Additional resources</span></span>

* [<span data-ttu-id="0a768-224">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a768-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a768-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a768-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

