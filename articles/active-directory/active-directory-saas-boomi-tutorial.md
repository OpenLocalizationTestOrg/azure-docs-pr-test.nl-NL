---
title: 'Zelfstudie: Azure Active Directory-integratie met Boomi | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="bb577-103">Zelfstudie: Azure Active Directory-integratie met Boomi</span><span class="sxs-lookup"><span data-stu-id="bb577-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="bb577-104">In deze zelfstudie leert u hoe toointegrate Boomi met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb577-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb577-105">Boomi integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bb577-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb577-106">U kunt beheren in Azure AD die tooBoomi toegang heeft</span><span class="sxs-lookup"><span data-stu-id="bb577-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="bb577-107">U kunt uw gebruikers tooautomatically get aangemelde tooBoomi (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="bb577-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb577-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bb577-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb577-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb577-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb577-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bb577-110">Prerequisites</span></span>

<span data-ttu-id="bb577-111">Azure AD-integratie met Boomi tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="bb577-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="bb577-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bb577-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb577-113">Een Boomi eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bb577-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb577-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bb577-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb577-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bb577-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb577-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bb577-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb577-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb577-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb577-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bb577-118">Scenario description</span></span>
<span data-ttu-id="bb577-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bb577-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb577-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bb577-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb577-121">Het toevoegen van Boomi van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bb577-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="bb577-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bb577-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="bb577-123">Het toevoegen van Boomi van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bb577-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="bb577-124">tooconfigure hello integratie van Boomi in Azure AD, moet u tooadd Boomi uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bb577-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb577-125">**tooadd Boomi via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bb577-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb577-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bb577-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb577-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bb577-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb577-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bb577-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bb577-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bb577-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bb577-133">Typ in het zoekvak Hallo **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="bb577-133">In hello search box, type **Boomi**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="bb577-135">Selecteer in het deelvenster resultaten hello, **Boomi**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bb577-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb577-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bb577-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb577-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Boomi op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="bb577-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bb577-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Boomi is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb577-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="bb577-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Boomi toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="bb577-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="bb577-141">Wijs in Boomi, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="bb577-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bb577-142">tooconfigure en eenmalige aanmelding Azure AD-test met Boomi, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bb577-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb577-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="bb577-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb577-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb577-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb577-145">**[Maken van een testgebruiker Boomi](#creating-a-boomi-test-user)**  -toohave een equivalent van Britta Simon in Boomi die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bb577-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb577-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bb577-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb577-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bb577-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb577-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bb577-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb577-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Boomi configureren.</span><span class="sxs-lookup"><span data-stu-id="bb577-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="bb577-150">**Azure AD tooconfigure eenmalige aanmelding met Boomi, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bb577-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb577-151">In de Azure-portal op Hallo Hallo **Boomi** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bb577-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bb577-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bb577-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="bb577-155">Op Hallo **Boomi domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bb577-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="bb577-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb577-157">a.</span></span> <span data-ttu-id="bb577-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="bb577-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="bb577-159">b.</span><span class="sxs-lookup"><span data-stu-id="bb577-159">b.</span></span> <span data-ttu-id="bb577-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="bb577-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb577-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="bb577-161">These values are not real.</span></span> <span data-ttu-id="bb577-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="bb577-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="bb577-163">Neem contact op met [Boomi ondersteuningsteam](https://boomi.com/company/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="bb577-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="bb577-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bb577-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="bb577-166">Hallo SAML asserties verwacht Boomi toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="bb577-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="bb577-167">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="bb577-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="bb577-168">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="bb577-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="bb577-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="bb577-169">hello following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="bb577-171">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster uitvoeren Hallo volgende stappen uit voor elke rij in Hallo tabel hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="bb577-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="bb577-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb577-172">Attribute Name</span></span> | <span data-ttu-id="bb577-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb577-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="bb577-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="bb577-174">FEDERATION_ID</span></span> | <span data-ttu-id="bb577-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="bb577-175">user.mail</span></span> |
    
    <span data-ttu-id="bb577-176">a.</span><span class="sxs-lookup"><span data-stu-id="bb577-176">a.</span></span> <span data-ttu-id="bb577-177">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bb577-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="bb577-180">b.</span><span class="sxs-lookup"><span data-stu-id="bb577-180">b.</span></span> <span data-ttu-id="bb577-181">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="bb577-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bb577-182">c.</span><span class="sxs-lookup"><span data-stu-id="bb577-182">c.</span></span> <span data-ttu-id="bb577-183">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="bb577-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bb577-184">d.</span><span class="sxs-lookup"><span data-stu-id="bb577-184">d.</span></span> <span data-ttu-id="bb577-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb577-185">Click **Ok**.</span></span>

6. <span data-ttu-id="bb577-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bb577-186">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bb577-188">Op Hallo **Boomi configuratie** sectie, klikt u op **configureren Boomi** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bb577-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb577-189">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bb577-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="bb577-191">In een ander browservenster, meld u bij uw bedrijf Boomi site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bb577-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="bb577-192">Navigeer te**bedrijfsnaam** en ga te**instellen**.</span><span class="sxs-lookup"><span data-stu-id="bb577-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="bb577-193">Klik op Hallo **SSO opties** tabblad en Voer onderstaande stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="bb577-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="bb577-195">a.</span><span class="sxs-lookup"><span data-stu-id="bb577-195">a.</span></span> <span data-ttu-id="bb577-196">Controleer **inschakelen SAML Single Sign-On** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="bb577-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="bb577-197">b.</span><span class="sxs-lookup"><span data-stu-id="bb577-197">b.</span></span> <span data-ttu-id="bb577-198">Klik op **importeren** tooupload Hallo certificaat gedownload vanuit Azure AD te**Provider identiteitscertificaat**.</span><span class="sxs-lookup"><span data-stu-id="bb577-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="bb577-199">c.</span><span class="sxs-lookup"><span data-stu-id="bb577-199">c.</span></span> <span data-ttu-id="bb577-200">In Hallo **identiteit Provider aanmeldings-URL** textbox Hallo-waarde van **SAML Single Sign-On Service-URL** van het venster voor configuratie van Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bb577-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="bb577-201">d.</span><span class="sxs-lookup"><span data-stu-id="bb577-201">d.</span></span> <span data-ttu-id="bb577-202">Als **Federation Id locatie**, selecteer **Federation-Id wordt FEDERATION_ID kenmerk element** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="bb577-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="bb577-203">e.</span><span class="sxs-lookup"><span data-stu-id="bb577-203">e.</span></span> <span data-ttu-id="bb577-204">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bb577-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="bb577-205">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="bb577-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb577-206">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="bb577-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb577-207">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb577-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb577-208">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bb577-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb577-209">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bb577-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bb577-211">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bb577-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb577-212">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bb577-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb577-214">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bb577-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb577-216">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="bb577-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb577-218">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bb577-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb577-220">a.</span><span class="sxs-lookup"><span data-stu-id="bb577-220">a.</span></span> <span data-ttu-id="bb577-221">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb577-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb577-222">b.</span><span class="sxs-lookup"><span data-stu-id="bb577-222">b.</span></span> <span data-ttu-id="bb577-223">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bb577-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb577-224">c.</span><span class="sxs-lookup"><span data-stu-id="bb577-224">c.</span></span> <span data-ttu-id="bb577-225">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bb577-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb577-226">d.</span><span class="sxs-lookup"><span data-stu-id="bb577-226">d.</span></span> <span data-ttu-id="bb577-227">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bb577-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="bb577-228">Een testgebruiker Boomi maken</span><span class="sxs-lookup"><span data-stu-id="bb577-228">Creating a Boomi test user</span></span>

<span data-ttu-id="bb577-229">In de volgorde tooenable Azure AD gebruikers toolog in tooBoomi, moeten ze worden ingericht in Boomi.</span><span class="sxs-lookup"><span data-stu-id="bb577-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="bb577-230">In geval van Boomi Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bb577-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="bb577-231">een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bb577-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="bb577-232">Aanmelden tooyour Boomi bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bb577-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="bb577-233">Na het aanmelden, te navigeren**Gebruikersbeheer** en ga te**gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bb577-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="bb577-234">![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="bb577-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="bb577-235">Klik op  **+**  pictogram en Hallo **toevoegen/onderhouden gebruikersrollen** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="bb577-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="bb577-236">![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="bb577-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="bb577-237">![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="bb577-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="bb577-238">a.</span><span class="sxs-lookup"><span data-stu-id="bb577-238">a.</span></span> <span data-ttu-id="bb577-239">In Hallo **e-mailadres gebruiker** textbox type Hallo e-mailadres van de gebruiker, zoals BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bb577-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="bb577-240">b.</span><span class="sxs-lookup"><span data-stu-id="bb577-240">b.</span></span> <span data-ttu-id="bb577-241">In Hallo **voornaam** textbox type Hallo voornaam van gebruiker zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="bb577-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="bb577-242">c.</span><span class="sxs-lookup"><span data-stu-id="bb577-242">c.</span></span> <span data-ttu-id="bb577-243">In Hallo **achternaam** textbox type Hallo achternaam van gebruiker zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="bb577-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="bb577-244">d.</span><span class="sxs-lookup"><span data-stu-id="bb577-244">d.</span></span> <span data-ttu-id="bb577-245">Voer van Hallo gebruiker **Federatie-ID**.</span><span class="sxs-lookup"><span data-stu-id="bb577-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="bb577-246">Elke gebruiker moet een Federation-ID die een unieke identificatie van Hallo gebruiker binnen Hallo-account hebben.</span><span class="sxs-lookup"><span data-stu-id="bb577-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="bb577-247">e.</span><span class="sxs-lookup"><span data-stu-id="bb577-247">e.</span></span> <span data-ttu-id="bb577-248">Hallo toewijzen **standaardgebruiker** rol toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bb577-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="bb577-249">Geen toewijzen Hallo beheerdersrol omdat die hem normale lucht toegang als één aanmelding toegang wilt geven.</span><span class="sxs-lookup"><span data-stu-id="bb577-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="bb577-250">f.</span><span class="sxs-lookup"><span data-stu-id="bb577-250">f.</span></span> <span data-ttu-id="bb577-251">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb577-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="bb577-252">Hallo-gebruiker ontvangt een e-mailmelding Welkom met een wachtwoord dat gebruikt toolog in toohello AtomSphere account worden kan omdat het wachtwoord wordt beheerd via Hallo id-provider niet.</span><span class="sxs-lookup"><span data-stu-id="bb577-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="bb577-253">U kunt andere Boomi gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Boomi tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bb577-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb577-254">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb577-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb577-255">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBoomi toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="bb577-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bb577-257">**tooassign Britta Simon tooBoomi, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bb577-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb577-258">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bb577-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bb577-260">Selecteer in de lijst met de toepassingen van Hallo **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="bb577-260">In hello applications list, select **Boomi**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="bb577-262">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bb577-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bb577-264">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bb577-264">Click **Add** button.</span></span> <span data-ttu-id="bb577-265">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bb577-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bb577-267">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="bb577-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb577-268">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bb577-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb577-269">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bb577-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb577-270">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bb577-270">Testing single sign-on</span></span>

<span data-ttu-id="bb577-271">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bb577-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bb577-272">Als u op Hallo Boomi tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Boomi toepassing.</span><span class="sxs-lookup"><span data-stu-id="bb577-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb577-273">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bb577-273">Additional resources</span></span>

* [<span data-ttu-id="bb577-274">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb577-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb577-275">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb577-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

