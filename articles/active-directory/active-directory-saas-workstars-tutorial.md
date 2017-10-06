---
title: 'Zelfstudie: Azure Active Directory-integratie met Workstars | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Workstars.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="58815-103">Zelfstudie: Azure Active Directory-integratie met Workstars</span><span class="sxs-lookup"><span data-stu-id="58815-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="58815-104">In deze zelfstudie leert u hoe toointegrate Workstars met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58815-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58815-105">Workstars integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="58815-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="58815-106">U kunt beheren in Azure AD die tooWorkstars toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="58815-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="58815-107">U kunt uw gebruikers tooautomatically get aangemelde tooWorkstars (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="58815-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="58815-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="58815-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="58815-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58815-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58815-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="58815-110">Prerequisites</span></span>

<span data-ttu-id="58815-111">Azure AD-integratie met Workstars tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="58815-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="58815-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="58815-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58815-113">Een Workstars eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="58815-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58815-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="58815-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58815-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="58815-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58815-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="58815-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58815-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58815-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58815-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="58815-118">Scenario description</span></span>
<span data-ttu-id="58815-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="58815-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58815-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="58815-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58815-121">Het toevoegen van Workstars van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="58815-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="58815-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="58815-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="58815-123">Het toevoegen van Workstars van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="58815-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="58815-124">tooconfigure hello integratie van Workstars in Azure AD, moet u tooadd Workstars uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="58815-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="58815-125">**tooadd Workstars via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="58815-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="58815-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="58815-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="58815-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="58815-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="58815-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="58815-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="58815-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="58815-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="58815-133">Typ in het zoekvak Hallo **Workstars**, selecteer **Workstars** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="58815-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars in de lijst met resultaten Hallo](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="58815-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="58815-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="58815-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Workstars op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="58815-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58815-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Workstars is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58815-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="58815-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Workstars toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="58815-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="58815-139">Wijs in Workstars, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="58815-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="58815-140">tooconfigure en eenmalige aanmelding Azure AD-test met Workstars, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="58815-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="58815-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="58815-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="58815-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58815-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58815-143">**[Maak een testgebruiker Workstars](#create-a-workstars-test-user)**  -toohave een equivalent van Britta Simon in Workstars die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="58815-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="58815-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="58815-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58815-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="58815-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="58815-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="58815-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="58815-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Workstars configureren.</span><span class="sxs-lookup"><span data-stu-id="58815-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="58815-148">**Azure AD tooconfigure eenmalige aanmelding met Workstars, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="58815-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="58815-149">In de Azure-portal op Hallo Hallo **Workstars** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="58815-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="58815-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="58815-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="58815-153">Op Hallo **Workstars domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="58815-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Workstars domein eenmalige aanmelding informatie](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="58815-155">a.</span><span class="sxs-lookup"><span data-stu-id="58815-155">a.</span></span> <span data-ttu-id="58815-156">In Hallo **id** textbox type Hallo URL:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="58815-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="58815-157">b.</span><span class="sxs-lookup"><span data-stu-id="58815-157">b.</span></span> <span data-ttu-id="58815-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="58815-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="58815-159">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="58815-159">hello value is not real.</span></span> <span data-ttu-id="58815-160">Waarde van de update Hallo met Hallo werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="58815-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="58815-161">Neem contact op met [Workstars ondersteuningsteam](https://support.workstars.com) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="58815-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="58815-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="58815-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="58815-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="58815-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="58815-166">Op Hallo **Workstars configuratie** sectie, klikt u op **configureren Workstars** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="58815-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="58815-167">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="58815-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Workstars configuratie](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="58815-169">Een ander browservenster geopend Meld u aan bij tooyour Workstars bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="58815-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="58815-170">Klik in het Hallo hoofdwerkbalk op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="58815-170">In hello main toolbar, click **Settings**.</span></span>

    ![Workstars TAKENL](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="58815-172">Ga te**aanmelding** > **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="58815-172">Go too**Sign On** > **Settings**.</span></span>

    ![Workstars aanmelden](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Workstars instellingen](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="58815-175">Op Hallo **eenmalige aanmelding op (SAML) - instellingen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="58815-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="58815-177">a.</span><span class="sxs-lookup"><span data-stu-id="58815-177">a.</span></span> <span data-ttu-id="58815-178">In **identiteit providernaam** textbox type **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="58815-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="58815-179">b.</span><span class="sxs-lookup"><span data-stu-id="58815-179">b.</span></span> <span data-ttu-id="58815-180">In Hallo **identiteit Provider entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="58815-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="58815-181">c.</span><span class="sxs-lookup"><span data-stu-id="58815-181">c.</span></span> <span data-ttu-id="58815-182">Hallo-inhoud van de gedownloade certificaatbestand Hallo kopiëren in Kladblok en plak deze in Hallo **x509 certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="58815-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="58815-183">d.</span><span class="sxs-lookup"><span data-stu-id="58815-183">d.</span></span> <span data-ttu-id="58815-184">In Hallo **SAML SSO URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="58815-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="58815-185">e.</span><span class="sxs-lookup"><span data-stu-id="58815-185">e.</span></span> <span data-ttu-id="58815-186">In Hallo **externe URL voor afmelden** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="58815-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="58815-187">f.</span><span class="sxs-lookup"><span data-stu-id="58815-187">f.</span></span> <span data-ttu-id="58815-188">Selecteer **naam-ID** als **e (standaard)**.</span><span class="sxs-lookup"><span data-stu-id="58815-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="58815-189">g.</span><span class="sxs-lookup"><span data-stu-id="58815-189">g.</span></span> <span data-ttu-id="58815-190">Klik op **bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="58815-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="58815-191">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="58815-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="58815-192">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="58815-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="58815-193">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="58815-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="58815-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="58815-194">Create an Azure AD test user</span></span>

<span data-ttu-id="58815-195">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="58815-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="58815-197">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="58815-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="58815-198">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="58815-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="58815-200">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="58815-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="58815-202">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="58815-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="58815-204">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="58815-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="58815-206">a.</span><span class="sxs-lookup"><span data-stu-id="58815-206">a.</span></span> <span data-ttu-id="58815-207">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58815-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58815-208">b.</span><span class="sxs-lookup"><span data-stu-id="58815-208">b.</span></span> <span data-ttu-id="58815-209">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="58815-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="58815-210">c.</span><span class="sxs-lookup"><span data-stu-id="58815-210">c.</span></span> <span data-ttu-id="58815-211">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="58815-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="58815-212">d.</span><span class="sxs-lookup"><span data-stu-id="58815-212">d.</span></span> <span data-ttu-id="58815-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="58815-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="58815-214">Een testgebruiker Workstars maken</span><span class="sxs-lookup"><span data-stu-id="58815-214">Create a Workstars test user</span></span>

<span data-ttu-id="58815-215">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Workstars maken.</span><span class="sxs-lookup"><span data-stu-id="58815-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="58815-216">Werken met [Workstars ondersteuningsteam](https://support.workstars.com) tooadd Hallo gebruikers in Hallo Workstars platform.</span><span class="sxs-lookup"><span data-stu-id="58815-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="58815-217">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="58815-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="58815-218">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWorkstars toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="58815-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="58815-220">**tooassign Britta Simon tooWorkstars, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="58815-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="58815-221">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="58815-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="58815-223">Selecteer in de lijst met de toepassingen van Hallo **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="58815-223">In hello applications list, select **Workstars**.</span></span>

    ![Hallo Workstars koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="58815-225">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="58815-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="58815-227">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="58815-227">Click **Add** button.</span></span> <span data-ttu-id="58815-228">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="58815-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="58815-230">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="58815-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="58815-231">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="58815-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58815-232">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="58815-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="58815-233">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="58815-233">Test single sign-on</span></span>

<span data-ttu-id="58815-234">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="58815-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="58815-235">Als u op Hallo Workstars-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Workstars toepassing.</span><span class="sxs-lookup"><span data-stu-id="58815-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="58815-236">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="58815-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="58815-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="58815-237">Additional resources</span></span>

* [<span data-ttu-id="58815-238">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58815-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58815-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="58815-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

