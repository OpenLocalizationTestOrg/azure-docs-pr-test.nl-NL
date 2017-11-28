---
title: 'Zelfstudie: Azure Active Directory-integratie met Tango Analytics | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Tango Analytics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 2076397e746235692f07241650d5556afb3c3d28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="62dcb-103">Zelfstudie: Azure Active Directory-integratie met Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="62dcb-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="62dcb-104">In deze zelfstudie leert u hoe toointegrate Tango Analytics met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62dcb-104">In this tutorial, you learn how toointegrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62dcb-105">Tango Analytics integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="62dcb-105">Integrating Tango Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62dcb-106">U kunt beheren in Azure AD wie toegang tot tooTango Analytics heeft</span><span class="sxs-lookup"><span data-stu-id="62dcb-106">You can control in Azure AD who has access tooTango Analytics</span></span>
- <span data-ttu-id="62dcb-107">U kunt uw gebruikers tooautomatically get aangemelde tooTango Analytics (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="62dcb-107">You can enable your users tooautomatically get signed-on tooTango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62dcb-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="62dcb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="62dcb-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62dcb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62dcb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="62dcb-110">Prerequisites</span></span>

<span data-ttu-id="62dcb-111">Azure AD-integratie met Tango Analytics tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="62dcb-111">tooconfigure Azure AD integration with Tango Analytics, you need hello following items:</span></span>

- <span data-ttu-id="62dcb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="62dcb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62dcb-113">Een Tango Analytics eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="62dcb-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62dcb-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="62dcb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62dcb-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="62dcb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62dcb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="62dcb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62dcb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62dcb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62dcb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="62dcb-118">Scenario description</span></span>
<span data-ttu-id="62dcb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="62dcb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62dcb-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="62dcb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62dcb-121">Het toevoegen van Tango Analytics van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="62dcb-121">Adding Tango Analytics from hello gallery</span></span>
2. <span data-ttu-id="62dcb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="62dcb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-hello-gallery"></a><span data-ttu-id="62dcb-123">Het toevoegen van Tango Analytics van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="62dcb-123">Adding Tango Analytics from hello gallery</span></span>
<span data-ttu-id="62dcb-124">tooconfigure hello integratie van Tango Analytics met Azure AD, moet u tooadd Tango Analytics uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="62dcb-124">tooconfigure hello integration of Tango Analytics into Azure AD, you need tooadd Tango Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62dcb-125">**tooadd Tango Analytics via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62dcb-125">**tooadd Tango Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62dcb-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="62dcb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62dcb-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="62dcb-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="62dcb-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62dcb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="62dcb-133">Typ in het zoekvak Hallo **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-133">In hello search box, type **Tango Analytics**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

5. <span data-ttu-id="62dcb-135">Selecteer in het deelvenster resultaten hello, **Tango Analytics**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="62dcb-135">In hello results panel, select **Tango Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62dcb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="62dcb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62dcb-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tango Analytics op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="62dcb-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62dcb-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Tango Analytics is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62dcb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tango Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="62dcb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Tango Analytics toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="62dcb-140">In other words, a link relationship between an Azure AD user and hello related user in Tango Analytics needs toobe established.</span></span>

<span data-ttu-id="62dcb-141">Wijs in Tango Analytics, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als Hallo-waarde van Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="62dcb-141">In Tango Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="62dcb-142">tooconfigure en test eenmalige aanmelding Azure AD met Tango Analytics, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="62dcb-142">tooconfigure and test Azure AD single sign-on with Tango Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62dcb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="62dcb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62dcb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62dcb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62dcb-145">**[Maken van een testgebruiker Tango Analytics](#creating-a-tango-analytics-test-user)**  -toohave een equivalent van Britta Simon in Tango analyses die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="62dcb-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - toohave a counterpart of Britta Simon in Tango Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="62dcb-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="62dcb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62dcb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="62dcb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62dcb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="62dcb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62dcb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="62dcb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="62dcb-150">**Azure AD tooconfigure eenmalige aanmelding met Tango Analytics, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62dcb-150">**tooconfigure Azure AD single sign-on with Tango Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="62dcb-151">In de Azure-portal op Hallo Hallo **Tango Analytics** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-151">In hello Azure portal, on hello **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="62dcb-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="62dcb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

3. <span data-ttu-id="62dcb-155">Op Hallo **Tango Analytics domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="62dcb-155">On hello **Tango Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="62dcb-157">a.</span><span class="sxs-lookup"><span data-stu-id="62dcb-157">a.</span></span> <span data-ttu-id="62dcb-158">In Hallo **id** textbox Hallo typewaarde`TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="62dcb-158">In hello **Identifier** textbox, type hello value `TACORE_SSO`</span></span>

    <span data-ttu-id="62dcb-159">b.</span><span class="sxs-lookup"><span data-stu-id="62dcb-159">b.</span></span> <span data-ttu-id="62dcb-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="62dcb-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62dcb-161">Hallo antwoord-URL-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="62dcb-161">hello Reply URL value is not real.</span></span> <span data-ttu-id="62dcb-162">Dit bijwerken met Hallo werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="62dcb-162">Update this with hello actual Reply URL.</span></span> <span data-ttu-id="62dcb-163">Neem contact op met [Tango Analytics ondersteuningsteam](mailto:support@tangoanalytics.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="62dcb-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) tooget this value.</span></span>

4. <span data-ttu-id="62dcb-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="62dcb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

5. <span data-ttu-id="62dcb-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="62dcb-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62dcb-168">tooconfigure eenmalige aanmelding op **Tango Analytics** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Tango Analytics ondersteuningsteam](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="62dcb-168">tooconfigure single sign-on on **Tango Analytics** side, you need toosend hello downloaded **Metadata XML** too[Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="62dcb-169">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="62dcb-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="62dcb-170">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="62dcb-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="62dcb-171">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="62dcb-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="62dcb-172">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62dcb-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62dcb-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="62dcb-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="62dcb-174">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="62dcb-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="62dcb-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62dcb-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62dcb-177">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="62dcb-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62dcb-179">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62dcb-181">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="62dcb-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62dcb-183">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="62dcb-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62dcb-185">a.</span><span class="sxs-lookup"><span data-stu-id="62dcb-185">a.</span></span> <span data-ttu-id="62dcb-186">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62dcb-187">b.</span><span class="sxs-lookup"><span data-stu-id="62dcb-187">b.</span></span> <span data-ttu-id="62dcb-188">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62dcb-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62dcb-189">c.</span><span class="sxs-lookup"><span data-stu-id="62dcb-189">c.</span></span> <span data-ttu-id="62dcb-190">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="62dcb-191">d.</span><span class="sxs-lookup"><span data-stu-id="62dcb-191">d.</span></span> <span data-ttu-id="62dcb-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="62dcb-193">Maken van een testgebruiker Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="62dcb-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="62dcb-194">In deze sectie maakt maakt u een gebruiker die Britta Simon aangeroepen in Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="62dcb-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="62dcb-195">Werken met [Tango Analytics ondersteuningsteam](mailto:support@tangoanalytics.com) Hallo gebruikers toevoegen in Hallo Tango Analytics platform.</span><span class="sxs-lookup"><span data-stu-id="62dcb-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add hello users in hello Tango Analytics platform.</span></span> <span data-ttu-id="62dcb-196">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="62dcb-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62dcb-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="62dcb-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62dcb-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTango Analytics.</span><span class="sxs-lookup"><span data-stu-id="62dcb-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTango Analytics.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="62dcb-200">**tooassign Britta Simon tooTango Analytics, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62dcb-200">**tooassign Britta Simon tooTango Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="62dcb-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="62dcb-203">Selecteer in de lijst met de toepassingen van Hallo **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-203">In hello applications list, select **Tango Analytics**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

3. <span data-ttu-id="62dcb-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="62dcb-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="62dcb-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="62dcb-207">Click **Add** button.</span></span> <span data-ttu-id="62dcb-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62dcb-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="62dcb-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="62dcb-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="62dcb-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62dcb-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62dcb-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62dcb-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62dcb-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="62dcb-213">Testing single sign-on</span></span>

<span data-ttu-id="62dcb-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="62dcb-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="62dcb-215">Als u op Hallo Tango Analytics-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Tango Analytics-toepassing.</span><span class="sxs-lookup"><span data-stu-id="62dcb-215">When you click hello Tango Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Tango Analytics application.</span></span>
<span data-ttu-id="62dcb-216">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62dcb-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62dcb-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="62dcb-217">Additional resources</span></span>

* [<span data-ttu-id="62dcb-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62dcb-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62dcb-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62dcb-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_203.png

