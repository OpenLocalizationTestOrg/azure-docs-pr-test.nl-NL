---
title: 'Zelfstudie: Azure Active Directory-integratie met FM:Systems | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FM:Systems.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="11faf-103">Zelfstudie: Azure Active Directory-integratie met FM:Systems</span><span class="sxs-lookup"><span data-stu-id="11faf-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="11faf-104">In deze zelfstudie leert u hoe toointegrate FM:Systems met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11faf-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11faf-105">FM:Systems integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="11faf-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="11faf-106">U kunt beheren in Azure AD die tooFM:Systems toegang heeft</span><span class="sxs-lookup"><span data-stu-id="11faf-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="11faf-107">U kunt uw gebruikers tooautomatically get aangemelde tooFM:Systems (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="11faf-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11faf-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="11faf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="11faf-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11faf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11faf-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="11faf-110">Prerequisites</span></span>

<span data-ttu-id="11faf-111">Azure AD-integratie met FM:Systems tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="11faf-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="11faf-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="11faf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11faf-113">Een FM:Systems eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="11faf-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11faf-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="11faf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11faf-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="11faf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11faf-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="11faf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11faf-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11faf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11faf-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="11faf-118">Scenario description</span></span>
<span data-ttu-id="11faf-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="11faf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11faf-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="11faf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11faf-121">Het toevoegen van FM:Systems van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="11faf-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="11faf-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="11faf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="11faf-123">Het toevoegen van FM:Systems van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="11faf-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="11faf-124">tooconfigure hello integratie van FM:Systems in Azure AD, moet u tooadd FM:Systems uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="11faf-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="11faf-125">**tooadd FM:Systems via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11faf-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="11faf-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="11faf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11faf-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="11faf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="11faf-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="11faf-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="11faf-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11faf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="11faf-133">Typ in het zoekvak Hallo **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="11faf-133">In hello search box, type **FM:Systems**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="11faf-135">Selecteer in het deelvenster resultaten hello, **FM:Systems**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="11faf-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11faf-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="11faf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11faf-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met FM:Systems op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="11faf-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11faf-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FM:Systems is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11faf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="11faf-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in FM:Systems toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="11faf-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="11faf-141">Wijs in FM:Systems, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="11faf-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="11faf-142">tooconfigure en eenmalige aanmelding Azure AD-test met FM:Systems, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11faf-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="11faf-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="11faf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="11faf-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11faf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11faf-145">**[Maken van een testgebruiker FM:Systems](#creating-an-fmsystems-test-user)**  -toohave een equivalent van Britta Simon in FM:Systems die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="11faf-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="11faf-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="11faf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11faf-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="11faf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11faf-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="11faf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11faf-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing FM:Systems configureren.</span><span class="sxs-lookup"><span data-stu-id="11faf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="11faf-150">**Azure AD tooconfigure eenmalige aanmelding met FM:Systems, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11faf-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="11faf-151">In de Azure-portal op Hallo Hallo **FM:Systems** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="11faf-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="11faf-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="11faf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="11faf-155">Op Hallo **FM:Systems domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11faf-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="11faf-157">In Hallo **antwoord-URL** textbox, typt u uw FM:Systems **antwoord-URL**, type Hallo URL met Hallo patroon volgen:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="11faf-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11faf-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="11faf-158">This value is not real.</span></span> <span data-ttu-id="11faf-159">Deze waarde met de werkelijke antwoord-URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="11faf-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="11faf-160">Neem contact op met [FM:Systems ondersteuningsteam](https://fmsystems.com/ask-us/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="11faf-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="11faf-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="11faf-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="11faf-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="11faf-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11faf-165">tooconfigure eenmalige aanmelding op **FM:Systems** zijde, moet u toosend Hallo gedownload **Metadata XML** te[FM:Systems ondersteuningsteam](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="11faf-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="11faf-166">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="11faf-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="11faf-167">U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="11faf-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="11faf-168">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="11faf-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="11faf-169">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="11faf-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="11faf-170">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11faf-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11faf-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="11faf-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="11faf-172">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="11faf-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="11faf-174">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11faf-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="11faf-175">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="11faf-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11faf-177">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="11faf-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11faf-179">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="11faf-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11faf-181">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11faf-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11faf-183">a.</span><span class="sxs-lookup"><span data-stu-id="11faf-183">a.</span></span> <span data-ttu-id="11faf-184">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11faf-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11faf-185">b.</span><span class="sxs-lookup"><span data-stu-id="11faf-185">b.</span></span> <span data-ttu-id="11faf-186">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11faf-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11faf-187">c.</span><span class="sxs-lookup"><span data-stu-id="11faf-187">c.</span></span> <span data-ttu-id="11faf-188">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="11faf-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="11faf-189">d.</span><span class="sxs-lookup"><span data-stu-id="11faf-189">d.</span></span> <span data-ttu-id="11faf-190">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="11faf-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="11faf-191">Een testgebruiker FM:Systems maken</span><span class="sxs-lookup"><span data-stu-id="11faf-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="11faf-192">In een browservenster geopend, meld u bij uw bedrijf FM:Systems site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="11faf-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="11faf-193">Ga te**Systeembeheer \> beveiliging beheren \> gebruikers \> gebruikerslijst**.</span><span class="sxs-lookup"><span data-stu-id="11faf-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="11faf-194">![Systeembeheer](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="11faf-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="11faf-195">Klik op **nieuwe gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="11faf-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="11faf-196">![Nieuwe gebruiker maken](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "nieuwe gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="11faf-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="11faf-197">In Hallo **gebruiker maken** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11faf-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="11faf-198">![Gebruiker maken](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="11faf-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="11faf-199">a.</span><span class="sxs-lookup"><span data-stu-id="11faf-199">a.</span></span> <span data-ttu-id="11faf-200">Type Hallo **gebruikersnaam**, Hallo **wachtwoord**, **wachtwoord bevestigen**, **e** en Hallo **werknemer-ID**van een geldig Azure Active Directory-account die u wilt dat tooprovision in Hallo tekstvakken gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="11faf-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="11faf-201">b.</span><span class="sxs-lookup"><span data-stu-id="11faf-201">b.</span></span> <span data-ttu-id="11faf-202">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="11faf-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="11faf-203">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="11faf-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="11faf-204">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooFM:Systems toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="11faf-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="11faf-206">**tooassign Britta Simon tooFM:Systems, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11faf-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="11faf-207">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="11faf-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="11faf-209">Selecteer in de lijst met de toepassingen van Hallo **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="11faf-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="11faf-211">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="11faf-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="11faf-213">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="11faf-213">Click **Add** button.</span></span> <span data-ttu-id="11faf-214">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11faf-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="11faf-216">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="11faf-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="11faf-217">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11faf-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11faf-218">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11faf-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11faf-219">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="11faf-219">Testing single sign-on</span></span>

<span data-ttu-id="11faf-220">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="11faf-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="11faf-221">Als u op Hallo FM:Systems tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour FM:Systems toepassing.</span><span class="sxs-lookup"><span data-stu-id="11faf-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="11faf-222">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11faf-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11faf-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="11faf-223">Additional resources</span></span>

* [<span data-ttu-id="11faf-224">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11faf-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11faf-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11faf-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

