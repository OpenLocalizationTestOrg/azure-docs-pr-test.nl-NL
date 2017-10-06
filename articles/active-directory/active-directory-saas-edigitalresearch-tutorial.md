---
title: 'Zelfstudie: Azure Active Directory-integratie met eDigitalResearch | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en eDigitalResearch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="cd8da-103">Zelfstudie: Azure Active Directory-integratie met eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="cd8da-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="cd8da-104">In deze zelfstudie leert u hoe toointegrate eDigitalResearch met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cd8da-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd8da-105">EDigitalResearch integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="cd8da-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cd8da-106">U kunt beheren in Azure AD die tooeDigitalResearch toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="cd8da-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="cd8da-107">U kunt uw gebruikers tooautomatically get aangemelde tooeDigitalResearch (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cd8da-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cd8da-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="cd8da-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cd8da-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd8da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd8da-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cd8da-110">Prerequisites</span></span>

<span data-ttu-id="cd8da-111">Azure AD-integratie met eDigitalResearch tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="cd8da-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="cd8da-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="cd8da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd8da-113">Een eDigitalResearch eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="cd8da-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd8da-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cd8da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd8da-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="cd8da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd8da-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="cd8da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd8da-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd8da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd8da-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cd8da-118">Scenario description</span></span>
<span data-ttu-id="cd8da-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="cd8da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd8da-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="cd8da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd8da-121">Het toevoegen van eDigitalResearch van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cd8da-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="cd8da-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cd8da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="cd8da-123">Het toevoegen van eDigitalResearch van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cd8da-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="cd8da-124">tooconfigure hello integratie van eDigitalResearch in Azure AD, moet u tooadd eDigitalResearch uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="cd8da-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cd8da-125">**tooadd eDigitalResearch via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cd8da-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd8da-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cd8da-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="cd8da-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cd8da-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="cd8da-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cd8da-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="cd8da-133">Typ in het zoekvak Hallo **eDigitalResearch**, selecteer **eDigitalResearch** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cd8da-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![eDigitalResearch in de lijst met resultaten Hallo](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cd8da-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8da-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cd8da-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met eDigitalResearch op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="cd8da-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cd8da-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in eDigitalResearch is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd8da-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="cd8da-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in eDigitalResearch toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="cd8da-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="cd8da-139">Wijs in eDigitalResearch, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="cd8da-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cd8da-140">tooconfigure en eenmalige aanmelding Azure AD-test met eDigitalResearch, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd8da-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cd8da-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="cd8da-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cd8da-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd8da-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd8da-143">**[Maak een testgebruiker eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave een equivalent van Britta Simon in eDigitalResearch die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cd8da-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd8da-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cd8da-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd8da-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="cd8da-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cd8da-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="cd8da-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cd8da-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing eDigitalResearch configureren.</span><span class="sxs-lookup"><span data-stu-id="cd8da-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="cd8da-148">**Azure AD tooconfigure eenmalige aanmelding met eDigitalResearch, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cd8da-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd8da-149">In de Azure-portal op Hallo Hallo **eDigitalResearch** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="cd8da-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cd8da-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="cd8da-153">Op Hallo **eDigitalResearch domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd8da-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![eDigitalResearch domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="cd8da-155">a.</span><span class="sxs-lookup"><span data-stu-id="cd8da-155">a.</span></span> <span data-ttu-id="cd8da-156">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="cd8da-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="cd8da-157">b.</span><span class="sxs-lookup"><span data-stu-id="cd8da-157">b.</span></span> <span data-ttu-id="cd8da-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="cd8da-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd8da-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="cd8da-159">These values are not real.</span></span> <span data-ttu-id="cd8da-160">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="cd8da-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="cd8da-161">Neem contact op met [eDigitalResearch ondersteuningsteam](http://www.maruedr.com/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="cd8da-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="cd8da-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat Base(64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cd8da-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="cd8da-163">!</span><span class="sxs-lookup"><span data-stu-id="cd8da-163">!</span></span>![Hallo certificaat downloadkoppeling](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="cd8da-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="cd8da-165">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cd8da-167">Op Hallo **eDigitalResearch configuratie** sectie, klikt u op **configureren eDigitalResearch** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="cd8da-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cd8da-168">Kopiëren Hallo **Sign-Out-URL, de entiteit-ID SAML** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="cd8da-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![eDigitalResearch configuratie](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="cd8da-170">tooconfigure eenmalige aanmelding op **eDigitalResearch** zijde, moet u toosend Hallo gedownload **certificaatbestand (Base64)**, **SAML entiteit-ID**, en  **Afmelden URL** te[eDigitalResearch ondersteuningsteam](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="cd8da-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="cd8da-171">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cd8da-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cd8da-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="cd8da-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cd8da-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="cd8da-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cd8da-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd8da-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cd8da-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cd8da-175">Create an Azure AD test user</span></span>

<span data-ttu-id="cd8da-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cd8da-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="cd8da-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cd8da-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd8da-179">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="cd8da-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cd8da-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cd8da-183">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cd8da-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cd8da-185">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd8da-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cd8da-187">a.</span><span class="sxs-lookup"><span data-stu-id="cd8da-187">a.</span></span> <span data-ttu-id="cd8da-188">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd8da-189">b.</span><span class="sxs-lookup"><span data-stu-id="cd8da-189">b.</span></span> <span data-ttu-id="cd8da-190">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="cd8da-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cd8da-191">c.</span><span class="sxs-lookup"><span data-stu-id="cd8da-191">c.</span></span> <span data-ttu-id="cd8da-192">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="cd8da-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cd8da-193">d.</span><span class="sxs-lookup"><span data-stu-id="cd8da-193">d.</span></span> <span data-ttu-id="cd8da-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="cd8da-195">Een testgebruiker eDigitalResearch maken</span><span class="sxs-lookup"><span data-stu-id="cd8da-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="cd8da-196">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in eDigitalResearch van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cd8da-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="cd8da-197">Werken met Hallo [eDigitalResearch ondersteuningsteam](http://www.maruedr.com/contact) tooget gebruikers die zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cd8da-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="cd8da-198">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="cd8da-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cd8da-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8da-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cd8da-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooeDigitalResearch toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="cd8da-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="cd8da-202">**tooassign Britta Simon tooeDigitalResearch, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cd8da-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd8da-203">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="cd8da-205">Selecteer in de lijst met de toepassingen van Hallo **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![Hallo eDigitalResearch koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="cd8da-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="cd8da-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="cd8da-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="cd8da-209">Click **Add** button.</span></span> <span data-ttu-id="cd8da-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cd8da-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="cd8da-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd8da-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cd8da-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cd8da-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd8da-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cd8da-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cd8da-215">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cd8da-215">Test single sign-on</span></span>

<span data-ttu-id="cd8da-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="cd8da-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cd8da-217">Als u op Hallo eDigitalResearch tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour eDigitalResearch toepassing.</span><span class="sxs-lookup"><span data-stu-id="cd8da-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="cd8da-218">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd8da-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cd8da-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cd8da-219">Additional resources</span></span>

* [<span data-ttu-id="cd8da-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd8da-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd8da-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd8da-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

