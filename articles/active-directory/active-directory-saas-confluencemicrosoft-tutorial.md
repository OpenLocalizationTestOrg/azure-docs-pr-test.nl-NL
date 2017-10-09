---
title: 'Zelfstudie: Azure Active Directory-integratie met samenloop SAML SSO door Microsoft | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en samenloop SAML SSO door Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="a422f-103">Zelfstudie: Azure Active Directory-integratie met samenloop SAML SSO door Microsoft</span><span class="sxs-lookup"><span data-stu-id="a422f-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="a422f-104">In deze zelfstudie leert u hoe toointegrate samenloop SAML SSO door Microsoft met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a422f-104">In this tutorial, you learn how toointegrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a422f-105">Samenloop SAML SSO door Microsoft integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a422f-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a422f-106">U kunt beheren in Azure AD wie toegang tot tooConfluence SAML SSO door Microsoft heeft</span><span class="sxs-lookup"><span data-stu-id="a422f-106">You can control in Azure AD who has access tooConfluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="a422f-107">U kunt uw gebruikers tooautomatically get aangemelde tooConfluence SAML SSO door Microsoft (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="a422f-107">You can enable your users tooautomatically get signed-on tooConfluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a422f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a422f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a422f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a422f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a422f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a422f-110">Prerequisites</span></span>

<span data-ttu-id="a422f-111">tooconfigure Azure AD-integratie met samenloop SAML SSO door Microsoft, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a422f-111">tooconfigure Azure AD integration with Confluence SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="a422f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a422f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a422f-113">Samenloop servertoepassing is geïnstalleerd op een Windows 64-bits-server (on-premises of cloud Hallo IaaS infrastructuur)</span><span class="sxs-lookup"><span data-stu-id="a422f-113">Confluence server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="a422f-114">Samenloop server is een HTTPS-functionaliteit</span><span class="sxs-lookup"><span data-stu-id="a422f-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="a422f-115">Opmerking Hallo ondersteund versies voor samenloop invoegtoepassing worden vermeld in onderstaande sectie.</span><span class="sxs-lookup"><span data-stu-id="a422f-115">Note hello supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="a422f-116">Samenloop server bereikbaar is op internet is met name tooAzure AD aanmelding pagina voor verificatie en moet kunnen tooreceive Hallo-token van Azure AD</span><span class="sxs-lookup"><span data-stu-id="a422f-116">Confluence server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="a422f-117">Beheerdersreferenties worden ingesteld in samenloop</span><span class="sxs-lookup"><span data-stu-id="a422f-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="a422f-118">WebSudo is uitgeschakeld in samenloop</span><span class="sxs-lookup"><span data-stu-id="a422f-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="a422f-119">Testgebruiker gemaakt in Hallo samenloop servertoepassing</span><span class="sxs-lookup"><span data-stu-id="a422f-119">Test user created in hello Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="a422f-120">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving van samenloop.</span><span class="sxs-lookup"><span data-stu-id="a422f-120">tootest hello steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="a422f-121">Hallo-integratie eerst testen in ontwikkeling of staging-omgeving van toepassing hello en vervolgens gebruik Hallo productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="a422f-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="a422f-122">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a422f-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a422f-123">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a422f-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a422f-124">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a422f-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="a422f-125">Ondersteunde versies van samenloop</span><span class="sxs-lookup"><span data-stu-id="a422f-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="a422f-126">Vanaf nu de volgende versies van samenloop worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="a422f-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="a422f-127">Samenloop: 5.0 too5.10</span><span class="sxs-lookup"><span data-stu-id="a422f-127">Confluence: 5.0 too5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a422f-128">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a422f-128">Scenario description</span></span>
<span data-ttu-id="a422f-129">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a422f-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a422f-130">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a422f-130">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a422f-131">Het toevoegen van samenloop SAML SSO door Microsoft van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a422f-131">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="a422f-132">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a422f-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="a422f-133">Het toevoegen van samenloop SAML SSO door Microsoft van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a422f-133">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="a422f-134">tooconfigure hello integratie van samenloop SAML SSO door Microsoft in Azure AD, moet u tooadd samenloop SAML SSO door Microsoft in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a422f-134">tooconfigure hello integration of Confluence SAML SSO by Microsoft into Azure AD, you need tooadd Confluence SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a422f-135">**tooadd samenloop SAML SSO door Microsoft via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a422f-135">**tooadd Confluence SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a422f-136">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a422f-136">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a422f-138">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a422f-138">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a422f-139">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a422f-139">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a422f-141">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a422f-141">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a422f-143">Typ in het zoekvak Hallo **samenloop SAML SSO door Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a422f-143">In hello search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="a422f-145">Selecteer in het deelvenster resultaten hello, **samenloop SAML SSO door Microsoft**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a422f-145">In hello results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a422f-147">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a422f-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a422f-148">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met samenloop SAML SSO door Microsoft op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a422f-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a422f-149">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in samenloop SAML SSO door Microsoft is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a422f-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Confluence SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="a422f-150">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in samenloop SAML SSO door Microsoft toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a422f-150">In other words, a link relationship between an Azure AD user and hello related user in Confluence SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="a422f-151">In samenloop SAML SSO door Microsoft, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a422f-151">In Confluence SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a422f-152">tooconfigure en eenmalige aanmelding Azure AD-test met samenloop SAML SSO door Microsoft, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a422f-152">tooconfigure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a422f-153">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a422f-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a422f-154">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a422f-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a422f-155">**[Maken van een SSO samenloop SAML door Microsoft testgebruiker](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave een equivalent van Britta Simon in samenloop SAML SSO door Microsoft die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a422f-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a422f-156">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a422f-156">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a422f-157">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a422f-157">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a422f-158">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a422f-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a422f-159">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw samenloop SAML eenmalige aanmelding configureren door toepassing van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a422f-159">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="a422f-160">**tooconfigure eenmalige aanmelding Azure AD met samenloop SAML SSO door Microsoft, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a422f-160">**tooconfigure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="a422f-161">In de Azure-portal op Hallo Hallo **samenloop SAML SSO door Microsoft** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a422f-161">In hello Azure portal, on hello **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a422f-163">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a422f-163">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="a422f-165">Op Hallo **samenloop SAML SSO door Microsoft-Domain en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a422f-165">On hello **Confluence SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="a422f-167">a.</span><span class="sxs-lookup"><span data-stu-id="a422f-167">a.</span></span> <span data-ttu-id="a422f-168">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="a422f-168">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="a422f-169">b.</span><span class="sxs-lookup"><span data-stu-id="a422f-169">b.</span></span> <span data-ttu-id="a422f-170">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="a422f-170">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="a422f-171">c.</span><span class="sxs-lookup"><span data-stu-id="a422f-171">c.</span></span> <span data-ttu-id="a422f-172">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="a422f-172">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a422f-173">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a422f-173">These values are not real.</span></span> <span data-ttu-id="a422f-174">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="a422f-174">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a422f-175">Poort is optioneel, mocht dat een benoemde URL.</span><span class="sxs-lookup"><span data-stu-id="a422f-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="a422f-176">Deze waarden worden ontvangen tijdens de configuratie van Hallo van samenloop-invoegtoepassing wordt verderop in de zelfstudie Hallo besproken.</span><span class="sxs-lookup"><span data-stu-id="a422f-176">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>
 

4. <span data-ttu-id="a422f-177">Hallo toogenerate **metagegevens** -url, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a422f-177">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="a422f-178">a.</span><span class="sxs-lookup"><span data-stu-id="a422f-178">a.</span></span> <span data-ttu-id="a422f-179">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="a422f-179">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="a422f-181">b.</span><span class="sxs-lookup"><span data-stu-id="a422f-181">b.</span></span> <span data-ttu-id="a422f-182">Klik op **eindpunten** tooopen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a422f-182">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="a422f-184">c.</span><span class="sxs-lookup"><span data-stu-id="a422f-184">c.</span></span> <span data-ttu-id="a422f-185">Klik op Hallo kopie knop toocopy **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="a422f-185">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="a422f-187">d.</span><span class="sxs-lookup"><span data-stu-id="a422f-187">d.</span></span> <span data-ttu-id="a422f-188">Ga nu toohello eigenschappenpagina van **samenloop SAML SSO door Microsoft** en kopiëren Hallo **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="a422f-188">Now go toohello property page of **Confluence SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="a422f-190">e.</span><span class="sxs-lookup"><span data-stu-id="a422f-190">e.</span></span> <span data-ttu-id="a422f-191">Hallo genereren **metagegevens-URL** met Hallo patroon volgen: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` en kopieer deze waarde in Kladblok, zoals het later voor de configuratie van Hallo van Hallo-invoegtoepassing gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="a422f-191">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="a422f-192">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a422f-192">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a422f-194">Neem contact op met [Microsoft](mailto:waadpartners@microsoft.com) met de volgende informatie voor Hallo samenloop invoegtoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="a422f-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello Confluence plugin.</span></span>
    
    *   <span data-ttu-id="a422f-195">Naam van de klant:</span><span class="sxs-lookup"><span data-stu-id="a422f-195">Customer Name:</span></span>
    *   <span data-ttu-id="a422f-196">De naam van de primaire domeincontroller:</span><span class="sxs-lookup"><span data-stu-id="a422f-196">Primary domain name:</span></span>
    *   <span data-ttu-id="a422f-197">Azure AD Premium: Ja/Nee (invoegtoepassing zijn beschikbaar tooall Hallo klant vrije-, Basic- en Premium-SKU gebruikt)</span><span class="sxs-lookup"><span data-stu-id="a422f-197">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="a422f-198">Het aantal gebruikers met behulp van deze integratie:</span><span class="sxs-lookup"><span data-stu-id="a422f-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="a422f-199">Samenloop versie:</span><span class="sxs-lookup"><span data-stu-id="a422f-199">Confluence Version:</span></span>
    *   <span data-ttu-id="a422f-200">Opmerkingen:</span><span class="sxs-lookup"><span data-stu-id="a422f-200">Comments:</span></span>

7. <span data-ttu-id="a422f-201">Meld u in een ander browservenster in tooyour samenloop exemplaar als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a422f-201">In a different web browser window, log in tooyour Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="a422f-202">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a422f-202">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="a422f-204">Klik onder sectie tabblad invoegtoepassingen op **invoegtoepassingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="a422f-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="a422f-206">Handmatig uploaden Hallo invoegtoepassing geleverd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a422f-206">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="a422f-207">Zodra het Hallo-invoegtoepassing is geïnstalleerd, wordt deze weergegeven **gebruiker geïnstalleerd** invoegtoepassingen sectie van **beheren invoegtoepassing** sectie.</span><span class="sxs-lookup"><span data-stu-id="a422f-207">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="a422f-208">Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="a422f-208">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="a422f-209">Voer de volgende stappen uit op de configuratiepagina:</span><span class="sxs-lookup"><span data-stu-id="a422f-209">Perform following steps on configuration page:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="a422f-211">a.</span><span class="sxs-lookup"><span data-stu-id="a422f-211">a.</span></span> <span data-ttu-id="a422f-212">In **metagegevens-URL** Hallo plakken **metagegevens-URL** gegenereerd op basis van Azure AD en klikt u op Hallo **oplossen** knop.</span><span class="sxs-lookup"><span data-stu-id="a422f-212">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="a422f-213">Hallo IdP metagegevens-URL worden gelezen en alle informatie van Hallo velden gevuld.</span><span class="sxs-lookup"><span data-stu-id="a422f-213">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="a422f-214">Gebruikers-ID van SAML-standaardlocatie is naam-id.</span><span class="sxs-lookup"><span data-stu-id="a422f-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="a422f-215">U kunt deze optie tooan-kenmerk wijzigen en Hallo relevante kenmerknaam invoeren.</span><span class="sxs-lookup"><span data-stu-id="a422f-215">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="a422f-216">Zorg ervoor dat er slechts één certificaat toegewezen tegen Hallo app zodat er geen fout is bij het oplossen van Hallo metagegevens.</span><span class="sxs-lookup"><span data-stu-id="a422f-216">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="a422f-217">Als er meerdere certificaten, bij het omzetten van metagegevens hello, haalt de beheerder een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="a422f-217">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="a422f-218">b.</span><span class="sxs-lookup"><span data-stu-id="a422f-218">b.</span></span> <span data-ttu-id="a422f-219">Kopiëren Hallo **id, de antwoord-URL en de URL met eenmalige** waarden en plak ze in **id, de antwoord-URL en de URL met eenmalige** respectievelijk in tekstvakken **samenloop SAML SSO door Microsoft-Domain en URL's**  sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a422f-219">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="a422f-220">c.</span><span class="sxs-lookup"><span data-stu-id="a422f-220">c.</span></span> <span data-ttu-id="a422f-221">In **aanmeldingsnaam van de knop** Hallo-typenaam van knop voor uw organisatie wil dat Hallo gebruikers toosee op het aanmeldingsscherm.</span><span class="sxs-lookup"><span data-stu-id="a422f-221">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="a422f-222">d.</span><span class="sxs-lookup"><span data-stu-id="a422f-222">d.</span></span> <span data-ttu-id="a422f-223">In **SAML-ID gebruikerslocaties** Selecteer **gebruikersnaam wordt Hallo NameIdentifier element Hallo onderwerp instructie** of **gebruikers-ID is in een kenmerkelement**.</span><span class="sxs-lookup"><span data-stu-id="a422f-223">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="a422f-224">Deze ID heeft toobe Hallo samenloop gebruikers-id. Als het Hallo-gebruikersnaam niet overeenkomt, kan vervolgens niet worden gebruikers toolog in.</span><span class="sxs-lookup"><span data-stu-id="a422f-224">This ID has toobe hello Confluence user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="a422f-225">e.</span><span class="sxs-lookup"><span data-stu-id="a422f-225">e.</span></span> <span data-ttu-id="a422f-226">Als u selecteert **gebruikers-ID is in een kenmerkelement** optie, klik dan in **kenmerknaam** textbox typenaam Hallo van Hallo kenmerk waar gebruikers-Id wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="a422f-226">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="a422f-227">f.</span><span class="sxs-lookup"><span data-stu-id="a422f-227">f.</span></span> <span data-ttu-id="a422f-228">Als u federatieve domein hello (zoals ADFS enz.) met Azure AD gebruikt, klikt u op Hallo **inschakelen Thuisrealmdetectie** optie en configureer Hallo **domeinnaam**.</span><span class="sxs-lookup"><span data-stu-id="a422f-228">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="a422f-229">g.</span><span class="sxs-lookup"><span data-stu-id="a422f-229">g.</span></span> <span data-ttu-id="a422f-230">In **domeinnaam** type Hallo domeinnaam hier in geval van een Hallo op basis van AD FS-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a422f-230">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="a422f-231">h.</span><span class="sxs-lookup"><span data-stu-id="a422f-231">h.</span></span> <span data-ttu-id="a422f-232">Controleer **eenmalige aanmelding inschakelen uit** desgewenst toolog uit vanuit Azure AD wanneer een gebruiker zich afmeldt van samenloop.</span><span class="sxs-lookup"><span data-stu-id="a422f-232">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="a422f-233">ik.</span><span class="sxs-lookup"><span data-stu-id="a422f-233">i.</span></span> <span data-ttu-id="a422f-234">Klik op **opslaan** knop toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="a422f-234">Click **Save** button toosave hello settings.</span></span>


> [!TIP]
> <span data-ttu-id="a422f-235">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a422f-235">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a422f-236">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a422f-236">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a422f-237">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a422f-237">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a422f-238">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a422f-238">Creating an Azure AD test user</span></span>
<span data-ttu-id="a422f-239">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a422f-239">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a422f-241">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a422f-241">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a422f-242">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a422f-242">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a422f-244">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a422f-244">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a422f-246">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a422f-246">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a422f-248">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a422f-248">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a422f-250">a.</span><span class="sxs-lookup"><span data-stu-id="a422f-250">a.</span></span> <span data-ttu-id="a422f-251">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a422f-251">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a422f-252">b.</span><span class="sxs-lookup"><span data-stu-id="a422f-252">b.</span></span> <span data-ttu-id="a422f-253">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a422f-253">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a422f-254">c.</span><span class="sxs-lookup"><span data-stu-id="a422f-254">c.</span></span> <span data-ttu-id="a422f-255">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a422f-255">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a422f-256">d.</span><span class="sxs-lookup"><span data-stu-id="a422f-256">d.</span></span> <span data-ttu-id="a422f-257">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a422f-257">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="a422f-258">Maken van een SSO samenloop SAML door Microsoft testgebruiker</span><span class="sxs-lookup"><span data-stu-id="a422f-258">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="a422f-259">Azure AD tooenable gebruikers toolog in tooConfluence op de lokale server ze moeten worden ingericht in samenloop SAML SSO door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a422f-259">tooenable Azure AD users toolog in tooConfluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="a422f-260">Voor samenloop SAML SSO door Microsoft is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a422f-260">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="a422f-261">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a422f-261">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a422f-262">Tooyour samenloop op de lokale server aanmelden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a422f-262">Log in tooyour Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="a422f-263">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="a422f-263">Hover on cog and click hello **User management**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="a422f-265">Klik onder de sectie gebruikers op **gebruikers toevoegen** tabblad. Op Hallo **'Gebruiker toevoegen'** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a422f-265">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="a422f-267">a.</span><span class="sxs-lookup"><span data-stu-id="a422f-267">a.</span></span> <span data-ttu-id="a422f-268">In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker zoals Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a422f-268">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="a422f-269">b.</span><span class="sxs-lookup"><span data-stu-id="a422f-269">b.</span></span> <span data-ttu-id="a422f-270">In Hallo **volledige naam** textbox type Hallo volledige naam van gebruiker zoals Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a422f-270">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="a422f-271">c.</span><span class="sxs-lookup"><span data-stu-id="a422f-271">c.</span></span> <span data-ttu-id="a422f-272">In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a422f-272">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="a422f-273">d.</span><span class="sxs-lookup"><span data-stu-id="a422f-273">d.</span></span> <span data-ttu-id="a422f-274">In Hallo **wachtwoord** textbox Hallo een wachtwoord op voor Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a422f-274">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="a422f-275">e.</span><span class="sxs-lookup"><span data-stu-id="a422f-275">e.</span></span> <span data-ttu-id="a422f-276">Klik op **wachtwoord bevestigen** Hallo wachtwoord opnieuw invoeren.</span><span class="sxs-lookup"><span data-stu-id="a422f-276">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="a422f-277">f.</span><span class="sxs-lookup"><span data-stu-id="a422f-277">f.</span></span> <span data-ttu-id="a422f-278">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a422f-278">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a422f-279">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a422f-279">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a422f-280">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooConfluence SAML SSO door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a422f-280">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConfluence SAML SSO by Microsoft.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a422f-282">**tooassign Britta Simon tooConfluence SAML SSO door Microsoft, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a422f-282">**tooassign Britta Simon tooConfluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="a422f-283">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a422f-283">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a422f-285">Selecteer in de lijst met de toepassingen van Hallo **samenloop SAML SSO door Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a422f-285">In hello applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="a422f-287">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a422f-287">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a422f-289">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a422f-289">Click **Add** button.</span></span> <span data-ttu-id="a422f-290">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a422f-290">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a422f-292">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a422f-292">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a422f-293">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a422f-293">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a422f-294">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a422f-294">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a422f-295">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a422f-295">Testing single sign-on</span></span>

<span data-ttu-id="a422f-296">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a422f-296">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a422f-297">Als u op Hallo samenloop SAML SSO door Microsoft-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour samenloop SAML SSO door toepassing van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a422f-297">When you click hello Confluence SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="a422f-298">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a422f-298">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a422f-299">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a422f-299">Additional resources</span></span>

* [<span data-ttu-id="a422f-300">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a422f-300">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a422f-301">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a422f-301">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

