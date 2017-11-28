---
title: 'Zelfstudie: Azure Active Directory-integratie met Thoughtworks Singleplayer | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Thoughtworks Singleplayer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="6ebcc-103">Zelfstudie: Azure Active Directory-integratie met Thoughtworks Singleplayer</span><span class="sxs-lookup"><span data-stu-id="6ebcc-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="6ebcc-104">In deze zelfstudie leert u hoe toointegrate Thoughtworks Singleplayer met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ebcc-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ebcc-105">Thoughtworks Singleplayer integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6ebcc-106">U kunt beheren in Azure AD wie toegang tot tooThoughtworks Mingle heeft</span><span class="sxs-lookup"><span data-stu-id="6ebcc-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="6ebcc-107">U kunt uw gebruikers tooautomatically get aangemelde tooThoughtworks Mingle (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6ebcc-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ebcc-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6ebcc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6ebcc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ebcc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ebcc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ebcc-110">Prerequisites</span></span>

<span data-ttu-id="6ebcc-111">Azure AD-integratie met Thoughtworks Singleplayer tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="6ebcc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6ebcc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ebcc-113">Een Thoughtworks Singleplayer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6ebcc-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ebcc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ebcc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ebcc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ebcc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ebcc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ebcc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6ebcc-118">Scenario description</span></span>
<span data-ttu-id="6ebcc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ebcc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ebcc-121">Het toevoegen van Thoughtworks Singleplayer van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6ebcc-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="6ebcc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ebcc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="6ebcc-123">Het toevoegen van Thoughtworks Singleplayer van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6ebcc-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="6ebcc-124">tooconfigure hello integratie van Thoughtworks Singleplayer in Azure AD, moet u tooadd Thoughtworks Singleplayer uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6ebcc-125">**tooadd Thoughtworks Singleplayer via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6ebcc-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ebcc-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="6ebcc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6ebcc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="6ebcc-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="6ebcc-133">Typ in het zoekvak Hallo **Thoughtworks Singleplayer**, selecteer **Thoughtworks Singleplayer** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Thoughtworks Singleplayer in de lijst met resultaten Hallo](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6ebcc-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ebcc-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6ebcc-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Thoughtworks Singleplayer op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ebcc-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Thoughtworks Singleplayer is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="6ebcc-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Thoughtworks Singleplayer toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="6ebcc-139">Wijs in het Thoughtworks Singleplayer, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6ebcc-140">tooconfigure en eenmalige aanmelding Azure AD-test met Thoughtworks Singleplayer, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6ebcc-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6ebcc-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ebcc-143">**[Maak een testgebruiker Thoughtworks Singleplayer](#create-a-thoughtworks-mingle-test-user)**  -toohave een equivalent van Britta Simon in Thoughtworks Singleplayer die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ebcc-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ebcc-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6ebcc-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6ebcc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6ebcc-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Thoughtworks Singleplayer configureren.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="6ebcc-148">**Azure AD tooconfigure eenmalige aanmelding met Thoughtworks Singleplayer, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6ebcc-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ebcc-149">In de Azure-portal op Hallo Hallo **Thoughtworks Singleplayer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6ebcc-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="6ebcc-153">Op Hallo **Thoughtworks Singleplayer domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Thoughtworks Singleplayer domein eenmalige aanmelding informatie](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="6ebcc-155">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="6ebcc-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ebcc-156">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-156">hello value is not real.</span></span> <span data-ttu-id="6ebcc-157">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6ebcc-158">Neem contact op met [Thoughtworks Singleplayer Client ondersteuningsteam](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="6ebcc-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="6ebcc-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6ebcc-163">Meld u bij tooyour **Thoughtworks Singleplayer** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="6ebcc-164">Klik op Hallo **Admin** tabblad en klik vervolgens op **SSO-Config**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="6ebcc-165">![Tabblad beheer](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="6ebcc-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="6ebcc-166">In Hallo **SSO-Config** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6ebcc-167">![SSO-Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="6ebcc-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="6ebcc-168">a.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-168">a.</span></span> <span data-ttu-id="6ebcc-169">metagegevensbestand tooupload hello, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="6ebcc-170">b.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-170">b.</span></span> <span data-ttu-id="6ebcc-171">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6ebcc-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6ebcc-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6ebcc-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ebcc-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6ebcc-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6ebcc-175">Create an Azure AD test user</span></span>
<span data-ttu-id="6ebcc-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="6ebcc-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6ebcc-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ebcc-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ebcc-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ebcc-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ebcc-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ebcc-187">a.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-187">a.</span></span> <span data-ttu-id="6ebcc-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ebcc-189">b.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-189">b.</span></span> <span data-ttu-id="6ebcc-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ebcc-191">c.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-191">c.</span></span> <span data-ttu-id="6ebcc-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6ebcc-193">d.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-193">d.</span></span> <span data-ttu-id="6ebcc-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="6ebcc-195">Een testgebruiker Thoughtworks Singleplayer maken</span><span class="sxs-lookup"><span data-stu-id="6ebcc-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="6ebcc-196">Voor Azure AD gebruikers toobe kunnen toosign in, moeten ze ingerichte toohello Thoughtworks Singleplayer toepassing met behulp van de namen van de Azure Active Directory-gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="6ebcc-197">In geval van Thoughtworks Singleplayer Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="6ebcc-198">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6ebcc-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ebcc-199">Aanmelden tooyour Thoughtworks Singleplayer bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="6ebcc-200">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="6ebcc-201">![Uw eerste Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "uw eerste Project")</span><span class="sxs-lookup"><span data-stu-id="6ebcc-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="6ebcc-202">Klik op Hallo **Admin** tabblad en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="6ebcc-203">![Gebruikers](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="6ebcc-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="6ebcc-204">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-204">Click **New User**.</span></span>
   
    <span data-ttu-id="6ebcc-205">![Nieuwe gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="6ebcc-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="6ebcc-206">Op Hallo **nieuwe gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ebcc-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="6ebcc-207">![Dialoogvenster Nieuwe gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="6ebcc-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="6ebcc-208">a.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-208">a.</span></span> <span data-ttu-id="6ebcc-209">Type Hallo **aanmeldingsnaam**, **weergavenaam**, **Kies wachtwoord**, **wachtwoord bevestigen** van een geldig Azure AD-account die u wilt dat tooprovision gerelateerde in Hallo tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="6ebcc-210">b.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-210">b.</span></span> <span data-ttu-id="6ebcc-211">Als **gebruikerstype**, selecteer **volledige gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="6ebcc-212">c.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-212">c.</span></span> <span data-ttu-id="6ebcc-213">Klik op **maken van dit profiel**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="6ebcc-214">U kunt andere Thoughtworks Singleplayer gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door tooprovision Thoughtworks Singleplayer AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6ebcc-215">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ebcc-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6ebcc-216">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooThoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="6ebcc-218">**tooassign Britta Simon tooThoughtworks Mingle, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6ebcc-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ebcc-219">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6ebcc-221">Selecteer in de lijst met de toepassingen van Hallo **Thoughtworks Singleplayer**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![Hallo Thoughtworks Singleplayer koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="6ebcc-223">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="6ebcc-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-225">Click **Add** button.</span></span> <span data-ttu-id="6ebcc-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="6ebcc-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6ebcc-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ebcc-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6ebcc-231">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ebcc-231">Test single sign-on</span></span>

<span data-ttu-id="6ebcc-232">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6ebcc-233">Als u op Hallo Thoughtworks Singleplayer tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Thoughtworks Singleplayer toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ebcc-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ebcc-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6ebcc-234">Additional resources</span></span>

* [<span data-ttu-id="6ebcc-235">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ebcc-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ebcc-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6ebcc-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

