---
title: 'Zelfstudie: Azure Active Directory-integratie met NetDocuments | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en NetDocuments.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="79fe5-103">Zelfstudie: Azure Active Directory-integratie met NetDocuments</span><span class="sxs-lookup"><span data-stu-id="79fe5-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="79fe5-104">In deze zelfstudie leert u hoe toointegrate NetDocuments met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79fe5-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79fe5-105">NetDocuments integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="79fe5-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79fe5-106">U kunt beheren in Azure AD die tooNetDocuments toegang heeft</span><span class="sxs-lookup"><span data-stu-id="79fe5-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="79fe5-107">U kunt uw gebruikers tooautomatically get aangemelde tooNetDocuments (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="79fe5-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79fe5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="79fe5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79fe5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79fe5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79fe5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="79fe5-110">Prerequisites</span></span>

<span data-ttu-id="79fe5-111">Azure AD-integratie met NetDocuments tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="79fe5-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="79fe5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="79fe5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79fe5-113">Een NetDocuments eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="79fe5-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79fe5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="79fe5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79fe5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="79fe5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79fe5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="79fe5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79fe5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79fe5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79fe5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="79fe5-118">Scenario description</span></span>
<span data-ttu-id="79fe5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="79fe5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79fe5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="79fe5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79fe5-121">Het toevoegen van NetDocuments van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="79fe5-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="79fe5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79fe5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="79fe5-123">Het toevoegen van NetDocuments van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="79fe5-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="79fe5-124">tooconfigure hello integratie van NetDocuments in Azure AD, moet u tooadd NetDocuments uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="79fe5-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79fe5-125">**tooadd NetDocuments via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79fe5-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79fe5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="79fe5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79fe5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79fe5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="79fe5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79fe5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="79fe5-133">Typ in het zoekvak Hallo **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-133">In hello search box, type **NetDocuments**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="79fe5-135">Selecteer in het deelvenster resultaten hello, **NetDocuments**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="79fe5-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79fe5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79fe5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79fe5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met NetDocuments op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="79fe5-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79fe5-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in NetDocuments is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79fe5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="79fe5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in NetDocuments toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="79fe5-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="79fe5-141">Wijs in NetDocuments, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="79fe5-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79fe5-142">tooconfigure en eenmalige aanmelding Azure AD-test met NetDocuments, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79fe5-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79fe5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="79fe5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79fe5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79fe5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79fe5-145">**[Maken van een testgebruiker NetDocuments](#creating-a-netdocuments-test-user)**  -toohave een equivalent van Britta Simon in NetDocuments die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="79fe5-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79fe5-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="79fe5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79fe5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="79fe5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79fe5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="79fe5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79fe5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing NetDocuments configureren.</span><span class="sxs-lookup"><span data-stu-id="79fe5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="79fe5-150">**Azure AD tooconfigure eenmalige aanmelding met NetDocuments, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79fe5-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="79fe5-151">In de Azure-portal op Hallo Hallo **NetDocuments** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="79fe5-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="79fe5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="79fe5-155">Op Hallo **NetDocuments domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79fe5-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="79fe5-157">a.</span><span class="sxs-lookup"><span data-stu-id="79fe5-157">a.</span></span> <span data-ttu-id="79fe5-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="79fe5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="79fe5-159">b.</span><span class="sxs-lookup"><span data-stu-id="79fe5-159">b.</span></span> <span data-ttu-id="79fe5-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="79fe5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79fe5-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="79fe5-161">These values are not real.</span></span> <span data-ttu-id="79fe5-162">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="79fe5-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="79fe5-163">Neem contact op met [NetDocuments ondersteuningsteam](https://support.netdocuments.com/hc/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="79fe5-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="79fe5-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="79fe5-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="79fe5-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="79fe5-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79fe5-168">In een ander browservenster, meld u bij uw bedrijf NetDocuments site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="79fe5-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="79fe5-169">Ga te**Admin**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="79fe5-170">Klik op **toevoegen en verwijderen van gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="79fe5-171">![Opslagplaats](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "opslagplaats")</span><span class="sxs-lookup"><span data-stu-id="79fe5-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="79fe5-172">Klik op **geavanceerde verificatieopties configureren**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="79fe5-173">![Configureer geavanceerde verificatieopties](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "geavanceerde verificatieopties configureren")</span><span class="sxs-lookup"><span data-stu-id="79fe5-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="79fe5-174">Op Hallo **federatieve identiteit** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="79fe5-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="79fe5-175">![Federatieve Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "federatieve Identitty")</span><span class="sxs-lookup"><span data-stu-id="79fe5-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="79fe5-176">a.</span><span class="sxs-lookup"><span data-stu-id="79fe5-176">a.</span></span> <span data-ttu-id="79fe5-177">Als **federatieve identiteit servertype**, selecteer **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="79fe5-178">b.</span><span class="sxs-lookup"><span data-stu-id="79fe5-178">b.</span></span> <span data-ttu-id="79fe5-179">Klik op **bestand kiezen**, tooupload Hallo gedownload bestand met metagegevens die u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="79fe5-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="79fe5-180">c.</span><span class="sxs-lookup"><span data-stu-id="79fe5-180">c.</span></span> <span data-ttu-id="79fe5-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="79fe5-182">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="79fe5-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79fe5-183">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="79fe5-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79fe5-184">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79fe5-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79fe5-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="79fe5-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="79fe5-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="79fe5-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="79fe5-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79fe5-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79fe5-189">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="79fe5-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79fe5-191">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79fe5-193">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="79fe5-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79fe5-195">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79fe5-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79fe5-197">a.</span><span class="sxs-lookup"><span data-stu-id="79fe5-197">a.</span></span> <span data-ttu-id="79fe5-198">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79fe5-199">b.</span><span class="sxs-lookup"><span data-stu-id="79fe5-199">b.</span></span> <span data-ttu-id="79fe5-200">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79fe5-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79fe5-201">c.</span><span class="sxs-lookup"><span data-stu-id="79fe5-201">c.</span></span> <span data-ttu-id="79fe5-202">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79fe5-203">d.</span><span class="sxs-lookup"><span data-stu-id="79fe5-203">d.</span></span> <span data-ttu-id="79fe5-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="79fe5-205">Een testgebruiker NetDocuments maken</span><span class="sxs-lookup"><span data-stu-id="79fe5-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="79fe5-206">Azure AD tooenable gebruikers toolog in tooNetDocuments, ze in NetDocuments moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="79fe5-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="79fe5-207">In geval van NetDocuments Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="79fe5-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="79fe5-208">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79fe5-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="79fe5-209">Sing op tooyour **NetDocuments** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="79fe5-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="79fe5-210">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="79fe5-211">![Beheerder](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="79fe5-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="79fe5-212">Klik op **toevoegen en verwijderen van gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="79fe5-213">![Opslagplaats](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "opslagplaats")</span><span class="sxs-lookup"><span data-stu-id="79fe5-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="79fe5-214">In Hallo **e-mailadres** textbox type Hallo e-mailadres van een geldige Azure Active Directory-account dat u wilt tooprovision en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="79fe5-215">![E-mailadres](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "e-mailadres")</span><span class="sxs-lookup"><span data-stu-id="79fe5-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="79fe5-216">Hello Azure Active Directory-accounthouder krijgt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="79fe5-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="79fe5-217">U kunt andere NetDocuments gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door NetDocuments tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="79fe5-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79fe5-218">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="79fe5-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79fe5-219">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooNetDocuments toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="79fe5-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="79fe5-221">**tooassign Britta Simon tooNetDocuments, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79fe5-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="79fe5-222">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="79fe5-224">Selecteer in de lijst met de toepassingen van Hallo **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="79fe5-226">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="79fe5-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="79fe5-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="79fe5-228">Click **Add** button.</span></span> <span data-ttu-id="79fe5-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79fe5-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="79fe5-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="79fe5-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79fe5-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79fe5-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79fe5-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79fe5-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79fe5-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79fe5-234">Testing single sign-on</span></span>

<span data-ttu-id="79fe5-235">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="79fe5-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79fe5-236">Als u op Hallo NetDocuments-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour NetDocuments toepassing.</span><span class="sxs-lookup"><span data-stu-id="79fe5-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="79fe5-237">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79fe5-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79fe5-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="79fe5-238">Additional resources</span></span>

* [<span data-ttu-id="79fe5-239">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79fe5-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79fe5-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79fe5-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

