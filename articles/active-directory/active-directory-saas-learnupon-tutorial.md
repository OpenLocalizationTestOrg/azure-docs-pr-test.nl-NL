---
title: 'Zelfstudie: Azure Active Directory-integratie met LearnUpon | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LearnUpon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="c366f-103">Zelfstudie: Azure Active Directory-integratie met LearnUpon</span><span class="sxs-lookup"><span data-stu-id="c366f-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="c366f-104">In deze zelfstudie leert u hoe toointegrate LearnUpon met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c366f-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c366f-105">LearnUpon integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c366f-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c366f-106">U kunt beheren in Azure AD die tooLearnUpon toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c366f-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="c366f-107">U kunt uw gebruikers tooautomatically get aangemelde tooLearnUpon (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c366f-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c366f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c366f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c366f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c366f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c366f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c366f-110">Prerequisites</span></span>

<span data-ttu-id="c366f-111">Azure AD-integratie met LearnUpon tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c366f-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="c366f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c366f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c366f-113">Een LearnUpon eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c366f-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c366f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c366f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c366f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c366f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c366f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c366f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c366f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c366f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c366f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c366f-118">Scenario description</span></span>
<span data-ttu-id="c366f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c366f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c366f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c366f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c366f-121">Het toevoegen van LearnUpon van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c366f-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="c366f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c366f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="c366f-123">Het toevoegen van LearnUpon van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c366f-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="c366f-124">tooconfigure hello integratie van LearnUpon in Azure AD, moet u tooadd LearnUpon uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c366f-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c366f-125">**tooadd LearnUpon via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c366f-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c366f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c366f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c366f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c366f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c366f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c366f-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c366f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c366f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c366f-133">Typ in het zoekvak Hallo **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="c366f-133">In hello search box, type **LearnUpon**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="c366f-135">Selecteer in het deelvenster resultaten hello, **LearnUpon**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c366f-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c366f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c366f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c366f-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met LearnUpon op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c366f-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c366f-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LearnUpon is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c366f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="c366f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in LearnUpon toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c366f-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="c366f-141">Wijs in LearnUpon, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c366f-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c366f-142">tooconfigure en eenmalige aanmelding Azure AD-test met LearnUpon, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c366f-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c366f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c366f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c366f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c366f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c366f-145">**[Maken van een testgebruiker LearnUpon](#creating-a-learnupon-test-user)**  -toohave een equivalent van Britta Simon in LearnUpon die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c366f-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c366f-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c366f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c366f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c366f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c366f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c366f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c366f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LearnUpon configureren.</span><span class="sxs-lookup"><span data-stu-id="c366f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="c366f-150">**Azure AD tooconfigure eenmalige aanmelding met LearnUpon, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c366f-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="c366f-151">In de Azure-portal op Hallo Hallo **LearnUpon** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c366f-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c366f-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c366f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="c366f-155">Op Hallo **LearnUpon domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c366f-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="c366f-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="c366f-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c366f-158">Houd er rekening mee dat dit geen Hallo echte waarde is.</span><span class="sxs-lookup"><span data-stu-id="c366f-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="c366f-159">u hebt deze waarde met de werkelijke antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="c366f-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="c366f-160">Neem contact op met tooget deze waarde [LearnUpon ondersteuningsteam](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="c366f-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="c366f-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c366f-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="c366f-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c366f-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c366f-165">Op Hallo **LearnUpon configuratie** sectie, klikt u op **configureren LearnUpon** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c366f-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c366f-166">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c366f-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="c366f-168">Open een ander browserexemplaar en meld u aan bij LearnUpon met een administratoraccount.</span><span class="sxs-lookup"><span data-stu-id="c366f-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="c366f-169">Klik op Hallo **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c366f-169">Click hello **settings** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="c366f-171">Klik op **eenmalige aanmelding - SAML**, en klik vervolgens op **algemene instellingen** tooconfigure SAML-instellingen.</span><span class="sxs-lookup"><span data-stu-id="c366f-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="c366f-173">In Hallo **algemene instellingen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c366f-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="c366f-175">a.</span><span class="sxs-lookup"><span data-stu-id="c366f-175">a.</span></span> <span data-ttu-id="c366f-176">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="c366f-176">Select **Enabled**.</span></span>

    <span data-ttu-id="c366f-177">b.</span><span class="sxs-lookup"><span data-stu-id="c366f-177">b.</span></span> <span data-ttu-id="c366f-178">Selecteer **versie** als **2.0**.</span><span class="sxs-lookup"><span data-stu-id="c366f-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="c366f-179">c.</span><span class="sxs-lookup"><span data-stu-id="c366f-179">c.</span></span> <span data-ttu-id="c366f-180">Selecteer **overslaan voorwaarden** als **Nee**.</span><span class="sxs-lookup"><span data-stu-id="c366f-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="c366f-181">d.</span><span class="sxs-lookup"><span data-stu-id="c366f-181">d.</span></span> <span data-ttu-id="c366f-182">In Hallo **SAML-Token boeken param naam** textbox Hallo-typenaam van de aanvraag post parameter toohello SAML consumer URL hierboven genoemde met Hallo van SAML-verklaring toobe gecontroleerd en geverifieerd - bijvoorbeeld  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="c366f-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="c366f-183">e.</span><span class="sxs-lookup"><span data-stu-id="c366f-183">e.</span></span> <span data-ttu-id="c366f-184">In Hallo **indeling van de id** textbox type Hallo waarde die waar uw gebruikers van SAML-verklaring Hallo id (e-mailadres) zich bevindt aangeeft-bijvoorbeeld **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="c366f-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="c366f-185">f.</span><span class="sxs-lookup"><span data-stu-id="c366f-185">f.</span></span> <span data-ttu-id="c366f-186">In Hallo **Providerlocatie identificeren** textbox, type Hallo waarde die aangeeft waar hello gebruikers worden verzonden tooif ze klikt u op uw geüploade pictogram van het scherm van uw Azure-portal aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c366f-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="c366f-187">g.</span><span class="sxs-lookup"><span data-stu-id="c366f-187">g.</span></span> <span data-ttu-id="c366f-188">In Hallo **afmelden URL** textbox plakken Hallo **Sign-Out URL** die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c366f-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="c366f-189">h.</span><span class="sxs-lookup"><span data-stu-id="c366f-189">h.</span></span> <span data-ttu-id="c366f-190">Klik op **vinger afdrukken bestellen beheren**, en vervolgens de vingerafdruk Hallo van uw gedownloade certificaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="c366f-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="c366f-191">Klik op **gebruikersinstellingen**, en klik vervolgens op Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c366f-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="c366f-193">a.</span><span class="sxs-lookup"><span data-stu-id="c366f-193">a.</span></span> <span data-ttu-id="c366f-194">In Hallo **voornaam id indeling** textbox Hallo typewaarde die vertellen waar in uw voornaam SAML-verklaring Hallo gebruikers zich bevindt - voorbeeld: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="c366f-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="c366f-195">b.</span><span class="sxs-lookup"><span data-stu-id="c366f-195">b.</span></span> <span data-ttu-id="c366f-196">In Hallo **laatste naamnotatie id** textbox Hallo typewaarde die vertellen waar in uw achternaam SAML-verklaring Hallo gebruikers zich bevindt - voorbeeld: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="c366f-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="c366f-197">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c366f-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c366f-198">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c366f-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c366f-199">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c366f-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c366f-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c366f-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c366f-201">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c366f-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c366f-203">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c366f-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c366f-204">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c366f-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c366f-206">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c366f-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c366f-208">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c366f-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c366f-210">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c366f-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c366f-212">a.</span><span class="sxs-lookup"><span data-stu-id="c366f-212">a.</span></span> <span data-ttu-id="c366f-213">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c366f-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c366f-214">b.</span><span class="sxs-lookup"><span data-stu-id="c366f-214">b.</span></span> <span data-ttu-id="c366f-215">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c366f-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c366f-216">c.</span><span class="sxs-lookup"><span data-stu-id="c366f-216">c.</span></span> <span data-ttu-id="c366f-217">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c366f-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c366f-218">d.</span><span class="sxs-lookup"><span data-stu-id="c366f-218">d.</span></span> <span data-ttu-id="c366f-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c366f-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="c366f-220">Een testgebruiker LearnUpon maken</span><span class="sxs-lookup"><span data-stu-id="c366f-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="c366f-221">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in LearnUpon van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c366f-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="c366f-222">LearnUpon ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c366f-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c366f-223">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="c366f-223">There is no action item for you in this section.</span></span> <span data-ttu-id="c366f-224">Een nieuwe gebruiker wordt tijdens een poging tooaccess LearnUpon gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="c366f-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="c366f-225">[Configureren van Azure AD voor eenmalige aanmelding](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c366f-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="c366f-226">Als u een gebruiker toocreate handmatig nodig hebt, moet u toocontact [LearnUpon ondersteuningsteam](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="c366f-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c366f-227">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c366f-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c366f-228">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLearnUpon toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c366f-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c366f-230">**tooassign Britta Simon tooLearnUpon, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c366f-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="c366f-231">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c366f-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c366f-233">Selecteer in de lijst met de toepassingen van Hallo **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="c366f-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="c366f-235">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c366f-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c366f-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c366f-237">Click **Add** button.</span></span> <span data-ttu-id="c366f-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c366f-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c366f-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c366f-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c366f-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c366f-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c366f-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c366f-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c366f-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c366f-243">Testing single sign-on</span></span>

<span data-ttu-id="c366f-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c366f-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c366f-245">Als u op Hallo LearnUpon tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour LearnUpon toepassing.</span><span class="sxs-lookup"><span data-stu-id="c366f-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="c366f-246">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c366f-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c366f-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c366f-247">Additional resources</span></span>

* [<span data-ttu-id="c366f-248">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c366f-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c366f-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c366f-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

