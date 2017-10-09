---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler Beta | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zscaler Beta.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="787f0-103">Zelfstudie: Azure Active Directory-integratie met Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="787f0-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="787f0-104">In deze zelfstudie leert u hoe toointegrate Zscaler Beta met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="787f0-104">In this tutorial, you learn how toointegrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="787f0-105">Zscaler Beta integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="787f0-105">Integrating Zscaler Beta with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="787f0-106">U kunt beheren in Azure AD wie toegang tot tooZscaler Beta heeft</span><span class="sxs-lookup"><span data-stu-id="787f0-106">You can control in Azure AD who has access tooZscaler Beta</span></span>
- <span data-ttu-id="787f0-107">U kunt uw gebruikers tooautomatically get aangemelde tooZscaler Beta (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="787f0-107">You can enable your users tooautomatically get signed-on tooZscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="787f0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="787f0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="787f0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="787f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="787f0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="787f0-110">Prerequisites</span></span>

<span data-ttu-id="787f0-111">Azure AD-integratie met Zscaler Beta tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="787f0-111">tooconfigure Azure AD integration with Zscaler Beta, you need hello following items:</span></span>

- <span data-ttu-id="787f0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="787f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="787f0-113">Een Zscaler Beta eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="787f0-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="787f0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="787f0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="787f0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="787f0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="787f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="787f0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="787f0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="787f0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="787f0-118">Scenario description</span></span>
<span data-ttu-id="787f0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="787f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="787f0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="787f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="787f0-121">Het toevoegen van Zscaler Beta van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="787f0-121">Adding Zscaler Beta from hello gallery</span></span>
2. <span data-ttu-id="787f0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="787f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-hello-gallery"></a><span data-ttu-id="787f0-123">Het toevoegen van Zscaler Beta van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="787f0-123">Adding Zscaler Beta from hello gallery</span></span>
<span data-ttu-id="787f0-124">tooconfigure hello integratie van Zscaler Beta in Azure AD, moet u tooadd Zscaler Beta uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="787f0-124">tooconfigure hello integration of Zscaler Beta into Azure AD, you need tooadd Zscaler Beta from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="787f0-125">**tooadd Zscaler Beta via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="787f0-125">**tooadd Zscaler Beta from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="787f0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="787f0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="787f0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="787f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="787f0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="787f0-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="787f0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="787f0-133">Typ in het zoekvak Hallo **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="787f0-133">In hello search box, type **Zscaler Beta**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="787f0-135">Selecteer in het deelvenster resultaten hello, **Zscaler Beta**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="787f0-135">In hello results panel, select **Zscaler Beta**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="787f0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="787f0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="787f0-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Zscaler Beta op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="787f0-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="787f0-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Zscaler Beta is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="787f0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Beta is tooa user in Azure AD.</span></span> <span data-ttu-id="787f0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo Zscaler bètaversie toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="787f0-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Beta needs toobe established.</span></span>

<span data-ttu-id="787f0-141">In Zscaler Bèta, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="787f0-141">In Zscaler Beta, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="787f0-142">tooconfigure en eenmalige aanmelding Azure AD-test met Zscaler Bèta, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-142">tooconfigure and test Azure AD single sign-on with Zscaler Beta, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="787f0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="787f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="787f0-144">**[Proxy-instellingen configureren](#configuring-proxy-settings)**  -tooconfigure Hallo proxy-instellingen in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="787f0-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="787f0-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="787f0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="787f0-146">**[Maken van een testgebruiker Zscaler Beta](#creating-a-zscaler-beta-test-user)**  -toohave een equivalent van Britta Simon Zscaler bètaversie die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="787f0-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - toohave a counterpart of Britta Simon in Zscaler Beta that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="787f0-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="787f0-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="787f0-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="787f0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="787f0-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="787f0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="787f0-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="787f0-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="787f0-151">**Voer tooconfigure Azure AD eenmalige aanmelding met Zscaler Bèta, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="787f0-151">**tooconfigure Azure AD single sign-on with Zscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="787f0-152">In de Azure-portal op Hallo Hallo **Zscaler Beta** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="787f0-152">In hello Azure portal, on hello **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="787f0-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="787f0-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="787f0-156">Op Hallo **Zscaler Beta domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-156">On hello **Zscaler Beta Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="787f0-158">Typ in het tekstvak URL gebruikersportal Hallo eenmalige aanmelding, Hallo-URL die door uw gebruikers toosign op tooyour Zscaler Beta-toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="787f0-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="787f0-159">U hebt tooupdate deze waarde Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="787f0-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="787f0-160">Neem contact op met [Zscaler bèta-Client-ondersteuningsteam](https://www.zscaler.com/company/contact) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="787f0-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="787f0-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="787f0-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="787f0-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="787f0-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="787f0-165">Op Hallo **Zscaler Beta configuratie** sectie, klikt u op **configureren Zscaler Beta** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="787f0-165">On hello **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="787f0-166">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="787f0-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="787f0-168">In een ander browservenster aanmelden tooyour Zscaler Beta bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="787f0-168">In a different web browser window, log in tooyour Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="787f0-169">Klik in het menu bovenaan Hallo Hallo **beheer**.</span><span class="sxs-lookup"><span data-stu-id="787f0-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="787f0-170">![Beheer](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="787f0-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="787f0-171">Onder **beheerders beheren en rollen**, klikt u op **gebruikers beheren & verificatie**.</span><span class="sxs-lookup"><span data-stu-id="787f0-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="787f0-172">![Gebruikers & verificatie beheren](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "gebruikers & verificatie beheren")</span><span class="sxs-lookup"><span data-stu-id="787f0-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="787f0-173">In Hallo **verificatie-opties kiezen voor uw organisatie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="787f0-174">![Verificatie](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="787f0-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="787f0-175">a.</span><span class="sxs-lookup"><span data-stu-id="787f0-175">a.</span></span> <span data-ttu-id="787f0-176">Selecteer **verificatie met eenmalige aanmelding SAML**.</span><span class="sxs-lookup"><span data-stu-id="787f0-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="787f0-177">b.</span><span class="sxs-lookup"><span data-stu-id="787f0-177">b.</span></span> <span data-ttu-id="787f0-178">Klik op **één SAML aanmelding Parameters configureren**.</span><span class="sxs-lookup"><span data-stu-id="787f0-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="787f0-179">Op Hallo **configureren SAML Single Sign-On Parameters** dialoogvenster pagina Hallo volgende stappen uit te voeren en klik vervolgens op **gedaan**</span><span class="sxs-lookup"><span data-stu-id="787f0-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="787f0-180">![Eenmalige aanmelding](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="787f0-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="787f0-181">a.</span><span class="sxs-lookup"><span data-stu-id="787f0-181">a.</span></span> <span data-ttu-id="787f0-182">Plakken Hallo **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **URL Hallo SAML Portal toowhich gebruikers worden verzonden voor verificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="787f0-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="787f0-183">b.</span><span class="sxs-lookup"><span data-stu-id="787f0-183">b.</span></span> <span data-ttu-id="787f0-184">In Hallo **kenmerk met naam van de aanmelding** textbox type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="787f0-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="787f0-185">c.</span><span class="sxs-lookup"><span data-stu-id="787f0-185">c.</span></span> <span data-ttu-id="787f0-186">tooupload uw gedownloade certificaat, klik op **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="787f0-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="787f0-187">d.</span><span class="sxs-lookup"><span data-stu-id="787f0-187">d.</span></span> <span data-ttu-id="787f0-188">Selecteer **SAML automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="787f0-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="787f0-189">Op Hallo **gebruikersverificatie configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="787f0-190">![Beheer](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="787f0-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="787f0-191">a.</span><span class="sxs-lookup"><span data-stu-id="787f0-191">a.</span></span> <span data-ttu-id="787f0-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="787f0-192">Click **Save**.</span></span>

    <span data-ttu-id="787f0-193">b.</span><span class="sxs-lookup"><span data-stu-id="787f0-193">b.</span></span> <span data-ttu-id="787f0-194">Klik op **nu activeren**.</span><span class="sxs-lookup"><span data-stu-id="787f0-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="787f0-195">Proxy-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="787f0-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="787f0-196">tooconfigure hello proxy-instellingen in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="787f0-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="787f0-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="787f0-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="787f0-198">Selecteer **Internetopties** van Hallo **extra** menu voor open Hallo **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="787f0-199">![Internetopties](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internetopties")</span><span class="sxs-lookup"><span data-stu-id="787f0-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="787f0-200">Klik op Hallo **verbindingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="787f0-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="787f0-201">![Verbindingen](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "verbindingen")</span><span class="sxs-lookup"><span data-stu-id="787f0-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="787f0-202">Klik op **LAN-instellingen** tooopen hello **LAN-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="787f0-203">Voer in Hallo sectie Proxy-server, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="787f0-204">![Proxyserver](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "proxyserver")</span><span class="sxs-lookup"><span data-stu-id="787f0-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="787f0-205">a.</span><span class="sxs-lookup"><span data-stu-id="787f0-205">a.</span></span> <span data-ttu-id="787f0-206">Selecteer **een proxyserver gebruiken voor uw LAN**.</span><span class="sxs-lookup"><span data-stu-id="787f0-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="787f0-207">b.</span><span class="sxs-lookup"><span data-stu-id="787f0-207">b.</span></span> <span data-ttu-id="787f0-208">Typ in het tekstvak voor het adres van Hallo **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="787f0-208">In hello Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="787f0-209">c.</span><span class="sxs-lookup"><span data-stu-id="787f0-209">c.</span></span> <span data-ttu-id="787f0-210">Typ in het tekstvak poort Hallo **80**.</span><span class="sxs-lookup"><span data-stu-id="787f0-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="787f0-211">d.</span><span class="sxs-lookup"><span data-stu-id="787f0-211">d.</span></span> <span data-ttu-id="787f0-212">Selecteer **proxyserver niet gebruiken voor lokale adressen**.</span><span class="sxs-lookup"><span data-stu-id="787f0-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="787f0-213">e.</span><span class="sxs-lookup"><span data-stu-id="787f0-213">e.</span></span> <span data-ttu-id="787f0-214">Klik op **OK** tooclose hello **Local Area Network (LAN)-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="787f0-215">Klik op **OK** tooclose hello **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="787f0-216">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="787f0-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="787f0-217">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="787f0-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="787f0-218">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="787f0-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="787f0-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="787f0-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="787f0-220">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="787f0-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="787f0-222">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="787f0-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="787f0-223">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="787f0-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="787f0-225">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="787f0-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="787f0-227">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="787f0-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="787f0-229">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="787f0-231">a.</span><span class="sxs-lookup"><span data-stu-id="787f0-231">a.</span></span> <span data-ttu-id="787f0-232">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="787f0-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="787f0-233">b.</span><span class="sxs-lookup"><span data-stu-id="787f0-233">b.</span></span> <span data-ttu-id="787f0-234">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="787f0-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="787f0-235">c.</span><span class="sxs-lookup"><span data-stu-id="787f0-235">c.</span></span> <span data-ttu-id="787f0-236">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="787f0-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="787f0-237">d.</span><span class="sxs-lookup"><span data-stu-id="787f0-237">d.</span></span> <span data-ttu-id="787f0-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="787f0-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="787f0-239">Maken van een testgebruiker Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="787f0-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="787f0-240">Azure AD tooenable gebruikers toolog in tooZscaler Bèta, moeten ze ingerichte tooZscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="787f0-240">tooenable Azure AD users toolog in tooZscaler Beta, they must be provisioned tooZscaler Beta.</span></span> <span data-ttu-id="787f0-241">In geval van Zscaler Beta Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="787f0-241">In hello case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="787f0-242">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="787f0-243">Meld u bij tooyour **Zscaler Beta** tenant.</span><span class="sxs-lookup"><span data-stu-id="787f0-243">Log in tooyour **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="787f0-244">Klik op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="787f0-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="787f0-245">![Beheer](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="787f0-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="787f0-246">Klik op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="787f0-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="787f0-247">![Voeg](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="787f0-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="787f0-248">In Hallo **gebruikers** tabblad **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="787f0-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="787f0-249">![Voeg](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="787f0-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="787f0-250">Voer in Hallo sectie gebruiker toevoegen, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="787f0-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="787f0-251">![Gebruiker toevoegen](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="787f0-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="787f0-252">a.</span><span class="sxs-lookup"><span data-stu-id="787f0-252">a.</span></span> <span data-ttu-id="787f0-253">Type Hallo **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen**en Hallo **afdeling** van een geldig Azure AD-account die u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="787f0-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="787f0-254">b.</span><span class="sxs-lookup"><span data-stu-id="787f0-254">b.</span></span> <span data-ttu-id="787f0-255">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="787f0-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="787f0-256">U kunt andere Zscaler Beta gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Zscaler Beta tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="787f0-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="787f0-257">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="787f0-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="787f0-258">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooZscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="787f0-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Beta.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="787f0-260">**tooassign Britta Simon tooZscaler Bèta, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="787f0-260">**tooassign Britta Simon tooZscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="787f0-261">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="787f0-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="787f0-263">Selecteer in de lijst met de toepassingen van Hallo **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="787f0-263">In hello applications list, select **Zscaler Beta**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="787f0-265">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="787f0-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="787f0-267">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="787f0-267">Click **Add** button.</span></span> <span data-ttu-id="787f0-268">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="787f0-270">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="787f0-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="787f0-271">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="787f0-272">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="787f0-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="787f0-273">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="787f0-273">Testing single sign-on</span></span>

<span data-ttu-id="787f0-274">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="787f0-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="787f0-275">Als u op Hallo Zscaler Beta-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zscaler Beta-toepassing.</span><span class="sxs-lookup"><span data-stu-id="787f0-275">When you click hello Zscaler Beta tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Beta application.</span></span>
<span data-ttu-id="787f0-276">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="787f0-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="787f0-277">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="787f0-277">Additional resources</span></span>

* [<span data-ttu-id="787f0-278">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="787f0-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="787f0-279">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="787f0-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

