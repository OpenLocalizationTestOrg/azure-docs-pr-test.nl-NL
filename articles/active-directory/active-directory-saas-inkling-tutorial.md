---
title: 'Zelfstudie: Azure Active Directory-integratie met Inkling | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Inkling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="94451-103">Zelfstudie: Azure Active Directory-integratie met Inkling</span><span class="sxs-lookup"><span data-stu-id="94451-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="94451-104">In deze zelfstudie leert u hoe toointegrate Inkling met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94451-104">In this tutorial, you learn how toointegrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94451-105">Inkling integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="94451-105">Integrating Inkling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="94451-106">U kunt beheren in Azure AD die tooInkling toegang heeft</span><span class="sxs-lookup"><span data-stu-id="94451-106">You can control in Azure AD who has access tooInkling</span></span>
- <span data-ttu-id="94451-107">U kunt uw gebruikers tooautomatically get aangemelde tooInkling (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="94451-107">You can enable your users tooautomatically get signed-on tooInkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94451-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="94451-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="94451-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94451-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94451-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="94451-110">Prerequisites</span></span>

<span data-ttu-id="94451-111">Azure AD-integratie met Inkling tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="94451-111">tooconfigure Azure AD integration with Inkling, you need hello following items:</span></span>

- <span data-ttu-id="94451-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="94451-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94451-113">Een Inkling eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="94451-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="94451-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="94451-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="94451-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="94451-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94451-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="94451-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="94451-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94451-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="94451-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="94451-118">Scenario description</span></span>
<span data-ttu-id="94451-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="94451-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94451-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="94451-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94451-121">Het toevoegen van Inkling van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="94451-121">Adding Inkling from hello gallery</span></span>
2. <span data-ttu-id="94451-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94451-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-hello-gallery"></a><span data-ttu-id="94451-123">Het toevoegen van Inkling van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="94451-123">Adding Inkling from hello gallery</span></span>
<span data-ttu-id="94451-124">tooconfigure hello integratie van Inkling in Azure AD, moet u tooadd Inkling uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="94451-124">tooconfigure hello integration of Inkling into Azure AD, you need tooadd Inkling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="94451-125">**tooadd Inkling via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94451-125">**tooadd Inkling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="94451-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="94451-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94451-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94451-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="94451-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94451-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="94451-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="94451-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="94451-133">Typ in het zoekvak Hallo **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="94451-133">In hello search box, type **Inkling**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="94451-135">Selecteer in het deelvenster resultaten hello, **Inkling**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="94451-135">In hello results panel, select **Inkling**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94451-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94451-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94451-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Inkling op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="94451-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94451-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Inkling is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94451-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Inkling is tooa user in Azure AD.</span></span> <span data-ttu-id="94451-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Inkling toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="94451-140">In other words, a link relationship between an Azure AD user and hello related user in Inkling needs toobe established.</span></span>

<span data-ttu-id="94451-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Inkling.</span><span class="sxs-lookup"><span data-stu-id="94451-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Inkling.</span></span>

<span data-ttu-id="94451-142">tooconfigure en eenmalige aanmelding Azure AD-test met Inkling, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94451-142">tooconfigure and test Azure AD single sign-on with Inkling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="94451-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="94451-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="94451-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94451-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94451-145">**[Maken van een testgebruiker Inkling](#creating-an-inkling-test-user)**  -toohave een equivalent van Britta Simon in Inkling die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="94451-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - toohave a counterpart of Britta Simon in Inkling that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="94451-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="94451-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94451-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="94451-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94451-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="94451-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94451-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing Inkling configureren.</span><span class="sxs-lookup"><span data-stu-id="94451-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="94451-150">**Azure AD tooconfigure eenmalige aanmelding met Inkling, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94451-150">**tooconfigure Azure AD single sign-on with Inkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="94451-151">In hello Azure Management portal op Hallo **Inkling** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="94451-151">In hello Azure Management portal, on hello **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="94451-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="94451-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="94451-155">Op Hallo **Inkling domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94451-155">On hello **Inkling Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="94451-157">a.</span><span class="sxs-lookup"><span data-stu-id="94451-157">a.</span></span> <span data-ttu-id="94451-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="94451-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="94451-159">b.</span><span class="sxs-lookup"><span data-stu-id="94451-159">b.</span></span> <span data-ttu-id="94451-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="94451-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94451-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="94451-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="94451-162">U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="94451-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="94451-163">Neem contact op met [Inkling ondersteuningsteam](mailto:press@inkling.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="94451-163">Contact [Inkling support team](mailto:press@inkling.com) tooget these values.</span></span>

4. <span data-ttu-id="94451-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="94451-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="94451-166">Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="94451-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="94451-167">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="94451-167">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="94451-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="94451-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="94451-171">Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="94451-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="94451-173">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="94451-173">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="94451-175">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [Inkling ondersteuningsteam](mailto:press@inkling.com) en bieden ze gedownload met **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="94451-175">tooget SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94451-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="94451-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="94451-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="94451-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="94451-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94451-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="94451-180">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="94451-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94451-182">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="94451-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94451-184">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94451-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94451-186">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94451-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94451-188">a.</span><span class="sxs-lookup"><span data-stu-id="94451-188">a.</span></span> <span data-ttu-id="94451-189">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94451-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94451-190">b.</span><span class="sxs-lookup"><span data-stu-id="94451-190">b.</span></span> <span data-ttu-id="94451-191">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94451-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94451-192">c.</span><span class="sxs-lookup"><span data-stu-id="94451-192">c.</span></span> <span data-ttu-id="94451-193">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="94451-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="94451-194">d.</span><span class="sxs-lookup"><span data-stu-id="94451-194">d.</span></span> <span data-ttu-id="94451-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="94451-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="94451-196">Een testgebruiker Inkling maken</span><span class="sxs-lookup"><span data-stu-id="94451-196">Creating an Inkling test user</span></span>

<span data-ttu-id="94451-197">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Inkling maken.</span><span class="sxs-lookup"><span data-stu-id="94451-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="94451-198">Neem contact op met [Inkling ondersteuningsteam](mailto:press@inkling.com) tooadd Hallo gebruikers in Hallo Inkling platform.</span><span class="sxs-lookup"><span data-stu-id="94451-198">Please work with [Inkling support team](mailto:press@inkling.com) tooadd hello users in hello Inkling platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="94451-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="94451-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="94451-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooInkling toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="94451-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooInkling.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="94451-202">**tooassign Britta Simon tooInkling, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94451-202">**tooassign Britta Simon tooInkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="94451-203">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94451-203">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="94451-205">Selecteer in de lijst met de toepassingen van Hallo **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="94451-205">In hello applications list, select **Inkling**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="94451-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="94451-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="94451-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="94451-209">Click **Add** button.</span></span> <span data-ttu-id="94451-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94451-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="94451-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="94451-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="94451-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94451-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94451-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94451-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="94451-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94451-215">Testing single sign-on</span></span>

<span data-ttu-id="94451-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="94451-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="94451-217">Als u op Hallo Inkling tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Inkling toepassing.</span><span class="sxs-lookup"><span data-stu-id="94451-217">When you click hello Inkling tile in hello Access Panel, you should get automatically signed-on tooyour Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="94451-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="94451-218">Additional resources</span></span>

* [<span data-ttu-id="94451-219">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94451-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94451-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94451-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png