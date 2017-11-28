---
title: 'Zelfstudie: Azure Active Directory-integratie met LockPath Keylight | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LockPath Keylight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="f83e5-103">Zelfstudie: Azure Active Directory-integratie met LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="f83e5-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="f83e5-104">In deze zelfstudie leert u hoe toointegrate LockPath Keylight met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f83e5-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f83e5-105">LockPath Keylight integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f83e5-106">U kunt beheren in Azure AD wie toegang tot tooLockPath Keylight heeft</span><span class="sxs-lookup"><span data-stu-id="f83e5-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="f83e5-107">U kunt uw gebruikers tooautomatically get aangemelde tooLockPath Keylight (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f83e5-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f83e5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f83e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f83e5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f83e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f83e5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f83e5-110">Prerequisites</span></span>

<span data-ttu-id="f83e5-111">Azure AD-integratie met LockPath Keylight tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f83e5-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="f83e5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f83e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f83e5-113">Een LockPath Keylight eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f83e5-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f83e5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f83e5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f83e5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f83e5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f83e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f83e5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f83e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f83e5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f83e5-118">Scenario description</span></span>
<span data-ttu-id="f83e5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f83e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f83e5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f83e5-121">Het toevoegen van LockPath Keylight van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f83e5-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="f83e5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f83e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="f83e5-123">Het toevoegen van LockPath Keylight van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f83e5-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="f83e5-124">tooconfigure hello integratie van LockPath Keylight in Azure AD, moet u tooadd LockPath Keylight uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f83e5-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f83e5-125">**tooadd LockPath Keylight via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83e5-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83e5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f83e5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f83e5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f83e5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f83e5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83e5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f83e5-133">Typ in het zoekvak Hallo **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="f83e5-135">Selecteer in het deelvenster resultaten hello, **LockPath Keylight**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f83e5-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f83e5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f83e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f83e5-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met LockPath Keylight op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f83e5-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f83e5-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LockPath Keylight is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f83e5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="f83e5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in LockPath Keylight toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f83e5-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="f83e5-141">Wijs in LockPath Keylight, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als Hallo-waarde van Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f83e5-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f83e5-142">tooconfigure en eenmalige aanmelding Azure AD-test met LockPath Keylight, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f83e5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f83e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f83e5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f83e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f83e5-145">**[Maken van een testgebruiker LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave een equivalent van Britta Simon in LockPath Keylight die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f83e5-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f83e5-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f83e5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f83e5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f83e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f83e5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f83e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f83e5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LockPath Keylight configureren.</span><span class="sxs-lookup"><span data-stu-id="f83e5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="f83e5-150">**Azure AD tooconfigure eenmalige aanmelding met LockPath Keylight, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83e5-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83e5-151">In de Azure-portal op Hallo Hallo **LockPath Keylight** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f83e5-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f83e5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="f83e5-155">Op Hallo **LockPath Keylight domein en de URL's** sectie, voert u stappen te volgen Hallo::</span><span class="sxs-lookup"><span data-stu-id="f83e5-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="f83e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="f83e5-157">a.</span></span> <span data-ttu-id="f83e5-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="f83e5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="f83e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="f83e5-159">b.</span></span> <span data-ttu-id="f83e5-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="f83e5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="f83e5-161">c.</span><span class="sxs-lookup"><span data-stu-id="f83e5-161">c.</span></span> <span data-ttu-id="f83e5-162">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="f83e5-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f83e5-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f83e5-163">These values are not real.</span></span> <span data-ttu-id="f83e5-164">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f83e5-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f83e5-165">Neem contact op met [LockPath Keylight Client ondersteuningsteam](https://www.lockpath.com/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="f83e5-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f83e5-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="f83e5-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f83e5-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f83e5-170">Op Hallo **LockPath Keylight configuratie** sectie, klikt u op **configureren LockPath Keylight** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f83e5-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f83e5-171">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f83e5-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="f83e5-173">tooenable SSO in LockPath Keylight, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="f83e5-174">a.</span><span class="sxs-lookup"><span data-stu-id="f83e5-174">a.</span></span> <span data-ttu-id="f83e5-175">Eenmalige aanmelding tooyour LockPath Keylight account als administrator.</span><span class="sxs-lookup"><span data-stu-id="f83e5-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="f83e5-176">b.</span><span class="sxs-lookup"><span data-stu-id="f83e5-176">b.</span></span> <span data-ttu-id="f83e5-177">Klik in het menu bovenaan Hallo Hallo **persoon**, en selecteer **Keylight Setup**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="f83e5-179">c.</span><span class="sxs-lookup"><span data-stu-id="f83e5-179">c.</span></span> <span data-ttu-id="f83e5-180">In de structuurweergave Hallo op Hallo links, klikt u op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="f83e5-182">d.</span><span class="sxs-lookup"><span data-stu-id="f83e5-182">d.</span></span> <span data-ttu-id="f83e5-183">Op Hallo **SAML instellingen** dialoogvenster, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="f83e5-185">Op Hallo **SAML-instellingen bewerken** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="f83e5-187">a.</span><span class="sxs-lookup"><span data-stu-id="f83e5-187">a.</span></span> <span data-ttu-id="f83e5-188">Stel **SAML-verificatie** te**Active**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="f83e5-189">b.</span><span class="sxs-lookup"><span data-stu-id="f83e5-189">b.</span></span> <span data-ttu-id="f83e5-190">Plakken Hallo **SAML Single Sign-On Service-URL** waarde die u hebt gekopieerd uit hello Azure-portal in Hallo **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f83e5-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="f83e5-191">c.</span><span class="sxs-lookup"><span data-stu-id="f83e5-191">c.</span></span> <span data-ttu-id="f83e5-192">Plakken Hallo **Service-URL met eenmalige Sign-Out** waarde die u hebt gekopieerd uit hello Azure-portal in Hallo **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f83e5-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="f83e5-193">d.</span><span class="sxs-lookup"><span data-stu-id="f83e5-193">d.</span></span> <span data-ttu-id="f83e5-194">Klik op **bestand kiezen** tooselect uw gedownloade LockPath Keylight van het certificaat, en klik vervolgens op **Open** tooupload Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="f83e5-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="f83e5-195">e.</span><span class="sxs-lookup"><span data-stu-id="f83e5-195">e.</span></span> <span data-ttu-id="f83e5-196">Ingesteld **SAML-gebruikersnaam locatie** te**NameIdentifier-element van Hallo onderwerp instructie**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="f83e5-197">f.</span><span class="sxs-lookup"><span data-stu-id="f83e5-197">f.</span></span> <span data-ttu-id="f83e5-198">Hallo bieden **Keylight serviceprovider** met Hallo patroon volgen: **https://&lt;NaamBedrijf&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="f83e5-199">g.</span><span class="sxs-lookup"><span data-stu-id="f83e5-199">g.</span></span> <span data-ttu-id="f83e5-200">Stel **automatisch inrichten gebruikers** te**Active**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="f83e5-201">h.</span><span class="sxs-lookup"><span data-stu-id="f83e5-201">h.</span></span> <span data-ttu-id="f83e5-202">Stel **automatisch inrichten accounttype** te**volledige gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="f83e5-203">ik.</span><span class="sxs-lookup"><span data-stu-id="f83e5-203">i.</span></span> <span data-ttu-id="f83e5-204">Stel **automatisch inrichten beveiligingsrol**, selecteer **standaardgebruiker met SAML**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="f83e5-205">j.</span><span class="sxs-lookup"><span data-stu-id="f83e5-205">j.</span></span> <span data-ttu-id="f83e5-206">Stel **automatisch inrichten beveiliging config**, selecteer **standaardconfiguratie van de gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="f83e5-207">k.</span><span class="sxs-lookup"><span data-stu-id="f83e5-207">k.</span></span> <span data-ttu-id="f83e5-208">In Hallo **e kenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="f83e5-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="f83e5-209">l.</span><span class="sxs-lookup"><span data-stu-id="f83e5-209">l.</span></span> <span data-ttu-id="f83e5-210">In Hallo **voornaam kenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="f83e5-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="f83e5-211">m.</span><span class="sxs-lookup"><span data-stu-id="f83e5-211">m.</span></span> <span data-ttu-id="f83e5-212">In Hallo **laatste naamkenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="f83e5-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="f83e5-213">n.</span><span class="sxs-lookup"><span data-stu-id="f83e5-213">n.</span></span> <span data-ttu-id="f83e5-214">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f83e5-215">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f83e5-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f83e5-216">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f83e5-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f83e5-217">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f83e5-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f83e5-218">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f83e5-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="f83e5-219">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f83e5-221">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83e5-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83e5-222">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f83e5-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f83e5-224">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f83e5-226">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f83e5-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f83e5-228">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f83e5-230">a.</span><span class="sxs-lookup"><span data-stu-id="f83e5-230">a.</span></span> <span data-ttu-id="f83e5-231">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f83e5-232">b.</span><span class="sxs-lookup"><span data-stu-id="f83e5-232">b.</span></span> <span data-ttu-id="f83e5-233">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f83e5-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f83e5-234">c.</span><span class="sxs-lookup"><span data-stu-id="f83e5-234">c.</span></span> <span data-ttu-id="f83e5-235">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f83e5-236">d.</span><span class="sxs-lookup"><span data-stu-id="f83e5-236">d.</span></span> <span data-ttu-id="f83e5-237">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="f83e5-238">Een testgebruiker LockPath Keylight maken</span><span class="sxs-lookup"><span data-stu-id="f83e5-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="f83e5-239">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in LockPath Keylight maken.</span><span class="sxs-lookup"><span data-stu-id="f83e5-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="f83e5-240">LockPath Keylight ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f83e5-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="f83e5-241">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f83e5-241">There is no action item for you in this section.</span></span> <span data-ttu-id="f83e5-242">Een nieuwe gebruiker wordt gemaakt bij het openen van LockPath Keylight als Hallo gebruiker nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f83e5-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="f83e5-243">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [LockPath Keylight Client ondersteuningsteam](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f83e5-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f83e5-244">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f83e5-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f83e5-245">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="f83e5-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f83e5-247">**tooassign Britta Simon tooLockPath Keylight, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83e5-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83e5-248">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f83e5-250">Selecteer in de lijst met de toepassingen van Hallo **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="f83e5-252">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f83e5-254">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f83e5-254">Click **Add** button.</span></span> <span data-ttu-id="f83e5-255">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83e5-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f83e5-257">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f83e5-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f83e5-258">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83e5-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f83e5-259">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83e5-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f83e5-260">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f83e5-260">Testing single sign-on</span></span>

<span data-ttu-id="f83e5-261">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f83e5-262">Als u op Hallo LockPath Keylight-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour LockPath Keylight toepassing.</span><span class="sxs-lookup"><span data-stu-id="f83e5-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f83e5-263">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f83e5-263">Additional resources</span></span>

* [<span data-ttu-id="f83e5-264">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f83e5-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f83e5-265">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f83e5-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

