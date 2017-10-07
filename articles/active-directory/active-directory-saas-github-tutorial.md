---
title: 'Zelfstudie: Azure Active Directory-integratie met GitHub | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="aaa32-103">Zelfstudie: Azure Active Directory-integratie met GitHub</span><span class="sxs-lookup"><span data-stu-id="aaa32-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="aaa32-104">In deze zelfstudie leert u hoe toointegrate GitHub met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aaa32-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aaa32-105">GitHub integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="aaa32-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aaa32-106">U kunt beheren in Azure AD die tooGitHub toegang heeft</span><span class="sxs-lookup"><span data-stu-id="aaa32-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="aaa32-107">U kunt uw gebruikers tooautomatically get aangemelde tooGitHub (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="aaa32-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aaa32-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="aaa32-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="aaa32-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aaa32-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aaa32-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aaa32-110">Prerequisites</span></span>

<span data-ttu-id="aaa32-111">tooconfigure Azure AD-integratie met GitHub, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="aaa32-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="aaa32-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="aaa32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aaa32-113">Een GitHub-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="aaa32-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="aaa32-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="aaa32-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="aaa32-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="aaa32-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aaa32-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="aaa32-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="aaa32-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aaa32-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="aaa32-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="aaa32-118">Scenario description</span></span>
<span data-ttu-id="aaa32-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="aaa32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aaa32-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="aaa32-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aaa32-121">Het toevoegen van GitHub van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="aaa32-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="aaa32-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aaa32-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="aaa32-123">Het toevoegen van GitHub van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="aaa32-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="aaa32-124">tooconfigure hello integratie van GitHub in Azure AD, moet u tooadd GitHub uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="aaa32-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aaa32-125">**tooadd GitHub via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aaa32-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aaa32-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aaa32-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aaa32-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aaa32-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="aaa32-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="aaa32-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="aaa32-133">Typ in het zoekvak Hallo **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-133">In hello search box, type **GitHub.com**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="aaa32-135">Selecteer in het deelvenster resultaten hello, **GitHub**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aaa32-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aaa32-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aaa32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aaa32-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met GitHub op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="aaa32-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aaa32-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in GitHub is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aaa32-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="aaa32-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in GitHub toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="aaa32-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="aaa32-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in GitHub.</span><span class="sxs-lookup"><span data-stu-id="aaa32-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="aaa32-142">tooconfigure en eenmalige aanmelding Azure AD-test met GitHub, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aaa32-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aaa32-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="aaa32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aaa32-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aaa32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aaa32-145">**[Maken van een testgebruiker GitHub](#creating-a-GitHub-test-user)**  -toohave een equivalent van Britta Simon in GitHub die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="aaa32-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="aaa32-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aaa32-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aaa32-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="aaa32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aaa32-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="aaa32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aaa32-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw GitHub-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aaa32-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="aaa32-150">**Azure AD tooconfigure eenmalige aanmelding met GitHub, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aaa32-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="aaa32-151">In hello Azure Management portal op Hallo **GitHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="aaa32-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aaa32-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="aaa32-155">Op Hallo **GitHub-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aaa32-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="aaa32-157">a.</span><span class="sxs-lookup"><span data-stu-id="aaa32-157">a.</span></span> <span data-ttu-id="aaa32-158">In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="aaa32-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="aaa32-159">b.</span><span class="sxs-lookup"><span data-stu-id="aaa32-159">b.</span></span> <span data-ttu-id="aaa32-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="aaa32-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aaa32-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="aaa32-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="aaa32-162">U hebt deze waarden met Hallo werkelijke Kana-URL en id tooupdate.</span><span class="sxs-lookup"><span data-stu-id="aaa32-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="aaa32-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="aaa32-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="aaa32-164">Ga tooGitHub Admin sectie tooretrieve deze waarden.</span><span class="sxs-lookup"><span data-stu-id="aaa32-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="aaa32-165">Op Hallo **gebruikerskenmerken** sectie **gebruikers-id** als user.mail.</span><span class="sxs-lookup"><span data-stu-id="aaa32-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="aaa32-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="aaa32-169">Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="aaa32-170">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="aaa32-170">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="aaa32-172">Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="aaa32-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="aaa32-174">Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="aaa32-176">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="aaa32-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="aaa32-178">Op Hallo **GitHub configuratie** sectie, klikt u op **configureren GitHub** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="aaa32-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="aaa32-181">Meld u in een ander browservenster in uw organisatie GitHub site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aaa32-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="aaa32-182">Navigeer te**instellingen** en klik op **beveiliging**</span><span class="sxs-lookup"><span data-stu-id="aaa32-182">Navigate too**Settings** and click **Security**</span></span>

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="aaa32-184">Controleer Hallo **inschakelen SAML-verificatie** vak Hallo Single Sign-on configuratievelden weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aaa32-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="aaa32-185">Gebruik vervolgens Hallo eenmalige aanmelding URL waarde tooupdate Hallo één aanmeldings-URL op Azure AD-configuratie.</span><span class="sxs-lookup"><span data-stu-id="aaa32-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="aaa32-187">Hallo velden volgende configureren:</span><span class="sxs-lookup"><span data-stu-id="aaa32-187">Configure hello following fields:</span></span>

    <span data-ttu-id="aaa32-188">a.</span><span class="sxs-lookup"><span data-stu-id="aaa32-188">a.</span></span> <span data-ttu-id="aaa32-189">**Meld u aan op de URL voor**: Voer **SAML eenmalige aanmelding Service-URL** van Hallo **GitHub configureren** sectie over Azure AD</span><span class="sxs-lookup"><span data-stu-id="aaa32-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="aaa32-190">b.</span><span class="sxs-lookup"><span data-stu-id="aaa32-190">b.</span></span> <span data-ttu-id="aaa32-191">**Certificaatverlener**: Voer **SAML entiteit-ID** van Hallo **GitHub configureren** sectie over Azure AD</span><span class="sxs-lookup"><span data-stu-id="aaa32-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="aaa32-192">c.</span><span class="sxs-lookup"><span data-stu-id="aaa32-192">c.</span></span> <span data-ttu-id="aaa32-193">**Openbaar certificaat**: Open Hallo certificaat gedownload vanuit Azure AD in Kladblok en kopieer Hallo inhoud zoals 'BEGIN CERTIFICATE' en 'END CERTIFICATE'</span><span class="sxs-lookup"><span data-stu-id="aaa32-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="aaa32-195">Klik op **Test SAML-configuratie** tooconfirm die geen validatiefouten of fouten tijdens eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aaa32-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="aaa32-197">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="aaa32-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aaa32-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="aaa32-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="aaa32-199">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="aaa32-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="aaa32-201">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aaa32-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aaa32-202">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aaa32-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aaa32-204">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="aaa32-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aaa32-206">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aaa32-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aaa32-208">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aaa32-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aaa32-210">a.</span><span class="sxs-lookup"><span data-stu-id="aaa32-210">a.</span></span> <span data-ttu-id="aaa32-211">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aaa32-212">b.</span><span class="sxs-lookup"><span data-stu-id="aaa32-212">b.</span></span> <span data-ttu-id="aaa32-213">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aaa32-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aaa32-214">c.</span><span class="sxs-lookup"><span data-stu-id="aaa32-214">c.</span></span> <span data-ttu-id="aaa32-215">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aaa32-216">d.</span><span class="sxs-lookup"><span data-stu-id="aaa32-216">d.</span></span> <span data-ttu-id="aaa32-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="aaa32-218">De gebruiker van een GitHub-test maken</span><span class="sxs-lookup"><span data-stu-id="aaa32-218">Creating a GitHub test user</span></span>

<span data-ttu-id="aaa32-219">In de volgorde tooenable Azure AD gebruikers toolog in GitHub, moeten ze worden ingericht in GitHub.</span><span class="sxs-lookup"><span data-stu-id="aaa32-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="aaa32-220">In geval van GitHub Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="aaa32-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="aaa32-221">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="aaa32-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="aaa32-222">Aanmelden tooyour GitHub bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aaa32-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="aaa32-223">Klik op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-223">Click **People**.</span></span>

    <span data-ttu-id="aaa32-224">![Mensen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "personen")</span><span class="sxs-lookup"><span data-stu-id="aaa32-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="aaa32-225">Klik op **uitnodiging lid**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-225">Click **Invite member**.</span></span>

    <span data-ttu-id="aaa32-226">![Gebruikers uitnodigen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "gebruikers uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="aaa32-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="aaa32-227">Op Hallo **uitnodiging lid** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aaa32-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="aaa32-228">a.</span><span class="sxs-lookup"><span data-stu-id="aaa32-228">a.</span></span> <span data-ttu-id="aaa32-229">In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="aaa32-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="aaa32-230">![Personen uitnodigen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="aaa32-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="aaa32-231">b.</span><span class="sxs-lookup"><span data-stu-id="aaa32-231">b.</span></span> <span data-ttu-id="aaa32-232">Klik op **uitnodiging**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="aaa32-233">![Personen uitnodigen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="aaa32-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="aaa32-234">Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="aaa32-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aaa32-235">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aaa32-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aaa32-236">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooGitHub toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="aaa32-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="aaa32-238">**tooassign Britta Simon tooGitHub, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aaa32-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="aaa32-239">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="aaa32-241">Selecteer in de lijst met de toepassingen van Hallo **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="aaa32-243">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="aaa32-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="aaa32-245">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="aaa32-245">Click **Add** button.</span></span> <span data-ttu-id="aaa32-246">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aaa32-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="aaa32-248">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="aaa32-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aaa32-249">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aaa32-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aaa32-250">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aaa32-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="aaa32-251">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aaa32-251">Testing single sign-on</span></span>

<span data-ttu-id="aaa32-252">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="aaa32-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aaa32-253">Als u op Hallo GitHub-tegel in Hallo Toegangsvenster, krijgt u aangemelde tooyour GitHub-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aaa32-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="aaa32-254">U moet als een organisatie-account maar moeten toolog worden aanmelden met uw persoonlijke account.</span><span class="sxs-lookup"><span data-stu-id="aaa32-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="aaa32-255">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="aaa32-255">Additional resources</span></span>

* [<span data-ttu-id="aaa32-256">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aaa32-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aaa32-257">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aaa32-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
