---
title: 'Zelfstudie: Azure Active Directory-integratie met Symantec Web Security Service (WSS) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Symantec Web Security Service (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="9a629-103">Zelfstudie: Azure Active Directory-integratie met Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="9a629-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="9a629-104">In deze zelfstudie leert u hoe toointegrate uw Symantec Web Security Service (WSS) rekening met uw account voor Azure Active Directory (Azure AD) zodat WSS een eindgebruiker ingericht in Azure AD Hallo kan verifiëren met behulp van SAML-verificatie en afdwingen van de gebruiker of groep niveau beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="9a629-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="9a629-105">Symantec Web Security Service (WSS) integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9a629-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a629-106">Alle Hallo end gebruikers en groepen die worden gebruikt door uw WSS-account van uw Azure AD-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="9a629-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="9a629-107">Hallo end gebruikers tooauthenticate zelf in toestaan WSS met hun Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="9a629-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="9a629-108">Inschakelen Hallo afdwinging van gebruiker en groep niveau beleidsregels die zijn gedefinieerd in uw WSS-account.</span><span class="sxs-lookup"><span data-stu-id="9a629-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="9a629-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a629-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a629-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9a629-110">Prerequisites</span></span>

<span data-ttu-id="9a629-111">tooconfigure Azure AD-integratie met Symantec Web Security Service (WSS), moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="9a629-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="9a629-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9a629-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a629-113">Een account Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="9a629-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="9a629-114">tootest hello stappen in deze zelfstudie, raden we niet met een WSS-account dat momenteel wordt gebruikt voor productie-doel.</span><span class="sxs-lookup"><span data-stu-id="9a629-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="9a629-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9a629-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a629-116">Gebruik niet uw WSS-account dat momenteel wordt gebruikt voor productie-doel voor deze test als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="9a629-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="9a629-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a629-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a629-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a629-118">Scenario description</span></span>
<span data-ttu-id="9a629-119">In deze zelfstudie configureert u uw Azure AD tooenable eenmalige aanmelding tooWSS met de referenties van de eindgebruiker Hallo gedefinieerd in uw Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="9a629-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="9a629-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9a629-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a629-121">Hallo Symantec Web Security Service (WSS) app uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a629-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="9a629-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a629-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="9a629-123">Het toevoegen van Symantec Web Security Service (WSS) van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="9a629-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="9a629-124">tooconfigure hello integratie van Symantec Web Security Service (WSS) in Azure AD, moet u tooadd Symantec Web Security Service (WSS) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9a629-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a629-125">**tooadd Symantec Web Security Service (WSS) uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a629-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a629-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9a629-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="9a629-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a629-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a629-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a629-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="9a629-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a629-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="9a629-133">Typ in het zoekvak Hallo **Symantec Web Security Service (WSS)**, selecteer **Symantec Web Security Service (WSS)** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a629-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Symantec Web Security Service (WSS) in de lijst met resultaten Hallo](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a629-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a629-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a629-136">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Symantec Web Security Service (WSS) hebt op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9a629-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a629-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Symantec Web Security Service (WSS) is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a629-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="9a629-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in Symantec Web Security Service (WSS) toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="9a629-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="9a629-139">In Symantec Web Security Service (WSS), wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="9a629-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9a629-140">tooconfigure en test eenmalige aanmelding Azure AD met Symantec Web Security Service (WSS), moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a629-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a629-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="9a629-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a629-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a629-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a629-143">**[Maak een testgebruiker Symantec Web Security Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave een equivalent van Britta Simon in Symantec Web Security Service (WSS) die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9a629-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a629-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a629-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a629-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9a629-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a629-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9a629-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a629-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9a629-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="9a629-148">**tooconfigure eenmalige aanmelding Azure AD met Symantec Web Security Service (WSS), Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a629-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="9a629-149">In de Azure-portal op Hallo Hallo **Symantec Web Security Service (WSS)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9a629-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9a629-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a629-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="9a629-153">Op Hallo **Symantec Web Service (WSS) beveiligingsdomein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a629-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Symantec Web Security Service (WSS)-domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="9a629-155">a.</span><span class="sxs-lookup"><span data-stu-id="9a629-155">a.</span></span> <span data-ttu-id="9a629-156">In Hallo **id** textbox type Hallo URL:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="9a629-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="9a629-157">b.</span><span class="sxs-lookup"><span data-stu-id="9a629-157">b.</span></span> <span data-ttu-id="9a629-158">In Hallo **antwoord-URL** textbox type Hallo URL:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="9a629-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a629-159">Neem contact op met de Hallo [Symantec Web Security Service (WSS) Client ondersteuningsteam](https://www.symantec.com/contact-us) als Hallo voor Hallo waarden **id** en **antwoord-URL** zijn voor een bepaalde reden niet werkt.</span><span class="sxs-lookup"><span data-stu-id="9a629-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="9a629-160">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9a629-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="9a629-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9a629-162">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="9a629-164">Raadpleeg toohello WSS onlinedocumentatie tooconfigure eenmalige aanmelding op Hallo kant Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9a629-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="9a629-165">Hallo gedownload **Metadata XML** bestand moet toobe geïmporteerd in Hallo WSS-portal.</span><span class="sxs-lookup"><span data-stu-id="9a629-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="9a629-166">Neem contact op met Hallo [Symantec Web Security Service (WSS) ondersteuningsteam](https://www.symantec.com/contact-us) als u hulp nodig hebt bij Hallo-configuratie op Hallo WSS-portal.</span><span class="sxs-lookup"><span data-stu-id="9a629-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="9a629-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="9a629-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a629-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="9a629-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a629-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a629-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a629-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9a629-170">Create an Azure AD test user</span></span>

<span data-ttu-id="9a629-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9a629-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="9a629-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a629-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a629-174">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="9a629-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9a629-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9a629-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9a629-178">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a629-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9a629-180">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a629-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9a629-182">a.</span><span class="sxs-lookup"><span data-stu-id="9a629-182">a.</span></span> <span data-ttu-id="9a629-183">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a629-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a629-184">b.</span><span class="sxs-lookup"><span data-stu-id="9a629-184">b.</span></span> <span data-ttu-id="9a629-185">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="9a629-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9a629-186">c.</span><span class="sxs-lookup"><span data-stu-id="9a629-186">c.</span></span> <span data-ttu-id="9a629-187">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="9a629-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9a629-188">d.</span><span class="sxs-lookup"><span data-stu-id="9a629-188">d.</span></span> <span data-ttu-id="9a629-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a629-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="9a629-190">Maak een testgebruiker Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="9a629-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="9a629-191">In deze sectie maakt u een gebruiker met de naam Britta Simon in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9a629-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="9a629-192">Hallo overeenkomende end gebruikersnaam kan handmatig worden gemaakt in Hallo WSS-portal of u kunt wachten op Hallo gebruikers/groepen ingericht in hello Azure AD gesynchroniseerd toobe toohello WSS-portal na een paar minuten (~ 15 minuten).</span><span class="sxs-lookup"><span data-stu-id="9a629-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="9a629-193">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9a629-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="9a629-194">Hallo openbaar IP-adres van de machine eindgebruiker hello, die wordt gebruikt toobrowse websites moet ook toobe ingericht in Hallo Symantec Web Security Service (WSS)-portal.</span><span class="sxs-lookup"><span data-stu-id="9a629-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9a629-195">Neem [Klik hier](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget uw machine het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="9a629-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9a629-196">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a629-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9a629-197">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSymantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="9a629-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="9a629-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS) uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a629-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="9a629-200">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a629-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9a629-202">Selecteer in de lijst met de toepassingen van Hallo **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="9a629-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Hallo Symantec Web Security Service (WSS) koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="9a629-204">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9a629-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="9a629-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9a629-206">Click **Add** button.</span></span> <span data-ttu-id="9a629-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a629-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="9a629-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="9a629-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a629-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a629-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a629-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a629-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a629-212">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a629-212">Test single sign-on</span></span>

<span data-ttu-id="9a629-213">In deze sectie maakt u test Hallo één functionaliteit van eenmalige aanmelding nu dat u hebt uw account WSS toouse geconfigureerd uw Azure AD voor SAML-verificatie.</span><span class="sxs-lookup"><span data-stu-id="9a629-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="9a629-214">Nadat u hebt geconfigureerd omgeleid uw browser tooproxy webverkeer tooWSS, wanneer u uw webbrowser Open en u vervolgens toobrowse tooa site probeert, moet de pagina toohello Azure eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a629-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="9a629-215">Hallo referenties opgeven van eindgebruiker van het Hallo-test die is ingericht in hello Azure AD (dat wil zeggen, BrittaSimon) en bijbehorende wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="9a629-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="9a629-216">Eenmaal is geverifieerd, zult u kunnen toobrowse toohello website die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="9a629-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="9a629-217">U moet een beleidsregel op Hallo WSS side tooblock BrittaSimon van tooa bepaalde site te bladeren en vervolgens u Hallo WSS blok pagina ziet wanneer u toobrowse toothat site als gebruiker BrittaSimon probeert maken.</span><span class="sxs-lookup"><span data-stu-id="9a629-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a629-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9a629-218">Additional resources</span></span>

* [<span data-ttu-id="9a629-219">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a629-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a629-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a629-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

