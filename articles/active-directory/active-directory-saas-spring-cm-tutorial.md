---
title: 'Zelfstudie: Azure Active Directory-integratie met SpringCM | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SpringCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="624dc-103">Zelfstudie: Azure Active Directory-integratie met SpringCM</span><span class="sxs-lookup"><span data-stu-id="624dc-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="624dc-104">In deze zelfstudie leert u hoe toointegrate SpringCM met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="624dc-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="624dc-105">SpringCM integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="624dc-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="624dc-106">U kunt beheren in Azure AD die tooSpringCM toegang heeft</span><span class="sxs-lookup"><span data-stu-id="624dc-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="624dc-107">U kunt uw gebruikers tooautomatically get aangemelde tooSpringCM (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="624dc-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="624dc-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="624dc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="624dc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="624dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="624dc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="624dc-110">Prerequisites</span></span>

<span data-ttu-id="624dc-111">Azure AD-integratie met SpringCM tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="624dc-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="624dc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="624dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="624dc-113">Een SpringCM eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="624dc-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="624dc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="624dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="624dc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="624dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="624dc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="624dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="624dc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="624dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="624dc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="624dc-118">Scenario description</span></span>
<span data-ttu-id="624dc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="624dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="624dc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="624dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="624dc-121">Het toevoegen van SpringCM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="624dc-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="624dc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="624dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="624dc-123">Het toevoegen van SpringCM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="624dc-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="624dc-124">tooconfigure hello integratie van SpringCM in Azure AD, moet u tooadd SpringCM uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="624dc-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="624dc-125">**tooadd SpringCM via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="624dc-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="624dc-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="624dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="624dc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="624dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="624dc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="624dc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="624dc-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="624dc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="624dc-133">Typ in het zoekvak Hallo **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="624dc-133">In hello search box, type **SpringCM**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="624dc-135">Selecteer in het deelvenster resultaten hello, **SpringCM**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="624dc-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="624dc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="624dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="624dc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SpringCM op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="624dc-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="624dc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SpringCM is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="624dc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="624dc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SpringCM toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="624dc-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="624dc-141">Wijs in SpringCM, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="624dc-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="624dc-142">tooconfigure en eenmalige aanmelding Azure AD-test met SpringCM, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="624dc-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="624dc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="624dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="624dc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="624dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="624dc-145">**[Maken van een testgebruiker SpringCM](#creating-a-springcm-test-user)**  -toohave een equivalent van Britta Simon in SpringCM die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="624dc-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="624dc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="624dc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="624dc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="624dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="624dc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="624dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="624dc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing SpringCM configureren.</span><span class="sxs-lookup"><span data-stu-id="624dc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="624dc-150">**Azure AD tooconfigure eenmalige aanmelding met SpringCM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="624dc-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="624dc-151">In de Azure-portal op Hallo Hallo **SpringCM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="624dc-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="624dc-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="624dc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="624dc-155">Op Hallo **SpringCM domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="624dc-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="624dc-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="624dc-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="624dc-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="624dc-158">This value is not real.</span></span> <span data-ttu-id="624dc-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="624dc-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="624dc-160">Neem contact op met [SpringCM Client ondersteuningsteam](https://knowledge.springcm.com/support) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="624dc-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="624dc-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="624dc-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="624dc-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="624dc-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="624dc-165">Op Hallo **SpringCM configuratie** sectie, klikt u op **configureren SpringCM** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="624dc-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="624dc-166">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="624dc-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="624dc-168">Een ander browservenster, meld u aan bij tooyour **SpringCM** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="624dc-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="624dc-169">Klik in het menu bovenaan Hallo Hallo **Ga naar**, klikt u op **voorkeuren**, en klikt u op Hallo **accountvoorkeuren** sectie, klikt u op **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="624dc-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="624dc-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML EENMALIGE AANMELDING")</span><span class="sxs-lookup"><span data-stu-id="624dc-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="624dc-171">Uitvoeren in Hallo identiteit Provider-configuratiesectie, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="624dc-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="624dc-172">![Configuratie van de Provider identiteit](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "providerconfiguratie identiteit")</span><span class="sxs-lookup"><span data-stu-id="624dc-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="624dc-173">a.</span><span class="sxs-lookup"><span data-stu-id="624dc-173">a.</span></span> <span data-ttu-id="624dc-174">tooupload uw gedownloade certificaat van de Azure Active Directory, klikt u op **uitgeverscertificaat selecteren** of **wijziging uitgeverscertificaat**.</span><span class="sxs-lookup"><span data-stu-id="624dc-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="624dc-175">b.</span><span class="sxs-lookup"><span data-stu-id="624dc-175">b.</span></span> <span data-ttu-id="624dc-176">Plakken **SAML entiteit-ID** waarde, die u hebt gekopieerd vanuit Azure-portal in Hallo **verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="624dc-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="624dc-177">c.</span><span class="sxs-lookup"><span data-stu-id="624dc-177">c.</span></span> <span data-ttu-id="624dc-178">Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **Service Provider (SP) geïnitieerd eindpunt** textbox.</span><span class="sxs-lookup"><span data-stu-id="624dc-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="624dc-179">d.</span><span class="sxs-lookup"><span data-stu-id="624dc-179">d.</span></span> <span data-ttu-id="624dc-180">Selecteer **SAML ingeschakeld** als **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="624dc-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="624dc-181">e.</span><span class="sxs-lookup"><span data-stu-id="624dc-181">e.</span></span> <span data-ttu-id="624dc-182">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="624dc-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="624dc-183">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="624dc-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="624dc-184">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="624dc-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="624dc-185">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="624dc-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="624dc-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="624dc-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="624dc-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="624dc-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="624dc-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="624dc-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="624dc-190">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="624dc-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="624dc-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="624dc-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="624dc-194">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="624dc-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="624dc-196">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="624dc-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="624dc-198">a.</span><span class="sxs-lookup"><span data-stu-id="624dc-198">a.</span></span> <span data-ttu-id="624dc-199">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="624dc-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="624dc-200">b.</span><span class="sxs-lookup"><span data-stu-id="624dc-200">b.</span></span> <span data-ttu-id="624dc-201">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="624dc-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="624dc-202">c.</span><span class="sxs-lookup"><span data-stu-id="624dc-202">c.</span></span> <span data-ttu-id="624dc-203">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="624dc-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="624dc-204">d.</span><span class="sxs-lookup"><span data-stu-id="624dc-204">d.</span></span> <span data-ttu-id="624dc-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="624dc-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="624dc-206">Een testgebruiker SpringCM maken</span><span class="sxs-lookup"><span data-stu-id="624dc-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="624dc-207">tooenable Azure Active Directory-gebruikers toolog in tooSpringCM, ze in SpringCM moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="624dc-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="624dc-208">In geval van SpringCM Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="624dc-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="624dc-209">Zie voor meer informatie [maken en bewerken van een gebruiker SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="624dc-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="624dc-210">**een gebruiker account-tooSpringCM tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="624dc-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="624dc-211">Meld u bij tooyour **SpringCM** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="624dc-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="624dc-212">Klik op **GOTO**, en klik vervolgens op **ADRESBOEK**.</span><span class="sxs-lookup"><span data-stu-id="624dc-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="624dc-213">![Gebruiker maken](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="624dc-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="624dc-214">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="624dc-214">Click **Create User**.</span></span>

4. <span data-ttu-id="624dc-215">Selecteer een **gebruikersrol**.</span><span class="sxs-lookup"><span data-stu-id="624dc-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="624dc-216">Selecteer **activering E-mail verzenden**.</span><span class="sxs-lookup"><span data-stu-id="624dc-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="624dc-217">Type Hallo voornaam en achternaam e-mailadres van een geldige Azure Active Directory-gebruikersaccount gewenste tooprovision in Hallo gerelateerd tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="624dc-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="624dc-218">Toevoegen van Hallo gebruiker tooa **beveiligingsgroep**.</span><span class="sxs-lookup"><span data-stu-id="624dc-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="624dc-219">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="624dc-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="624dc-220">U kunt andere SpringCM gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door SpringCM tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="624dc-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="624dc-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="624dc-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="624dc-222">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSpringCM toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="624dc-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="624dc-224">**tooassign Britta Simon tooSpringCM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="624dc-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="624dc-225">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="624dc-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="624dc-227">Selecteer in de lijst met de toepassingen van Hallo **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="624dc-227">In hello applications list, select **SpringCM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="624dc-229">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="624dc-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="624dc-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="624dc-231">Click **Add** button.</span></span> <span data-ttu-id="624dc-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="624dc-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="624dc-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="624dc-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="624dc-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="624dc-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="624dc-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="624dc-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="624dc-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="624dc-237">Testing single sign-on</span></span>

<span data-ttu-id="624dc-238">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="624dc-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="624dc-239">Als u op Hallo SpringCM tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SpringCM toepassing.</span><span class="sxs-lookup"><span data-stu-id="624dc-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="624dc-240">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="624dc-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="624dc-241">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="624dc-241">Additional resources</span></span>

* [<span data-ttu-id="624dc-242">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="624dc-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="624dc-243">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="624dc-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

