---
title: 'Zelfstudie: Azure Active Directory-integratie met werken als een team | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werken als een team.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="4a1b2-103">Zelfstudie: Azure Active Directory-integratie met werken als een team</span><span class="sxs-lookup"><span data-stu-id="4a1b2-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="4a1b2-104">In deze zelfstudie leert u hoe toointegrate werken als een team met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a1b2-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a1b2-105">Werken als een team integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4a1b2-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a1b2-106">U kunt beheren in Azure AD die tooTeamwork toegang heeft</span><span class="sxs-lookup"><span data-stu-id="4a1b2-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="4a1b2-107">U kunt uw gebruikers tooautomatically get aangemelde tooTeamwork (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4a1b2-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a1b2-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="4a1b2-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="4a1b2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a1b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a1b2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4a1b2-110">Prerequisites</span></span>

<span data-ttu-id="4a1b2-111">Azure AD-integratie met werken als een team tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4a1b2-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="4a1b2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4a1b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a1b2-113">Een werken als een team eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4a1b2-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="4a1b2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="4a1b2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4a1b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a1b2-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4a1b2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a1b2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="4a1b2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4a1b2-118">Scenario description</span></span>
<span data-ttu-id="4a1b2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a1b2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4a1b2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a1b2-121">Het toevoegen van werken als een team van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4a1b2-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="4a1b2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4a1b2-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="4a1b2-123">Het toevoegen van werken als een team van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4a1b2-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="4a1b2-124">tooconfigure hello integratie van werken als een team in Azure AD, moet u tooadd werken als een team van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a1b2-125">**tooadd werken als een team via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4a1b2-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a1b2-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4a1b2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a1b2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4a1b2-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4a1b2-133">Typ in het zoekvak Hallo **werken als een team**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-133">In hello search box, type **Teamwork**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="4a1b2-135">Selecteer in het deelvenster resultaten hello, **werken als een team**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a1b2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4a1b2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a1b2-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met werken als een team op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a1b2-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in werken als een team is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="4a1b2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in werken als een team toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="4a1b2-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in werken als een team.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="4a1b2-142">tooconfigure en eenmalige aanmelding Azure AD-test met werken als een team, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a1b2-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a1b2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a1b2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a1b2-145">**[Maken van een testgebruiker werken als een team](#creating-a-teamwork-test-user)**  -toohave een equivalent van Britta Simon in werken als een team dat is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="4a1b2-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a1b2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a1b2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4a1b2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a1b2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing werken als een team.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="4a1b2-150">**Azure AD tooconfigure eenmalige aanmelding met werken als een team, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a1b2-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a1b2-151">In hello Azure Management portal op Hallo **werken als een team** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4a1b2-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="4a1b2-155">Op Hallo **werken als een team domein en de URL's** sectie in Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="4a1b2-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="4a1b2-157">Houd er rekening mee dat dit geen Hallo echte waarde is.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="4a1b2-158">U hebt deze waarde Hello werkelijke aanmelden URL tooupdate.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="4a1b2-159">Neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="4a1b2-160">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="4a1b2-162">Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="4a1b2-163">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-163">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="4a1b2-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="4a1b2-167">Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4a1b2-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="4a1b2-171">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) en voorzien Hallo gedownload **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a1b2-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4a1b2-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a1b2-173">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4a1b2-175">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a1b2-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a1b2-176">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a1b2-178">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a1b2-180">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a1b2-182">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a1b2-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a1b2-184">a.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-184">a.</span></span> <span data-ttu-id="4a1b2-185">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a1b2-186">b.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-186">b.</span></span> <span data-ttu-id="4a1b2-187">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a1b2-188">c.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-188">c.</span></span> <span data-ttu-id="4a1b2-189">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a1b2-190">d.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-190">d.</span></span> <span data-ttu-id="4a1b2-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="4a1b2-192">Een testgebruiker werken als een team maken</span><span class="sxs-lookup"><span data-stu-id="4a1b2-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="4a1b2-193">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in werken als een team.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="4a1b2-194">Neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) tooadd Hallo gebruikers in Hallo werken als een team platform.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4a1b2-195">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a1b2-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4a1b2-196">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooTeamwork toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4a1b2-198">**tooassign Britta Simon tooTeamwork, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a1b2-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a1b2-199">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4a1b2-201">Selecteer in de lijst met de toepassingen van Hallo **werken als een team**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-201">In hello applications list, select **Teamwork**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="4a1b2-203">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4a1b2-205">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-205">Click **Add** button.</span></span> <span data-ttu-id="4a1b2-206">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4a1b2-208">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a1b2-209">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a1b2-210">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="4a1b2-211">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4a1b2-211">Testing single sign-on</span></span>

<span data-ttu-id="4a1b2-212">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4a1b2-213">Als u op Hallo werken als een team tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour werken als een team toepassing.</span><span class="sxs-lookup"><span data-stu-id="4a1b2-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4a1b2-214">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4a1b2-214">Additional resources</span></span>

* [<span data-ttu-id="4a1b2-215">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a1b2-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a1b2-216">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a1b2-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png