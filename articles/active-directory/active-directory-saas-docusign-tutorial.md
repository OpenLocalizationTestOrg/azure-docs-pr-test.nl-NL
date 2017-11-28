---
title: 'Zelfstudie: Azure Active Directory-integratie met DocuSign | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="c1d6b-103">Zelfstudie: Azure Active Directory-integratie met DocuSign</span><span class="sxs-lookup"><span data-stu-id="c1d6b-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="c1d6b-104">In deze zelfstudie leert u hoe toointegrate DocuSign met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1d6b-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1d6b-105">DocuSign integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c1d6b-106">U kunt beheren in Azure AD die tooDocuSign toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c1d6b-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="c1d6b-107">U kunt uw gebruikers tooautomatically get aangemelde tooDocuSign (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c1d6b-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1d6b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c1d6b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c1d6b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1d6b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1d6b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c1d6b-110">Prerequisites</span></span>

<span data-ttu-id="c1d6b-111">Azure AD-integratie met DocuSign tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="c1d6b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c1d6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1d6b-113">Een DocuSign eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c1d6b-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1d6b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1d6b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1d6b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1d6b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1d6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1d6b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c1d6b-118">Scenario description</span></span>
<span data-ttu-id="c1d6b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1d6b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1d6b-121">Het toevoegen van DocuSign van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c1d6b-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="c1d6b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c1d6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="c1d6b-123">Het toevoegen van DocuSign van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c1d6b-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="c1d6b-124">tooconfigure hello integratie van DocuSign in Azure AD, moet u tooadd DocuSign uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c1d6b-125">**tooadd DocuSign via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c1d6b-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1d6b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1d6b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c1d6b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c1d6b-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c1d6b-133">Typ in het zoekvak Hallo **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-133">In hello search box, type **DocuSign**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="c1d6b-135">Selecteer in het deelvenster resultaten hello, **DocuSign**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1d6b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c1d6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1d6b-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met DocuSign op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c1d6b-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c1d6b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in DocuSign is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="c1d6b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in DocuSign toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="c1d6b-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in DocuSign.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="c1d6b-142">tooconfigure en eenmalige aanmelding Azure AD-test met DocuSign, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c1d6b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c1d6b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1d6b-145">**[Maken van een testgebruiker DocuSign](#creating-a-docusign-test-user)**  -toohave een equivalent van Britta Simon in DocuSign die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1d6b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1d6b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1d6b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c1d6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1d6b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing DocuSign configureren.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="c1d6b-150">**Azure AD tooconfigure eenmalige aanmelding met DocuSign, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c1d6b-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1d6b-151">In de Azure-portal op Hallo Hallo **DocuSign** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c1d6b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="c1d6b-155">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base 64)** en sla het bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="c1d6b-157">Op Hallo **DocuSign configuratie** sectie van de Azure-portal klikt u op **DocuSign configureren** venster tooopen configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="c1d6b-158">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c1d6b-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="c1d6b-160">In een andere web-browservenster aanmelding tooyour **DocuSign-beheerportal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="c1d6b-161">Klik in het navigatiemenu aan de linkerkant Hallo Hallo op **domeinen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Eenmalige aanmelding configureren][51]

7. <span data-ttu-id="c1d6b-163">Klik in het rechterdeelvenster Hallo **Claim domein**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Eenmalige aanmelding configureren][52]

8. <span data-ttu-id="c1d6b-165">Op Hallo **claimen van een domein** dialoogvenster in Hallo **domeinnaam** textbox, typt u het domein van uw bedrijf en klik vervolgens op **Claim**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="c1d6b-166">Zorg ervoor dat u Hallo domein verifiëren en Hallo status actief is.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Eenmalige aanmelding configureren][53]

9. <span data-ttu-id="c1d6b-168">Klik in het menu aan de linkerkant Hallo **id-Providers**</span><span class="sxs-lookup"><span data-stu-id="c1d6b-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Eenmalige aanmelding configureren][54]
10. <span data-ttu-id="c1d6b-170">Klik in het rechterdeelvenster hello, **identiteitsprovider toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Eenmalige aanmelding configureren][55]

11. <span data-ttu-id="c1d6b-172">Op Hallo **identiteit Providerinstellingen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren][56]

    <span data-ttu-id="c1d6b-174">a.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-174">a.</span></span> <span data-ttu-id="c1d6b-175">In Hallo **naam** textbox, typ een unieke naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="c1d6b-176">Gebruik geen spaties.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-176">Do not use spaces.</span></span>

    <span data-ttu-id="c1d6b-177">b.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-177">b.</span></span> <span data-ttu-id="c1d6b-178">Plakken **SAML entiteit-ID** in Hallo **identiteit Provider verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="c1d6b-179">c.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-179">c.</span></span> <span data-ttu-id="c1d6b-180">Plakken **SAML Single Sign-On Service-URL** in Hallo **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="c1d6b-181">d.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-181">d.</span></span> <span data-ttu-id="c1d6b-182">Plakken **Sign-Out URL** in Hallo **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="c1d6b-183">e.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-183">e.</span></span> <span data-ttu-id="c1d6b-184">Selecteer **AuthN aanvraag ondertekenen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="c1d6b-185">f.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-185">f.</span></span> <span data-ttu-id="c1d6b-186">Als **aanvraag verzenden AuthN door**, selecteer **POST**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="c1d6b-187">g.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-187">g.</span></span> <span data-ttu-id="c1d6b-188">Als **afmelding Verzendaanvraag door**, selecteer **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="c1d6b-189">In Hallo **toewijzing van aangepast kenmerk** sectie, kies Hallo veld gewenste toomap met Azure AD Claim.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="c1d6b-190">In dit voorbeeld Hallo **emailaddress** claim is toegewezen met de Hallo waarde **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="c1d6b-191">Het is Hallo standaardnaam claim van Azure AD voor e-mailbericht claim.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="c1d6b-192">Gebruik Hallo juiste **gebruikers-id** toomap Hallo gebruiker van Azure AD tooDocuSign gebruiker toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="c1d6b-193">Selecteer Hallo juiste veld en Voer Hallo geschikte waarde op basis van de instellingen van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Eenmalige aanmelding configureren][57]

13. <span data-ttu-id="c1d6b-195">In Hallo **Provider identiteitscertificaat** sectie, klikt u op **certificaat toevoegen**, en u hebt gedownload van Azure AD-portal Hallo-certificaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Eenmalige aanmelding configureren][58]

14. <span data-ttu-id="c1d6b-197">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-197">Click **Save**.</span></span>

15. <span data-ttu-id="c1d6b-198">In Hallo **identiteitsproviders** sectie, klikt u op **acties**, en klik vervolgens op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Eenmalige aanmelding configureren][59]
 
16. <span data-ttu-id="c1d6b-200">In Hallo **SAML 2.0-eindpunten weergeven** sectie op **DocuSign-beheerportal**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren][60]
   
    <span data-ttu-id="c1d6b-202">a.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-202">a.</span></span> <span data-ttu-id="c1d6b-203">Kopiëren Hallo **URL-Service Provider verlener**, en plak in Hallo **id** textbox op **DocuSign domein en de URL's** sectie van de Azure portal volgende Hallo Hallo patroon: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="c1d6b-204">b.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-204">b.</span></span> <span data-ttu-id="c1d6b-205">Kopiëren Hallo **aanmeldings-URL voor Service Provider**, en plak in Hallo **aanmelding op URL** textbox op **DocuSign domein en de URL's** sectie van de Azure portal volgende Hallo Hallo patroon: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="c1d6b-207">c.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-207">c.</span></span>  <span data-ttu-id="c1d6b-208">Klik op **sluiten**</span><span class="sxs-lookup"><span data-stu-id="c1d6b-208">Click **Close**</span></span>
    
17. <span data-ttu-id="c1d6b-209">Klik op Hallo Azure-portal, **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="c1d6b-211">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c1d6b-212">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c1d6b-213">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1d6b-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1d6b-214">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c1d6b-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1d6b-215">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c1d6b-217">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c1d6b-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1d6b-218">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1d6b-220">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1d6b-222">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1d6b-224">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1d6b-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1d6b-226">a.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-226">a.</span></span> <span data-ttu-id="c1d6b-227">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1d6b-228">b.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-228">b.</span></span> <span data-ttu-id="c1d6b-229">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1d6b-230">c.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-230">c.</span></span> <span data-ttu-id="c1d6b-231">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c1d6b-232">d.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-232">d.</span></span> <span data-ttu-id="c1d6b-233">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="c1d6b-234">Een testgebruiker DocuSign maken</span><span class="sxs-lookup"><span data-stu-id="c1d6b-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="c1d6b-235">Toepassing ondersteunt **Just in time gebruikersaanvragen** en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c1d6b-236">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1d6b-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c1d6b-237">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooDocuSign toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c1d6b-239">**tooassign Britta Simon tooDocuSign, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c1d6b-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1d6b-240">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c1d6b-242">Selecteer in de lijst met de toepassingen van Hallo **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-242">In hello applications list, select **DocuSign**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="c1d6b-244">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c1d6b-246">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-246">Click **Add** button.</span></span> <span data-ttu-id="c1d6b-247">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c1d6b-249">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c1d6b-250">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1d6b-251">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1d6b-252">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c1d6b-252">Testing single sign-on</span></span>

<span data-ttu-id="c1d6b-253">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c1d6b-254">Als u op Hallo DocuSign tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour DocuSign toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1d6b-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="c1d6b-255">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c1d6b-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c1d6b-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c1d6b-256">Additional resources</span></span>

* [<span data-ttu-id="c1d6b-257">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1d6b-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1d6b-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1d6b-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c1d6b-259">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="c1d6b-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

