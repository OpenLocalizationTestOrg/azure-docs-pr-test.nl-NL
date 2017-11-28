---
title: 'Zelfstudie: Azure Active Directory-integratie met Wikispaces | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Wikispaces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="c5890-103">Zelfstudie: Azure Active Directory-integratie met Wikispaces</span><span class="sxs-lookup"><span data-stu-id="c5890-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="c5890-104">In deze zelfstudie leert u hoe toointegrate Wikispaces met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5890-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5890-105">Wikispaces integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c5890-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5890-106">U kunt beheren in Azure AD die tooWikispaces toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c5890-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="c5890-107">U kunt uw gebruikers tooautomatically get aangemelde tooWikispaces (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c5890-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5890-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c5890-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5890-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5890-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5890-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c5890-110">Prerequisites</span></span>

<span data-ttu-id="c5890-111">Azure AD-integratie met Wikispaces tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c5890-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="c5890-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c5890-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5890-113">Een Wikispaces eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c5890-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5890-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c5890-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5890-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c5890-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5890-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c5890-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5890-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5890-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5890-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c5890-118">Scenario description</span></span>
<span data-ttu-id="c5890-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c5890-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5890-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c5890-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5890-121">Het toevoegen van Wikispaces van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c5890-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="c5890-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c5890-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="c5890-123">Het toevoegen van Wikispaces van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c5890-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="c5890-124">tooconfigure hello integratie van Wikispaces in Azure AD, moet u tooadd Wikispaces uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c5890-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5890-125">**tooadd Wikispaces via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c5890-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5890-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c5890-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5890-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c5890-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5890-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c5890-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c5890-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c5890-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c5890-133">Typ in het zoekvak Hallo **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="c5890-133">In hello search box, type **Wikispaces**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="c5890-135">Selecteer in het deelvenster resultaten hello, **Wikispaces**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c5890-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5890-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c5890-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5890-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Wikispaces op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c5890-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5890-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Wikispaces is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5890-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="c5890-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Wikispaces toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c5890-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="c5890-141">Wijs in Wikispaces, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c5890-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5890-142">tooconfigure en eenmalige aanmelding Azure AD-test met Wikispaces, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c5890-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5890-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c5890-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5890-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5890-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5890-145">**[Maken van een testgebruiker Wikispaces](#creating-a-wikispaces-test-user)**  -toohave een equivalent van Britta Simon in Wikispaces die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c5890-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5890-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c5890-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5890-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c5890-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5890-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c5890-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5890-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Wikispaces configureren.</span><span class="sxs-lookup"><span data-stu-id="c5890-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="c5890-150">**Azure AD tooconfigure eenmalige aanmelding met Wikispaces, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c5890-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5890-151">In de Azure-portal op Hallo Hallo **Wikispaces** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c5890-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c5890-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c5890-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="c5890-155">Op Hallo **Wikispaces domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c5890-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="c5890-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5890-157">a.</span></span> <span data-ttu-id="c5890-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="c5890-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="c5890-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5890-159">b.</span></span> <span data-ttu-id="c5890-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c5890-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5890-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c5890-161">These values are not real.</span></span> <span data-ttu-id="c5890-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="c5890-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5890-163">Neem contact op met [Wikispaces Client ondersteuningsteam](https://www.wikispaces.com/site/help) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c5890-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="c5890-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c5890-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="c5890-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c5890-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5890-168">tooconfigure eenmalige aanmelding op **Wikispaces** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Wikispaces ondersteuningsteam](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="c5890-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="c5890-169">U ontvangt een melding zodra het Hallo-configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c5890-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="c5890-170">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c5890-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5890-171">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c5890-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5890-172">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5890-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5890-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c5890-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5890-174">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c5890-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c5890-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c5890-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5890-177">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c5890-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5890-179">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c5890-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5890-181">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c5890-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5890-183">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c5890-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5890-185">a.</span><span class="sxs-lookup"><span data-stu-id="c5890-185">a.</span></span> <span data-ttu-id="c5890-186">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5890-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5890-187">b.</span><span class="sxs-lookup"><span data-stu-id="c5890-187">b.</span></span> <span data-ttu-id="c5890-188">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5890-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5890-189">c.</span><span class="sxs-lookup"><span data-stu-id="c5890-189">c.</span></span> <span data-ttu-id="c5890-190">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c5890-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5890-191">d.</span><span class="sxs-lookup"><span data-stu-id="c5890-191">d.</span></span> <span data-ttu-id="c5890-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c5890-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="c5890-193">Een testgebruiker Wikispaces maken</span><span class="sxs-lookup"><span data-stu-id="c5890-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="c5890-194">In de volgorde tooenable Azure AD gebruikers toolog in tooWikispaces, moeten ze worden ingericht in Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="c5890-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="c5890-195">In geval van Wikispaces Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c5890-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="c5890-196">tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c5890-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="c5890-197">Meld u bij tooyour **Wikispaces** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c5890-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="c5890-198">Ga te**leden**.</span><span class="sxs-lookup"><span data-stu-id="c5890-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="c5890-199">![Leden](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "leden")</span><span class="sxs-lookup"><span data-stu-id="c5890-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="c5890-200">Klik op Hallo **personen uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="c5890-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="c5890-201">![Personen uitnodigen](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="c5890-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="c5890-202">In Hallo **personen uitnodigen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c5890-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c5890-203">![Personen uitnodigen](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="c5890-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="c5890-204">a.</span><span class="sxs-lookup"><span data-stu-id="c5890-204">a.</span></span> <span data-ttu-id="c5890-205">Type Hallo **gebruikersnamen of e-mailadres** van tekstvakken met betrekking tot een geldige AAD-account u wilt dat tooprovision in Hallo.</span><span class="sxs-lookup"><span data-stu-id="c5890-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="c5890-206">b.</span><span class="sxs-lookup"><span data-stu-id="c5890-206">b.</span></span> <span data-ttu-id="c5890-207">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="c5890-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="c5890-208">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="c5890-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="c5890-209">U kunt andere Wikispaces gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Wikispaces tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c5890-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5890-210">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5890-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5890-211">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWikispaces toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c5890-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c5890-213">**tooassign Britta Simon tooWikispaces, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c5890-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5890-214">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c5890-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c5890-216">Selecteer in de lijst met de toepassingen van Hallo **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="c5890-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="c5890-218">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c5890-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c5890-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c5890-220">Click **Add** button.</span></span> <span data-ttu-id="c5890-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c5890-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c5890-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c5890-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5890-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c5890-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5890-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c5890-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5890-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c5890-226">Testing single sign-on</span></span>

<span data-ttu-id="c5890-227">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c5890-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5890-228">Als u op Hallo Wikispaces-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Wikispaces toepassing.</span><span class="sxs-lookup"><span data-stu-id="c5890-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="c5890-229">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5890-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5890-230">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c5890-230">Additional resources</span></span>

* [<span data-ttu-id="c5890-231">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5890-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5890-232">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5890-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

