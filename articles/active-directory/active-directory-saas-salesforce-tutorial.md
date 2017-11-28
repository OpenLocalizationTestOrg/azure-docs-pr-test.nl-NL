---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="ad07a-103">Zelfstudie: Azure Active Directory-integratie met Salesforce</span><span class="sxs-lookup"><span data-stu-id="ad07a-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="ad07a-104">In deze zelfstudie leert u hoe toointegrate Salesforce met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad07a-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad07a-105">Salesforce integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad07a-106">U kunt beheren in Azure AD die tooSalesforce toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ad07a-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="ad07a-107">U kunt uw gebruikers tooautomatically get aangemelde tooSalesforce (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ad07a-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad07a-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ad07a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad07a-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad07a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad07a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ad07a-110">Prerequisites</span></span>

<span data-ttu-id="ad07a-111">Azure AD-integratie met Salesforce tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ad07a-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="ad07a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ad07a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad07a-113">Een Salesforce eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ad07a-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad07a-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad07a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad07a-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad07a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ad07a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad07a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad07a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad07a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ad07a-118">Scenario description</span></span>
<span data-ttu-id="ad07a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad07a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad07a-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad07a-121">Het toevoegen van Salesforce van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ad07a-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="ad07a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad07a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="ad07a-123">Het toevoegen van Salesforce van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ad07a-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="ad07a-124">tooconfigure hello integratie van Salesforce in Azure AD, moet u tooadd Salesforce uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ad07a-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad07a-125">**tooadd Salesforce via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad07a-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad07a-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad07a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad07a-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad07a-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ad07a-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ad07a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ad07a-133">Typ in het zoekvak Hallo **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-133">In hello search box, type **Salesforce**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="ad07a-135">Selecteer in het deelvenster resultaten hello, **Salesforce**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad07a-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad07a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad07a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad07a-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Salesforce op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ad07a-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ad07a-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Salesforce is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad07a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="ad07a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Salesforce toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ad07a-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="ad07a-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ad07a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="ad07a-142">tooconfigure en eenmalige aanmelding Azure AD-test met Salesforce, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad07a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ad07a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad07a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad07a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad07a-145">**[Maken van een testgebruiker Salesforce](#creating-a-salesforce-test-user)**  -toohave een equivalent van Britta Simon in Salesforce die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ad07a-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad07a-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ad07a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad07a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ad07a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad07a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ad07a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad07a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Salesforce-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad07a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="ad07a-150">**Azure AD tooconfigure eenmalige aanmelding met Salesforce, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad07a-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad07a-151">In de Azure-portal op Hallo Hallo **Salesforce** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ad07a-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ad07a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="ad07a-155">Op Hallo **Salesforce-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="ad07a-157">In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="ad07a-158">Account voor de onderneming:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ad07a-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="ad07a-159">Developer-account:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ad07a-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad07a-160">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="ad07a-160">These values are not hello real.</span></span> <span data-ttu-id="ad07a-161">Werk deze waarden met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="ad07a-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="ad07a-162">Neem contact op met [Salesforce Client ondersteuningsteam](https://help.salesforce.com/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ad07a-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="ad07a-163">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ad07a-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="ad07a-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ad07a-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad07a-167">Op Hallo **Salesforce configuratie** sectie, klikt u op **configureren Salesforce** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ad07a-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ad07a-168">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ad07a-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="ad07a-169">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="ad07a-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="ad07a-170">Een nieuw tabblad openen in uw browser en meld u bij tooyour Salesforce administrator-account.</span><span class="sxs-lookup"><span data-stu-id="ad07a-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="ad07a-171">Onder Hallo **beheerder** navigatiedeelvenster, klikt u op **beveiligingsmechanismen** tooexpand Hallo gerelateerde sectie.</span><span class="sxs-lookup"><span data-stu-id="ad07a-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="ad07a-172">Klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-172">Then click **Single Sign-On Settings**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="ad07a-174">Op Hallo **instellingen voor eenmalige aanmelding** pagina, klikt u op Hallo **bewerken** knop.</span><span class="sxs-lookup"><span data-stu-id="ad07a-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="ad07a-175">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="ad07a-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="ad07a-176">Als u instellingen voor eenmalige aanmelding niet kan tooenable voor uw Salesforce-account zijn, moet u mogelijk toocontact [Salesforce Client ondersteuningsteam](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="ad07a-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="ad07a-177">Selecteer **SAML ingeschakeld**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="ad07a-179">tooconfigure uw SAML eenmalige aanmelding-instellingen, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="ad07a-181">Op Hallo **SAML Single Sign-On instelling bewerken** maken Hallo volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="ad07a-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="ad07a-183">a.</span><span class="sxs-lookup"><span data-stu-id="ad07a-183">a.</span></span> <span data-ttu-id="ad07a-184">Voor Hallo **naam** veld, typ een beschrijvende naam voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="ad07a-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="ad07a-185">Om een waarde voor **naam** automatisch invullen Hallo **API-naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="ad07a-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="ad07a-186">b.</span><span class="sxs-lookup"><span data-stu-id="ad07a-186">b.</span></span> <span data-ttu-id="ad07a-187">Plakken **SMAL entiteit-ID** waarde in Hallo **verlener** veld in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ad07a-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="ad07a-188">c.</span><span class="sxs-lookup"><span data-stu-id="ad07a-188">c.</span></span> <span data-ttu-id="ad07a-189">In Hallo **tekstvak voor de entiteit-Id**, typ de naam van uw Salesforce-domein met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="ad07a-190">Account voor de onderneming:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ad07a-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="ad07a-191">Developer-account:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ad07a-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="ad07a-192">d.</span><span class="sxs-lookup"><span data-stu-id="ad07a-192">d.</span></span> <span data-ttu-id="ad07a-193">Klik op **Bladeren** of **bestand kiezen** tooopen hello **bestand kiezen tooUpload** dialoogvenster uw Salesforce-certificaat selecteren en klik vervolgens op **Openen**tooupload Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="ad07a-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="ad07a-194">e.</span><span class="sxs-lookup"><span data-stu-id="ad07a-194">e.</span></span> <span data-ttu-id="ad07a-195">Voor **SAML identiteitstype**, selecteer **verklaring van de gebruiker salesforce.com gebruikersnaam bevat**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="ad07a-196">f.</span><span class="sxs-lookup"><span data-stu-id="ad07a-196">f.</span></span> <span data-ttu-id="ad07a-197">Voor **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentifier element van Hallo onderwerp instructie**</span><span class="sxs-lookup"><span data-stu-id="ad07a-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="ad07a-198">g.</span><span class="sxs-lookup"><span data-stu-id="ad07a-198">g.</span></span> <span data-ttu-id="ad07a-199">Plakken **Single Sign-On Service-URL** in Hallo **identiteit Provider aanmeldings-URL** veld in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ad07a-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="ad07a-200">h.</span><span class="sxs-lookup"><span data-stu-id="ad07a-200">h.</span></span> <span data-ttu-id="ad07a-201">Voor **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP-omleiding**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="ad07a-202">ik.</span><span class="sxs-lookup"><span data-stu-id="ad07a-202">i.</span></span> <span data-ttu-id="ad07a-203">Tot slot op **opslaan** tooapply uw SAML eenmalige aanmelding-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ad07a-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="ad07a-204">Klik op Hallo navigatiedeelvenster links in Salesforce **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="ad07a-206">Schuif omlaag toohello **verificatieconfiguratie** sectie en op Hallo **bewerken** knop.</span><span class="sxs-lookup"><span data-stu-id="ad07a-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="ad07a-208">In Hallo **verificatieservice** sectie, beschrijvende naam van uw configuratie SAML SSO Hallo selecteren en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="ad07a-210">Als meer dan één authentication-service is ingeschakeld, kunnen gebruikers zich na vragen aan gebruiker tooselect welke verificatieservice die ze willen toosign met tijdens de initialisatie van eenmalige aanmelding tooyour Salesforce-omgeving.</span><span class="sxs-lookup"><span data-stu-id="ad07a-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="ad07a-211">Als u niet dat deze toohappen wilt, dan u moet **laat alle andere verificatieservices uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="ad07a-212">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ad07a-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad07a-213">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ad07a-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad07a-214">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad07a-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad07a-215">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ad07a-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad07a-216">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ad07a-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ad07a-218">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad07a-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad07a-219">Op Hallo linkernavigatiedeelvenster in Hallo **Azure-portal**, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad07a-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad07a-221">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad07a-223">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad07a-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad07a-225">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad07a-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad07a-227">a.</span><span class="sxs-lookup"><span data-stu-id="ad07a-227">a.</span></span> <span data-ttu-id="ad07a-228">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad07a-229">b.</span><span class="sxs-lookup"><span data-stu-id="ad07a-229">b.</span></span> <span data-ttu-id="ad07a-230">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad07a-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad07a-231">c.</span><span class="sxs-lookup"><span data-stu-id="ad07a-231">c.</span></span> <span data-ttu-id="ad07a-232">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad07a-233">d.</span><span class="sxs-lookup"><span data-stu-id="ad07a-233">d.</span></span> <span data-ttu-id="ad07a-234">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="ad07a-235">Een testgebruiker Salesforce maken</span><span class="sxs-lookup"><span data-stu-id="ad07a-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="ad07a-236">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ad07a-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="ad07a-237">SalesForce ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ad07a-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="ad07a-238">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="ad07a-238">There is no action item for you in this section.</span></span> <span data-ttu-id="ad07a-239">Als een gebruiker in Salesforce nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess Salesforce probeert.</span><span class="sxs-lookup"><span data-stu-id="ad07a-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad07a-240">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad07a-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad07a-241">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSalesforce toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ad07a-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ad07a-243">**tooassign Britta Simon tooSalesforce, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad07a-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad07a-244">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ad07a-246">Selecteer in de lijst met de toepassingen van Hallo **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-246">In hello applications list, select **Salesforce**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="ad07a-248">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ad07a-250">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ad07a-250">Click **Add** button.</span></span> <span data-ttu-id="ad07a-251">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad07a-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ad07a-253">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad07a-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad07a-254">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad07a-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad07a-255">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad07a-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad07a-256">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad07a-256">Testing single sign-on</span></span>

<span data-ttu-id="ad07a-257">tootest uw eenmalige aanmelding-instellingen, open Hallo Toegangsvenster op [https://myapps.microsoft.com](https://myapps.microsoft.com/), meldt u zich bij Hallo test-account en klikt u op **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="ad07a-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad07a-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad07a-258">Additional resources</span></span>

* [<span data-ttu-id="ad07a-259">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad07a-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad07a-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad07a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ad07a-261">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="ad07a-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

