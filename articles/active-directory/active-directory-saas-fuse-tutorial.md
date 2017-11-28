---
title: 'Zelfstudie: Azure Active Directory-integratie met zekering | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en zekering.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="56b8c-103">Zelfstudie: Azure Active Directory-integratie met zekering</span><span class="sxs-lookup"><span data-stu-id="56b8c-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="56b8c-104">In deze zelfstudie leert u hoe toointegrate integreert met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56b8c-104">In this tutorial, you learn how toointegrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56b8c-105">Zekering integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="56b8c-105">Integrating Fuse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="56b8c-106">U kunt beheren in Azure AD die tooFuse toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="56b8c-106">You can control in Azure AD who has access tooFuse.</span></span>
- <span data-ttu-id="56b8c-107">U kunt uw gebruikers tooautomatically get aangemelde tooFuse (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="56b8c-107">You can enable your users tooautomatically get signed-on tooFuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="56b8c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="56b8c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="56b8c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56b8c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56b8c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="56b8c-110">Prerequisites</span></span>

<span data-ttu-id="56b8c-111">tooconfigure Azure AD-integratie met zekering, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="56b8c-111">tooconfigure Azure AD integration with Fuse, you need hello following items:</span></span>

- <span data-ttu-id="56b8c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="56b8c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56b8c-113">Een zekering eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="56b8c-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56b8c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="56b8c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56b8c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="56b8c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56b8c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="56b8c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56b8c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56b8c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56b8c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="56b8c-118">Scenario description</span></span>
<span data-ttu-id="56b8c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="56b8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56b8c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="56b8c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56b8c-121">Zekering van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="56b8c-121">Add Fuse from hello gallery</span></span>
2. <span data-ttu-id="56b8c-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="56b8c-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-hello-gallery"></a><span data-ttu-id="56b8c-123">Zekering van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="56b8c-123">Add Fuse from hello gallery</span></span>
<span data-ttu-id="56b8c-124">tooconfigure hello integratie van zekering in Azure AD, moet u tooadd zekering uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="56b8c-124">tooconfigure hello integration of Fuse into Azure AD, you need tooadd Fuse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="56b8c-125">**tooadd zekering via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56b8c-125">**tooadd Fuse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b8c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="56b8c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="56b8c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="56b8c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="56b8c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56b8c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="56b8c-133">Typ in het zoekvak Hallo **integreert**, selecteer **integreert** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b8c-133">In hello search box, type **Fuse**, select **Fuse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Integreert in de lijst met resultaten Hallo](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="56b8c-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="56b8c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="56b8c-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met zekering op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="56b8c-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56b8c-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in zekering is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56b8c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuse is tooa user in Azure AD.</span></span> <span data-ttu-id="56b8c-138">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in zekering behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="56b8c-138">In other words, a link relationship between an Azure AD user and hello related user in Fuse needs toobe established.</span></span>

<span data-ttu-id="56b8c-139">Wijs in zekering, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="56b8c-139">In Fuse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="56b8c-140">tooconfigure en eenmalige aanmelding Azure AD-test met zekering, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="56b8c-140">tooconfigure and test Azure AD single sign-on with Fuse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="56b8c-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="56b8c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="56b8c-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56b8c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56b8c-143">**[Maak een testgebruiker zekering](#create-a-fuse-test-user)**  -toohave een equivalent van Britta Simon in zekering die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="56b8c-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - toohave a counterpart of Britta Simon in Fuse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="56b8c-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="56b8c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56b8c-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="56b8c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="56b8c-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="56b8c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="56b8c-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing zekering configureren.</span><span class="sxs-lookup"><span data-stu-id="56b8c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="56b8c-148">**tooconfigure eenmalige aanmelding Azure AD met zekering, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56b8c-148">**tooconfigure Azure AD single sign-on with Fuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b8c-149">In de Azure-portal op Hallo Hallo **integreert** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-149">In hello Azure portal, on hello **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="56b8c-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="56b8c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="56b8c-153">Op Hallo **integreert domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="56b8c-153">On hello **Fuse Domain and URLs** section, perform hello following steps:</span></span>

    ![Integreert domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="56b8c-155">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="56b8c-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56b8c-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="56b8c-156">This value is not real.</span></span> <span data-ttu-id="56b8c-157">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="56b8c-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="56b8c-158">Neem contact op met [Client integreert ondersteuningsteam](mailto:support@fusion-universal.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="56b8c-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="56b8c-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="56b8c-159">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="56b8c-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="56b8c-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="56b8c-163">Op Hallo **integreert configuratie** sectie, klikt u op **configureren integreert** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="56b8c-163">On hello **Fuse Configuration** section, click **Configure Fuse** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="56b8c-164">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="56b8c-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Integreert configuratie](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="56b8c-166">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [zekering ondersteuningsteam](mailto:support@fusion-universal.com) en voorzien Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="56b8c-166">tooget SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with hello following:</span></span>

    * <span data-ttu-id="56b8c-167">Hallo gedownload **certificaatbestand (Raw)**</span><span class="sxs-lookup"><span data-stu-id="56b8c-167">hello downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="56b8c-168">Hallo **SAML Single Sign-On Service-URL**</span><span class="sxs-lookup"><span data-stu-id="56b8c-168">hello **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="56b8c-169">Hallo **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="56b8c-169">hello **SAML Entity ID**</span></span>
    * <span data-ttu-id="56b8c-170">Hallo **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="56b8c-170">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="56b8c-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="56b8c-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="56b8c-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="56b8c-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="56b8c-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56b8c-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="56b8c-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="56b8c-174">Create an Azure AD test user</span></span>

<span data-ttu-id="56b8c-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="56b8c-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="56b8c-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56b8c-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b8c-178">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="56b8c-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="56b8c-180">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="56b8c-182">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56b8c-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="56b8c-184">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="56b8c-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="56b8c-186">a.</span><span class="sxs-lookup"><span data-stu-id="56b8c-186">a.</span></span> <span data-ttu-id="56b8c-187">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56b8c-188">b.</span><span class="sxs-lookup"><span data-stu-id="56b8c-188">b.</span></span> <span data-ttu-id="56b8c-189">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="56b8c-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="56b8c-190">c.</span><span class="sxs-lookup"><span data-stu-id="56b8c-190">c.</span></span> <span data-ttu-id="56b8c-191">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="56b8c-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="56b8c-192">d.</span><span class="sxs-lookup"><span data-stu-id="56b8c-192">d.</span></span> <span data-ttu-id="56b8c-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="56b8c-194">Een testgebruiker zekering maken</span><span class="sxs-lookup"><span data-stu-id="56b8c-194">Create a Fuse test user</span></span>

<span data-ttu-id="56b8c-195">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in zekering maken.</span><span class="sxs-lookup"><span data-stu-id="56b8c-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="56b8c-196">Neem contact op met [zekering ondersteuningsteam](mailto:support@fusion-universal.com) tooadd Hallo gebruikers in Hallo zekering platform.</span><span class="sxs-lookup"><span data-stu-id="56b8c-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) tooadd hello users in hello Fuse platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="56b8c-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="56b8c-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="56b8c-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooFuse toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="56b8c-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFuse.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="56b8c-200">**tooassign Britta Simon tooFuse, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56b8c-200">**tooassign Britta Simon tooFuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b8c-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="56b8c-203">Selecteer in de lijst met de toepassingen van Hallo **integreert**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-203">In hello applications list, select **Fuse**.</span></span>

    ![Hallo zekering koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="56b8c-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="56b8c-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="56b8c-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="56b8c-207">Click **Add** button.</span></span> <span data-ttu-id="56b8c-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56b8c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="56b8c-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="56b8c-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="56b8c-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56b8c-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56b8c-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56b8c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="56b8c-213">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="56b8c-213">Test single sign-on</span></span>

<span data-ttu-id="56b8c-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="56b8c-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="56b8c-215">Als u op Hallo zekering tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour zekering van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b8c-215">When you click hello Fuse tile in hello Access Panel, you should get automatically signed-on tooyour Fuse application.</span></span>
<span data-ttu-id="56b8c-216">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="56b8c-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="56b8c-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="56b8c-217">Additional resources</span></span>

* [<span data-ttu-id="56b8c-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56b8c-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56b8c-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56b8c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

