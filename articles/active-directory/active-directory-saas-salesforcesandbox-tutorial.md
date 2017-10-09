---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="fbeeb-103">Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="fbeeb-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="fbeeb-104">In deze zelfstudie leert u hoe toointegrate Salesforce Sandbox met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbeeb-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbeeb-105">Salesforce Sandbox integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbeeb-106">U kunt beheren in Azure AD wie toegang tot tooSalesforce Sandbox heeft</span><span class="sxs-lookup"><span data-stu-id="fbeeb-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="fbeeb-107">U kunt uw gebruikers tooautomatically get aangemelde tooSalesforce Sandbox (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="fbeeb-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbeeb-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fbeeb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fbeeb-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbeeb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbeeb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fbeeb-110">Prerequisites</span></span>

<span data-ttu-id="fbeeb-111">Azure AD-integratie met Salesforce Sandbox tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="fbeeb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fbeeb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbeeb-113">Een Salesforce Sandbox eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fbeeb-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbeeb-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbeeb-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbeeb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbeeb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbeeb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbeeb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fbeeb-118">Scenario description</span></span>
<span data-ttu-id="fbeeb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbeeb-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbeeb-121">Het toevoegen van Salesforce Sandbox van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fbeeb-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="fbeeb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fbeeb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="fbeeb-123">Het toevoegen van Salesforce Sandbox van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fbeeb-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="fbeeb-124">tooconfigure hello integratie van Salesforce Sandbox in Azure AD, moet u tooadd Salesforce Sandbox uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbeeb-125">**tooadd Salesforce Sandbox via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbeeb-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbeeb-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbeeb-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbeeb-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="fbeeb-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="fbeeb-133">Typ in het zoekvak Hallo **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="fbeeb-135">Selecteer in het deelvenster resultaten hello, **Salesforce Sandbox**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbeeb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fbeeb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbeeb-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Salesforce-Sandbox op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="fbeeb-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fbeeb-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Salesforce Sandbox is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="fbeeb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Salesforce Sandbox toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="fbeeb-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="fbeeb-142">tooconfigure en eenmalige aanmelding Azure AD-test met Salesforce Sandbox, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbeeb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbeeb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbeeb-145">**[Maken van een testgebruiker Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave een equivalent van Britta Simon in Salesforce Sandbox die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbeeb-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbeeb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbeeb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fbeeb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbeeb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Salesforce-Sandbox-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="fbeeb-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Salesforce-Sandbox Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbeeb-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbeeb-151">In Azure-portal op Hallo Hallo **Salesforce Sandbox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fbeeb-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="fbeeb-155">Op Hallo **Salesforce sandbox-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="fbeeb-157">In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="fbeeb-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbeeb-158">Deze waarde is geen echte Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-158">This value is not hello real.</span></span> <span data-ttu-id="fbeeb-159">Deze waarde bijwerken met Hallo werkelijke aanmeldings-URL. Neem contact op met [Salesforce Sandbox Client ondersteuningsteam](https://help.salesforce.com/support) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="fbeeb-160">Als u al eenmalige aanmelding voor een ander exemplaar van Salesforce Sandbox hebt geconfigureerd in uw directory, dan moet u ook Hallo configureren **id** toohave dezelfde waarde als Hallo Hallo **aanmelden URL**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="fbeeb-161">Hallo **id** veld kan worden gevonden door te controleren Hallo **weergeven geavanceerde instellingen** selectievakje op Hallo **App-URL configureren** van Hallo menu</span><span class="sxs-lookup"><span data-stu-id="fbeeb-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="fbeeb-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="fbeeb-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-164">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="fbeeb-166">Op Hallo **Salesforce Sandbox configuratie** sectie, klikt u op **Salesforce Sandbox configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbeeb-167">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="fbeeb-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="fbeeb-168">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="fbeeb-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="fbeeb-169">Een nieuw tabblad openen in uw browser en meld u bij tooyour Salesforce Sandbox administrator-account.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="fbeeb-170">Klik in het menu bovenaan Hallo Hallo **Setup**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="fbeeb-172">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="fbeeb-174">Voer op Hallo sectie instellingen voor eenmalige aanmelding, Hallo stappen te volgen: ![configureren eenmalige aanmelding](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="fbeeb-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="fbeeb-175">a.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-175">a.</span></span>  <span data-ttu-id="fbeeb-176">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="fbeeb-177">b.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-177">b.</span></span>  <span data-ttu-id="fbeeb-178">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-178">Click **New**.</span></span>

12. <span data-ttu-id="fbeeb-179">Op Hallo SAML Single Sign-On zoekinstellingen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="fbeeb-181">a.In hello naam textbox, Hallo typenaam van Hallo-configuratie (bijvoorbeeld: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="fbeeb-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="fbeeb-182">b.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-182">b.</span></span> <span data-ttu-id="fbeeb-183">Plakken **SMAL entiteit-ID** waarde in Hallo **verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="fbeeb-184">c.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-184">c.</span></span> <span data-ttu-id="fbeeb-185">In Hallo **entiteit-Id** textbox type **https://test.salesforce.com** als het eerste exemplaar van Salesforce Sandbox toe te voegen tooyour directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="fbeeb-186">Als u al een exemplaar van Salesforce Sandbox, moet u voor Hallo hebt toegevoegd **entiteit-ID** type in Hallo **aanmelding op URL**, die moet worden in deze indeling:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="fbeeb-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="fbeeb-187">d.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-187">d.</span></span> <span data-ttu-id="fbeeb-188">Klik op **Bladeren** tooupload Hallo certificaat gedownload.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="fbeeb-189">e.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-189">e.</span></span> <span data-ttu-id="fbeeb-190">Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="fbeeb-191">f.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-191">f.</span></span> <span data-ttu-id="fbeeb-192">Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentifier element van Hallo onderwerp instructie**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="fbeeb-193">g.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-193">g.</span></span> <span data-ttu-id="fbeeb-194">Plakken **Single Sign-On Service-URL** in Hallo **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="fbeeb-195">h.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-195">h.</span></span> <span data-ttu-id="fbeeb-196">SFDC biedt geen ondersteuning voor SAML-afmelden.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="fbeeb-197">Als een tijdelijke oplossing 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' te plakken in Hallo **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="fbeeb-198">ik.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-198">i.</span></span> <span data-ttu-id="fbeeb-199">Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="fbeeb-200">j.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-200">j.</span></span> <span data-ttu-id="fbeeb-201">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="fbeeb-202">Uw domein inschakelen</span><span class="sxs-lookup"><span data-stu-id="fbeeb-202">Enable your domain</span></span>
<span data-ttu-id="fbeeb-203">Deze sectie wordt ervan uitgegaan dat u al hebt gemaakt een domein.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="fbeeb-204">Zie voor meer informatie [definiëren van uw domeinnaam](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="fbeeb-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="fbeeb-205">**tooenable uw domein Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="fbeeb-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbeeb-206">Klik in het Hallo navigatiedeelvenster links op **domeinbeheer**, en klik vervolgens op **mijn domein.**</span><span class="sxs-lookup"><span data-stu-id="fbeeb-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="fbeeb-208">Zorg dat uw domein correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="fbeeb-209">In Hallo **aanmelding paginainstellingen** sectie, klikt u op **bewerken**, naarmate **verificatieservice**, selecteer Hallo-naam van Hallo SAML Single Sign-On-instelling van de vorige Hallo sectie en ten slotte op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="fbeeb-211">Als u een domein geconfigureerd hebt, moeten uw gebruikers Hallo domein URL toologin toohello Salesforce sandbox gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="fbeeb-212">tooget Hallo waarde van de URL van de hello, klikt u op Hallo SSO profiel die u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="fbeeb-213">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbeeb-214">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbeeb-215">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbeeb-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbeeb-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fbeeb-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbeeb-217">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fbeeb-219">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbeeb-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbeeb-220">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbeeb-222">toodisplay hello lijst met gebruikers te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbeeb-224">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbeeb-226">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbeeb-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbeeb-228">a.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-228">a.</span></span> <span data-ttu-id="fbeeb-229">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbeeb-230">b.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-230">b.</span></span> <span data-ttu-id="fbeeb-231">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbeeb-232">c.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-232">c.</span></span> <span data-ttu-id="fbeeb-233">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fbeeb-234">d.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-234">d.</span></span> <span data-ttu-id="fbeeb-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="fbeeb-236">Maken van een testgebruiker Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="fbeeb-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="fbeeb-237">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="fbeeb-238">SalesForce Sandbox ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="fbeeb-239">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-239">There is no action item for you in this section.</span></span> <span data-ttu-id="fbeeb-240">Als een gebruiker in Salesforce Sandbox nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess Salesforce Sandbox probeert.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fbeeb-241">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbeeb-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fbeeb-242">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fbeeb-244">**tooassign Britta Simon tooSalesforce Sandbox, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbeeb-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbeeb-245">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fbeeb-247">Selecteer in de lijst met de toepassingen van Hallo **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="fbeeb-249">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="fbeeb-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-251">Click **Add** button.</span></span> <span data-ttu-id="fbeeb-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="fbeeb-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbeeb-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbeeb-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbeeb-257">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fbeeb-257">Testing single sign-on</span></span>

<span data-ttu-id="fbeeb-258">Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="fbeeb-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="fbeeb-259">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbeeb-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbeeb-260">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fbeeb-260">Additional resources</span></span>

* [<span data-ttu-id="fbeeb-261">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbeeb-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbeeb-262">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbeeb-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fbeeb-263">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="fbeeb-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

