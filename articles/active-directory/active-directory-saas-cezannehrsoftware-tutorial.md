---
title: 'Zelfstudie: Azure Active Directory-integratie met Cezanne HR software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Cezanne HR-software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="32523-103">Zelfstudie: Azure Active Directory integreren met Cezanne HR-software</span><span class="sxs-lookup"><span data-stu-id="32523-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="32523-104">In deze zelfstudie leert u hoe toointegrate Cezanne HR-software met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32523-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32523-105">Cezanne HR software integreren met Azure AD biedt u Hallo volgende voordelen.</span><span class="sxs-lookup"><span data-stu-id="32523-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="32523-106">U kunt:</span><span class="sxs-lookup"><span data-stu-id="32523-106">You can:</span></span>

- <span data-ttu-id="32523-107">Beheren in Azure AD die toegang tooCezanne heeft HR-software.</span><span class="sxs-lookup"><span data-stu-id="32523-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="32523-108">Schakel uw gebruikers tooautomatically aanmelding tooCezanne HR-software met eenmalige aanmelding (SSO) met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="32523-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="32523-109">Uw accounts beheren via één centrale locatie: hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="32523-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="32523-110">Zie toolearn meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en SSO met Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32523-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32523-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="32523-111">Prerequisites</span></span>

<span data-ttu-id="32523-112">tooconfigure Azure AD-integratie met Cezanne HR-software, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="32523-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="32523-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="32523-113">An Azure AD subscription</span></span>
- <span data-ttu-id="32523-114">Een Cezanne HR software abonnement SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="32523-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32523-115">tootest hello stappen in deze zelfstudie, het is raadzaam dat u niet een productieomgeving gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32523-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="32523-116">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="32523-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="32523-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="32523-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32523-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32523-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32523-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="32523-119">Scenario description</span></span>
<span data-ttu-id="32523-120">In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="32523-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="32523-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="32523-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="32523-122">Het toevoegen van Cezanne HR-software van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="32523-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="32523-123">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="32523-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="32523-124">Cezanne HR software uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="32523-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="32523-125">tooconfigure hello integratie van Cezanne HR-software in Azure AD Cezanne HR software uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="32523-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32523-126">tooadd Cezanne HR software uit de galerie hello, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="32523-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="32523-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="32523-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![Hallo 'Azure Active Directory' knop][1]

2. <span data-ttu-id="32523-129">Selecteer **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="32523-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Hallo 'Alle toepassingen' koppelen][2]
    
3. <span data-ttu-id="32523-131">een nieuwe toepassing hello boven aan het Hallo tooadd **alle toepassingen** dialoogvenster, **nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="32523-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    !['Nieuwe application' Hallo knop][3]

4. <span data-ttu-id="32523-133">Typ in het zoekvak Hallo **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="32523-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![Hallo zoekvak](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="32523-135">Selecteer in de lijst met resultaten Hallo **Cezanne HR Software** en selecteer vervolgens Hallo **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="32523-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![lijst met resultaten Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="32523-137">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="32523-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="32523-138">In deze sectie maakt u configureren en testen van Azure AD-SSO met Cezanne HR-software op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="32523-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32523-139">Voor eenmalige aanmelding toowork moet Azure AD tooknow hello Cezanne HR software equivalent toohello Azure AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="32523-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="32523-140">Met andere woorden, moet u een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker maken in Hallo Cezanne HR-software.</span><span class="sxs-lookup"><span data-stu-id="32523-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="32523-141">tooestablish hello koppeling relatie toewijzen Hallo Cezanne HR software **gebruikersnaam** waarde als hello Azure AD **gebruikersnaam** waarde.</span><span class="sxs-lookup"><span data-stu-id="32523-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="32523-142">tooconfigure en test Azure AD-SSO met behulp van Cezanne HR-software, volledige Hallo bouwstenen te volgen.</span><span class="sxs-lookup"><span data-stu-id="32523-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="32523-143">Azure AD-eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="32523-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="32523-144">In deze sectie kunt u Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en configureren van eenmalige aanmelding in uw toepassing Cezanne HR door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="32523-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="32523-145">In de Azure-portal op Hallo Hallo **Cezanne HR Software** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="32523-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![opdracht 'Single sign-on' Hallo][4]

2. <span data-ttu-id="32523-147">tooenable SSO in Hallo **eenmalige aanmelding** dialoogvenster, selecteer Hallo **modus** als **op basis van SAML aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="32523-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Hallo 'Modus' vak](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="32523-149">Onder **Cezanne HR Software domein en de URL's**, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="32523-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![de sectie 'Cezanne HR Software domein en URL's ' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="32523-151">a.</span><span class="sxs-lookup"><span data-stu-id="32523-151">a.</span></span> <span data-ttu-id="32523-152">In Hallo **aanmeldings-URL** vak een URL die is Hallo de volgende syntaxis:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="32523-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="32523-153">b.</span><span class="sxs-lookup"><span data-stu-id="32523-153">b.</span></span> <span data-ttu-id="32523-154">In Hallo **antwoord-URL** vak een URL die is Hallo de volgende syntaxis:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="32523-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="32523-155">Hallo voorgaande waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="32523-155">hello preceding values are not real.</span></span> <span data-ttu-id="32523-156">Deze bijwerken met Hallo werkelijke antwoord-URL en Hallo aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="32523-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="32523-157">tooobtain hello waarden, neem contact op met Hallo [Cezanne HR software client ondersteuningsteam](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="32523-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="32523-158">Onder **SAML-certificaat voor ondertekening van**, selecteer **certificaat (Base64)**, en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="32523-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![de sectie 'SAML handtekeningcertificaat' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="32523-160">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="32523-160">Select **Save**.</span></span>

    ![Hallo 'Opslaan' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="32523-162">Onder **Cezanne HR-softwareconfiguratie**, selecteer **Cezanne HR-Software configureren** tooopen hello **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="32523-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="32523-163">Kopiëren Hallo **SAML entiteit-ID** en **SAML Single Sign-On-Service** URL uit Hallo **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="32523-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![de sectie 'Cezanne HR softwareconfiguratie' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="32523-165">Een ander browservenster, meld u aan bij tooyour Cezanne HR software tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="32523-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="32523-166">Selecteer in het linkerdeelvenster Hallo **Setup van System**.</span><span class="sxs-lookup"><span data-stu-id="32523-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="32523-167">Selecteer **beveiligingsinstellingen** > **eenmalige aanmelding configuratie**.</span><span class="sxs-lookup"><span data-stu-id="32523-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Hallo 'Single Sign-On-configuratie' koppeling](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="32523-169">In Hallo **toestaan dat gebruikers toolog aan Hallo eenmalige aanmelding (SSO)-services te volgen met** deelvenster, selecteer Hallo **SAML 2.0** selectievakje in en selecteer Hallo **geavanceerde configuratie** optie.</span><span class="sxs-lookup"><span data-stu-id="32523-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Eenmalige aanmelding opties voor services](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="32523-171">Selecteer **nieuwe toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="32523-171">Select **Add New**.</span></span>

    ![Hallo "toevoegen" om](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="32523-173">Onder **SAML 2.0 identiteitsproviders**, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="32523-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![de sectie 'SAML 2.0 identiteitsproviders' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="32523-175">a.</span><span class="sxs-lookup"><span data-stu-id="32523-175">a.</span></span> <span data-ttu-id="32523-176">In Hallo **weergavenaam** Hallo- naam van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="32523-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="32523-177">b.</span><span class="sxs-lookup"><span data-stu-id="32523-177">b.</span></span> <span data-ttu-id="32523-178">In Hallo **entiteits-id** vak, plak Hallo **SAML entiteit-ID** die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="32523-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="32523-179">c.</span><span class="sxs-lookup"><span data-stu-id="32523-179">c.</span></span> <span data-ttu-id="32523-180">In Hallo **SAML Binding** keuzelijst met invoervak, selecteer **POST**.</span><span class="sxs-lookup"><span data-stu-id="32523-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="32523-181">d.</span><span class="sxs-lookup"><span data-stu-id="32523-181">d.</span></span> <span data-ttu-id="32523-182">In Hallo **Security Token Service-eindpunt** vak, plak Hallo **SAML Single Sign-On-Service** URL die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="32523-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="32523-183">e.</span><span class="sxs-lookup"><span data-stu-id="32523-183">e.</span></span> <span data-ttu-id="32523-184">In Hallo **gebruikersnaam van het ID-kenmerk** Voer `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="32523-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="32523-185">f.</span><span class="sxs-lookup"><span data-stu-id="32523-185">f.</span></span> <span data-ttu-id="32523-186">Hallo tooupload certificaat gedownload vanuit Azure AD, selecteer Hallo **uploaden** knop.</span><span class="sxs-lookup"><span data-stu-id="32523-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="32523-187">g.</span><span class="sxs-lookup"><span data-stu-id="32523-187">g.</span></span> <span data-ttu-id="32523-188">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="32523-188">Select **OK**.</span></span> 

12. <span data-ttu-id="32523-189">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="32523-189">Select **Save**.</span></span>

    ![Hallo 'Opslaan' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="32523-191">Bij het instellen van de app hello, vindt u een beknopte versie van de voorgaande instructies in Hallo Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32523-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="32523-192">Nadat u Hallo app toegevoegd uit Hallo **Active Directory** > **bedrijfstoepassingen** sectie, selecteer Hallo **eenmalige aanmelding** tabblad. Vervolgens toegang Hallo documentatie van Hallo ingesloten **configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="32523-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="32523-193">toolearn meer informatie over de functie voor Hallo embedded-documentatie, Zie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="32523-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="32523-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="32523-194">Create an Azure AD test user</span></span>
<span data-ttu-id="32523-195">In deze sectie maakt u testgebruiker Britta Simon in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="32523-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![Hallo testgebruiker Britta Simon][100]

<span data-ttu-id="32523-197">een testgebruiker in Azure AD toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="32523-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="32523-198">In Hallo **Azure-portal**, in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="32523-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![Hallo 'Azure Active Directory' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32523-200">toodisplay hello lijst met gebruikers, selecteer **gebruikers en groepen** > **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="32523-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Hallo 'Alle gebruikers' koppelen](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="32523-202">Hallo **alle gebruikers** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="32523-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="32523-203">Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="32523-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![de knop "Toevoegen" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32523-205">In Hallo **gebruiker** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="32523-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![Hallo 'Gebruiker' dialoogvenster](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32523-207">a.</span><span class="sxs-lookup"><span data-stu-id="32523-207">a.</span></span> <span data-ttu-id="32523-208">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32523-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32523-209">b.</span><span class="sxs-lookup"><span data-stu-id="32523-209">b.</span></span> <span data-ttu-id="32523-210">In Hallo **gebruikersnaam** vak gebruiker Britta Simon **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="32523-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="32523-211">c.</span><span class="sxs-lookup"><span data-stu-id="32523-211">c.</span></span> <span data-ttu-id="32523-212">Selecteer Hallo **wachtwoord weergeven** selectievakje en Opmerking Hallo waarde die is gegenereerd in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="32523-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="32523-213">d.</span><span class="sxs-lookup"><span data-stu-id="32523-213">d.</span></span> <span data-ttu-id="32523-214">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="32523-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="32523-215">Maak een testgebruiker Cezanne HR-software</span><span class="sxs-lookup"><span data-stu-id="32523-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="32523-216">Azure AD tooenable gebruikers toosign in tooCezanne HR-software, ze in Cezanne HR software moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="32523-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="32523-217">In geval van Cezanne HR software Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="32523-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="32523-218">Een gebruikersaccount inrichten door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="32523-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="32523-219">Meld u tooyour Cezanne HR software bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="32523-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="32523-220">Selecteer in het linkerdeelvenster Hallo **Setup van System** > **gebruikers beheren** > **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="32523-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="32523-221">![Hallo 'Nieuwe gebruiker toevoegen' koppeling](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="32523-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="32523-222">Onder **persoon Details**, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="32523-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="32523-223">![in de sectie 'Persoon Details' Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="32523-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="32523-224">a.</span><span class="sxs-lookup"><span data-stu-id="32523-224">a.</span></span> <span data-ttu-id="32523-225">Stel **interne gebruiker** als **OFF**.</span><span class="sxs-lookup"><span data-stu-id="32523-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="32523-226">b.</span><span class="sxs-lookup"><span data-stu-id="32523-226">b.</span></span> <span data-ttu-id="32523-227">In Hallo **voornaam** vak, type Hallo voornaam van gebruiker, bijvoorbeeld **Britta**.</span><span class="sxs-lookup"><span data-stu-id="32523-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="32523-228">c.</span><span class="sxs-lookup"><span data-stu-id="32523-228">c.</span></span> <span data-ttu-id="32523-229">In Hallo **achternaam** vak, type Hallo gebruiker achternaam op, bijvoorbeeld **Simon**.</span><span class="sxs-lookup"><span data-stu-id="32523-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="32523-230">d.</span><span class="sxs-lookup"><span data-stu-id="32523-230">d.</span></span> <span data-ttu-id="32523-231">In Hallo **e** e-mailadres van de gebruiker hello, bijvoorbeeld: Typ Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="32523-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="32523-232">Onder **accountgegevens**, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="32523-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="32523-233">![sectie "Gegevens" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="32523-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="32523-234">a.</span><span class="sxs-lookup"><span data-stu-id="32523-234">a.</span></span> <span data-ttu-id="32523-235">In Hallo **gebruikersnaam** e-mailadres van de gebruiker hello, bijvoorbeeld: Typ Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="32523-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="32523-236">b.</span><span class="sxs-lookup"><span data-stu-id="32523-236">b.</span></span> <span data-ttu-id="32523-237">In Hallo **wachtwoord** typt u het wachtwoord van gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="32523-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="32523-238">c.</span><span class="sxs-lookup"><span data-stu-id="32523-238">c.</span></span> <span data-ttu-id="32523-239">In Hallo **beveiligingsrol** de optie **HR Professional**.</span><span class="sxs-lookup"><span data-stu-id="32523-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="32523-240">d.</span><span class="sxs-lookup"><span data-stu-id="32523-240">d.</span></span> <span data-ttu-id="32523-241">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="32523-241">Select **OK**.</span></span>

5. <span data-ttu-id="32523-242">Op Hallo **eenmalige aanmelding** tabblad in Hallo **SAML 2.0-id's** sectie **nieuwe toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="32523-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="32523-243">![Hallo "toevoegen" om](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="32523-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="32523-244">In Hallo **identiteitsprovider** keuzelijst, selecteert u de id-provider.</span><span class="sxs-lookup"><span data-stu-id="32523-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="32523-245">In Hallo **gebruikers-id** Voer Hallo e-mailadres voor test gebruiker Britta Simon van account.</span><span class="sxs-lookup"><span data-stu-id="32523-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="32523-246">![vakken 'Identiteitsprovider' en 'Gebruikers-id' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="32523-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="32523-247">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="32523-247">Select **Save**.</span></span>

    <span data-ttu-id="32523-248">![Hallo 'Opslaan' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="32523-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="32523-249">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="32523-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="32523-250">In deze sectie kunt u testgebruiker Britta Simon toouse Azure eenmalige aanmelding inschakelen tooCezanne HR-software toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="32523-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Toegang van gebruikers testen][200] 

1. <span data-ttu-id="32523-252">In hello Azure-portal, opent u Hallo toepassingen weergeven en gaat toohello directory weergeven.</span><span class="sxs-lookup"><span data-stu-id="32523-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="32523-253">Selecteer **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="32523-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Hallo 'Alle toepassingen' koppelen][201] 

2. <span data-ttu-id="32523-255">Selecteer in de lijst met de toepassingen van Hallo **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="32523-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![lijst met Hallo 'Toepassingen'](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="32523-257">Selecteer in het menu aan de linkerkant Hallo Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="32523-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="32523-259">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="32523-259">Select **Add**.</span></span> <span data-ttu-id="32523-260">Klik dan in Hallo **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="32523-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][203]

5. <span data-ttu-id="32523-262">In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="32523-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="32523-263">In Hallo **gebruikers en groepen** dialoogvenster, **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="32523-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="32523-264">In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="32523-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="32523-265">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="32523-265">Test SSO</span></span>

<span data-ttu-id="32523-266">In deze sectie kunt u de configuratie van uw Azure AD SSO testen met behulp van Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="32523-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="32523-267">Wanneer u Hallo Cezanne HR software tegel in het deelvenster toegang Hallo selecteert, u zich aanmelden automatisch tooyour Cezanne HR softwaretoepassing.</span><span class="sxs-lookup"><span data-stu-id="32523-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32523-268">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32523-268">Next steps</span></span>

* [<span data-ttu-id="32523-269">Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32523-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32523-270">Wat is de toegang tot toepassingen en SSO met Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32523-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

