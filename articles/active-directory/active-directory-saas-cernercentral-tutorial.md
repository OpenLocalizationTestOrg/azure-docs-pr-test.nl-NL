---
title: 'Zelfstudie: Azure Active Directory-integratie met centraal Cerner | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Cerner centraal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="db17c-103">Zelfstudie: Azure Active Directory-integratie met Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="db17c-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="db17c-104">In deze zelfstudie leert u hoe toointegrate Cerner centraal met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="db17c-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db17c-105">Cerner centraal integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="db17c-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="db17c-106">U kunt beheren in Azure AD wie toegang tot tooCerner centraal heeft</span><span class="sxs-lookup"><span data-stu-id="db17c-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="db17c-107">U kunt uw gebruikers tooautomatically get aangemelde tooCerner centraal (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="db17c-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db17c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="db17c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="db17c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="db17c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db17c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="db17c-110">Prerequisites</span></span>

<span data-ttu-id="db17c-111">Azure AD-integratie met centraal Cerner tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="db17c-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="db17c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="db17c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db17c-113">Een goedgekeurde Cerner centrale systeemaccount</span><span class="sxs-lookup"><span data-stu-id="db17c-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="db17c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="db17c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="db17c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="db17c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db17c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="db17c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="db17c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="db17c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="db17c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="db17c-118">Scenario description</span></span>
<span data-ttu-id="db17c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="db17c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db17c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="db17c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db17c-121">Het toevoegen van Cerner centraal van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="db17c-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="db17c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="db17c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="db17c-123">Het toevoegen van Cerner centraal van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="db17c-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="db17c-124">tooconfigure hello integratie van Cerner centraal in Azure AD, moet u tooadd Cerner centraal uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="db17c-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="db17c-125">**tooadd Cerner centraal via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="db17c-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="db17c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="db17c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db17c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="db17c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="db17c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="db17c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="db17c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop boven op Hallo dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="db17c-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="db17c-133">Typ in het zoekvak Hallo **Cerner centraal**.</span><span class="sxs-lookup"><span data-stu-id="db17c-133">In hello search box, type **Cerner Central**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="db17c-135">Selecteer in het deelvenster resultaten hello, **Cerner centraal**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="db17c-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db17c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="db17c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="db17c-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Cerner centraal op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="db17c-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="db17c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Cerner centrale is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db17c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="db17c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Cerner centrale toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="db17c-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="db17c-141">tooconfigure en eenmalige aanmelding Azure AD-test met Cerner centraal, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="db17c-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="db17c-142">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="db17c-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="db17c-143">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="db17c-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db17c-144">**[Maken van een testgebruiker Cerner centraal](#creating-a-cerner-central-test-user)**  -toohave een equivalent van Britta Simon in Cerner centrale die is gekoppeld toohello Azure AD-weergave van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="db17c-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="db17c-145">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="db17c-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="db17c-146">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="db17c-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db17c-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="db17c-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db17c-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Cerner centraal configureren.</span><span class="sxs-lookup"><span data-stu-id="db17c-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="db17c-149">**Voer tooconfigure Azure AD eenmalige aanmelding met Cerner centraal, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="db17c-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="db17c-150">In de Azure-portal op Hallo Hallo **Cerner centraal** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="db17c-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="db17c-152">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="db17c-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="db17c-154">Op Hallo **Cerner centrale domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="db17c-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="db17c-156">a.</span><span class="sxs-lookup"><span data-stu-id="db17c-156">a.</span></span> <span data-ttu-id="db17c-157">In Hallo **id** textbox Hallo typewaarde met Hallo patronen te volgen:</span><span class="sxs-lookup"><span data-stu-id="db17c-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="db17c-158">b.</span><span class="sxs-lookup"><span data-stu-id="db17c-158">b.</span></span> <span data-ttu-id="db17c-159">In Hallo **antwoord-URL** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="db17c-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="db17c-160">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="db17c-160">These values are not hello real.</span></span> <span data-ttu-id="db17c-161">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="db17c-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="db17c-162">Neem contact op met [Cerner centraal ondersteuningsteam](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="db17c-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="db17c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="db17c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="db17c-165">Hallo toogenerate **metagegevens** -url, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="db17c-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="db17c-166">a.</span><span class="sxs-lookup"><span data-stu-id="db17c-166">a.</span></span> <span data-ttu-id="db17c-167">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="db17c-167">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="db17c-169">b.</span><span class="sxs-lookup"><span data-stu-id="db17c-169">b.</span></span> <span data-ttu-id="db17c-170">Klik op **eindpunten** tooopen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="db17c-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="db17c-172">c.</span><span class="sxs-lookup"><span data-stu-id="db17c-172">c.</span></span> <span data-ttu-id="db17c-173">Klik op Hallo kopie knop toocopy **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="db17c-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="db17c-175">d.</span><span class="sxs-lookup"><span data-stu-id="db17c-175">d.</span></span> <span data-ttu-id="db17c-176">Ga nu toohello eigenschappenpagina van **Cerner centraal** en kopiëren Hallo **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="db17c-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="db17c-178">e.</span><span class="sxs-lookup"><span data-stu-id="db17c-178">e.</span></span> <span data-ttu-id="db17c-179">Hallo genereren **metagegevens-URL** met Hallo patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="db17c-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="db17c-180">tooconfigure eenmalige aanmelding op **Cerner centraal** clientzijde, moet u toosend hello **metagegevens-URL** te[Cerner centraal ondersteuning](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="db17c-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="db17c-181">Ze configureren Hallo eenmalige aanmelding op de integratie van toepassingen aan clientzijde toocomplete Hallo.</span><span class="sxs-lookup"><span data-stu-id="db17c-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="db17c-182">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="db17c-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="db17c-183">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="db17c-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="db17c-184">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="db17c-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db17c-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="db17c-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="db17c-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="db17c-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Azure AD-gebruiker maken][100]

<span data-ttu-id="db17c-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="db17c-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="db17c-189">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="db17c-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db17c-191">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="db17c-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db17c-193">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="db17c-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db17c-195">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="db17c-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db17c-197">a.</span><span class="sxs-lookup"><span data-stu-id="db17c-197">a.</span></span> <span data-ttu-id="db17c-198">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="db17c-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db17c-199">b.</span><span class="sxs-lookup"><span data-stu-id="db17c-199">b.</span></span> <span data-ttu-id="db17c-200">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="db17c-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="db17c-201">c.</span><span class="sxs-lookup"><span data-stu-id="db17c-201">c.</span></span> <span data-ttu-id="db17c-202">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="db17c-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="db17c-203">d.</span><span class="sxs-lookup"><span data-stu-id="db17c-203">d.</span></span> <span data-ttu-id="db17c-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="db17c-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="db17c-205">Maken van een testgebruiker Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="db17c-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="db17c-206">**Cerner centraal** toepassing kunt verificatie van elke provider federatieve identiteiten.</span><span class="sxs-lookup"><span data-stu-id="db17c-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="db17c-207">Als een gebruiker kan toolog in toohello toepassing startpagina is, wordt deze federatieve zijn en niet nodig is voor handmatige inrichting.</span><span class="sxs-lookup"><span data-stu-id="db17c-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="db17c-208">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="db17c-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="db17c-209">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCerner centraal.</span><span class="sxs-lookup"><span data-stu-id="db17c-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="db17c-211">**tooassign Britta Simon tooCerner centraal, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="db17c-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="db17c-212">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="db17c-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="db17c-214">Selecteer in de lijst met de toepassingen van Hallo **Cerner centraal**.</span><span class="sxs-lookup"><span data-stu-id="db17c-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="db17c-216">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="db17c-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="db17c-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="db17c-218">Click **Add** button.</span></span> <span data-ttu-id="db17c-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="db17c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="db17c-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="db17c-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="db17c-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="db17c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db17c-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="db17c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="db17c-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="db17c-224">Testing single sign-on</span></span>

<span data-ttu-id="db17c-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="db17c-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="db17c-226">Als u op Hallo Cerner centraal-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Cerner centrale toepassing.</span><span class="sxs-lookup"><span data-stu-id="db17c-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="db17c-227">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="db17c-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db17c-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="db17c-228">Additional resources</span></span>

* [<span data-ttu-id="db17c-229">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db17c-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db17c-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="db17c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

