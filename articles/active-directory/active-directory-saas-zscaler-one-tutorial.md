---
title: "Zelfstudie: Azure Active Directory-integratie met één Zscaler | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en één Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 5179cb2cc54482334d574951a1ac64e722e5f578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a><span data-ttu-id="796d9-103">Zelfstudie: Azure Active Directory-integratie met één Zscaler</span><span class="sxs-lookup"><span data-stu-id="796d9-103">Tutorial: Azure Active Directory integration with Zscaler One</span></span>

<span data-ttu-id="796d9-104">In deze zelfstudie leert u hoe toointegrate één Zscaler met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="796d9-104">In this tutorial, you learn how toointegrate Zscaler One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="796d9-105">Een Zscaler integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="796d9-105">Integrating Zscaler One with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="796d9-106">U kunt beheren in Azure AD wie toegang tooZscaler een heeft</span><span class="sxs-lookup"><span data-stu-id="796d9-106">You can control in Azure AD who has access tooZscaler One</span></span>
- <span data-ttu-id="796d9-107">U kunt uw gebruikers tooautomatically get aangemelde tooZscaler een (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="796d9-107">You can enable your users tooautomatically get signed-on tooZscaler One (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="796d9-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="796d9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="796d9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="796d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="796d9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="796d9-110">Prerequisites</span></span>

<span data-ttu-id="796d9-111">Azure AD-integratie met één Zscaler tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="796d9-111">tooconfigure Azure AD integration with Zscaler One, you need hello following items:</span></span>

- <span data-ttu-id="796d9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="796d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="796d9-113">Een Zscaler een eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="796d9-113">A Zscaler One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="796d9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="796d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="796d9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="796d9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="796d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="796d9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="796d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="796d9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="796d9-118">Scenario description</span></span>
<span data-ttu-id="796d9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="796d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="796d9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="796d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="796d9-121">Het toevoegen van één Zscaler van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="796d9-121">Adding Zscaler One from hello gallery</span></span>
2. <span data-ttu-id="796d9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="796d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-one-from-hello-gallery"></a><span data-ttu-id="796d9-123">Het toevoegen van één Zscaler van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="796d9-123">Adding Zscaler One from hello gallery</span></span>
<span data-ttu-id="796d9-124">tooconfigure hello integratie van één Zscaler in Azure AD, moet u één Zscaler tooadd uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="796d9-124">tooconfigure hello integration of Zscaler One into Azure AD, you need tooadd Zscaler One from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="796d9-125">**tooadd Zscaler één via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="796d9-125">**tooadd Zscaler One from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="796d9-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="796d9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="796d9-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="796d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="796d9-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="796d9-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="796d9-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="796d9-133">Typ in het zoekvak Hallo **Zscaler één**.</span><span class="sxs-lookup"><span data-stu-id="796d9-133">In hello search box, type **Zscaler One**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. <span data-ttu-id="796d9-135">Selecteer in het deelvenster resultaten hello, **Zscaler één**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="796d9-135">In hello results panel, select **Zscaler One**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="796d9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="796d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="796d9-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Zscaler één, op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="796d9-138">In this section, you configure and test Azure AD single sign-on with Zscaler One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="796d9-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in één Zscaler is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="796d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler One is tooa user in Azure AD.</span></span> <span data-ttu-id="796d9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in één Zscaler toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="796d9-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler One needs toobe established.</span></span>

<span data-ttu-id="796d9-141">In één Zscaler, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="796d9-141">In Zscaler One, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="796d9-142">tooconfigure en eenmalige aanmelding Azure AD-test met één Zscaler, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-142">tooconfigure and test Azure AD single sign-on with Zscaler One, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="796d9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="796d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="796d9-144">**[Proxy-instellingen configureren](#configuring-proxy-settings)**  -tooconfigure Hallo proxy-instellingen in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="796d9-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="796d9-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="796d9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="796d9-146">**[Maken van een Zscaler een testgebruiker](#creating-a-zscaler-one-test-user)**  -toohave een equivalent van Britta Simon in Zscaler één die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="796d9-146">**[Creating a Zscaler One test user](#creating-a-zscaler-one-test-user)** - toohave a counterpart of Britta Simon in Zscaler One that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="796d9-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="796d9-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="796d9-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="796d9-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="796d9-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="796d9-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="796d9-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Zscaler één toepassing.</span><span class="sxs-lookup"><span data-stu-id="796d9-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler One application.</span></span>

<span data-ttu-id="796d9-151">**Voer tooconfigure Azure AD eenmalige aanmelding met een Zscaler, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="796d9-151">**tooconfigure Azure AD single sign-on with Zscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="796d9-152">In de Azure-portal op Hallo Hallo **Zscaler één** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="796d9-152">In hello Azure portal, on hello **Zscaler One** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="796d9-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="796d9-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. <span data-ttu-id="796d9-156">Op Hallo **Zscaler één domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-156">On hello **Zscaler One Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    <span data-ttu-id="796d9-158">Typ in Hallo aanmeldings-URL textbox Hallo-URL die door uw gebruikers toosign op tooyour Zscaler één toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="796d9-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler One application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="796d9-159">U hebt tooupdate deze waarde Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="796d9-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="796d9-160">Neem contact op met [Zscaler één Client ondersteuningsteam](https://www.zscaler.com/company/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="796d9-160">Contact [Zscaler One Client support team](https://www.zscaler.com/company/contact) tooget these values.</span></span>

4. <span data-ttu-id="796d9-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="796d9-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. <span data-ttu-id="796d9-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="796d9-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="796d9-165">Op Hallo **Zscaler één configuratie** sectie, klikt u op **configureren met één Zscaler** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="796d9-165">On hello **Zscaler One Configuration** section, click **Configure Zscaler One** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="796d9-166">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="796d9-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. <span data-ttu-id="796d9-168">In een ander browservenster, meld u aan tooyour Zscaler één bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="796d9-168">In a different web browser window, log in tooyour Zscaler One company site as an administrator.</span></span>

8. <span data-ttu-id="796d9-169">Klik in het menu bovenaan Hallo Hallo **beheer**.</span><span class="sxs-lookup"><span data-stu-id="796d9-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="796d9-170">![Beheer](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="796d9-170">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="796d9-171">Onder **beheerders beheren en rollen**, klikt u op **gebruikers beheren & verificatie**.</span><span class="sxs-lookup"><span data-stu-id="796d9-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="796d9-172">![Gebruikers & verificatie beheren](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "gebruikers & verificatie beheren")</span><span class="sxs-lookup"><span data-stu-id="796d9-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="796d9-173">In Hallo **verificatie-opties kiezen voor uw organisatie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="796d9-174">![Verificatie](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="796d9-174">![Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="796d9-175">a.</span><span class="sxs-lookup"><span data-stu-id="796d9-175">a.</span></span> <span data-ttu-id="796d9-176">Selecteer **verificatie met eenmalige aanmelding SAML**.</span><span class="sxs-lookup"><span data-stu-id="796d9-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="796d9-177">b.</span><span class="sxs-lookup"><span data-stu-id="796d9-177">b.</span></span> <span data-ttu-id="796d9-178">Klik op **één SAML aanmelding Parameters configureren**.</span><span class="sxs-lookup"><span data-stu-id="796d9-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="796d9-179">Op Hallo **configureren SAML Single Sign-On Parameters** dialoogvenster pagina Hallo volgende stappen uit te voeren en klik vervolgens op **gedaan**</span><span class="sxs-lookup"><span data-stu-id="796d9-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="796d9-180">![Eenmalige aanmelding](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="796d9-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="796d9-181">a.</span><span class="sxs-lookup"><span data-stu-id="796d9-181">a.</span></span> <span data-ttu-id="796d9-182">Plakken Hallo **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **URL Hallo SAML Portal toowhich gebruikers worden verzonden voor verificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="796d9-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="796d9-183">b.</span><span class="sxs-lookup"><span data-stu-id="796d9-183">b.</span></span> <span data-ttu-id="796d9-184">In Hallo **kenmerk met naam van de aanmelding** textbox type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="796d9-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="796d9-185">c.</span><span class="sxs-lookup"><span data-stu-id="796d9-185">c.</span></span> <span data-ttu-id="796d9-186">tooupload uw gedownloade certificaat, klik op **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="796d9-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="796d9-187">d.</span><span class="sxs-lookup"><span data-stu-id="796d9-187">d.</span></span> <span data-ttu-id="796d9-188">Selecteer **SAML automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="796d9-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="796d9-189">Op Hallo **gebruikersverificatie configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="796d9-190">![Beheer](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="796d9-190">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="796d9-191">a.</span><span class="sxs-lookup"><span data-stu-id="796d9-191">a.</span></span> <span data-ttu-id="796d9-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="796d9-192">Click **Save**.</span></span>

    <span data-ttu-id="796d9-193">b.</span><span class="sxs-lookup"><span data-stu-id="796d9-193">b.</span></span> <span data-ttu-id="796d9-194">Klik op **nu activeren**.</span><span class="sxs-lookup"><span data-stu-id="796d9-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="796d9-195">Proxy-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="796d9-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="796d9-196">tooconfigure hello proxy-instellingen in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="796d9-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="796d9-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="796d9-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="796d9-198">Selecteer **Internetopties** van Hallo **extra** menu voor open Hallo **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="796d9-199">![Internetopties](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internetopties")</span><span class="sxs-lookup"><span data-stu-id="796d9-199">![Internet Options](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="796d9-200">Klik op Hallo **verbindingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="796d9-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="796d9-201">![Verbindingen](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "verbindingen")</span><span class="sxs-lookup"><span data-stu-id="796d9-201">![Connections](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="796d9-202">Klik op **LAN-instellingen** tooopen hello **LAN-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="796d9-203">Voer in Hallo sectie Proxy-server, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="796d9-204">![Proxyserver](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "proxyserver")</span><span class="sxs-lookup"><span data-stu-id="796d9-204">![Proxy server](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="796d9-205">a.</span><span class="sxs-lookup"><span data-stu-id="796d9-205">a.</span></span> <span data-ttu-id="796d9-206">Selecteer **een proxyserver gebruiken voor uw LAN**.</span><span class="sxs-lookup"><span data-stu-id="796d9-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="796d9-207">b.</span><span class="sxs-lookup"><span data-stu-id="796d9-207">b.</span></span> <span data-ttu-id="796d9-208">Typ in het tekstvak voor het adres van Hallo **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="796d9-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="796d9-209">c.</span><span class="sxs-lookup"><span data-stu-id="796d9-209">c.</span></span> <span data-ttu-id="796d9-210">Typ in het tekstvak poort Hallo **80**.</span><span class="sxs-lookup"><span data-stu-id="796d9-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="796d9-211">d.</span><span class="sxs-lookup"><span data-stu-id="796d9-211">d.</span></span> <span data-ttu-id="796d9-212">Selecteer **proxyserver niet gebruiken voor lokale adressen**.</span><span class="sxs-lookup"><span data-stu-id="796d9-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="796d9-213">e.</span><span class="sxs-lookup"><span data-stu-id="796d9-213">e.</span></span> <span data-ttu-id="796d9-214">Klik op **OK** tooclose hello **Local Area Network (LAN)-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="796d9-215">Klik op **OK** tooclose hello **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="796d9-216">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="796d9-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="796d9-217">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="796d9-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="796d9-218">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="796d9-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="796d9-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="796d9-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="796d9-220">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="796d9-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="796d9-222">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="796d9-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="796d9-223">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="796d9-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="796d9-225">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="796d9-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="796d9-227">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="796d9-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="796d9-229">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="796d9-231">a.</span><span class="sxs-lookup"><span data-stu-id="796d9-231">a.</span></span> <span data-ttu-id="796d9-232">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="796d9-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="796d9-233">b.</span><span class="sxs-lookup"><span data-stu-id="796d9-233">b.</span></span> <span data-ttu-id="796d9-234">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="796d9-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="796d9-235">c.</span><span class="sxs-lookup"><span data-stu-id="796d9-235">c.</span></span> <span data-ttu-id="796d9-236">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="796d9-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="796d9-237">d.</span><span class="sxs-lookup"><span data-stu-id="796d9-237">d.</span></span> <span data-ttu-id="796d9-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="796d9-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-one-test-user"></a><span data-ttu-id="796d9-239">Een Zscaler een testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="796d9-239">Creating a Zscaler One test user</span></span>

<span data-ttu-id="796d9-240">Azure AD tooenable gebruikers toolog in één tooZscaler, moeten ze ingerichte tooZscaler een.</span><span class="sxs-lookup"><span data-stu-id="796d9-240">tooenable Azure AD users toolog in tooZscaler One, they must be provisioned tooZscaler One.</span></span> <span data-ttu-id="796d9-241">In geval van een Zscaler Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="796d9-241">In hello case of Zscaler One, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="796d9-242">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="796d9-243">Meld u bij tooyour **Zscaler één** tenant.</span><span class="sxs-lookup"><span data-stu-id="796d9-243">Log in tooyour **Zscaler One** tenant.</span></span>

2. <span data-ttu-id="796d9-244">Klik op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="796d9-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="796d9-245">![Beheer](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="796d9-245">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="796d9-246">Klik op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="796d9-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="796d9-247">![Voeg](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="796d9-247">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="796d9-248">In Hallo **gebruikers** tabblad **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="796d9-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="796d9-249">![Voeg](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="796d9-249">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="796d9-250">Voer in Hallo sectie gebruiker toevoegen, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="796d9-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="796d9-251">![Gebruiker toevoegen](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="796d9-251">![Add User](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="796d9-252">a.</span><span class="sxs-lookup"><span data-stu-id="796d9-252">a.</span></span> <span data-ttu-id="796d9-253">Type Hallo **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen**en Hallo **afdeling** van een geldig Azure AD-account die u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="796d9-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="796d9-254">b.</span><span class="sxs-lookup"><span data-stu-id="796d9-254">b.</span></span> <span data-ttu-id="796d9-255">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="796d9-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="796d9-256">U kunt andere Zscaler één gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door een Zscaler tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="796d9-256">You can use any other Zscaler One user account creation tools or APIs provided by Zscaler One tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="796d9-257">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="796d9-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="796d9-258">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooZscaler een.</span><span class="sxs-lookup"><span data-stu-id="796d9-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler One.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="796d9-260">**tooassign Britta Simon tooZscaler, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="796d9-260">**tooassign Britta Simon tooZscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="796d9-261">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="796d9-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="796d9-263">Selecteer in de lijst met de toepassingen van Hallo **Zscaler één**.</span><span class="sxs-lookup"><span data-stu-id="796d9-263">In hello applications list, select **Zscaler One**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. <span data-ttu-id="796d9-265">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="796d9-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="796d9-267">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="796d9-267">Click **Add** button.</span></span> <span data-ttu-id="796d9-268">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="796d9-270">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="796d9-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="796d9-271">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="796d9-272">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="796d9-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="796d9-273">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="796d9-273">Testing single sign-on</span></span>

<span data-ttu-id="796d9-274">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="796d9-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="796d9-275">Als u op Hallo Zscaler een tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zscaler één toepassing.</span><span class="sxs-lookup"><span data-stu-id="796d9-275">When you click hello Zscaler One tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler One application.</span></span>
<span data-ttu-id="796d9-276">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="796d9-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="796d9-277">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="796d9-277">Additional resources</span></span>

* [<span data-ttu-id="796d9-278">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="796d9-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="796d9-279">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="796d9-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

