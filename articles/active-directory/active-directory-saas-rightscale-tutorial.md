---
title: 'Zelfstudie: Azure Active Directory-integratie met Rightscale | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Rightscale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="f6b6f-103">Zelfstudie: Azure Active Directory-integratie met Rightscale</span><span class="sxs-lookup"><span data-stu-id="f6b6f-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="f6b6f-104">In deze zelfstudie leert u hoe toointegrate Rightscale met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6b6f-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6b6f-105">Rightscale integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f6b6f-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6b6f-106">U kunt beheren in Azure AD die tooRightscale toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f6b6f-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="f6b6f-107">U kunt uw gebruikers tooautomatically get aangemelde tooRightscale (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f6b6f-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6b6f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f6b6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f6b6f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6b6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6b6f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f6b6f-110">Prerequisites</span></span>

<span data-ttu-id="f6b6f-111">Azure AD-integratie met Rightscale tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f6b6f-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="f6b6f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f6b6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6b6f-113">Een Rightscale eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f6b6f-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6b6f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6b6f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f6b6f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6b6f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6b6f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6b6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6b6f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f6b6f-118">Scenario description</span></span>
<span data-ttu-id="f6b6f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6b6f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f6b6f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6b6f-121">Het toevoegen van Rightscale van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f6b6f-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="f6b6f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6b6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="f6b6f-123">Het toevoegen van Rightscale van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f6b6f-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="f6b6f-124">tooconfigure hello integratie van Rightscale in Azure AD, moet u tooadd Rightscale uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6b6f-125">**tooadd Rightscale via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f6b6f-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6b6f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6b6f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6b6f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f6b6f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f6b6f-133">Typ in het zoekvak Hallo **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-133">In hello search box, type **Rightscale**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="f6b6f-135">Selecteer in het deelvenster resultaten hello, **Rightscale**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6b6f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6b6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6b6f-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Rightscale op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6b6f-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Rightscale is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="f6b6f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Rightscale toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="f6b6f-141">Wijs in Rightscale, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f6b6f-142">tooconfigure en eenmalige aanmelding Azure AD-test met Rightscale, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f6b6f-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6b6f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6b6f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6b6f-145">**[Maken van een testgebruiker Rightscale](#creating-a-rightscale-test-user)**  -toohave een equivalent van Britta Simon in Rightscale die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6b6f-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6b6f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6b6f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f6b6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6b6f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Rightscale configureren.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="f6b6f-150">**Azure AD tooconfigure eenmalige aanmelding met Rightscale, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f6b6f-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6b6f-151">In de Azure-portal op Hallo Hallo **Rightscale** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f6b6f-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="f6b6f-155">Op Hallo **Rightscale domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus** u hebt geen tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="f6b6f-157">Op Hallo **Rightscale domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f6b6f-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="f6b6f-159">a.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-159">a.</span></span> <span data-ttu-id="f6b6f-160">Klik op Hallo **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="f6b6f-161">b.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-161">b.</span></span> <span data-ttu-id="f6b6f-162">In Hallo **aanmelding op URL** textbox type Hallo URL:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="f6b6f-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="f6b6f-163">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="f6b6f-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f6b6f-167">Op Hallo **Rightscale configuratie** sectie, klikt u op **configureren Rightscale** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f6b6f-168">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f6b6f-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="f6b6f-169">![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="f6b6f-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="f6b6f-170">tooget SSO is geconfigureerd voor uw toepassing, moet u toosign op tooyour RightScale tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="f6b6f-171">a.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-171">a.</span></span> <span data-ttu-id="f6b6f-172">Klik op Hallo in het menu bovenaan Hallo Hallo **instellingen** tabblad en selecteer **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="f6b6f-174">b.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-174">b.</span></span> <span data-ttu-id="f6b6f-175">Klik op Hallo '**nieuwe**' knop tooadd **uw SAML identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="f6b6f-177">c.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-177">c.</span></span> <span data-ttu-id="f6b6f-178">In het tekstvak Hallo van **weergavenaam**, voer de naam van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="f6b6f-180">d.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-180">d.</span></span> <span data-ttu-id="f6b6f-181">Selecteer **RightScale toestaan geïnitieerde eenmalige aanmelding met een hint detectie** en invoer uw **domeinnaam** in Hallo onder het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="f6b6f-183">e.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-183">e.</span></span> <span data-ttu-id="f6b6f-184">Hallo-waarde van plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal in **SAML SSO eindpunt** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="f6b6f-186">f.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-186">f.</span></span> <span data-ttu-id="f6b6f-187">Hallo-waarde van plakken **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal in **SAML id van de entiteit** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="f6b6f-189">g.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-189">g.</span></span> <span data-ttu-id="f6b6f-190">Klik op **Browser** knop tooupload Hallo certificaat dat u hebt gedownload van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="f6b6f-192">h.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-192">h.</span></span> <span data-ttu-id="f6b6f-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="f6b6f-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f6b6f-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f6b6f-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6b6f-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6b6f-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f6b6f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6b6f-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f6b6f-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f6b6f-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6b6f-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6b6f-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6b6f-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6b6f-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f6b6f-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6b6f-209">a.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-209">a.</span></span> <span data-ttu-id="f6b6f-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6b6f-211">b.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-211">b.</span></span> <span data-ttu-id="f6b6f-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6b6f-213">c.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-213">c.</span></span> <span data-ttu-id="f6b6f-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6b6f-215">d.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-215">d.</span></span> <span data-ttu-id="f6b6f-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="f6b6f-217">Een testgebruiker Rightscale maken</span><span class="sxs-lookup"><span data-stu-id="f6b6f-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="f6b6f-218">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in RightScale maken.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="f6b6f-219">Werken met [Rightscale Client ondersteuningsteam](mailto:support@rightscale.com) tooadd Hallo gebruikers in Hallo RightScale platform.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6b6f-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6b6f-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6b6f-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRightscale toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f6b6f-223">**tooassign Britta Simon tooRightscale, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f6b6f-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6b6f-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f6b6f-226">Selecteer in de lijst met de toepassingen van Hallo **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-226">In hello applications list, select **Rightscale**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="f6b6f-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f6b6f-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-230">Click **Add** button.</span></span> <span data-ttu-id="f6b6f-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f6b6f-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6b6f-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6b6f-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6b6f-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6b6f-236">Testing single sign-on</span></span>

<span data-ttu-id="f6b6f-237">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="f6b6f-238">Als u op Hallo RightScale tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour RightScale toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6b6f-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6b6f-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f6b6f-239">Additional resources</span></span>

* [<span data-ttu-id="f6b6f-240">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6b6f-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6b6f-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6b6f-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

