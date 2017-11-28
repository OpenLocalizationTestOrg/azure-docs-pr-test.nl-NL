---
title: 'Zelfstudie: Azure Active Directory-integratie met TalentLMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TalentLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="e60ae-103">Zelfstudie: Azure Active Directory-integratie met TalentLMS</span><span class="sxs-lookup"><span data-stu-id="e60ae-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="e60ae-104">In deze zelfstudie leert u hoe toointegrate TalentLMS met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e60ae-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e60ae-105">TalentLMS integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e60ae-106">U kunt beheren in Azure AD die tooTalentLMS toegang heeft</span><span class="sxs-lookup"><span data-stu-id="e60ae-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="e60ae-107">U kunt uw gebruikers tooautomatically get aangemelde tooTalentLMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e60ae-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e60ae-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e60ae-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e60ae-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e60ae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e60ae-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e60ae-110">Prerequisites</span></span>

<span data-ttu-id="e60ae-111">Azure AD-integratie met TalentLMS tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e60ae-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="e60ae-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e60ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e60ae-113">Een TalentLMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e60ae-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e60ae-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e60ae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e60ae-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e60ae-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e60ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e60ae-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e60ae-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e60ae-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e60ae-118">Scenario description</span></span>
<span data-ttu-id="e60ae-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e60ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e60ae-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e60ae-121">Het toevoegen van TalentLMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e60ae-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="e60ae-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e60ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="e60ae-123">Het toevoegen van TalentLMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e60ae-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="e60ae-124">tooconfigure hello integratie van TalentLMS in Azure AD, moet u tooadd TalentLMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e60ae-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e60ae-125">**tooadd TalentLMS via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e60ae-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60ae-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e60ae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e60ae-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e60ae-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e60ae-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e60ae-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e60ae-133">Typ in het zoekvak Hallo **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-133">In hello search box, type **TalentLMS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="e60ae-135">Selecteer in het deelvenster resultaten hello, **TalentLMS**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e60ae-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e60ae-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e60ae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e60ae-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met TalentLMS op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e60ae-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e60ae-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TalentLMS is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e60ae-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="e60ae-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TalentLMS toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e60ae-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="e60ae-141">Wijs in TalentLMS, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="e60ae-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e60ae-142">tooconfigure en eenmalige aanmelding Azure AD-test met TalentLMS, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e60ae-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e60ae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e60ae-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e60ae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e60ae-145">**[Maken van een testgebruiker TalentLMS](#creating-a-talentlms-test-user)**  -toohave een equivalent van Britta Simon in TalentLMS die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e60ae-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e60ae-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e60ae-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e60ae-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e60ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e60ae-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e60ae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e60ae-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TalentLMS configureren.</span><span class="sxs-lookup"><span data-stu-id="e60ae-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="e60ae-150">**Azure AD tooconfigure eenmalige aanmelding met TalentLMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e60ae-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60ae-151">In de Azure-portal op Hallo Hallo **TalentLMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e60ae-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e60ae-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="e60ae-155">Op Hallo **TalentLMS domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="e60ae-157">a.</span><span class="sxs-lookup"><span data-stu-id="e60ae-157">a.</span></span> <span data-ttu-id="e60ae-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="e60ae-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="e60ae-159">b.</span><span class="sxs-lookup"><span data-stu-id="e60ae-159">b.</span></span> <span data-ttu-id="e60ae-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="e60ae-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e60ae-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e60ae-161">These values are not real.</span></span> <span data-ttu-id="e60ae-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="e60ae-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e60ae-163">Neem contact op met [TalentLMS Client ondersteuningsteam](https://www.talentlms.com/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e60ae-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="e60ae-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="e60ae-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="e60ae-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e60ae-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e60ae-168">Op Hallo **TalentLMS configuratie** sectie, klikt u op **configureren TalentLMS** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e60ae-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e60ae-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e60ae-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="e60ae-171">In een ander browservenster, meld u aan tooyour TalentLMS bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="e60ae-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="e60ae-172">In Hallo **& Accountinstellingen** sectie, klikt u op Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e60ae-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="e60ae-173">![& Accountinstellingen](./media/active-directory-saas-talentlms-tutorial/IC777296.png "& Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="e60ae-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="e60ae-174">Klik op **eenmalige aanmelding (SSO)**,</span><span class="sxs-lookup"><span data-stu-id="e60ae-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="e60ae-175">Voer in Hallo Single Sign-On sectie, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e60ae-176">![Eenmalige aanmelding](./media/active-directory-saas-talentlms-tutorial/IC777297.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="e60ae-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="e60ae-177">a.</span><span class="sxs-lookup"><span data-stu-id="e60ae-177">a.</span></span> <span data-ttu-id="e60ae-178">Van Hallo **SSO-Integratietype** selecteert **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="e60ae-179">b.</span><span class="sxs-lookup"><span data-stu-id="e60ae-179">b.</span></span> <span data-ttu-id="e60ae-180">In Hallo **identiteitsprovider (IDP)** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e60ae-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e60ae-181">c.</span><span class="sxs-lookup"><span data-stu-id="e60ae-181">c.</span></span> <span data-ttu-id="e60ae-182">Plakken Hallo **vingerafdruk** waarde van de Azure-portal in Hallo **vingerafdruk van certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="e60ae-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="e60ae-183">d.</span><span class="sxs-lookup"><span data-stu-id="e60ae-183">d.</span></span>  <span data-ttu-id="e60ae-184">In Hallo **extern aanmelden URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e60ae-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e60ae-185">e.</span><span class="sxs-lookup"><span data-stu-id="e60ae-185">e.</span></span> <span data-ttu-id="e60ae-186">In Hallo **externe URL voor afmelden** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e60ae-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e60ae-187">f.</span><span class="sxs-lookup"><span data-stu-id="e60ae-187">f.</span></span> <span data-ttu-id="e60ae-188">Vul Hallo volgende in:</span><span class="sxs-lookup"><span data-stu-id="e60ae-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="e60ae-189">In Hallo **TargetedID** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="e60ae-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="e60ae-190">In Hallo **voornaam** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="e60ae-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="e60ae-191">In Hallo **achternaam** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="e60ae-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="e60ae-192">In Hallo **e** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="e60ae-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="e60ae-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="e60ae-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e60ae-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e60ae-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e60ae-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e60ae-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e60ae-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e60ae-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e60ae-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e60ae-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e60ae-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e60ae-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e60ae-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60ae-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e60ae-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e60ae-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e60ae-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e60ae-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e60ae-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e60ae-209">a.</span><span class="sxs-lookup"><span data-stu-id="e60ae-209">a.</span></span> <span data-ttu-id="e60ae-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e60ae-211">b.</span><span class="sxs-lookup"><span data-stu-id="e60ae-211">b.</span></span> <span data-ttu-id="e60ae-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e60ae-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e60ae-213">c.</span><span class="sxs-lookup"><span data-stu-id="e60ae-213">c.</span></span> <span data-ttu-id="e60ae-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e60ae-215">d.</span><span class="sxs-lookup"><span data-stu-id="e60ae-215">d.</span></span> <span data-ttu-id="e60ae-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="e60ae-217">Een testgebruiker TalentLMS maken</span><span class="sxs-lookup"><span data-stu-id="e60ae-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="e60ae-218">Azure AD tooenable gebruikers toolog in tooTalentLMS, ze in TalentLMS moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="e60ae-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="e60ae-219">In geval van TalentLMS Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e60ae-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="e60ae-220">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e60ae-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60ae-221">Meld u bij tooyour **TalentLMS** tenant.</span><span class="sxs-lookup"><span data-stu-id="e60ae-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="e60ae-222">Klik op **gebruikers**, en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="e60ae-223">Op Hallo **gebruiker toevoegen** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e60ae-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e60ae-224">![Gebruiker toevoegen](./media/active-directory-saas-talentlms-tutorial/IC777299.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e60ae-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="e60ae-225">a.</span><span class="sxs-lookup"><span data-stu-id="e60ae-225">a.</span></span> <span data-ttu-id="e60ae-226">In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="e60ae-227">b.</span><span class="sxs-lookup"><span data-stu-id="e60ae-227">b.</span></span> <span data-ttu-id="e60ae-228">In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="e60ae-229">c.</span><span class="sxs-lookup"><span data-stu-id="e60ae-229">c.</span></span> <span data-ttu-id="e60ae-230">In Hallo **e-mailadres** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e60ae-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e60ae-231">d.</span><span class="sxs-lookup"><span data-stu-id="e60ae-231">d.</span></span> <span data-ttu-id="e60ae-232">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="e60ae-233">U kunt andere TalentLMS gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TalentLMS tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e60ae-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e60ae-234">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e60ae-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e60ae-235">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTalentLMS toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="e60ae-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e60ae-237">**tooassign Britta Simon tooTalentLMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e60ae-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60ae-238">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e60ae-240">Selecteer in de lijst met de toepassingen van Hallo **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-240">In hello applications list, select **TalentLMS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="e60ae-242">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e60ae-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e60ae-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e60ae-244">Click **Add** button.</span></span> <span data-ttu-id="e60ae-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e60ae-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e60ae-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e60ae-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e60ae-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e60ae-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e60ae-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e60ae-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e60ae-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e60ae-250">Testing single sign-on</span></span>

<span data-ttu-id="e60ae-251">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="e60ae-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e60ae-252">Als u op Hallo TalentLMS-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TalentLMS toepassing</span><span class="sxs-lookup"><span data-stu-id="e60ae-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e60ae-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e60ae-253">Additional resources</span></span>

* [<span data-ttu-id="e60ae-254">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e60ae-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e60ae-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e60ae-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

