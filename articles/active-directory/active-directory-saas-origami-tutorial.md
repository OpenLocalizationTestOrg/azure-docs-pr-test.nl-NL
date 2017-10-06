---
title: 'Zelfstudie: Azure Active Directory-integratie met Origami | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Origami.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="ac918-103">Zelfstudie: Azure Active Directory-integratie met Origami</span><span class="sxs-lookup"><span data-stu-id="ac918-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="ac918-104">In deze zelfstudie leert u hoe toointegrate Origami met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac918-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac918-105">Origami integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ac918-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ac918-106">U kunt beheren in Azure AD die tooOrigami toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ac918-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="ac918-107">U kunt uw gebruikers tooautomatically get aangemelde tooOrigami (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ac918-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac918-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ac918-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ac918-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac918-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac918-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac918-110">Prerequisites</span></span>

<span data-ttu-id="ac918-111">Azure AD-integratie met Origami tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ac918-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="ac918-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ac918-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac918-113">Een Origami eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ac918-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac918-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac918-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac918-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ac918-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac918-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ac918-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac918-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac918-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac918-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ac918-118">Scenario description</span></span>
<span data-ttu-id="ac918-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac918-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac918-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ac918-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac918-121">Het toevoegen van Origami van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ac918-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="ac918-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac918-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="ac918-123">Het toevoegen van Origami van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ac918-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="ac918-124">tooconfigure hello integratie van Origami in Azure AD, moet u tooadd Origami uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ac918-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ac918-125">**tooadd Origami via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac918-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac918-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ac918-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ac918-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac918-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ac918-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac918-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ac918-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac918-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ac918-133">Typ in het zoekvak Hallo **Origami**.</span><span class="sxs-lookup"><span data-stu-id="ac918-133">In hello search box, type **Origami**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="ac918-135">Selecteer in het deelvenster resultaten hello, **Origami**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac918-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac918-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac918-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ac918-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Origami op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ac918-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ac918-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Origami is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac918-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="ac918-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Origami toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ac918-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="ac918-141">Wijs in Origami, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ac918-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ac918-142">tooconfigure en eenmalige aanmelding Azure AD-test met Origami, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac918-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ac918-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ac918-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ac918-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac918-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac918-145">**[Maken van een testgebruiker Origami](#creating-an-origami-test-user)**  -toohave een equivalent van Britta Simon in Origami die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ac918-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac918-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ac918-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac918-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ac918-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac918-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ac918-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac918-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Origami configureren.</span><span class="sxs-lookup"><span data-stu-id="ac918-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="ac918-150">**Azure AD tooconfigure eenmalige aanmelding met Origami, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac918-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac918-151">In de Azure-portal op Hallo Hallo **Origami** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ac918-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ac918-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ac918-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="ac918-155">Op Hallo **Origami domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac918-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="ac918-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="ac918-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ac918-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="ac918-158">hello value is not real.</span></span> <span data-ttu-id="ac918-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="ac918-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ac918-160">Neem contact op met [Origami Client ondersteuningsteam](https://wordpress.org/support/theme/origami) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="ac918-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="ac918-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ac918-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="ac918-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ac918-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ac918-165">Op Hallo **Origami configuratie** sectie, klikt u op **Origami configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ac918-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ac918-166">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ac918-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="ac918-168">Meld u bij toohello Origami account met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="ac918-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="ac918-169">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="ac918-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="ac918-171">Uitvoeren op Hallo Single Sign op Setup dialoogvenster pagina Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac918-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="ac918-173">a.</span><span class="sxs-lookup"><span data-stu-id="ac918-173">a.</span></span> <span data-ttu-id="ac918-174">Selecteer **eenmalige aanmelding inschakelen op**.</span><span class="sxs-lookup"><span data-stu-id="ac918-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="ac918-175">b.</span><span class="sxs-lookup"><span data-stu-id="ac918-175">b.</span></span> <span data-ttu-id="ac918-176">In Hallo **van de identiteitsprovider aanmelden pagina-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ac918-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ac918-177">c.</span><span class="sxs-lookup"><span data-stu-id="ac918-177">c.</span></span> <span data-ttu-id="ac918-178">In Hallo **Sign-out pagina-URL van de identiteitsprovider** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ac918-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ac918-179">d.</span><span class="sxs-lookup"><span data-stu-id="ac918-179">d.</span></span> <span data-ttu-id="ac918-180">Klik op **Bladeren** tooupload Hallo certificaat u hebt gedownload van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ac918-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="ac918-181">e.</span><span class="sxs-lookup"><span data-stu-id="ac918-181">e.</span></span> <span data-ttu-id="ac918-182">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ac918-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ac918-183">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ac918-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ac918-184">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ac918-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ac918-185">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac918-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac918-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ac918-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac918-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ac918-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ac918-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac918-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac918-190">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ac918-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac918-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ac918-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac918-194">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ac918-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac918-196">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac918-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac918-198">a.</span><span class="sxs-lookup"><span data-stu-id="ac918-198">a.</span></span> <span data-ttu-id="ac918-199">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac918-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac918-200">b.</span><span class="sxs-lookup"><span data-stu-id="ac918-200">b.</span></span> <span data-ttu-id="ac918-201">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ac918-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac918-202">c.</span><span class="sxs-lookup"><span data-stu-id="ac918-202">c.</span></span> <span data-ttu-id="ac918-203">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ac918-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ac918-204">d.</span><span class="sxs-lookup"><span data-stu-id="ac918-204">d.</span></span> <span data-ttu-id="ac918-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ac918-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="ac918-206">Een testgebruiker Origami maken</span><span class="sxs-lookup"><span data-stu-id="ac918-206">Creating an Origami test user</span></span>

<span data-ttu-id="ac918-207">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Origami maken.</span><span class="sxs-lookup"><span data-stu-id="ac918-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="ac918-208">Meld u bij toohello Origami account met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="ac918-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="ac918-209">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="ac918-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="ac918-211">Op Hallo **gebruikers en beveiliging** dialoogvenster, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ac918-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="ac918-213">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ac918-213">Click **Add New User**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="ac918-215">Voer in het dialoogvenster van de nieuwe gebruiker toevoegen hello, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac918-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="ac918-217">a.</span><span class="sxs-lookup"><span data-stu-id="ac918-217">a.</span></span> <span data-ttu-id="ac918-218">In Hallo **gebruikersnaam** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ac918-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="ac918-219">b.</span><span class="sxs-lookup"><span data-stu-id="ac918-219">b.</span></span> <span data-ttu-id="ac918-220">In Hallo **wachtwoord** textbox, typ een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ac918-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="ac918-221">c.</span><span class="sxs-lookup"><span data-stu-id="ac918-221">c.</span></span> <span data-ttu-id="ac918-222">In Hallo **wachtwoord bevestigen** textbox type Hallo wachtwoord opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ac918-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="ac918-223">d.</span><span class="sxs-lookup"><span data-stu-id="ac918-223">d.</span></span> <span data-ttu-id="ac918-224">In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ac918-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="ac918-225">e.</span><span class="sxs-lookup"><span data-stu-id="ac918-225">e.</span></span> <span data-ttu-id="ac918-226">In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ac918-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="ac918-227">f.</span><span class="sxs-lookup"><span data-stu-id="ac918-227">f.</span></span> <span data-ttu-id="ac918-228">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ac918-228">Click **Save**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="ac918-230">Wijs **gebruikersrollen** en **clienttoegang** toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ac918-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ac918-232">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac918-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ac918-233">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOrigami toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ac918-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ac918-235">**tooassign Britta Simon tooOrigami, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac918-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac918-236">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac918-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ac918-238">Selecteer in de lijst met de toepassingen van Hallo **Origami**.</span><span class="sxs-lookup"><span data-stu-id="ac918-238">In hello applications list, select **Origami**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="ac918-240">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ac918-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ac918-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ac918-242">Click **Add** button.</span></span> <span data-ttu-id="ac918-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac918-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ac918-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac918-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ac918-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac918-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac918-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac918-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac918-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac918-248">Testing single sign-on</span></span>

<span data-ttu-id="ac918-249">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ac918-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ac918-250">Als u op Hallo Origami tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Origami toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac918-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac918-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ac918-251">Additional resources</span></span>

* [<span data-ttu-id="ac918-252">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac918-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac918-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac918-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

