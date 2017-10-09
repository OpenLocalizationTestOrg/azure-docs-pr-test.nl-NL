---
title: 'Zelfstudie: Azure Active Directory-integratie met Aha! | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Aha!.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="a4e3a-104">Zelfstudie: Azure Active Directory-integratie met Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="a4e3a-105">In deze zelfstudie leert u hoe toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="a4e3a-106">met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4e3a-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4e3a-107">Integratie van Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-107">Integrating Aha!</span></span> <span data-ttu-id="a4e3a-108">met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a4e3a-109">U kunt beheren in Azure AD wie toegang tot tooAha heeft!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="a4e3a-110">U kunt uw gebruikers tooautomatically get aangemelde tooAha inschakelen!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="a4e3a-111">(Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="a4e3a-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4e3a-112">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a4e3a-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a4e3a-113">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4e3a-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4e3a-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a4e3a-114">Prerequisites</span></span>

<span data-ttu-id="a4e3a-115">Azure AD-integratie met Aha tooconfigure!, moet u de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="a4e3a-116">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a4e3a-116">An Azure AD subscription</span></span>
- <span data-ttu-id="a4e3a-117">Een Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-117">An Aha!</span></span> <span data-ttu-id="a4e3a-118">eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a4e3a-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4e3a-119">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a4e3a-120">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4e3a-121">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a4e3a-122">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4e3a-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4e3a-123">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a4e3a-123">Scenario description</span></span>
<span data-ttu-id="a4e3a-124">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4e3a-125">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4e3a-126">Toe te voegen Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-126">Adding Aha!</span></span> <span data-ttu-id="a4e3a-127">uit de galerie Hallo</span><span class="sxs-lookup"><span data-stu-id="a4e3a-127">from hello gallery</span></span>
2. <span data-ttu-id="a4e3a-128">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a4e3a-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="a4e3a-129">Toe te voegen Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-129">Adding Aha!</span></span> <span data-ttu-id="a4e3a-130">uit de galerie Hallo</span><span class="sxs-lookup"><span data-stu-id="a4e3a-130">from hello gallery</span></span>
<span data-ttu-id="a4e3a-131">tooconfigure hello integratie van Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="a4e3a-132">met Azure AD moet u tooadd Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="a4e3a-133">van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a4e3a-134">**tooadd Aha! uitvoeren vanuit Hallo-galerie Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a4e3a-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e3a-135">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4e3a-137">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a4e3a-138">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-138">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a4e3a-140">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a4e3a-142">Typ in het zoekvak Hallo **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-142">In hello search box, type **Aha!**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="a4e3a-144">Selecteer in het deelvenster resultaten hello, **Aha!**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4e3a-146">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a4e3a-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4e3a-147">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="a4e3a-148">op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a4e3a-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a4e3a-149">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker van het bijbehorende equivalent Hallo in Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="a4e3a-150">is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="a4e3a-151">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="a4e3a-152">moet toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-152">needs toobe established.</span></span>

<span data-ttu-id="a4e3a-153">In Aha!, waarde Hallo Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a4e3a-154">tooconfigure en Azure AD test eenmalige aanmelding met Aha!, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a4e3a-155">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a4e3a-156">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4e3a-157">**[Maken van een Aha! testgebruiker](#creating-an-aha-test-user)**  -toohave een equivalent van Britta Simon in Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="a4e3a-158">dat is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4e3a-159">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4e3a-160">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4e3a-161">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a4e3a-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4e3a-162">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="a4e3a-163">de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-163">application.</span></span>

<span data-ttu-id="a4e3a-164">**tooconfigure eenmalige aanmelding Azure AD met Aha!, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="a4e3a-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e3a-165">In de Azure-portal op Hallo Hallo **Aha!**</span><span class="sxs-lookup"><span data-stu-id="a4e3a-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="a4e3a-166">pagina van de integratie van toepassing, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-166">application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a4e3a-168">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="a4e3a-170">Op Hallo **Aha! Domein- en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="a4e3a-172">a.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-172">a.</span></span> <span data-ttu-id="a4e3a-173">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="a4e3a-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="a4e3a-174">b.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-174">b.</span></span> <span data-ttu-id="a4e3a-175">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="a4e3a-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a4e3a-176">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-176">These values are not real.</span></span> <span data-ttu-id="a4e3a-177">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a4e3a-178">Neem contact op met [Aha! Client-ondersteuningsteam](https://www.aha.io/company/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="a4e3a-179">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="a4e3a-181">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-181">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a4e3a-183">Aanmelden in een ander browservenster tooyour Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="a4e3a-184">bedrijf-site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-184">company site as an administrator.</span></span>

7. <span data-ttu-id="a4e3a-185">Klik in het menu bovenaan Hallo Hallo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="a4e3a-186">![Instellingen](./media/active-directory-saas-aha-tutorial/IC798950.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="a4e3a-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="a4e3a-187">Klik op **Account**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-187">Click **Account**.</span></span>
   
    <span data-ttu-id="a4e3a-188">![Profiel](./media/active-directory-saas-aha-tutorial/IC798951.png "profiel")</span><span class="sxs-lookup"><span data-stu-id="a4e3a-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="a4e3a-189">Klik op **beveiligings- en eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="a4e3a-190">![Beveiliging en eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798952.png "beveiligings- en eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="a4e3a-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="a4e3a-191">In **Single Sign-On** sectie als **identiteitsprovider**, selecteer **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="a4e3a-192">![Beveiliging en eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798953.png "beveiligings- en eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="a4e3a-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="a4e3a-193">Op Hallo **Single Sign-On** configuratie pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="a4e3a-194">![Eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798954.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="a4e3a-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="a4e3a-195">a.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-195">a.</span></span> <span data-ttu-id="a4e3a-196">In Hallo **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="a4e3a-197">b.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-197">b.</span></span> <span data-ttu-id="a4e3a-198">Voor **configureren met behulp van**, selecteer **metagegevensbestand**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="a4e3a-199">c.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-199">c.</span></span> <span data-ttu-id="a4e3a-200">tooupload uw gedownloade metagegevensbestand, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="a4e3a-201">d.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-201">d.</span></span> <span data-ttu-id="a4e3a-202">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="a4e3a-203">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a4e3a-204">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a4e3a-205">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a4e3a-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4e3a-206">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a4e3a-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4e3a-207">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a4e3a-209">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a4e3a-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e3a-210">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4e3a-212">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4e3a-214">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4e3a-216">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e3a-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4e3a-218">a.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-218">a.</span></span> <span data-ttu-id="a4e3a-219">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4e3a-220">b.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-220">b.</span></span> <span data-ttu-id="a4e3a-221">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4e3a-222">c.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-222">c.</span></span> <span data-ttu-id="a4e3a-223">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a4e3a-224">d.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-224">d.</span></span> <span data-ttu-id="a4e3a-225">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="a4e3a-226">Maken van een Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-226">Creating an Aha!</span></span> <span data-ttu-id="a4e3a-227">testgebruiker</span><span class="sxs-lookup"><span data-stu-id="a4e3a-227">test user</span></span>

<span data-ttu-id="a4e3a-228">Azure AD tooenable gebruikers toolog in tooAha!, deze moeten worden ingericht in Aha!.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="a4e3a-229">In geval van Aha Hallo!, wordt een geautomatiseerde taak ingericht.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="a4e3a-230">Er is geen actie-item voor u.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-230">There is no action item for you.</span></span>

<span data-ttu-id="a4e3a-231">Gebruikers worden automatisch gemaakt indien nodig tijdens Hallo eerste eenmalige aanmelding poging.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="a4e3a-232">U kunt andere Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-232">You can use any other Aha!</span></span> <span data-ttu-id="a4e3a-233">hulpmiddelen voor het maken van account of API's die worden geleverd door Aha!</span><span class="sxs-lookup"><span data-stu-id="a4e3a-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="a4e3a-234">tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a4e3a-235">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4e3a-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a4e3a-236">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAha!.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a4e3a-238">**tooassign Britta Simon tooAha!, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="a4e3a-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e3a-239">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a4e3a-241">Selecteer in de lijst met de toepassingen van Hallo **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-241">In hello applications list, select **Aha!**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="a4e3a-243">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a4e3a-245">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-245">Click **Add** button.</span></span> <span data-ttu-id="a4e3a-246">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a4e3a-248">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a4e3a-249">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4e3a-250">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4e3a-251">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a4e3a-251">Testing single sign-on</span></span>

<span data-ttu-id="a4e3a-252">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e3a-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="a4e3a-253">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4e3a-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4e3a-254">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a4e3a-254">Additional resources</span></span>

* [<span data-ttu-id="a4e3a-255">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4e3a-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4e3a-256">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4e3a-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

