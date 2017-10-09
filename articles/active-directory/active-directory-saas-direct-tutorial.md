---
title: 'Zelfstudie: Azure Active Directory-integratie met Direct | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Direct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="bdac6-103">Zelfstudie: Azure Active Directory-integratie met Direct</span><span class="sxs-lookup"><span data-stu-id="bdac6-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="bdac6-104">In deze zelfstudie leert u hoe toointegrate Direct met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdac6-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdac6-105">Directe integratie met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bdac6-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bdac6-106">U kunt beheren in Azure AD die tooDirect toegang heeft</span><span class="sxs-lookup"><span data-stu-id="bdac6-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="bdac6-107">U kunt uw gebruikers tooautomatically get aangemelde tooDirect (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="bdac6-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdac6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bdac6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bdac6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdac6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdac6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bdac6-110">Prerequisites</span></span>

<span data-ttu-id="bdac6-111">tooconfigure Azure AD-integratie met Direct, moet u de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="bdac6-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="bdac6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bdac6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdac6-113">Een directe eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bdac6-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdac6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bdac6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdac6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bdac6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdac6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bdac6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdac6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdac6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdac6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bdac6-118">Scenario description</span></span>
<span data-ttu-id="bdac6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bdac6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdac6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bdac6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdac6-121">Direct uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="bdac6-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="bdac6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bdac6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="bdac6-123">Direct uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="bdac6-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="bdac6-124">tooconfigure hello integratie van Direct in Azure AD, moet u tooadd Direct uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bdac6-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdac6-125">**tooadd Direct uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bdac6-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdac6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bdac6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bdac6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bdac6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bdac6-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bdac6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bdac6-133">Typ in het zoekvak Hallo **Direct**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-133">In hello search box, type **Direct**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="bdac6-135">Selecteer in het deelvenster resultaten hello, **Direct**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bdac6-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdac6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bdac6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdac6-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Direct op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bdac6-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bdac6-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Direct is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdac6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="bdac6-140">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in directe behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="bdac6-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="bdac6-141">In de directe, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="bdac6-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bdac6-142">tooconfigure en Azure AD test eenmalige aanmelding met Direct, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bdac6-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdac6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="bdac6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdac6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdac6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdac6-145">**[Maken van een directe testgebruiker](#creating-a-direct-test-user)**  -toohave een equivalent van Britta Simon in rechtstreeks die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bdac6-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdac6-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bdac6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdac6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bdac6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdac6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bdac6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdac6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing rechtstreeks configureren.</span><span class="sxs-lookup"><span data-stu-id="bdac6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="bdac6-150">**tooconfigure eenmalige aanmelding Azure AD met Direct kunnen uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bdac6-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdac6-151">In de Azure-portal op Hallo Hallo **Direct** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bdac6-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bdac6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="bdac6-155">Op Hallo **Direct domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="bdac6-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="bdac6-157">In Hallo **id** textbox type Hallo URL:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="bdac6-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="bdac6-158">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="bdac6-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="bdac6-160">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="bdac6-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="bdac6-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bdac6-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="bdac6-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bdac6-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bdac6-165">tooconfigure eenmalige aanmelding op **Direct** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Direct ondersteuningsteam](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="bdac6-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="bdac6-166">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="bdac6-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bdac6-167">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="bdac6-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bdac6-168">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdac6-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdac6-169">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bdac6-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdac6-170">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bdac6-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bdac6-172">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bdac6-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdac6-173">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bdac6-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bdac6-175">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bdac6-177">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="bdac6-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bdac6-179">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bdac6-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdac6-181">a.</span><span class="sxs-lookup"><span data-stu-id="bdac6-181">a.</span></span> <span data-ttu-id="bdac6-182">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdac6-183">b.</span><span class="sxs-lookup"><span data-stu-id="bdac6-183">b.</span></span> <span data-ttu-id="bdac6-184">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bdac6-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bdac6-185">c.</span><span class="sxs-lookup"><span data-stu-id="bdac6-185">c.</span></span> <span data-ttu-id="bdac6-186">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bdac6-187">d.</span><span class="sxs-lookup"><span data-stu-id="bdac6-187">d.</span></span> <span data-ttu-id="bdac6-188">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="bdac6-189">Een rechtstreekse testversie van de gebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bdac6-189">Creating a Direct test user</span></span>

<span data-ttu-id="bdac6-190">In deze sectie maakt u Britta Simon aangeroepen in rechtstreeks van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bdac6-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="bdac6-191">Werken met [Direct ondersteuningsteam](https://direct4b.com/ja/support.html#inquiry) Hallo gebruikers toevoegen in directe Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="bdac6-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="bdac6-192">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bdac6-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bdac6-193">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdac6-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bdac6-194">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDirect toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="bdac6-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bdac6-196">**tooassign Britta Simon tooDirect, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bdac6-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdac6-197">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bdac6-199">Selecteer in de lijst met de toepassingen van Hallo **Direct**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-199">In hello applications list, select **Direct**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="bdac6-201">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bdac6-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bdac6-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bdac6-203">Click **Add** button.</span></span> <span data-ttu-id="bdac6-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bdac6-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bdac6-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="bdac6-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bdac6-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bdac6-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdac6-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bdac6-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdac6-209">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bdac6-209">Testing single sign-on</span></span>

<span data-ttu-id="bdac6-210">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bdac6-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="bdac6-211">U kunt eventueel tootest in **IDP geïnitieerd modus**:</span><span class="sxs-lookup"><span data-stu-id="bdac6-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="bdac6-212">Wanneer u klikt op Hallo **Direct** tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour **Direct** toepassing.</span><span class="sxs-lookup"><span data-stu-id="bdac6-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="bdac6-213">U kunt eventueel tootest in **SP geïnitieerd modus**:</span><span class="sxs-lookup"><span data-stu-id="bdac6-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="bdac6-214">a.</span><span class="sxs-lookup"><span data-stu-id="bdac6-214">a.</span></span> <span data-ttu-id="bdac6-215">Klik op Hallo **directe** -tegel in Hallo Toegangspaneel en kunt u omgeleide toohello aanmelding toepassingspagina.</span><span class="sxs-lookup"><span data-stu-id="bdac6-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="bdac6-216">b.</span><span class="sxs-lookup"><span data-stu-id="bdac6-216">b.</span></span> <span data-ttu-id="bdac6-217">Voer uw `subdomain` in Hallo textbox weergegeven en druk op '次へ (volgende)' u moet ophalen en automatisch aangemelde tooyour **Direct** toepassing.</span><span class="sxs-lookup"><span data-stu-id="bdac6-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="bdac6-218">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdac6-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bdac6-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bdac6-219">Additional resources</span></span>

* [<span data-ttu-id="bdac6-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdac6-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdac6-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bdac6-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

