---
title: 'Zelfstudie: Azure Active Directory-integratie met EverBridge | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en EverBridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="dc827-103">Zelfstudie: Azure Active Directory-integratie met EverBridge</span><span class="sxs-lookup"><span data-stu-id="dc827-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="dc827-104">In deze zelfstudie leert u hoe toointegrate EverBridge met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc827-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc827-105">EverBridge integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="dc827-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dc827-106">U kunt beheren in Azure AD die tooEverBridge toegang heeft</span><span class="sxs-lookup"><span data-stu-id="dc827-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="dc827-107">U kunt uw gebruikers tooautomatically get aangemelde tooEverBridge (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="dc827-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc827-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="dc827-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dc827-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc827-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc827-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dc827-110">Prerequisites</span></span>

<span data-ttu-id="dc827-111">Azure AD-integratie met EverBridge tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="dc827-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="dc827-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="dc827-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc827-113">Een EverBridge eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="dc827-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc827-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="dc827-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc827-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="dc827-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc827-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="dc827-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc827-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc827-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc827-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="dc827-118">Scenario description</span></span>
<span data-ttu-id="dc827-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="dc827-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc827-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="dc827-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc827-121">Het toevoegen van EverBridge van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dc827-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="dc827-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dc827-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="dc827-123">Het toevoegen van EverBridge van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dc827-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="dc827-124">tooconfigure hello integratie van EverBridge in Azure AD, moet u tooadd EverBridge uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="dc827-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dc827-125">**tooadd EverBridge via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dc827-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc827-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dc827-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc827-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dc827-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dc827-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dc827-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="dc827-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dc827-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="dc827-133">Typ in het zoekvak Hallo **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="dc827-133">In hello search box, type **EverBridge**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="dc827-135">Selecteer in het deelvenster resultaten hello, **EverBridge**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dc827-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc827-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dc827-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc827-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met EverBridge op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="dc827-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc827-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in EverBridge is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc827-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="dc827-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in EverBridge toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="dc827-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="dc827-141">Wijs in EverBridge, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="dc827-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dc827-142">tooconfigure en eenmalige aanmelding Azure AD-test met EverBridge, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc827-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dc827-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="dc827-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dc827-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc827-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc827-145">**[Maken van een testgebruiker EverBridge](#creating-an-everbridge-test-user)**  -toohave een equivalent van Britta Simon in EverBridge die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dc827-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc827-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dc827-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc827-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="dc827-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc827-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="dc827-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc827-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing EverBridge configureren.</span><span class="sxs-lookup"><span data-stu-id="dc827-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="dc827-150">**Azure AD tooconfigure eenmalige aanmelding met EverBridge, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dc827-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc827-151">In de Azure-portal op Hallo Hallo **EverBridge** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="dc827-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="dc827-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dc827-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="dc827-155">Op Hallo **EverBridge domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc827-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="dc827-157">a.</span><span class="sxs-lookup"><span data-stu-id="dc827-157">a.</span></span> <span data-ttu-id="dc827-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="dc827-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="dc827-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc827-159">b.</span></span> <span data-ttu-id="dc827-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="dc827-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc827-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="dc827-161">These values are not real.</span></span> <span data-ttu-id="dc827-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="dc827-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="dc827-163">Neem contact op met [EverBridge ondersteuningsteam](mailto:support@everbridge.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="dc827-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="dc827-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="dc827-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="dc827-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="dc827-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dc827-168">Op Hallo **EverBridge configuratie** sectie, klikt u op **configureren EverBridge** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="dc827-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dc827-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="dc827-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="dc827-171">tooget SSO is geconfigureerd voor uw toepassing, moet u toosign op tooyour Everbridge tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="dc827-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="dc827-172">Klik op Hallo in het menu bovenaan Hallo Hallo **instellingen** tabblad en selecteer **Single Sign-On** onder **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="dc827-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="dc827-174">a.</span><span class="sxs-lookup"><span data-stu-id="dc827-174">a.</span></span> <span data-ttu-id="dc827-175">In Hallo **naam** textbox Hallo-typenaam van de id-Provider (bijvoorbeeld: naam van uw bedrijf).</span><span class="sxs-lookup"><span data-stu-id="dc827-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="dc827-176">b.</span><span class="sxs-lookup"><span data-stu-id="dc827-176">b.</span></span> <span data-ttu-id="dc827-177">In Hallo **API-naam** textbox Hallo-typenaam van de API.</span><span class="sxs-lookup"><span data-stu-id="dc827-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="dc827-178">c.</span><span class="sxs-lookup"><span data-stu-id="dc827-178">c.</span></span> <span data-ttu-id="dc827-179">Klik op **bestand kiezen** knop tooupload Hallo bestand met metagegevens die u hebt gedownload van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dc827-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="dc827-180">d.</span><span class="sxs-lookup"><span data-stu-id="dc827-180">d.</span></span> <span data-ttu-id="dc827-181">Selecteer in de Hallo SAML identiteit locatie, **identiteit is in Hallo NameIdentifier element van Hallo onderwerp instructie**.</span><span class="sxs-lookup"><span data-stu-id="dc827-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="dc827-182">e.</span><span class="sxs-lookup"><span data-stu-id="dc827-182">e.</span></span> <span data-ttu-id="dc827-183">In Hallo **identiteit Provider aanmeldings-URL** textbox plakken Hallo-waarde van SAML SSO-URL van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc827-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="dc827-185">f.</span><span class="sxs-lookup"><span data-stu-id="dc827-185">f.</span></span> <span data-ttu-id="dc827-186">Selecteer in het Hallo-Provider geïnitieerd aanvragen servicebinding, **HTTP-omleiding**.</span><span class="sxs-lookup"><span data-stu-id="dc827-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="dc827-187">g.</span><span class="sxs-lookup"><span data-stu-id="dc827-187">g.</span></span> <span data-ttu-id="dc827-188">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="dc827-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="dc827-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="dc827-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dc827-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="dc827-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dc827-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc827-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc827-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="dc827-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc827-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="dc827-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="dc827-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dc827-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc827-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dc827-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc827-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="dc827-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc827-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="dc827-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc827-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc827-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc827-204">a.</span><span class="sxs-lookup"><span data-stu-id="dc827-204">a.</span></span> <span data-ttu-id="dc827-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc827-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc827-206">b.</span><span class="sxs-lookup"><span data-stu-id="dc827-206">b.</span></span> <span data-ttu-id="dc827-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc827-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc827-208">c.</span><span class="sxs-lookup"><span data-stu-id="dc827-208">c.</span></span> <span data-ttu-id="dc827-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="dc827-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dc827-210">d.</span><span class="sxs-lookup"><span data-stu-id="dc827-210">d.</span></span> <span data-ttu-id="dc827-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc827-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="dc827-212">Een testgebruiker EverBridge maken</span><span class="sxs-lookup"><span data-stu-id="dc827-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="dc827-213">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Everbridge maken.</span><span class="sxs-lookup"><span data-stu-id="dc827-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="dc827-214">Werken met [EverBridge ondersteuningsteam](mailto:support@everbridge.com) tooadd Hallo gebruikers in Hallo Everbridge platform.</span><span class="sxs-lookup"><span data-stu-id="dc827-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dc827-215">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc827-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dc827-216">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEverBridge toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="dc827-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="dc827-218">**tooassign Britta Simon tooEverBridge, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dc827-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc827-219">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dc827-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="dc827-221">Selecteer in de lijst met de toepassingen van Hallo **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="dc827-221">In hello applications list, select **EverBridge**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="dc827-223">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="dc827-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="dc827-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="dc827-225">Click **Add** button.</span></span> <span data-ttu-id="dc827-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dc827-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="dc827-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc827-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dc827-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dc827-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc827-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dc827-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc827-231">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dc827-231">Testing single sign-on</span></span>

<span data-ttu-id="dc827-232">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="dc827-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dc827-233">Als u op Hallo Everbridge tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Everbridge toepassing.</span><span class="sxs-lookup"><span data-stu-id="dc827-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc827-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="dc827-234">Additional resources</span></span>

* [<span data-ttu-id="dc827-235">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc827-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc827-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc827-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

