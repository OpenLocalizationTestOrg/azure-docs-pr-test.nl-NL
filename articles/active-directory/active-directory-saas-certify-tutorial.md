---
title: 'Zelfstudie: Azure Active Directory-integratie met Certify | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en certificeren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 000bef7b679a6f291b1f3cb42e10cb3ed424b25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="14f4f-103">Zelfstudie: Azure Active Directory-integratie met Certify</span><span class="sxs-lookup"><span data-stu-id="14f4f-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="14f4f-104">In deze zelfstudie leert u hoe toointegrate certificeren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14f4f-104">In this tutorial, you learn how toointegrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14f4f-105">Certificeren integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="14f4f-105">Integrating Certify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="14f4f-106">U kunt beheren in Azure AD die tooCertify toegang heeft</span><span class="sxs-lookup"><span data-stu-id="14f4f-106">You can control in Azure AD who has access tooCertify</span></span>
- <span data-ttu-id="14f4f-107">U kunt uw gebruikers tooautomatically get aangemelde tooCertify (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="14f4f-107">You can enable your users tooautomatically get signed-on tooCertify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14f4f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="14f4f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="14f4f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14f4f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14f4f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="14f4f-110">Prerequisites</span></span>

<span data-ttu-id="14f4f-111">tooconfigure Azure AD-integratie met Certify u Hallo volgende items nodig:</span><span class="sxs-lookup"><span data-stu-id="14f4f-111">tooconfigure Azure AD integration with Certify, you need hello following items:</span></span>

- <span data-ttu-id="14f4f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="14f4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14f4f-113">Een certificeren eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="14f4f-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14f4f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="14f4f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14f4f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="14f4f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14f4f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="14f4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14f4f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14f4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14f4f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="14f4f-118">Scenario description</span></span>
<span data-ttu-id="14f4f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="14f4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14f4f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="14f4f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14f4f-121">Het toevoegen van certificeren van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="14f4f-121">Adding Certify from hello gallery</span></span>
2. <span data-ttu-id="14f4f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="14f4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-hello-gallery"></a><span data-ttu-id="14f4f-123">Het toevoegen van certificeren van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="14f4f-123">Adding Certify from hello gallery</span></span>
<span data-ttu-id="14f4f-124">tooconfigure hello integratie van Certify in Azure AD, moet u tooadd certificeren van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="14f4f-124">tooconfigure hello integration of Certify into Azure AD, you need tooadd Certify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="14f4f-125">**tooadd Certify via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="14f4f-125">**tooadd Certify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="14f4f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="14f4f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="14f4f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="14f4f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="14f4f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="14f4f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="14f4f-133">Typ in het zoekvak Hallo **Certify**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-133">In hello search box, type **Certify**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="14f4f-135">Selecteer in het deelvenster resultaten hello, **Certify**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="14f4f-135">In hello results panel, select **Certify**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="14f4f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="14f4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="14f4f-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Certify op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="14f4f-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="14f4f-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Certify is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14f4f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Certify is tooa user in Azure AD.</span></span> <span data-ttu-id="14f4f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Certify toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="14f4f-140">In other words, a link relationship between an Azure AD user and hello related user in Certify needs toobe established.</span></span>

<span data-ttu-id="14f4f-141">Wijs in Certify Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="14f4f-141">In Certify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="14f4f-142">tooconfigure en Azure AD test eenmalige aanmelding certificeren, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="14f4f-142">tooconfigure and test Azure AD single sign-on with Certify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="14f4f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="14f4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="14f4f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14f4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14f4f-145">**[Maken van een testgebruiker Certify](#creating-a-certify-test-user)**  -toohave een equivalent van Britta Simon in certificeren die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="14f4f-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - toohave a counterpart of Britta Simon in Certify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="14f4f-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="14f4f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14f4f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="14f4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="14f4f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="14f4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="14f4f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing certificeren.</span><span class="sxs-lookup"><span data-stu-id="14f4f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="14f4f-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Certify Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="14f4f-150">**tooconfigure Azure AD single sign-on with Certify, perform hello following steps:**</span></span>

1. <span data-ttu-id="14f4f-151">In de Azure-portal op Hallo Hallo **Certify** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-151">In hello Azure portal, on hello **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="14f4f-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="14f4f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="14f4f-155">Op Hallo **certificeren domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="14f4f-155">On hello **Certify Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="14f4f-157">In Hallo **id** textbox type Hallo URL:`https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="14f4f-157">In hello **Identifier** textbox, type hello URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="14f4f-158">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="14f4f-158">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="14f4f-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="14f4f-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="14f4f-162">Op Hallo **certificeren configuratie** sectie, klikt u op **configureren certificeren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="14f4f-162">On hello **Certify Configuration** section, click **Configure Certify** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="14f4f-163">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="14f4f-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="14f4f-165">tooconfigure eenmalige aanmelding op **Certify** zijde, moet u toosend Hallo gedownload **Certificate(Raw)** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**te[Certify ondersteuningsteam](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="14f4f-165">tooconfigure single sign-on on **Certify** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="14f4f-166">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="14f4f-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="14f4f-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="14f4f-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="14f4f-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="14f4f-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="14f4f-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14f4f-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="14f4f-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="14f4f-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="14f4f-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="14f4f-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="14f4f-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="14f4f-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="14f4f-174">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="14f4f-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14f4f-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14f4f-178">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="14f4f-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14f4f-180">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="14f4f-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14f4f-182">a.</span><span class="sxs-lookup"><span data-stu-id="14f4f-182">a.</span></span> <span data-ttu-id="14f4f-183">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14f4f-184">b.</span><span class="sxs-lookup"><span data-stu-id="14f4f-184">b.</span></span> <span data-ttu-id="14f4f-185">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="14f4f-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14f4f-186">c.</span><span class="sxs-lookup"><span data-stu-id="14f4f-186">c.</span></span> <span data-ttu-id="14f4f-187">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="14f4f-188">d.</span><span class="sxs-lookup"><span data-stu-id="14f4f-188">d.</span></span> <span data-ttu-id="14f4f-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="14f4f-190">Een testgebruiker certificeren maken</span><span class="sxs-lookup"><span data-stu-id="14f4f-190">Creating a Certify test user</span></span>

<span data-ttu-id="14f4f-191">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in certificeren van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="14f4f-191">hello objective of this section is toocreate a user called Britta Simon in Certify.</span></span> <span data-ttu-id="14f4f-192">Certificeren ondersteunt just-in-time-inrichting, is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="14f4f-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="14f4f-193">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="14f4f-193">There is no action item for you in this section.</span></span> <span data-ttu-id="14f4f-194">Een nieuwe gebruiker wordt tijdens een poging tooaccess certificeren gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="14f4f-194">A new user will be created during an attempt tooaccess Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="14f4f-195">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Certify ondersteuningsteam](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="14f4f-195">If you need toocreate an user manually, you need toocontact hello [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="14f4f-196">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="14f4f-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="14f4f-197">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooCertify toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="14f4f-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCertify.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="14f4f-199">**tooassign Britta Simon tooCertify, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="14f4f-199">**tooassign Britta Simon tooCertify, perform hello following steps:**</span></span>

1. <span data-ttu-id="14f4f-200">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="14f4f-202">Selecteer in de lijst met de toepassingen van Hallo **Certify**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-202">In hello applications list, select **Certify**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="14f4f-204">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="14f4f-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="14f4f-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="14f4f-206">Click **Add** button.</span></span> <span data-ttu-id="14f4f-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="14f4f-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="14f4f-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="14f4f-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="14f4f-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="14f4f-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14f4f-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="14f4f-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="14f4f-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="14f4f-212">Testing single sign-on</span></span>

<span data-ttu-id="14f4f-213">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="14f4f-213">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="14f4f-214">Als u op Hallo certificeren tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour certificeren toepassing.</span><span class="sxs-lookup"><span data-stu-id="14f4f-214">When you click hello Certify tile in hello Access Panel, you should get automatically signed-on tooyour Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14f4f-215">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="14f4f-215">Additional resources</span></span>

* [<span data-ttu-id="14f4f-216">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14f4f-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14f4f-217">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14f4f-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

