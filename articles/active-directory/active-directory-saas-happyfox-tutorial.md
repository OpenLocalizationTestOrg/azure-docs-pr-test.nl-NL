---
title: 'Zelfstudie: Azure Active Directory-integratie met HappyFox | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en HappyFox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="c7bfc-103">Zelfstudie: Azure Active Directory-integratie met HappyFox</span><span class="sxs-lookup"><span data-stu-id="c7bfc-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="c7bfc-104">In deze zelfstudie leert u hoe toointegrate HappyFox met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7bfc-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7bfc-105">HappyFox integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c7bfc-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7bfc-106">U kunt beheren in Azure AD die tooHappyFox toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c7bfc-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="c7bfc-107">U kunt uw gebruikers tooautomatically get aangemelde tooHappyFox (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c7bfc-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7bfc-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c7bfc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7bfc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7bfc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7bfc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c7bfc-110">Prerequisites</span></span>

<span data-ttu-id="c7bfc-111">Azure AD-integratie met HappyFox tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c7bfc-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="c7bfc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c7bfc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7bfc-113">Een HappyFox eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c7bfc-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7bfc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7bfc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c7bfc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7bfc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7bfc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7bfc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7bfc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c7bfc-118">Scenario description</span></span>
<span data-ttu-id="c7bfc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7bfc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c7bfc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7bfc-121">Het toevoegen van HappyFox van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c7bfc-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="c7bfc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c7bfc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="c7bfc-123">Het toevoegen van HappyFox van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c7bfc-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="c7bfc-124">tooconfigure hello integratie van HappyFox in Azure AD, moet u tooadd HappyFox uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7bfc-125">**tooadd HappyFox via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c7bfc-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7bfc-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7bfc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7bfc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c7bfc-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c7bfc-133">Typ in het zoekvak Hallo **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-133">In hello search box, type **HappyFox**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="c7bfc-135">Selecteer in het deelvenster resultaten hello, **HappyFox**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7bfc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c7bfc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7bfc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met HappyFox op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c7bfc-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7bfc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in HappyFox is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="c7bfc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in HappyFox toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="c7bfc-141">Wijs in HappyFox, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7bfc-142">tooconfigure en eenmalige aanmelding Azure AD-test met HappyFox, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7bfc-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7bfc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7bfc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7bfc-145">**[Maken van een testgebruiker HappyFox](#creating-a-happyfox-test-user)**  -toohave een equivalent van Britta Simon in HappyFox die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7bfc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7bfc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7bfc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c7bfc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7bfc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing HappyFox configureren.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="c7bfc-150">**Azure AD tooconfigure eenmalige aanmelding met HappyFox, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c7bfc-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7bfc-151">In de Azure-portal op Hallo Hallo **HappyFox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c7bfc-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="c7bfc-155">Op Hallo **HappyFox domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7bfc-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="c7bfc-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-157">a.</span></span> <span data-ttu-id="c7bfc-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="c7bfc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="c7bfc-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-159">b.</span></span> <span data-ttu-id="c7bfc-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="c7bfc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7bfc-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-161">These values are not real.</span></span> <span data-ttu-id="c7bfc-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c7bfc-163">Neem contact op met [HappyFox Client ondersteuningsteam](https://support.happyfox.com/home) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="c7bfc-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="c7bfc-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7bfc-168">Op Hallo **HappyFox configuratie** sectie, klikt u op **configureren HappyFox** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c7bfc-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="c7bfc-171">Meld u aan op tooyour HappyFox personeel portal en te navigeren**beheren**, klikt u op **integraties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="c7bfc-173">Op het tabblad Hallo integraties **configureren** onder **SAML-integratie** tooopen Hallo eenmalige aanmelding op instellingen.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="c7bfc-175">Plakken binnen een configuratiesectie SAML Hallo **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal in **doel-URL voor eenmalige aanmelding** textbox.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="c7bfc-177">Open Hallo-certificaat gedownload vanuit Azure-portal in Kladblok en plak de inhoud ervan in **IdP handtekening** sectie.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="c7bfc-179">Klik op **instellingen opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-179">Click **Save Settings** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="c7bfc-181">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7bfc-182">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7bfc-183">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7bfc-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7bfc-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c7bfc-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7bfc-185">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c7bfc-187">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c7bfc-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7bfc-188">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7bfc-190">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7bfc-192">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7bfc-194">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7bfc-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7bfc-196">a.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-196">a.</span></span> <span data-ttu-id="c7bfc-197">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7bfc-198">b.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-198">b.</span></span> <span data-ttu-id="c7bfc-199">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7bfc-200">c.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-200">c.</span></span> <span data-ttu-id="c7bfc-201">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7bfc-202">d.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-202">d.</span></span> <span data-ttu-id="c7bfc-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="c7bfc-204">Een testgebruiker HappyFox maken</span><span class="sxs-lookup"><span data-stu-id="c7bfc-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="c7bfc-205">Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c7bfc-206">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7bfc-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c7bfc-207">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHappyFox toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c7bfc-209">**tooassign Britta Simon tooHappyFox, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c7bfc-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7bfc-210">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c7bfc-212">Selecteer in de lijst met de toepassingen van Hallo **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-212">In hello applications list, select **HappyFox**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="c7bfc-214">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c7bfc-216">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-216">Click **Add** button.</span></span> <span data-ttu-id="c7bfc-217">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c7bfc-219">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7bfc-220">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7bfc-221">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7bfc-222">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c7bfc-222">Testing single sign-on</span></span>

<span data-ttu-id="c7bfc-223">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="c7bfc-224">Als u op Hallo HappyFox tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van HappyFox toepassing.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="c7bfc-225">U ziet Hallo **'SAML'** knop op de aanmeldingspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="c7bfc-227">Klik op Hallo **'SAML'** knop toolog in tooHappyFox met behulp van uw Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="c7bfc-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="c7bfc-228">Zie voor meer informatie over Hallo Toegangspaneel [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7bfc-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c7bfc-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c7bfc-229">Additional resources</span></span>

* [<span data-ttu-id="c7bfc-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7bfc-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7bfc-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7bfc-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

