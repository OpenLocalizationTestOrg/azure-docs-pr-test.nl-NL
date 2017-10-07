---
title: 'Zelfstudie: Azure Active Directory-integratie met Nomadic | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Nomadic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 8c1d3e350ce03c373cf475b2786ec299a7ce5f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="04616-103">Zelfstudie: Azure Active Directory-integratie met Nomadic</span><span class="sxs-lookup"><span data-stu-id="04616-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="04616-104">In deze zelfstudie leert u hoe toointegrate Nomadic met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="04616-104">In this tutorial, you learn how toointegrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04616-105">Nomadic integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="04616-105">Integrating Nomadic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="04616-106">U kunt beheren in Azure AD die tooNomadic toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="04616-106">You can control in Azure AD who has access tooNomadic.</span></span>
- <span data-ttu-id="04616-107">U kunt uw gebruikers tooautomatically get aangemelde tooNomadic (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="04616-107">You can enable your users tooautomatically get signed-on tooNomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="04616-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="04616-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="04616-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="04616-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04616-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="04616-110">Prerequisites</span></span>

<span data-ttu-id="04616-111">Azure AD-integratie met Nomadic tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="04616-111">tooconfigure Azure AD integration with Nomadic, you need hello following items:</span></span>

- <span data-ttu-id="04616-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="04616-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04616-113">Een Nomadic eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="04616-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04616-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="04616-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04616-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="04616-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04616-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="04616-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04616-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04616-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04616-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="04616-118">Scenario description</span></span>
<span data-ttu-id="04616-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="04616-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04616-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="04616-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04616-121">Nomadic van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="04616-121">Add Nomadic from hello gallery</span></span>
2. <span data-ttu-id="04616-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="04616-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-hello-gallery"></a><span data-ttu-id="04616-123">Nomadic van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="04616-123">Add Nomadic from hello gallery</span></span>
<span data-ttu-id="04616-124">tooconfigure hello integratie van Nomadic in Azure AD, moet u tooadd Nomadic uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="04616-124">tooconfigure hello integration of Nomadic into Azure AD, you need tooadd Nomadic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="04616-125">**tooadd Nomadic via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="04616-125">**tooadd Nomadic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="04616-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="04616-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="04616-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="04616-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="04616-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="04616-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="04616-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04616-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="04616-133">Typ in het zoekvak Hallo **Nomadic**, selecteer **Nomadic** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="04616-133">In hello search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button tooadd hello application.</span></span>

    ![In de lijst met resultaten Hallo nomadic](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="04616-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="04616-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="04616-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Nomadic op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="04616-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="04616-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Nomadic is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04616-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nomadic is tooa user in Azure AD.</span></span> <span data-ttu-id="04616-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Nomadic toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="04616-138">In other words, a link relationship between an Azure AD user and hello related user in Nomadic needs toobe established.</span></span>

<span data-ttu-id="04616-139">Wijs in Nomadic, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="04616-139">In Nomadic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="04616-140">tooconfigure en eenmalige aanmelding Azure AD-test met Nomadic, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="04616-140">tooconfigure and test Azure AD single sign-on with Nomadic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="04616-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="04616-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="04616-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04616-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04616-143">**[Maak een Nomadic testgebruiker](#create-a-nomadic-test-user)**  -toohave een equivalent van Britta Simon in Nomadic die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="04616-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - toohave a counterpart of Britta Simon in Nomadic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="04616-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="04616-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04616-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="04616-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="04616-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="04616-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="04616-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Nomadic configureren.</span><span class="sxs-lookup"><span data-stu-id="04616-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="04616-148">**Azure AD tooconfigure eenmalige aanmelding met Nomadic, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="04616-148">**tooconfigure Azure AD single sign-on with Nomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="04616-149">In de Azure-portal op Hallo Hallo **Nomadic** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="04616-149">In hello Azure portal, on hello **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="04616-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="04616-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="04616-153">Op Hallo **Nomadic domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="04616-153">On hello **Nomadic Domain and URLs** section, perform hello following steps:</span></span>

    ![Nomadic domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="04616-155">a.</span><span class="sxs-lookup"><span data-stu-id="04616-155">a.</span></span> <span data-ttu-id="04616-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="04616-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="04616-157">b.</span><span class="sxs-lookup"><span data-stu-id="04616-157">b.</span></span> <span data-ttu-id="04616-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen: `https://<company name>.nomadic.fm/auth/saml2/sp`,`https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="04616-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="04616-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="04616-159">These values are not real.</span></span> <span data-ttu-id="04616-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="04616-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="04616-161">Neem contact op met [Nomadic Client ondersteuningsteam](mailto:help@nomadic.fm) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="04616-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) tooget these values.</span></span> 
 


4. <span data-ttu-id="04616-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="04616-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="04616-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="04616-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="04616-166">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [Nomadic ondersteuningsteam](mailto:help@nomadic.fm) en voorzien Hallo gedownload **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="04616-166">tooget SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with hello downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="04616-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="04616-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="04616-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="04616-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="04616-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04616-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="04616-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="04616-170">Create an Azure AD test user</span></span>

<span data-ttu-id="04616-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="04616-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="04616-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="04616-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="04616-174">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="04616-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="04616-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="04616-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="04616-178">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04616-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="04616-180">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="04616-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="04616-182">a.</span><span class="sxs-lookup"><span data-stu-id="04616-182">a.</span></span> <span data-ttu-id="04616-183">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="04616-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04616-184">b.</span><span class="sxs-lookup"><span data-stu-id="04616-184">b.</span></span> <span data-ttu-id="04616-185">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="04616-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="04616-186">c.</span><span class="sxs-lookup"><span data-stu-id="04616-186">c.</span></span> <span data-ttu-id="04616-187">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="04616-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="04616-188">d.</span><span class="sxs-lookup"><span data-stu-id="04616-188">d.</span></span> <span data-ttu-id="04616-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="04616-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="04616-190">Een Nomadic testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="04616-190">Create a Nomadic test user</span></span>

<span data-ttu-id="04616-191">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Nomadic maken.</span><span class="sxs-lookup"><span data-stu-id="04616-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="04616-192">Neem contact op met [Nomadic ondersteuningsteam](mailto:help@nomadic.fm) tooadd Hallo gebruikers in Nomadic Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="04616-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) tooadd hello users in hello Nomadic platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="04616-193">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="04616-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="04616-194">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooNomadic toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="04616-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNomadic.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="04616-196">**tooassign Britta Simon tooNomadic, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="04616-196">**tooassign Britta Simon tooNomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="04616-197">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="04616-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="04616-199">Selecteer in de lijst met de toepassingen van Hallo **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="04616-199">In hello applications list, select **Nomadic**.</span></span>

    ![Hallo Nomadic koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="04616-201">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="04616-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="04616-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="04616-203">Click **Add** button.</span></span> <span data-ttu-id="04616-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04616-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="04616-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="04616-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="04616-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04616-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04616-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04616-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="04616-209">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="04616-209">Test single sign-on</span></span>

<span data-ttu-id="04616-210">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="04616-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="04616-211">Wanneer u klikt op Hallo Nomadic tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Nomadic toepassing.</span><span class="sxs-lookup"><span data-stu-id="04616-211">When you click hello Nomadic tile in hello Access Panel, you should get automatically signed-on tooyour Nomadic application.</span></span>
<span data-ttu-id="04616-212">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="04616-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="04616-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="04616-213">Additional resources</span></span>

* [<span data-ttu-id="04616-214">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04616-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04616-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="04616-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

