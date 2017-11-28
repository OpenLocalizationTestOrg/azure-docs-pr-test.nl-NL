---
title: 'Zelfstudie: Azure Active Directory-integratie met Workrite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Workrite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a663374ae3c8b102b53d8cf05a9cb083b80dbb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="48081-103">Zelfstudie: Azure Active Directory-integratie met Workrite</span><span class="sxs-lookup"><span data-stu-id="48081-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="48081-104">In deze zelfstudie leert u hoe toointegrate Workrite met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48081-104">In this tutorial, you learn how toointegrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48081-105">Workrite integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="48081-105">Integrating Workrite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="48081-106">U kunt beheren in Azure AD die tooWorkrite toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="48081-106">You can control in Azure AD who has access tooWorkrite.</span></span>
- <span data-ttu-id="48081-107">U kunt uw gebruikers tooautomatically get aangemelde tooWorkrite (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="48081-107">You can enable your users tooautomatically get signed-on tooWorkrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="48081-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="48081-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="48081-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48081-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48081-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="48081-110">Prerequisites</span></span>

<span data-ttu-id="48081-111">Azure AD-integratie met Workrite tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="48081-111">tooconfigure Azure AD integration with Workrite, you need hello following items:</span></span>

- <span data-ttu-id="48081-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="48081-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48081-113">Een Workrite eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="48081-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48081-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="48081-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48081-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="48081-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48081-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="48081-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48081-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48081-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48081-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="48081-118">Scenario description</span></span>
<span data-ttu-id="48081-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="48081-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48081-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="48081-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48081-121">Het toevoegen van Workrite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="48081-121">Adding Workrite from hello gallery</span></span>
2. <span data-ttu-id="48081-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="48081-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-hello-gallery"></a><span data-ttu-id="48081-123">Het toevoegen van Workrite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="48081-123">Adding Workrite from hello gallery</span></span>
<span data-ttu-id="48081-124">tooconfigure hello integratie van Workrite in Azure AD, moet u tooadd Workrite uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="48081-124">tooconfigure hello integration of Workrite into Azure AD, you need tooadd Workrite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="48081-125">**tooadd Workrite via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="48081-125">**tooadd Workrite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="48081-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="48081-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="48081-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="48081-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="48081-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="48081-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="48081-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48081-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="48081-133">Typ in het zoekvak Hallo **Workrite**, selecteer **Workrite** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="48081-133">In hello search box, type **Workrite**, select **Workrite** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workrite in de lijst met resultaten Hallo](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="48081-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="48081-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="48081-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Workrite op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="48081-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48081-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Workrite is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48081-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workrite is tooa user in Azure AD.</span></span> <span data-ttu-id="48081-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Workrite toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="48081-138">In other words, a link relationship between an Azure AD user and hello related user in Workrite needs toobe established.</span></span>

<span data-ttu-id="48081-139">Wijs in Workrite, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="48081-139">In Workrite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="48081-140">tooconfigure en eenmalige aanmelding Azure AD-test met Workrite, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="48081-140">tooconfigure and test Azure AD single sign-on with Workrite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="48081-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="48081-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="48081-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48081-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48081-143">**[Maak een testgebruiker Workrite](#create-a-workrite-test-user)**  -toohave een equivalent van Britta Simon in Workrite die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="48081-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - toohave a counterpart of Britta Simon in Workrite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="48081-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="48081-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48081-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="48081-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="48081-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="48081-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="48081-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Workrite configureren.</span><span class="sxs-lookup"><span data-stu-id="48081-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="48081-148">**Azure AD tooconfigure eenmalige aanmelding met Workrite, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="48081-148">**tooconfigure Azure AD single sign-on with Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="48081-149">In de Azure-portal op Hallo Hallo **Workrite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="48081-149">In hello Azure portal, on hello **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="48081-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="48081-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="48081-153">Op Hallo **Workrite domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="48081-153">On hello **Workrite Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Workrite domein eenmalige aanmelding informatie](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="48081-155">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="48081-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48081-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="48081-156">This value is not real.</span></span> <span data-ttu-id="48081-157">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="48081-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="48081-158">Neem contact op met [Workrite Client ondersteuningsteam](mailto:support@workrite.co.uk) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="48081-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) tooget this value.</span></span>

4. <span data-ttu-id="48081-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="48081-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="48081-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="48081-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48081-163">Op Hallo **Workrite configuratie** sectie, klikt u op **configureren Workrite** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="48081-163">On hello **Workrite Configuration** section, click **Configure Workrite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="48081-164">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="48081-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Workrite configuratie](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="48081-166">tooconfigure eenmalige aanmelding op **Workrite** zijde, moet u toosend Hallo gedownload **Certificate(Base64), Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Workrite ondersteuningsteam](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="48081-166">tooconfigure single sign-on on **Workrite** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="48081-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="48081-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="48081-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="48081-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="48081-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48081-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="48081-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="48081-170">Create an Azure AD test user</span></span>

<span data-ttu-id="48081-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="48081-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="48081-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="48081-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="48081-174">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="48081-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="48081-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="48081-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="48081-178">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48081-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="48081-180">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="48081-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="48081-182">a.</span><span class="sxs-lookup"><span data-stu-id="48081-182">a.</span></span> <span data-ttu-id="48081-183">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48081-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48081-184">b.</span><span class="sxs-lookup"><span data-stu-id="48081-184">b.</span></span> <span data-ttu-id="48081-185">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="48081-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="48081-186">c.</span><span class="sxs-lookup"><span data-stu-id="48081-186">c.</span></span> <span data-ttu-id="48081-187">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="48081-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="48081-188">d.</span><span class="sxs-lookup"><span data-stu-id="48081-188">d.</span></span> <span data-ttu-id="48081-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="48081-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="48081-190">Een testgebruiker Workrite maken</span><span class="sxs-lookup"><span data-stu-id="48081-190">Create a Workrite test user</span></span>

<span data-ttu-id="48081-191">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Workrite van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="48081-191">hello objective of this section is toocreate a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="48081-192">**een gebruiker Britta Simon aangeroepen in Workrite, toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="48081-192">**toocreate a user called Britta Simon in Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="48081-193">Tooyour workrite bedrijf site zich aanmelden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="48081-193">Sign on tooyour workrite company site as administrator.</span></span>

2. <span data-ttu-id="48081-194">Klik in het navigatiedeelvenster hello, **Admin**.</span><span class="sxs-lookup"><span data-stu-id="48081-194">In hello navigation pane, click **Admin**.</span></span>
   
    ![Controle van de beheerder][400]

3. <span data-ttu-id="48081-196">Ga tooQuick koppelingen en klik vervolgens op **maken van een gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="48081-196">Go tooQuick Links, and then click **Create a User**.</span></span>
   
    ![Sectie van de gebruiker maken][401]

4. <span data-ttu-id="48081-198">Op Hallo **gebruiker maken** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="48081-198">On hello **Create User** dialog, perform hello following steps:</span></span>
   
    ![Gebruiker Dailog maken][402]
    
    <span data-ttu-id="48081-200">a.</span><span class="sxs-lookup"><span data-stu-id="48081-200">a.</span></span> <span data-ttu-id="48081-201">In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="48081-201">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="48081-202">b.</span><span class="sxs-lookup"><span data-stu-id="48081-202">b.</span></span> <span data-ttu-id="48081-203">In Hallo **voornaam** textbox type Hallo firstname van gebruiker zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="48081-203">In hello **First Name** textbox, type hello firstname of user like Britta.</span></span>

    <span data-ttu-id="48081-204">c.</span><span class="sxs-lookup"><span data-stu-id="48081-204">c.</span></span> <span data-ttu-id="48081-205">In Hallo **achternaam** textbox type Hallo achternaam van de gebruiker zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="48081-205">In hello **Surname** textbox, type hello surname of user like Simon.</span></span>
    
    <span data-ttu-id="48081-206">d.</span><span class="sxs-lookup"><span data-stu-id="48081-206">d.</span></span> <span data-ttu-id="48081-207">Selecteer **Client Administrator** als **Kies rol**.</span><span class="sxs-lookup"><span data-stu-id="48081-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="48081-208">e.</span><span class="sxs-lookup"><span data-stu-id="48081-208">e.</span></span> <span data-ttu-id="48081-209">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="48081-209">Click **Save**.</span></span>   

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="48081-210">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="48081-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="48081-211">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWorkrite toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="48081-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkrite.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="48081-213">**tooassign Britta Simon tooWorkrite, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="48081-213">**tooassign Britta Simon tooWorkrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="48081-214">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="48081-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="48081-216">Selecteer in de lijst met de toepassingen van Hallo **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="48081-216">In hello applications list, select **Workrite**.</span></span>

    ![Hallo Workrite koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="48081-218">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="48081-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="48081-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="48081-220">Click **Add** button.</span></span> <span data-ttu-id="48081-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48081-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="48081-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="48081-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="48081-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48081-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48081-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48081-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="48081-226">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="48081-226">Test single sign-on</span></span>

<span data-ttu-id="48081-227">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="48081-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="48081-228">Als u op Hallo Workrite tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Workrite toepassing.</span><span class="sxs-lookup"><span data-stu-id="48081-228">When you click hello Workrite tile in hello Access Panel, you should get automatically signed-on tooyour Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48081-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="48081-229">Additional resources</span></span>

* [<span data-ttu-id="48081-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48081-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48081-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48081-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

