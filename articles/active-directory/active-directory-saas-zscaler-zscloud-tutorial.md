---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler ZSCloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zscaler ZSCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="91a14-103">Zelfstudie: Azure Active Directory-integratie met Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="91a14-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="91a14-104">In deze zelfstudie leert u hoe toointegrate Zscaler ZSCloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91a14-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91a14-105">Zscaler ZSCloud integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="91a14-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91a14-106">U kunt beheren in Azure AD wie toegang tot tooZscaler ZSCloud heeft</span><span class="sxs-lookup"><span data-stu-id="91a14-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="91a14-107">U kunt uw gebruikers tooautomatically get aangemelde tooZscaler ZSCloud (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="91a14-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91a14-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="91a14-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="91a14-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91a14-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91a14-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="91a14-110">Prerequisites</span></span>

<span data-ttu-id="91a14-111">Azure AD-integratie met Zscaler ZSCloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="91a14-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="91a14-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="91a14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91a14-113">Een Zscaler ZSCloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="91a14-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91a14-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="91a14-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91a14-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91a14-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="91a14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91a14-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91a14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91a14-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="91a14-118">Scenario description</span></span>
<span data-ttu-id="91a14-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="91a14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91a14-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="91a14-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91a14-121">Het toevoegen van Zscaler ZSCloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="91a14-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="91a14-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="91a14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="91a14-123">Het toevoegen van Zscaler ZSCloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="91a14-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="91a14-124">tooconfigure hello integratie van Zscaler ZSCloud in Azure AD, moet u tooadd Zscaler ZSCloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="91a14-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91a14-125">**tooadd Zscaler ZSCloud via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91a14-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91a14-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="91a14-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91a14-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="91a14-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91a14-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="91a14-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="91a14-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="91a14-133">Typ in het zoekvak Hallo **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="91a14-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="91a14-135">Selecteer in het deelvenster resultaten hello, **Zscaler ZSCloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91a14-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91a14-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="91a14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91a14-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Zscaler ZSCloud op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="91a14-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="91a14-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Zscaler ZSCloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91a14-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="91a14-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Zscaler ZSCloud toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="91a14-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="91a14-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="91a14-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="91a14-142">tooconfigure en eenmalige aanmelding Azure AD-test met Zscaler ZSCloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91a14-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="91a14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91a14-144">**[Proxy-instellingen configureren](#configuring-proxy-settings)**  -tooconfigure Hallo proxy-instellingen in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="91a14-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="91a14-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91a14-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91a14-146">**[Maken van een testgebruiker Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave een equivalent van Britta Simon in Zscaler ZSCloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="91a14-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91a14-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91a14-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91a14-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="91a14-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91a14-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="91a14-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91a14-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Zscaler ZSCloud configureren.</span><span class="sxs-lookup"><span data-stu-id="91a14-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="91a14-151">**Azure AD tooconfigure eenmalige aanmelding met Zscaler ZSCloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91a14-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="91a14-152">In de Azure-portal op Hallo Hallo **Zscaler ZSCloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="91a14-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="91a14-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91a14-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="91a14-156">Op Hallo **Zscaler ZSCloud domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="91a14-158">In Hallo **aanmeldings-URL** textbox type Hallo-URL die door uw gebruikers toosign op tooyour ZScaler ZSCloud toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="91a14-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="91a14-159">U hebt tooupdate deze waarde Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="91a14-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="91a14-160">Neem contact op met [Zscaler ZSCloud Client ondersteuningsteam](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="91a14-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="91a14-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="91a14-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="91a14-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="91a14-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91a14-165">Op Hallo **Zscaler ZSCloud configuratie** sectie, klikt u op **configureren Zscaler ZSCloud** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="91a14-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="91a14-166">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="91a14-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="91a14-168">In een ander browservenster aanmelden tooyour ZScaler ZSCloud bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="91a14-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="91a14-169">Klik in het menu bovenaan Hallo Hallo **beheer**.</span><span class="sxs-lookup"><span data-stu-id="91a14-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="91a14-170">![Beheer](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="91a14-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="91a14-171">Onder **beheerders beheren en rollen**, klikt u op **gebruikers beheren & verificatie**.</span><span class="sxs-lookup"><span data-stu-id="91a14-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="91a14-172">![Gebruikers & verificatie beheren](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "gebruikers & verificatie beheren")</span><span class="sxs-lookup"><span data-stu-id="91a14-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="91a14-173">In Hallo **verificatie-opties kiezen voor uw organisatie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="91a14-174">![Verificatie](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="91a14-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="91a14-175">a.</span><span class="sxs-lookup"><span data-stu-id="91a14-175">a.</span></span> <span data-ttu-id="91a14-176">Selecteer **verificatie met eenmalige aanmelding SAML**.</span><span class="sxs-lookup"><span data-stu-id="91a14-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="91a14-177">b.</span><span class="sxs-lookup"><span data-stu-id="91a14-177">b.</span></span> <span data-ttu-id="91a14-178">Klik op **één SAML aanmelding Parameters configureren**.</span><span class="sxs-lookup"><span data-stu-id="91a14-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="91a14-179">Op Hallo **configureren SAML Single Sign-On Parameters** dialoogvenster pagina Hallo volgende stappen uit te voeren en klik vervolgens op **gedaan**</span><span class="sxs-lookup"><span data-stu-id="91a14-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="91a14-180">![Eenmalige aanmelding](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="91a14-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="91a14-181">a.</span><span class="sxs-lookup"><span data-stu-id="91a14-181">a.</span></span> <span data-ttu-id="91a14-182">Plakken Hallo **SAML Single Sign-On Service-URL** waarde in Hallo **URL Hallo SAML Portal toowhich gebruikers worden verzonden voor verificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="91a14-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="91a14-183">b.</span><span class="sxs-lookup"><span data-stu-id="91a14-183">b.</span></span> <span data-ttu-id="91a14-184">In Hallo **kenmerk met naam van de aanmelding** textbox type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="91a14-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="91a14-185">c.</span><span class="sxs-lookup"><span data-stu-id="91a14-185">c.</span></span> <span data-ttu-id="91a14-186">tooupload uw gedownloade certificaat, klik op **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="91a14-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="91a14-187">d.</span><span class="sxs-lookup"><span data-stu-id="91a14-187">d.</span></span> <span data-ttu-id="91a14-188">Selecteer **SAML automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="91a14-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="91a14-189">Op Hallo **gebruikersverificatie configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="91a14-190">![Beheer](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="91a14-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="91a14-191">a.</span><span class="sxs-lookup"><span data-stu-id="91a14-191">a.</span></span> <span data-ttu-id="91a14-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="91a14-192">Click **Save**.</span></span>

    <span data-ttu-id="91a14-193">b.</span><span class="sxs-lookup"><span data-stu-id="91a14-193">b.</span></span> <span data-ttu-id="91a14-194">Klik op **nu activeren**.</span><span class="sxs-lookup"><span data-stu-id="91a14-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="91a14-195">Proxy-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="91a14-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="91a14-196">tooconfigure hello proxy-instellingen in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="91a14-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="91a14-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="91a14-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="91a14-198">Selecteer **Internetopties** van Hallo **extra** menu voor open Hallo **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="91a14-199">![Internetopties](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internetopties")</span><span class="sxs-lookup"><span data-stu-id="91a14-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="91a14-200">Klik op Hallo **verbindingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="91a14-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="91a14-201">![Verbindingen](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "verbindingen")</span><span class="sxs-lookup"><span data-stu-id="91a14-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="91a14-202">Klik op **LAN-instellingen** tooopen hello **LAN-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="91a14-203">Voer in Hallo sectie Proxy-server, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="91a14-204">![Proxyserver](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "proxyserver")</span><span class="sxs-lookup"><span data-stu-id="91a14-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="91a14-205">a.</span><span class="sxs-lookup"><span data-stu-id="91a14-205">a.</span></span> <span data-ttu-id="91a14-206">Selecteer **een proxyserver gebruiken voor uw LAN**.</span><span class="sxs-lookup"><span data-stu-id="91a14-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="91a14-207">b.</span><span class="sxs-lookup"><span data-stu-id="91a14-207">b.</span></span> <span data-ttu-id="91a14-208">Typ in het tekstvak voor het adres van Hallo **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="91a14-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="91a14-209">c.</span><span class="sxs-lookup"><span data-stu-id="91a14-209">c.</span></span> <span data-ttu-id="91a14-210">Typ in het tekstvak poort Hallo **80**.</span><span class="sxs-lookup"><span data-stu-id="91a14-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="91a14-211">d.</span><span class="sxs-lookup"><span data-stu-id="91a14-211">d.</span></span> <span data-ttu-id="91a14-212">Selecteer **proxyserver niet gebruiken voor lokale adressen**.</span><span class="sxs-lookup"><span data-stu-id="91a14-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="91a14-213">e.</span><span class="sxs-lookup"><span data-stu-id="91a14-213">e.</span></span> <span data-ttu-id="91a14-214">Klik op **OK** tooclose hello **Local Area Network (LAN)-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="91a14-215">Klik op **OK** tooclose hello **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91a14-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="91a14-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="91a14-217">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="91a14-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="91a14-219">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91a14-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91a14-220">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="91a14-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91a14-222">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="91a14-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91a14-224">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="91a14-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91a14-226">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91a14-228">a.</span><span class="sxs-lookup"><span data-stu-id="91a14-228">a.</span></span> <span data-ttu-id="91a14-229">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91a14-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91a14-230">b.</span><span class="sxs-lookup"><span data-stu-id="91a14-230">b.</span></span> <span data-ttu-id="91a14-231">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91a14-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91a14-232">c.</span><span class="sxs-lookup"><span data-stu-id="91a14-232">c.</span></span> <span data-ttu-id="91a14-233">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="91a14-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="91a14-234">d.</span><span class="sxs-lookup"><span data-stu-id="91a14-234">d.</span></span> <span data-ttu-id="91a14-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="91a14-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="91a14-236">Een testgebruiker Zscaler ZSCloud maken</span><span class="sxs-lookup"><span data-stu-id="91a14-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="91a14-237">Azure AD tooenable gebruikers toolog in tooZScaler ZSCloud, moeten ze ingerichte tooZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="91a14-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="91a14-238">In geval van ZScaler ZSCloud Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="91a14-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="91a14-239">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="91a14-240">Meld u bij tooyour **Zscaler** tenant.</span><span class="sxs-lookup"><span data-stu-id="91a14-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="91a14-241">Klik op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="91a14-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="91a14-242">![Beheer](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="91a14-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="91a14-243">Klik op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="91a14-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="91a14-244">![Voeg](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="91a14-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="91a14-245">In Hallo **gebruikers** tabblad **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="91a14-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="91a14-246">![Voeg](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="91a14-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="91a14-247">Voer in Hallo sectie gebruiker toevoegen, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91a14-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="91a14-248">![Gebruiker toevoegen](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="91a14-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="91a14-249">a.</span><span class="sxs-lookup"><span data-stu-id="91a14-249">a.</span></span> <span data-ttu-id="91a14-250">Type Hallo **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen**en Hallo **afdeling** van een geldige AAD-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="91a14-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="91a14-251">b.</span><span class="sxs-lookup"><span data-stu-id="91a14-251">b.</span></span> <span data-ttu-id="91a14-252">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="91a14-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="91a14-253">U kunt andere ZScaler ZSCloud gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door ZScaler ZSCloud tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="91a14-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91a14-254">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="91a14-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="91a14-255">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooZscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="91a14-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="91a14-257">**tooassign Britta Simon tooZscaler ZSCloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91a14-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="91a14-258">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="91a14-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="91a14-260">Selecteer in de lijst met de toepassingen van Hallo **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="91a14-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="91a14-262">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="91a14-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="91a14-264">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="91a14-264">Click **Add** button.</span></span> <span data-ttu-id="91a14-265">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="91a14-267">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="91a14-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91a14-268">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91a14-269">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91a14-270">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="91a14-270">Testing single sign-on</span></span>

<span data-ttu-id="91a14-271">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="91a14-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="91a14-272">Als u op Hallo Zscaler ZSCloud-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zscaler ZSCloud toepassing.</span><span class="sxs-lookup"><span data-stu-id="91a14-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="91a14-273">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="91a14-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="91a14-274">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="91a14-274">Additional resources</span></span>

* [<span data-ttu-id="91a14-275">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91a14-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91a14-276">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91a14-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

