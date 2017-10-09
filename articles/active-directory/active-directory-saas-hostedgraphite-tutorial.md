---
title: 'Zelfstudie: Azure Active Directory-integratie met gehost grafiek | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en de grafiek die worden gehost.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="6dd7a-103">Zelfstudie: Azure Active Directory-integratie met gehoste-grafiek</span><span class="sxs-lookup"><span data-stu-id="6dd7a-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="6dd7a-104">In deze zelfstudie leert u hoe toointegrate gehoste grafiek met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6dd7a-104">In this tutorial, you learn how toointegrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6dd7a-105">Grafiek gehost integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-105">Integrating Hosted Graphite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6dd7a-106">U kunt beheren in Azure AD wie toegang tot tooHosted grafiek heeft</span><span class="sxs-lookup"><span data-stu-id="6dd7a-106">You can control in Azure AD who has access tooHosted Graphite</span></span>
- <span data-ttu-id="6dd7a-107">U kunt uw gebruikers tooautomatically get aangemelde tooHosted grafiek (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6dd7a-107">You can enable your users tooautomatically get signed-on tooHosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6dd7a-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6dd7a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6dd7a-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6dd7a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dd7a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6dd7a-110">Prerequisites</span></span>

<span data-ttu-id="6dd7a-111">tooconfigure Azure AD-integratie met grafiek gehost, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-111">tooconfigure Azure AD integration with Hosted Graphite, you need hello following items:</span></span>

- <span data-ttu-id="6dd7a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6dd7a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6dd7a-113">Een grafiek gehost eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6dd7a-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6dd7a-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6dd7a-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6dd7a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6dd7a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6dd7a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6dd7a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6dd7a-118">Scenario description</span></span>
<span data-ttu-id="6dd7a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6dd7a-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6dd7a-121">Het toevoegen van grafiek gehost van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6dd7a-121">Adding Hosted Graphite from hello gallery</span></span>
2. <span data-ttu-id="6dd7a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6dd7a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-hello-gallery"></a><span data-ttu-id="6dd7a-123">Het toevoegen van grafiek gehost van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6dd7a-123">Adding Hosted Graphite from hello gallery</span></span>
<span data-ttu-id="6dd7a-124">tooconfigure hello integratie van de grafiek die worden gehost in Azure AD, moet u tooadd gehoste grafiek uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-124">tooconfigure hello integration of Hosted Graphite into Azure AD, you need tooadd Hosted Graphite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6dd7a-125">**tooadd gehoste grafiek via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6dd7a-125">**tooadd Hosted Graphite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dd7a-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6dd7a-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6dd7a-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6dd7a-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6dd7a-133">Typ in het zoekvak Hallo **grafiek gehost**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-133">In hello search box, type **Hosted Graphite**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="6dd7a-135">Selecteer in het deelvenster resultaten hello, **grafiek gehost**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-135">In hello results panel, select **Hosted Graphite**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6dd7a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6dd7a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6dd7a-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met gehost grafiek op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6dd7a-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de grafiek gehost is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hosted Graphite is tooa user in Azure AD.</span></span> <span data-ttu-id="6dd7a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de grafiek gehost Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-140">In other words, a link relationship between an Azure AD user and hello related user in Hosted Graphite needs toobe established.</span></span>

<span data-ttu-id="6dd7a-141">In de grafiek gehost Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-141">In Hosted Graphite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6dd7a-142">tooconfigure en eenmalige aanmelding Azure AD-test met grafiek gehost, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-142">tooconfigure and test Azure AD single sign-on with Hosted Graphite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6dd7a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6dd7a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6dd7a-145">**[Maken van een gehost grafiek testgebruiker](#creating-a-hosted-graphite-test-user)**  -toohave een equivalent van Britta Simon in gehost grafiek die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - toohave a counterpart of Britta Simon in Hosted Graphite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6dd7a-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6dd7a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6dd7a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6dd7a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6dd7a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing grafiek gehost.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="6dd7a-150">**Voer tooconfigure Azure AD eenmalige aanmelding met gehost grafiek Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6dd7a-150">**tooconfigure Azure AD single sign-on with Hosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dd7a-151">In Azure-portal op Hallo Hallo **grafiek gehost** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-151">In hello Azure portal, on hello **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6dd7a-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="6dd7a-155">Op Hallo **grafiek domein gehost en URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-155">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="6dd7a-157">a.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-157">a.</span></span> <span data-ttu-id="6dd7a-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="6dd7a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="6dd7a-159">b.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-159">b.</span></span> <span data-ttu-id="6dd7a-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="6dd7a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="6dd7a-161">Op Hallo **grafiek domein gehost en URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-161">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="6dd7a-163">a.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-163">a.</span></span> <span data-ttu-id="6dd7a-164">Klik op Hallo **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="6dd7a-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="6dd7a-165">b.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-165">b.</span></span> <span data-ttu-id="6dd7a-166">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="6dd7a-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="6dd7a-167">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="6dd7a-168">U hebt tooupdate deze waarden Hello werkelijke id, antwoord-URL's en meld u op.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-168">You have tooupdate these values with hello actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="6dd7a-169">tooget deze waarden, gaat u tooAccess -> SAML setup op uw toepassing aan clientzijde of neem contact op met [grafiek gehost ondersteuningsteam](mailto:help@hostedgraphite.com).</span><span class="sxs-lookup"><span data-stu-id="6dd7a-169">tooget these values, you can go tooAccess->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="6dd7a-170">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="6dd7a-172">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-172">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6dd7a-174">Op Hallo **gehost grafiek configuratie** sectie, klikt u op **gehost grafiek configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-174">On hello **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6dd7a-175">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6dd7a-175">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="6dd7a-177">Eenmalige aanmelding tooyour gehost grafiek tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-177">Sign-on tooyour Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="6dd7a-178">Ga toohello **SAML installatiepagina** in de zijbalk hello (**toegang SAML-instellingen ->**).</span><span class="sxs-lookup"><span data-stu-id="6dd7a-178">Go toohello **SAML Setup page** in hello sidebar (**Access -> SAML Setup**).</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="6dd7a-180">Bevestig deze URL's overeenkomen met uw configuratie uitgevoerd op Hallo **grafiek domein gehost en URL's** sectie Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-180">Confirm these URls match your configuration done on hello **Hosted Graphite Domain and URLs** section of hello Azure portal.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="6dd7a-182">In **entiteit of ID van de verlener** en **aanmeldings-URL voor eenmalige aanmelding** tekstvakken, plak Hallo-waarde van **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste hello value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="6dd7a-184">Selecteer "**alleen-lezen**' als **standaard gebruikersrol**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="6dd7a-186">De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="6dd7a-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="6dd7a-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6dd7a-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6dd7a-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6dd7a-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6dd7a-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6dd7a-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6dd7a-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6dd7a-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6dd7a-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dd7a-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6dd7a-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6dd7a-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6dd7a-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6dd7a-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6dd7a-204">a.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-204">a.</span></span> <span data-ttu-id="6dd7a-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6dd7a-206">b.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-206">b.</span></span> <span data-ttu-id="6dd7a-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6dd7a-208">c.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-208">c.</span></span> <span data-ttu-id="6dd7a-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6dd7a-210">d.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-210">d.</span></span> <span data-ttu-id="6dd7a-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="6dd7a-212">Een grafiek gehost testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6dd7a-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="6dd7a-213">Hallo-doel van deze sectie is toocreate een gebruiker Britta Simon aangeroepen in de grafiek die worden gehost.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-213">hello objective of this section is toocreate a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="6dd7a-214">Gehoste grafiek ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6dd7a-215">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-215">There is no action item for you in this section.</span></span> <span data-ttu-id="6dd7a-216">Een nieuwe gebruiker wordt tijdens een poging tooaccess gehoste grafiek worden gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-216">A new user will be created during an attempt tooaccess Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6dd7a-217">Als u handmatig een gebruiker toocreate nodig, moet u toocontact Hallo gehost grafiek ondersteuningsteam via < mailto:help@hostedgraphite.com >.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-217">If you need toocreate a user manually, you need toocontact hello Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6dd7a-218">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6dd7a-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6dd7a-219">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooHosted grafiek.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHosted Graphite.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6dd7a-221">**tooassign Britta Simon tooHosted grafiek, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6dd7a-221">**tooassign Britta Simon tooHosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dd7a-222">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6dd7a-224">Selecteer in de lijst met de toepassingen van Hallo **grafiek gehost**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-224">In hello applications list, select **Hosted Graphite**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="6dd7a-226">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6dd7a-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-228">Click **Add** button.</span></span> <span data-ttu-id="6dd7a-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6dd7a-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6dd7a-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6dd7a-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6dd7a-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6dd7a-234">Testing single sign-on</span></span>

<span data-ttu-id="6dd7a-235">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="6dd7a-236">Als u op Hallo gehost grafiek tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour grafiek gehoste toepassing.</span><span class="sxs-lookup"><span data-stu-id="6dd7a-236">When you click hello Hosted Graphite tile in hello Access Panel, you should get automatically signed-on tooyour Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6dd7a-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6dd7a-237">Additional resources</span></span>

* [<span data-ttu-id="6dd7a-238">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6dd7a-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6dd7a-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6dd7a-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

