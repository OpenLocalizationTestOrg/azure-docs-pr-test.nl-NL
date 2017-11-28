---
title: 'Zelfstudie: Azure Active Directory-integratie met & eerlijk gezegd | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en & eerlijk gezegd.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="64101-103">Zelfstudie: Azure Active Directory-integratie met & eerlijk gezegd</span><span class="sxs-lookup"><span data-stu-id="64101-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="64101-104">In deze zelfstudie leert u hoe toointegrate & eerlijk gezegd met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64101-104">In this tutorial, you learn how toointegrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64101-105">Integratie van & eerlijk gezegd met Azure AD biedt u Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="64101-105">Integrating &frankly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64101-106">U kunt beheren in Azure AD die toegang te & eerlijk gezegd heeft</span><span class="sxs-lookup"><span data-stu-id="64101-106">You can control in Azure AD who has access too&frankly</span></span>
- <span data-ttu-id="64101-107">U kunt uw tooautomatically te & eerlijk gezegd ophalen aangemelde gebruikers inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="64101-107">You can enable your users tooautomatically get signed-on too&frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64101-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="64101-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="64101-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64101-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64101-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64101-110">Prerequisites</span></span>

<span data-ttu-id="64101-111">tooconfigure Azure AD-integratie met & eerlijk gezegd, u moet Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="64101-111">tooconfigure Azure AD integration with &frankly, you need hello following items:</span></span>

- <span data-ttu-id="64101-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="64101-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64101-113">A & eerlijk gezegd eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="64101-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64101-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="64101-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64101-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="64101-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64101-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="64101-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64101-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64101-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64101-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="64101-118">Scenario description</span></span>
<span data-ttu-id="64101-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="64101-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64101-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="64101-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64101-121">Toe te voegen & eerlijk gezegd van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="64101-121">Adding &frankly from hello gallery</span></span>
2. <span data-ttu-id="64101-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="64101-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-hello-gallery"></a><span data-ttu-id="64101-123">Toe te voegen & eerlijk gezegd van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="64101-123">Adding &frankly from hello gallery</span></span>
<span data-ttu-id="64101-124">tooconfigure hello integratie van & eerlijk gezegd met Azure AD, moet u tooadd & eerlijk gezegd van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="64101-124">tooconfigure hello integration of &frankly into Azure AD, you need tooadd &frankly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64101-125">**tooadd & eerlijk gezegd via Hallo gallery Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="64101-125">**tooadd &frankly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64101-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="64101-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64101-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="64101-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64101-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="64101-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="64101-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64101-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="64101-133">Typ in het zoekvak Hallo **& eerlijk gezegd**.</span><span class="sxs-lookup"><span data-stu-id="64101-133">In hello search box, type **&frankly**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="64101-135">Selecteer in het deelvenster resultaten hello, **& eerlijk gezegd**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="64101-135">In hello results panel, select **&frankly**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64101-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="64101-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64101-138">In deze sectie u configureren en testen van Azure AD eenmalige aanmelding met & eerlijk gezegd op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="64101-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="64101-139">Voor één aanmelding toowork moet Azure AD tooknow wat Hallo equivalent gebruiker in & eerlijk gezegd tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64101-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in &frankly is tooa user in Azure AD.</span></span> <span data-ttu-id="64101-140">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en verwante gebruiker Hallo in & eerlijk gezegd behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="64101-140">In other words, a link relationship between an Azure AD user and hello related user in &frankly needs toobe established.</span></span>

<span data-ttu-id="64101-141">In & eerlijk gezegd Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="64101-141">In &frankly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="64101-142">tooconfigure en test eenmalige aanmelding Azure AD met behulp van & eerlijk gezegd, u moet toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64101-142">tooconfigure and test Azure AD single sign-on with &frankly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64101-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="64101-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64101-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64101-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64101-145">**[Maken van een & eerlijk gezegd testgebruiker](#creating-a-frankly-test-user)**  -toohave een equivalent van Britta Simon in & eerlijk gezegd die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="64101-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - toohave a counterpart of Britta Simon in &frankly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="64101-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="64101-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64101-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="64101-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64101-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="64101-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64101-149">In deze sectie maakt u Azure AD eenmalige aanmelding in hello Azure-portal inschakelen en configureren eenmalige aanmelding in uw & eerlijk gezegd groep.</span><span class="sxs-lookup"><span data-stu-id="64101-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="64101-150">**Azure AD tooconfigure één aanmelding met & eerlijk gezegd Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="64101-150">**tooconfigure Azure AD single sign-on with &frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="64101-151">In de Azure-portal op Hallo Hallo **& eerlijk gezegd** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="64101-151">In hello Azure portal, on hello **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="64101-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="64101-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="64101-155">Op Hallo **& eerlijk gezegd domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="64101-155">On hello **&frankly Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="64101-157">a.</span><span class="sxs-lookup"><span data-stu-id="64101-157">a.</span></span> <span data-ttu-id="64101-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="64101-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="64101-159">b.</span><span class="sxs-lookup"><span data-stu-id="64101-159">b.</span></span> <span data-ttu-id="64101-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="64101-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="64101-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="64101-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="64101-162">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="64101-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="64101-164">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="64101-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="64101-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="64101-165">These values are not real.</span></span> <span data-ttu-id="64101-166">Bijwerken van deze waarden met Hallo werkelijke-id en eenmalige aanmelding en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="64101-166">Update these values with hello actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="64101-167">Neem contact op met [andfrankly ondersteuningsteam](mailto:help@andfrankly.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="64101-167">Contact [andfrankly support team](mailto:help@andfrankly.com) tooget these values.</span></span>

5. <span data-ttu-id="64101-168">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="64101-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="64101-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="64101-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="64101-172">tooconfigure eenmalige aanmelding op **& eerlijk gezegd** zijde, moet u toosend Hallo gedownload **Metadata XML** te[andfrankly ondersteuningsteam](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="64101-172">tooconfigure single sign-on on **&frankly** side, you need toosend hello downloaded **Metadata XML** too[andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="64101-173">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="64101-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="64101-174">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="64101-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="64101-175">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64101-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64101-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="64101-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="64101-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="64101-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="64101-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="64101-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64101-180">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="64101-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64101-182">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="64101-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64101-184">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="64101-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64101-186">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64101-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64101-188">a.</span><span class="sxs-lookup"><span data-stu-id="64101-188">a.</span></span> <span data-ttu-id="64101-189">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64101-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64101-190">b.</span><span class="sxs-lookup"><span data-stu-id="64101-190">b.</span></span> <span data-ttu-id="64101-191">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="64101-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64101-192">c.</span><span class="sxs-lookup"><span data-stu-id="64101-192">c.</span></span> <span data-ttu-id="64101-193">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="64101-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="64101-194">d.</span><span class="sxs-lookup"><span data-stu-id="64101-194">d.</span></span> <span data-ttu-id="64101-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="64101-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="64101-196">Maken van een & eerlijk gezegd testgebruiker</span><span class="sxs-lookup"><span data-stu-id="64101-196">Creating a &frankly test user</span></span>

<span data-ttu-id="64101-197">In deze sectie maakt u een gebruiker met de naam Britta Simon in & eerlijk gezegd.</span><span class="sxs-lookup"><span data-stu-id="64101-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="64101-198">Werken met [andfrankly ondersteuningsteam](mailto:help@andfrankly.com) tooadd Hallo gebruikers in Hallo & eerlijk gezegd platform.</span><span class="sxs-lookup"><span data-stu-id="64101-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) tooadd hello users in hello &frankly platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="64101-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="64101-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="64101-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang te & eerlijk gezegd.</span><span class="sxs-lookup"><span data-stu-id="64101-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too&frankly.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="64101-202">**tooassign Britta Simon te & eerlijk gezegd uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="64101-202">**tooassign Britta Simon too&frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="64101-203">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="64101-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="64101-205">Selecteer in de lijst met de toepassingen van Hallo **& eerlijk gezegd**.</span><span class="sxs-lookup"><span data-stu-id="64101-205">In hello applications list, select **&frankly**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="64101-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="64101-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="64101-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="64101-209">Click **Add** button.</span></span> <span data-ttu-id="64101-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64101-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="64101-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="64101-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64101-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64101-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64101-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64101-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64101-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="64101-215">Testing single sign-on</span></span>

<span data-ttu-id="64101-216">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="64101-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="64101-217">Wanneer u klikt u op Hallo & eerlijk gezegd-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour & eerlijk gezegd groep</span><span class="sxs-lookup"><span data-stu-id="64101-217">When you click hello &frankly tile in hello Access Panel, you should get automatically signed-on tooyour &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64101-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="64101-218">Additional resources</span></span>

* [<span data-ttu-id="64101-219">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64101-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64101-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64101-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

