---
title: 'Zelfstudie: Azure Active Directory-integratie met Bime | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Bime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="2c142-103">Zelfstudie: Azure Active Directory-integratie met Bime</span><span class="sxs-lookup"><span data-stu-id="2c142-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="2c142-104">In deze zelfstudie leert u hoe toointegrate Bime met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2c142-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2c142-105">Bime integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2c142-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2c142-106">U kunt beheren in Azure AD die tooBime toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2c142-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="2c142-107">U kunt uw gebruikers tooautomatically get aangemelde tooBime (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c142-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2c142-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2c142-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2c142-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2c142-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c142-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c142-110">Prerequisites</span></span>

<span data-ttu-id="2c142-111">Azure AD-integratie met Bime tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2c142-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="2c142-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2c142-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2c142-113">Een Bime eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2c142-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2c142-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2c142-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2c142-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2c142-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2c142-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2c142-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2c142-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c142-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2c142-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2c142-118">Scenario description</span></span>
<span data-ttu-id="2c142-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2c142-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2c142-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2c142-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2c142-121">Het toevoegen van Bime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2c142-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="2c142-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c142-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="2c142-123">Het toevoegen van Bime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2c142-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="2c142-124">tooconfigure hello integratie van Bime in Azure AD, moet u tooadd Bime uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2c142-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2c142-125">**tooadd Bime via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c142-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c142-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2c142-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2c142-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c142-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2c142-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c142-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2c142-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c142-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2c142-133">Typ in het zoekvak Hallo **Bime**.</span><span class="sxs-lookup"><span data-stu-id="2c142-133">In hello search box, type **Bime**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="2c142-135">Selecteer in het deelvenster resultaten hello, **Bime**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c142-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2c142-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c142-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2c142-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Bime op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2c142-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2c142-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Bime is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c142-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="2c142-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Bime toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2c142-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="2c142-141">Wijs in Bime, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2c142-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2c142-142">tooconfigure en eenmalige aanmelding Azure AD-test met Bime, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c142-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2c142-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2c142-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2c142-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2c142-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2c142-145">**[Maken van een testgebruiker Bime](#creating-a-bime-test-user)**  -toohave een equivalent van Britta Simon in Bime die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2c142-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2c142-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2c142-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2c142-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2c142-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2c142-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2c142-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2c142-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Bime configureren.</span><span class="sxs-lookup"><span data-stu-id="2c142-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="2c142-150">**Azure AD tooconfigure eenmalige aanmelding met Bime, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c142-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c142-151">In de Azure-portal op Hallo Hallo **Bime** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2c142-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2c142-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2c142-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="2c142-155">Op Hallo **Bime domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c142-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="2c142-157">a.</span><span class="sxs-lookup"><span data-stu-id="2c142-157">a.</span></span> <span data-ttu-id="2c142-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="2c142-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="2c142-159">b.</span><span class="sxs-lookup"><span data-stu-id="2c142-159">b.</span></span> <span data-ttu-id="2c142-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="2c142-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2c142-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2c142-161">These values are not real.</span></span> <span data-ttu-id="2c142-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="2c142-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2c142-163">Neem contact op met [Bime Client ondersteuningsteam](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2c142-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="2c142-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="2c142-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="2c142-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2c142-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2c142-168">Op Hallo **Bime configuratie** sectie, klikt u op **configureren Bime** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2c142-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2c142-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2c142-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="2c142-171">In een ander browservenster, meld u bij uw bedrijf Bime site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2c142-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="2c142-172">Klik in de werkbalk Hallo op **Admin**, en vervolgens **Account**.</span><span class="sxs-lookup"><span data-stu-id="2c142-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="2c142-173">![Beheerder](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="2c142-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="2c142-174">Voer op Hallo account de configuratiepagina Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c142-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2c142-175">![Eenmalige aanmelding configureren](./media/active-directory-saas-bime-tutorial/ic775559.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="2c142-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="2c142-176">a.</span><span class="sxs-lookup"><span data-stu-id="2c142-176">a.</span></span> <span data-ttu-id="2c142-177">Selecteer **inschakelen SAML-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="2c142-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="2c142-178">b.</span><span class="sxs-lookup"><span data-stu-id="2c142-178">b.</span></span> <span data-ttu-id="2c142-179">In Hallo **externe aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2c142-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2c142-180">c.</span><span class="sxs-lookup"><span data-stu-id="2c142-180">c.</span></span>  <span data-ttu-id="2c142-181">Plakken Hallo **vingerafdruk** waarde van de Azure-portal in Hallo **vingerafdruk van certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="2c142-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="2c142-182">d.</span><span class="sxs-lookup"><span data-stu-id="2c142-182">d.</span></span> <span data-ttu-id="2c142-183">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2c142-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2c142-184">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2c142-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2c142-185">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2c142-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2c142-186">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2c142-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2c142-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2c142-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="2c142-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2c142-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2c142-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c142-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c142-191">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2c142-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2c142-193">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2c142-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2c142-195">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2c142-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2c142-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c142-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2c142-199">a.</span><span class="sxs-lookup"><span data-stu-id="2c142-199">a.</span></span> <span data-ttu-id="2c142-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2c142-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2c142-201">b.</span><span class="sxs-lookup"><span data-stu-id="2c142-201">b.</span></span> <span data-ttu-id="2c142-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2c142-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2c142-203">c.</span><span class="sxs-lookup"><span data-stu-id="2c142-203">c.</span></span> <span data-ttu-id="2c142-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2c142-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2c142-205">d.</span><span class="sxs-lookup"><span data-stu-id="2c142-205">d.</span></span> <span data-ttu-id="2c142-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2c142-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="2c142-207">Een testgebruiker Bime maken</span><span class="sxs-lookup"><span data-stu-id="2c142-207">Creating a Bime test user</span></span>

<span data-ttu-id="2c142-208">In de volgorde tooenable Azure AD gebruikers toolog in tooBime, moeten ze worden ingericht in Bime.</span><span class="sxs-lookup"><span data-stu-id="2c142-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="2c142-209">In geval van Bime Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="2c142-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="2c142-210">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c142-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c142-211">Meld u bij tooyour **Bime** tenant.</span><span class="sxs-lookup"><span data-stu-id="2c142-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="2c142-212">Klik in de werkbalk Hallo op **Admin**, en vervolgens **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2c142-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="2c142-213">![Beheerder](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="2c142-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="2c142-214">In Hallo **gebruikerslijst**, klikt u op **nieuwe gebruiker toevoegen** ('+').</span><span class="sxs-lookup"><span data-stu-id="2c142-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="2c142-215">![Gebruikers](./media/active-directory-saas-bime-tutorial/ic775562.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="2c142-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="2c142-216">Op Hallo **Gebruikersdetails** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c142-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2c142-217">![Details van gebruiker](./media/active-directory-saas-bime-tutorial/ic775563.png "Gebruikersdetails")</span><span class="sxs-lookup"><span data-stu-id="2c142-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="2c142-218">a.</span><span class="sxs-lookup"><span data-stu-id="2c142-218">a.</span></span> <span data-ttu-id="2c142-219">In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2c142-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="2c142-220">b.</span><span class="sxs-lookup"><span data-stu-id="2c142-220">b.</span></span> <span data-ttu-id="2c142-221">In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2c142-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="2c142-222">c.</span><span class="sxs-lookup"><span data-stu-id="2c142-222">c.</span></span> <span data-ttu-id="2c142-223">In Hallo **e** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2c142-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2c142-224">d.</span><span class="sxs-lookup"><span data-stu-id="2c142-224">d.</span></span> <span data-ttu-id="2c142-225">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2c142-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="2c142-226">U kunt andere Bime gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Bime tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="2c142-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2c142-227">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c142-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2c142-228">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBime toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2c142-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2c142-230">**tooassign Britta Simon tooBime, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c142-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c142-231">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c142-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2c142-233">Selecteer in de lijst met de toepassingen van Hallo **Bime**.</span><span class="sxs-lookup"><span data-stu-id="2c142-233">In hello applications list, select **Bime**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="2c142-235">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2c142-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2c142-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2c142-237">Click **Add** button.</span></span> <span data-ttu-id="2c142-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c142-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2c142-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c142-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2c142-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c142-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2c142-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c142-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2c142-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c142-243">Testing single sign-on</span></span>

<span data-ttu-id="2c142-244">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2c142-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2c142-245">Als u op Hallo Bime tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Bime toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c142-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c142-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2c142-246">Additional resources</span></span>

* [<span data-ttu-id="2c142-247">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c142-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c142-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2c142-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

