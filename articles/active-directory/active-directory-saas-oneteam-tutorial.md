---
title: 'Zelfstudie: Azure Active Directory-integratie met Oneteam | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Oneteam.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 7964aaaf9b9570d460f28d86de34b5e87693ba93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="3c063-103">Zelfstudie: Azure Active Directory-integratie met Oneteam</span><span class="sxs-lookup"><span data-stu-id="3c063-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="3c063-104">In deze zelfstudie leert u hoe toointegrate Oneteam met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3c063-104">In this tutorial, you learn how toointegrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c063-105">Oneteam integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3c063-105">Integrating Oneteam with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3c063-106">U kunt beheren in Azure AD die tooOneteam toegang heeft</span><span class="sxs-lookup"><span data-stu-id="3c063-106">You can control in Azure AD who has access tooOneteam</span></span>
- <span data-ttu-id="3c063-107">U kunt uw gebruikers tooautomatically get aangemelde tooOneteam (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3c063-107">You can enable your users tooautomatically get signed-on tooOneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c063-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3c063-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3c063-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c063-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c063-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c063-110">Prerequisites</span></span>

<span data-ttu-id="3c063-111">Azure AD-integratie met Oneteam tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3c063-111">tooconfigure Azure AD integration with Oneteam, you need hello following items:</span></span>

- <span data-ttu-id="3c063-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3c063-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c063-113">Een Oneteam eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3c063-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c063-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3c063-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c063-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3c063-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c063-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3c063-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c063-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c063-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c063-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3c063-118">Scenario description</span></span>
<span data-ttu-id="3c063-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3c063-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c063-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3c063-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c063-121">Het toevoegen van Oneteam van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3c063-121">Adding Oneteam from hello gallery</span></span>
2. <span data-ttu-id="3c063-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3c063-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-hello-gallery"></a><span data-ttu-id="3c063-123">Het toevoegen van Oneteam van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3c063-123">Adding Oneteam from hello gallery</span></span>
<span data-ttu-id="3c063-124">tooconfigure hello integratie van Oneteam in Azure AD, moet u tooadd Oneteam uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3c063-124">tooconfigure hello integration of Oneteam into Azure AD, you need tooadd Oneteam from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3c063-125">**tooadd Oneteam via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3c063-125">**tooadd Oneteam from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c063-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3c063-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c063-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3c063-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3c063-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3c063-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3c063-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c063-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3c063-133">Typ in het zoekvak Hallo **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="3c063-133">In hello search box, type **Oneteam**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="3c063-135">Selecteer in het deelvenster resultaten hello, **Oneteam**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c063-135">In hello results panel, select **Oneteam**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c063-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3c063-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3c063-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Oneteam op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3c063-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3c063-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Oneteam is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c063-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Oneteam is tooa user in Azure AD.</span></span> <span data-ttu-id="3c063-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Oneteam toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3c063-140">In other words, a link relationship between an Azure AD user and hello related user in Oneteam needs toobe established.</span></span>

<span data-ttu-id="3c063-141">Wijs in Oneteam, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="3c063-141">In Oneteam, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3c063-142">tooconfigure en eenmalige aanmelding Azure AD-test met Oneteam, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c063-142">tooconfigure and test Azure AD single sign-on with Oneteam, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3c063-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3c063-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3c063-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3c063-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c063-145">**[Maken van een testgebruiker Oneteam](#creating-a-oneteam-test-user)**  -toohave een equivalent van Britta Simon in Oneteam die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3c063-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - toohave a counterpart of Britta Simon in Oneteam that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c063-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3c063-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c063-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3c063-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c063-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3c063-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c063-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Oneteam configureren.</span><span class="sxs-lookup"><span data-stu-id="3c063-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="3c063-150">**Azure AD tooconfigure eenmalige aanmelding met Oneteam, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3c063-150">**tooconfigure Azure AD single sign-on with Oneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c063-151">In de Azure-portal op Hallo Hallo **Oneteam** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3c063-151">In hello Azure portal, on hello **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3c063-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3c063-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="3c063-155">Op Hallo **Oneteam domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="3c063-155">On hello **Oneteam Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="3c063-157">a.</span><span class="sxs-lookup"><span data-stu-id="3c063-157">a.</span></span> <span data-ttu-id="3c063-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="3c063-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="3c063-159">b.</span><span class="sxs-lookup"><span data-stu-id="3c063-159">b.</span></span> <span data-ttu-id="3c063-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="3c063-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="3c063-161">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="3c063-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="3c063-163">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="3c063-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3c063-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="3c063-164">These values are not real.</span></span> <span data-ttu-id="3c063-165">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="3c063-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3c063-166">Neem contact op met [Oneteam Client ondersteuningsteam](https://support.one-team.com/hc/requests/new) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3c063-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) tooget these values.</span></span> 



5. <span data-ttu-id="3c063-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3c063-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="3c063-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3c063-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3c063-171">tooget SSO is geconfigureerd voor uw toepassing, kunt u de ondersteuningsticket Hallo met verhogen [Oneteam ondersteuningsteam](https://support.one-team.com/hc/requests/new) en bieden ze Hallo gedownload **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="3c063-171">tooget SSO configured for your application, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them hello downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="3c063-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="3c063-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3c063-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="3c063-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3c063-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c063-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c063-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3c063-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c063-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3c063-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3c063-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3c063-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c063-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3c063-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c063-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3c063-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c063-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3c063-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c063-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c063-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c063-187">a.</span><span class="sxs-lookup"><span data-stu-id="3c063-187">a.</span></span> <span data-ttu-id="3c063-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3c063-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c063-189">b.</span><span class="sxs-lookup"><span data-stu-id="3c063-189">b.</span></span> <span data-ttu-id="3c063-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3c063-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c063-191">c.</span><span class="sxs-lookup"><span data-stu-id="3c063-191">c.</span></span> <span data-ttu-id="3c063-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3c063-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3c063-193">d.</span><span class="sxs-lookup"><span data-stu-id="3c063-193">d.</span></span> <span data-ttu-id="3c063-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3c063-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="3c063-195">Een testgebruiker Oneteam maken</span><span class="sxs-lookup"><span data-stu-id="3c063-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="3c063-196">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Oneteam van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3c063-196">hello objective of this section is toocreate a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="3c063-197">Oneteam ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3c063-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="3c063-198">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3c063-198">There is no action item for you in this section.</span></span> <span data-ttu-id="3c063-199">Een nieuwe gebruiker wordt gemaakt tijdens een poging tooaccess Oneteam, als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c063-199">A new user will be created during an attempt tooaccess Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="3c063-200">Als u handmatig een gebruiker toocreate nodig, kunt u de ondersteuningsticket Hallo met verhogen [Oneteam ondersteuningsteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="3c063-200">If you need toocreate an user manually, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3c063-201">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c063-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3c063-202">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOneteam toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="3c063-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOneteam.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3c063-204">**tooassign Britta Simon tooOneteam, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3c063-204">**tooassign Britta Simon tooOneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c063-205">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3c063-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3c063-207">Selecteer in de lijst met de toepassingen van Hallo **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="3c063-207">In hello applications list, select **Oneteam**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="3c063-209">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3c063-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3c063-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3c063-211">Click **Add** button.</span></span> <span data-ttu-id="3c063-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c063-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3c063-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c063-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3c063-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c063-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c063-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c063-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c063-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3c063-217">Testing single sign-on</span></span>

<span data-ttu-id="3c063-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3c063-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3c063-219">Als u op Hallo Oneteam tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Oneteam toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c063-219">When you click hello Oneteam tile in hello Access Panel, you should get automatically signed-on tooyour Oneteam application.</span></span>
<span data-ttu-id="3c063-220">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c063-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3c063-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3c063-221">Additional resources</span></span>

* [<span data-ttu-id="3c063-222">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c063-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c063-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3c063-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

