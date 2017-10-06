---
title: 'Zelfstudie: Azure Active Directory-integratie met Evernote | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Evernote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="8f615-103">Zelfstudie: Azure Active Directory-integratie met Evernote</span><span class="sxs-lookup"><span data-stu-id="8f615-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="8f615-104">In deze zelfstudie leert u hoe toointegrate Evernote met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f615-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f615-105">Evernote integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8f615-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8f615-106">U kunt beheren in Azure AD die tooEvernote toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="8f615-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="8f615-107">U kunt uw gebruikers tooautomatically get aangemelde tooEvernote (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8f615-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8f615-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="8f615-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8f615-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f615-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f615-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8f615-110">Prerequisites</span></span>

<span data-ttu-id="8f615-111">Azure AD-integratie met Evernote tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8f615-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="8f615-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8f615-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f615-113">Een Evernote eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8f615-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f615-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8f615-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f615-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8f615-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f615-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8f615-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f615-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f615-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f615-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8f615-118">Scenario description</span></span>
<span data-ttu-id="8f615-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8f615-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f615-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8f615-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f615-121">Het toevoegen van Evernote van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8f615-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="8f615-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8f615-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="8f615-123">Het toevoegen van Evernote van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8f615-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="8f615-124">tooconfigure hello integratie van Evernote in Azure AD, moet u tooadd Evernote uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8f615-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8f615-125">**tooadd Evernote via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f615-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f615-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8f615-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="8f615-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8f615-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8f615-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8f615-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="8f615-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f615-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="8f615-133">Typ in het zoekvak Hallo **Evernote**, selecteer **Evernote** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8f615-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evernote in de lijst met resultaten Hallo](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8f615-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f615-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8f615-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Evernote op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="8f615-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8f615-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Evernote is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f615-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="8f615-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Evernote toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="8f615-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="8f615-139">Wijs in Evernote, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="8f615-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8f615-140">tooconfigure en eenmalige aanmelding Azure AD-test met Evernote, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f615-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8f615-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="8f615-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8f615-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f615-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f615-143">**[Maken van een testgebruiker Evernote](#create-an-evernote-test-user)**  -toohave een equivalent van Britta Simon in Evernote die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8f615-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f615-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8f615-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f615-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8f615-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8f615-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8f615-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8f615-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Evernote configureren.</span><span class="sxs-lookup"><span data-stu-id="8f615-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="8f615-148">**Azure AD tooconfigure eenmalige aanmelding met Evernote, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f615-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f615-149">In de Azure-portal op Hallo Hallo **Evernote** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8f615-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8f615-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8f615-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="8f615-153">Op Hallo **Evernote domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wenst tooconfigure Hallo toepassing in de IDP geïnitieerd modus:</span><span class="sxs-lookup"><span data-stu-id="8f615-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![URL's en Evernote domein eenmalige aanmelding informatie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="8f615-155">In Hallo **id** textbox type Hallo URL:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="8f615-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="8f615-156">Controleer **weergeven geavanceerde instellingen voor URL** en uitvoeren van de volgende stap als u wilt dat tooconfigure Hallo toepassing in Hallo **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="8f615-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![URL's en Evernote domein eenmalige aanmelding informatie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="8f615-158">In Hallo **aanmelden URL** textbox type Hallo URL:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="8f615-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="8f615-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8f615-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="8f615-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8f615-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8f615-163">Op Hallo **Evernote configuratie** sectie, klikt u op **configureren Evernote** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="8f615-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8f615-164">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="8f615-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Evernote configuratie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="8f615-166">In een ander browservenster, meld u bij uw bedrijf Evernote site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8f615-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="8f615-167">Ga te**Admin-Console**</span><span class="sxs-lookup"><span data-stu-id="8f615-167">Go too**'Admin Console'**</span></span>

    ![-Beheerconsole](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="8f615-169">Van Hallo **Admin-Console**, gaat u te**'Security'** en selecteer **' Single Sign-On'**</span><span class="sxs-lookup"><span data-stu-id="8f615-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-instelling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="8f615-171">Configureer Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="8f615-171">Configure hello following values:</span></span>

    ![Certificaat-instelling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="8f615-173">a.</span><span class="sxs-lookup"><span data-stu-id="8f615-173">a.</span></span>  <span data-ttu-id="8f615-174">**Eenmalige aanmelding inschakelen:** eenmalige aanmelding is standaard ingeschakeld (Klik op **uitschakelen Single Sign-on** tooremove Hallo SSO vereiste)</span><span class="sxs-lookup"><span data-stu-id="8f615-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="8f615-175">b.</span><span class="sxs-lookup"><span data-stu-id="8f615-175">b.</span></span> <span data-ttu-id="8f615-176">Plakken **SAML eenmalige aanmelding Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **SAML HTTP-verzoek-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8f615-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="8f615-177">c.</span><span class="sxs-lookup"><span data-stu-id="8f615-177">c.</span></span> <span data-ttu-id="8f615-178">Hallo gedownloade certificaat openen vanuit Azure AD in Kladblok en kopieer Hallo inhoud zoals 'BEGIN CERTIFICATE' en 'END CERTIFICATE' en plak deze in Hallo **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="8f615-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="8f615-179">d.Click **wijzigingen opslaan**</span><span class="sxs-lookup"><span data-stu-id="8f615-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="8f615-180">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="8f615-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8f615-181">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="8f615-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8f615-182">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f615-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8f615-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8f615-183">Create an Azure AD test user</span></span>

<span data-ttu-id="8f615-184">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8f615-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="8f615-186">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f615-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f615-187">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="8f615-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8f615-189">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8f615-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8f615-191">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f615-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8f615-193">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f615-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8f615-195">a.</span><span class="sxs-lookup"><span data-stu-id="8f615-195">a.</span></span> <span data-ttu-id="8f615-196">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f615-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f615-197">b.</span><span class="sxs-lookup"><span data-stu-id="8f615-197">b.</span></span> <span data-ttu-id="8f615-198">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="8f615-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8f615-199">c.</span><span class="sxs-lookup"><span data-stu-id="8f615-199">c.</span></span> <span data-ttu-id="8f615-200">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="8f615-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8f615-201">d.</span><span class="sxs-lookup"><span data-stu-id="8f615-201">d.</span></span> <span data-ttu-id="8f615-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8f615-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="8f615-203">Een testgebruiker Evernote maken</span><span class="sxs-lookup"><span data-stu-id="8f615-203">Create an Evernote test user</span></span>

<span data-ttu-id="8f615-204">In de volgorde tooenable Azure AD gebruikers toolog in Evernote, moeten ze worden ingericht in Evernote.</span><span class="sxs-lookup"><span data-stu-id="8f615-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="8f615-205">In geval van Evernote Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="8f615-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="8f615-206">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="8f615-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f615-207">Aanmelden tooyour Evernote bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8f615-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="8f615-208">Klik op Hallo **Admin-Console**.</span><span class="sxs-lookup"><span data-stu-id="8f615-208">Click hello **'Admin Console'**.</span></span>

    ![-Beheerconsole](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="8f615-210">Van Hallo **Admin-Console**, gaat u te**toevoegen van gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8f615-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Voeg testgebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="8f615-212">**Teamleden toevoegen** in Hallo **e** textbox, typ de e-mailadres Hallo van gebruikersaccount en klik op **uit te nodigen.**</span><span class="sxs-lookup"><span data-stu-id="8f615-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Voeg testgebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="8f615-214">Nadat uitnodiging is verzonden, is het hello Azure Active Directory-accounthouder ontvangt een e-mailadres tooaccept Hallo uitnodiging.</span><span class="sxs-lookup"><span data-stu-id="8f615-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8f615-215">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f615-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8f615-216">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEvernote toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="8f615-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="8f615-218">**tooassign Britta Simon tooEvernote, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f615-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f615-219">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8f615-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8f615-221">Selecteer in de lijst met de toepassingen van Hallo **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="8f615-221">In hello applications list, select **Evernote**.</span></span>

    ![Hallo Evernote koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="8f615-223">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8f615-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="8f615-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8f615-225">Click **Add** button.</span></span> <span data-ttu-id="8f615-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f615-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="8f615-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f615-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8f615-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f615-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f615-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f615-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8f615-231">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8f615-231">Test single sign-on</span></span>

<span data-ttu-id="8f615-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8f615-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8f615-233">Als u op Hallo Evernote tegel in Hallo Toegangsvenster, krijgt u aangemelde tooyour Evernote toepassing.</span><span class="sxs-lookup"><span data-stu-id="8f615-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="8f615-234">U moet als een organisatie-account maar moeten toolog worden aanmelden met uw persoonlijke account.</span><span class="sxs-lookup"><span data-stu-id="8f615-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8f615-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8f615-235">Additional resources</span></span>

* [<span data-ttu-id="8f615-236">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f615-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f615-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f615-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

