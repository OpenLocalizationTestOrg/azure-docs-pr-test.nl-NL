---
title: 'Zelfstudie: Azure Active Directory-integratie met xMatters OnDemand | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="d764c-103">Zelfstudie: Azure Active Directory-integratie met xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="d764c-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="d764c-104">In deze zelfstudie leert u hoe toointegrate xMatters OnDemand met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d764c-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d764c-105">XMatters OnDemand integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d764c-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d764c-106">U kunt beheren in Azure AD wie toegang tot tooxMatters OnDemand heeft</span><span class="sxs-lookup"><span data-stu-id="d764c-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="d764c-107">U kunt uw gebruikers tooautomatically get aangemelde tooxMatters OnDemand (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d764c-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d764c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d764c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d764c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d764c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d764c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d764c-110">Prerequisites</span></span>

<span data-ttu-id="d764c-111">Azure AD-integratie met xMatters OnDemand tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d764c-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="d764c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d764c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d764c-113">Een xMatters eenmalige aanmelding OnDemand abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="d764c-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d764c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d764c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d764c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d764c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d764c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d764c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d764c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d764c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d764c-118">Scenario description</span></span>
<span data-ttu-id="d764c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d764c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d764c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d764c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d764c-121">Het toevoegen van xMatters OnDemand van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d764c-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="d764c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d764c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="d764c-123">Het toevoegen van xMatters OnDemand van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d764c-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="d764c-124">tooconfigure hello integratie van xMatters OnDemand in Azure AD, moet u tooadd xMatters OnDemand uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d764c-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d764c-125">**tooadd xMatters OnDemand via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d764c-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d764c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d764c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d764c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d764c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d764c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d764c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d764c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d764c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d764c-133">Typ in het zoekvak Hallo **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="d764c-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="d764c-135">Selecteer in het deelvenster resultaten hello, **xMatters OnDemand**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d764c-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d764c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d764c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d764c-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met xMatters die OnDemand op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d764c-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d764c-139">Voor één aanmelding toowork Azure AD moet tooknow welke Hallo equivalent in xMatters OnDemand is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d764c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="d764c-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in xMatters moet OnDemand toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d764c-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="d764c-141">In xMatters OnDemand, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="d764c-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d764c-142">tooconfigure en eenmalige aanmelding Azure AD-test met xMatters OnDemand, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d764c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d764c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d764c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d764c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d764c-145">**[Maken van een gebruiker xMatters OnDemand test](#creating-a-xmatters-ondemand-test-user)**  -toohave een equivalent van Britta Simon in xMatters OnDemand die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d764c-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d764c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d764c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d764c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d764c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d764c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d764c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d764c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw xMatters OnDemand-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d764c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="d764c-150">**Azure AD tooconfigure eenmalige aanmelding met xMatters OnDemand, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d764c-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="d764c-151">In de Azure-portal op Hallo Hallo **xMatters OnDemand** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d764c-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d764c-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d764c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="d764c-155">Op Hallo **xMatters OnDemand domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="d764c-157">a.</span><span class="sxs-lookup"><span data-stu-id="d764c-157">a.</span></span> <span data-ttu-id="d764c-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="d764c-159">b.</span><span class="sxs-lookup"><span data-stu-id="d764c-159">b.</span></span> <span data-ttu-id="d764c-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="d764c-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="d764c-161">These values are not real.</span></span> <span data-ttu-id="d764c-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="d764c-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d764c-163">Neem contact op met [ondersteuningsteam voor OnDemand xMatters](https://www.xmatters.com/company/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d764c-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="d764c-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand van Hallo lokaal als **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="d764c-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="d764c-166">U moet tooforward Hallo certificaat toohello [ondersteuningsteam voor OnDemand xMatters](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="d764c-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="d764c-167">Hallo-certificaat moet toobe geüpload door Hallo xMatters ondersteuningsteam voordat u kunt één Hallo aanmelding configuratie voltooien.</span><span class="sxs-lookup"><span data-stu-id="d764c-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="d764c-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d764c-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d764c-170">Op Hallo **xMatters OnDemand configuratie** sectie, klikt u op **xMatters OnDemand configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d764c-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d764c-171">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d764c-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="d764c-173">In een ander browservenster aanmelden tooyour XMatters OnDemand bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d764c-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="d764c-174">Klik in de werkbalk bovenaan Hallo Hallo op **Admin**, en klik vervolgens op **bedrijfsgegevens** in de navigatiebalk Hallo op Hallo linkerkant.</span><span class="sxs-lookup"><span data-stu-id="d764c-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="d764c-175">![Beheerder](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="d764c-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="d764c-176">Op Hallo **SAML-configuratie** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d764c-177">![De SAML-configuratie](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="d764c-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="d764c-178">a.</span><span class="sxs-lookup"><span data-stu-id="d764c-178">a.</span></span> <span data-ttu-id="d764c-179">Selecteer **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="d764c-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="d764c-180">b.</span><span class="sxs-lookup"><span data-stu-id="d764c-180">b.</span></span> <span data-ttu-id="d764c-181">Plakken **SAML entiteit-ID**, die u hebt gekopieerd uit hello Azure-portal in Hallo **identiteit Provider-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="d764c-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="d764c-182">c.</span><span class="sxs-lookup"><span data-stu-id="d764c-182">c.</span></span> <span data-ttu-id="d764c-183">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **eenmalige aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d764c-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="d764c-184">d.</span><span class="sxs-lookup"><span data-stu-id="d764c-184">d.</span></span> <span data-ttu-id="d764c-185">Plakken **Sign-Out URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **-URL met eenmalige afmelding** textbox.</span><span class="sxs-lookup"><span data-stu-id="d764c-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="d764c-186">e.</span><span class="sxs-lookup"><span data-stu-id="d764c-186">e.</span></span> <span data-ttu-id="d764c-187">Klik op Hallo bedrijfsgegevens pagina boven Hallo op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d764c-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="d764c-188">![Details voor de bedrijfsportal](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "details voor de bedrijfsportal")</span><span class="sxs-lookup"><span data-stu-id="d764c-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="d764c-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="d764c-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d764c-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="d764c-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d764c-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d764c-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d764c-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d764c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d764c-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d764c-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d764c-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d764c-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d764c-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d764c-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d764c-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d764c-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d764c-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d764c-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d764c-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d764c-204">a.</span><span class="sxs-lookup"><span data-stu-id="d764c-204">a.</span></span> <span data-ttu-id="d764c-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d764c-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d764c-206">b.</span><span class="sxs-lookup"><span data-stu-id="d764c-206">b.</span></span> <span data-ttu-id="d764c-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d764c-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d764c-208">c.</span><span class="sxs-lookup"><span data-stu-id="d764c-208">c.</span></span> <span data-ttu-id="d764c-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d764c-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d764c-210">d.</span><span class="sxs-lookup"><span data-stu-id="d764c-210">d.</span></span> <span data-ttu-id="d764c-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d764c-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="d764c-212">Maken van een gebruiker xMatters OnDemand testen</span><span class="sxs-lookup"><span data-stu-id="d764c-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="d764c-213">In volgorde tooenable Azure AD gebruikers toolog in tooXMatters OnDemand, moeten ze worden ingericht in XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="d764c-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="d764c-214">In geval van XMatters OnDemand Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="d764c-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="d764c-215">tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d764c-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="d764c-216">Meld u bij tooyour **XMatters OnDemand** tenant.</span><span class="sxs-lookup"><span data-stu-id="d764c-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="d764c-217">Klik op **gebruikers** tabblad en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d764c-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="d764c-218">![Gebruikers](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="d764c-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="d764c-219">In Hallo **toevoegen van een gebruiker** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d764c-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d764c-220">![Een gebruiker toevoegen](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "een gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="d764c-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="d764c-221">a.</span><span class="sxs-lookup"><span data-stu-id="d764c-221">a.</span></span> <span data-ttu-id="d764c-222">Selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="d764c-222">Select **Active**.</span></span>

    <span data-ttu-id="d764c-223">b.</span><span class="sxs-lookup"><span data-stu-id="d764c-223">b.</span></span> <span data-ttu-id="d764c-224">In Hallo **gebruikers-ID** textbox type Hallo id van gebruiker zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d764c-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="d764c-225">c.</span><span class="sxs-lookup"><span data-stu-id="d764c-225">c.</span></span> <span data-ttu-id="d764c-226">In Hallo **voornaam** textbox type voornaam van de gebruiker Hallo zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="d764c-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="d764c-227">d.</span><span class="sxs-lookup"><span data-stu-id="d764c-227">d.</span></span> <span data-ttu-id="d764c-228">In Hallo **achternaam** textbox achternaam van de gebruiker Hallo zoals Simon type.</span><span class="sxs-lookup"><span data-stu-id="d764c-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="d764c-229">e.</span><span class="sxs-lookup"><span data-stu-id="d764c-229">e.</span></span> <span data-ttu-id="d764c-230">In Hallo **Site** textbox Enter Hallo geldige site van een geldig Azure AD-account die u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d764c-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="d764c-231">f.</span><span class="sxs-lookup"><span data-stu-id="d764c-231">f.</span></span> <span data-ttu-id="d764c-232">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d764c-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d764c-233">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d764c-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d764c-234">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooxMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="d764c-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d764c-236">**tooassign Britta Simon tooxMatters OnDemand, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d764c-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="d764c-237">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d764c-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d764c-239">Selecteer in de lijst met de toepassingen van Hallo **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="d764c-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="d764c-241">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d764c-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d764c-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d764c-243">Click **Add** button.</span></span> <span data-ttu-id="d764c-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d764c-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d764c-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d764c-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d764c-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d764c-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d764c-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d764c-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d764c-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d764c-249">Testing single sign-on</span></span>

<span data-ttu-id="d764c-250">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d764c-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d764c-251">Als u op Hallo xMatters OnDemand-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour xMatters OnDemand-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d764c-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="d764c-252">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d764c-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d764c-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d764c-253">Additional resources</span></span>

* [<span data-ttu-id="d764c-254">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d764c-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d764c-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d764c-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

