---
title: 'Zelfstudie: Azure Active Directory-integratie met Adobe teken | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Adobe aanmelding.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="e66ce-103">Zelfstudie: Azure Active Directory-integratie met Adobe teken</span><span class="sxs-lookup"><span data-stu-id="e66ce-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="e66ce-104">In deze zelfstudie leert u hoe toointegrate Adobe Meld u aan bij Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e66ce-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e66ce-105">Meld u Adobe integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e66ce-106">U kunt beheren in Azure AD wie toegang tot tooAdobe aanmelding heeft</span><span class="sxs-lookup"><span data-stu-id="e66ce-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="e66ce-107">U kunt uw gebruikers tooautomatically get aangemelde tooAdobe aanmelding (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e66ce-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e66ce-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e66ce-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e66ce-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e66ce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e66ce-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e66ce-110">Prerequisites</span></span>

<span data-ttu-id="e66ce-111">Azure AD-integratie met Adobe teken tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e66ce-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="e66ce-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e66ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e66ce-113">Een Adobe aanmelding eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e66ce-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e66ce-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e66ce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e66ce-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e66ce-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e66ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e66ce-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e66ce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e66ce-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e66ce-118">Scenario description</span></span>
<span data-ttu-id="e66ce-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e66ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e66ce-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e66ce-121">Het toevoegen van Adobe aanmelding van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e66ce-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="e66ce-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e66ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="e66ce-123">Het toevoegen van Adobe aanmelding van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e66ce-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="e66ce-124">tooconfigure hello integratie van Adobe aanmelding in Azure AD, moet u tooadd Adobe aanmelding uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e66ce-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e66ce-125">**tooadd Adobe teken uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e66ce-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e66ce-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e66ce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e66ce-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e66ce-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e66ce-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e66ce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e66ce-133">Typ in het zoekvak Hallo **Adobe aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="e66ce-135">Selecteer in het deelvenster resultaten hello, **Adobe aanmelding**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e66ce-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e66ce-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e66ce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e66ce-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Adobe aanmelding op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e66ce-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e66ce-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Adobe aanmelding is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e66ce-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="e66ce-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Adobe aanmelding toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e66ce-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="e66ce-141">In Adobe teken, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="e66ce-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e66ce-142">tooconfigure en eenmalige aanmelding Azure AD-test met Adobe ondertekenen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e66ce-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e66ce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e66ce-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e66ce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e66ce-145">**[Maken van een testgebruiker Adobe aanmelding](#creating-an-adobe-sign-test-user)**  -toohave een equivalent van Britta Simon in Adobe aanmelding die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e66ce-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e66ce-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e66ce-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e66ce-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e66ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e66ce-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e66ce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e66ce-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Adobe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e66ce-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="e66ce-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Adobe-teken Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e66ce-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e66ce-151">In Azure-portal op Hallo Hallo **Adobe aanmelding** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e66ce-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e66ce-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="e66ce-155">Op Hallo **Adobe aanmelding domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="e66ce-157">a.</span><span class="sxs-lookup"><span data-stu-id="e66ce-157">a.</span></span> <span data-ttu-id="e66ce-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="e66ce-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="e66ce-159">b.</span><span class="sxs-lookup"><span data-stu-id="e66ce-159">b.</span></span> <span data-ttu-id="e66ce-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="e66ce-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e66ce-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e66ce-161">These values are not real.</span></span> <span data-ttu-id="e66ce-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="e66ce-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e66ce-163">Neem contact op met [Adobe aanmelding Client ondersteuningsteam](https://helpx.adobe.com/in/contact/support.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e66ce-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="e66ce-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e66ce-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="e66ce-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e66ce-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e66ce-168">Op Hallo **Adobe aanmelding configuratie** sectie, klikt u op **Adobe aanmelding configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e66ce-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e66ce-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e66ce-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="e66ce-171">In een ander browservenster, meld u aan tooyour Adobe aanmelding bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="e66ce-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="e66ce-172">Klik in het menu bovenaan Hallo Hallo **Account**, en klik vervolgens in het navigatievenster aan de linkerkant Hallo Hallo op **SAML instellingen** onder **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="e66ce-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span><span class="sxs-lookup"><span data-stu-id="e66ce-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="e66ce-174">Voer in Hallo sectie SAML-instellingen, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e66ce-175">![Instellingen voor SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="e66ce-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="e66ce-176">a.</span><span class="sxs-lookup"><span data-stu-id="e66ce-176">a.</span></span> <span data-ttu-id="e66ce-177">Als **SAML modus**, selecteer **SAML verplichte**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="e66ce-178">b.</span><span class="sxs-lookup"><span data-stu-id="e66ce-178">b.</span></span> <span data-ttu-id="e66ce-179">Selecteer **EchoSign accountbeheerders toestaan toolog aan met hun referenties EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="e66ce-180">c.</span><span class="sxs-lookup"><span data-stu-id="e66ce-180">c.</span></span> <span data-ttu-id="e66ce-181">Als **maken van een gebruikersaccount**, selecteer **automatisch toevoegen van gebruikers worden geverifieerd via SAML**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="e66ce-182">Verplaatsen, uitvoeren Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="e66ce-183">![Instellingen voor SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="e66ce-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="e66ce-184">a.</span><span class="sxs-lookup"><span data-stu-id="e66ce-184">a.</span></span> <span data-ttu-id="e66ce-185">Plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal in Hallo **IdP entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="e66ce-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="e66ce-186">b.</span><span class="sxs-lookup"><span data-stu-id="e66ce-186">b.</span></span> <span data-ttu-id="e66ce-187">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal in Hallo **IdP aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e66ce-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="e66ce-188">c.</span><span class="sxs-lookup"><span data-stu-id="e66ce-188">c.</span></span> <span data-ttu-id="e66ce-189">Plakken **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal in Hallo **IdP afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e66ce-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="e66ce-190">d.</span><span class="sxs-lookup"><span data-stu-id="e66ce-190">d.</span></span> <span data-ttu-id="e66ce-191">Open uw gedownloade **Certificate(Base64)** -bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **IdP certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="e66ce-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="e66ce-192">e.</span><span class="sxs-lookup"><span data-stu-id="e66ce-192">e.</span></span> <span data-ttu-id="e66ce-193">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e66ce-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e66ce-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e66ce-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e66ce-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e66ce-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e66ce-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e66ce-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e66ce-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e66ce-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e66ce-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e66ce-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e66ce-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e66ce-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e66ce-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e66ce-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e66ce-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e66ce-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e66ce-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e66ce-209">a.</span><span class="sxs-lookup"><span data-stu-id="e66ce-209">a.</span></span> <span data-ttu-id="e66ce-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e66ce-211">b.</span><span class="sxs-lookup"><span data-stu-id="e66ce-211">b.</span></span> <span data-ttu-id="e66ce-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e66ce-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e66ce-213">c.</span><span class="sxs-lookup"><span data-stu-id="e66ce-213">c.</span></span> <span data-ttu-id="e66ce-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e66ce-215">d.</span><span class="sxs-lookup"><span data-stu-id="e66ce-215">d.</span></span> <span data-ttu-id="e66ce-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="e66ce-217">Een testgebruiker Adobe aanmelding maken</span><span class="sxs-lookup"><span data-stu-id="e66ce-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="e66ce-218">Azure AD tooenable gebruikers toolog in tooAdobe aanmelding, ze in Adobe aanmelding moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="e66ce-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="e66ce-219">In geval van Adobe aanmelding Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e66ce-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e66ce-220">U kunt andere Adobe aanmelding gebruiker account hulpmiddelen voor het maken of API's geleverd door Adobe aanmelding tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e66ce-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="e66ce-221">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e66ce-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e66ce-222">Meld u bij tooyour **Adobe aanmelding** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="e66ce-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="e66ce-223">Klik in het menu bovenaan Hallo Hallo **Account**, en klik vervolgens in het navigatievenster aan de linkerkant Hallo Hallo op **gebruikers en groepen**, en klik vervolgens op **Maak een nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="e66ce-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span><span class="sxs-lookup"><span data-stu-id="e66ce-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="e66ce-225">In Hallo **nieuwe gebruiker maken** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e66ce-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e66ce-226">![Gebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="e66ce-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="e66ce-227">a.</span><span class="sxs-lookup"><span data-stu-id="e66ce-227">a.</span></span> <span data-ttu-id="e66ce-228">Type Hallo **e-mailadres**, **voornaam**, en **achternaam** van tekstvakken met betrekking tot een geldige AAD-account u wilt dat tooprovision in Hallo.</span><span class="sxs-lookup"><span data-stu-id="e66ce-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="e66ce-229">b.</span><span class="sxs-lookup"><span data-stu-id="e66ce-229">b.</span></span> <span data-ttu-id="e66ce-230">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="e66ce-231">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="e66ce-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e66ce-232">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e66ce-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e66ce-233">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAdobe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e66ce-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e66ce-235">**tooassign Britta Simon tooAdobe teken, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e66ce-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e66ce-236">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e66ce-238">Selecteer in de lijst met de toepassingen van Hallo **Adobe aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="e66ce-240">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e66ce-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e66ce-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e66ce-242">Click **Add** button.</span></span> <span data-ttu-id="e66ce-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e66ce-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e66ce-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e66ce-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e66ce-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e66ce-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e66ce-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e66ce-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e66ce-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e66ce-248">Testing single sign-on</span></span>

<span data-ttu-id="e66ce-249">Als u op Hallo Adobe aanmelding-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour programma Adobe ondertekenen.</span><span class="sxs-lookup"><span data-stu-id="e66ce-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="e66ce-250">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e66ce-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e66ce-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e66ce-251">Additional resources</span></span>

* [<span data-ttu-id="e66ce-252">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e66ce-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e66ce-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e66ce-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

