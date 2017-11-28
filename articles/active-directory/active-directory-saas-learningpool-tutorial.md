---
title: 'Zelfstudie: Azure Active Directory-integratie met Learningpool Act | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Learningpool Act.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="0dae8-103">Zelfstudie: Azure Active Directory-integratie met Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="0dae8-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="0dae8-104">In deze zelfstudie leert u hoe toointegrate Learningpool fungeren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0dae8-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dae8-105">Learningpool Act integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dae8-106">U kunt beheren in Azure AD wie toegang tot tooLearningpool Act heeft</span><span class="sxs-lookup"><span data-stu-id="0dae8-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="0dae8-107">U kunt uw gebruikers tooautomatically get aangemelde tooLearningpool Act (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0dae8-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dae8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0dae8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0dae8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0dae8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dae8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0dae8-110">Prerequisites</span></span>

<span data-ttu-id="0dae8-111">Azure AD-integratie met Learningpool Act tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0dae8-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="0dae8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0dae8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dae8-113">Een Learningpool Act eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0dae8-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dae8-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0dae8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dae8-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dae8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0dae8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0dae8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dae8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dae8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0dae8-118">Scenario description</span></span>
<span data-ttu-id="0dae8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0dae8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dae8-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dae8-121">Het toevoegen van Learningpool Act van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0dae8-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="0dae8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0dae8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="0dae8-123">Het toevoegen van Learningpool Act van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0dae8-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="0dae8-124">tooconfigure hello integratie van Learningpool Act in Azure AD, moet u tooadd Learningpool Act uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0dae8-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dae8-125">**tooadd Learningpool Act via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0dae8-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dae8-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0dae8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0dae8-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dae8-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0dae8-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dae8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0dae8-133">Typ in het zoekvak Hallo **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="0dae8-135">Selecteer in het deelvenster resultaten hello, **Learningpool Act**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0dae8-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dae8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0dae8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0dae8-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Learningpool Act op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0dae8-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0dae8-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Learningpool Act is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dae8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="0dae8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Learningpool Act toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0dae8-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="0dae8-141">In de Learningpool Act, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="0dae8-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0dae8-142">tooconfigure en eenmalige aanmelding Azure AD-test met Learningpool Act, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dae8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0dae8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dae8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0dae8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dae8-145">**[Maken van een testgebruiker Learningpool Act](#creating-a-learningpool-act-test-user)**  -toohave een equivalent van Britta Simon in Learningpool Act die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0dae8-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0dae8-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0dae8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dae8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0dae8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dae8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0dae8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dae8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Learningpool Act configureren.</span><span class="sxs-lookup"><span data-stu-id="0dae8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="0dae8-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Learningpool Act, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0dae8-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dae8-151">In de Azure-portal op Hallo Hallo **Learningpool Act** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0dae8-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0dae8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="0dae8-155">Op Hallo **Learningpool Act-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="0dae8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dae8-157">a.</span></span> <span data-ttu-id="0dae8-158">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="0dae8-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="0dae8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dae8-159">b.</span></span> <span data-ttu-id="0dae8-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="0dae8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="0dae8-161">These values are not real.</span></span> <span data-ttu-id="0dae8-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="0dae8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0dae8-163">Neem contact op met [Learningpool Act Client ondersteuningsteam](https://www.Learningpool.com/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="0dae8-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="0dae8-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0dae8-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="0dae8-166">Hallo SAML asserties verwacht Learningpool Act toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="0dae8-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0dae8-167">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="0dae8-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="0dae8-168">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Atrribute'** tabblad van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="0dae8-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="0dae8-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="0dae8-169">hello following screenshot shows an example for this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="0dae8-171">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="0dae8-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0dae8-172">Attribute Name</span></span> | <span data-ttu-id="0dae8-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0dae8-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="0dae8-174">urn: oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="0dae8-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="0dae8-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0dae8-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="0dae8-176">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="0dae8-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="0dae8-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0dae8-177">user.givenname</span></span> |
    | <span data-ttu-id="0dae8-178">urn: oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="0dae8-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="0dae8-179">User.mail</span><span class="sxs-lookup"><span data-stu-id="0dae8-179">user.mail</span></span> |    
    | <span data-ttu-id="0dae8-180">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="0dae8-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="0dae8-181">User.surname</span><span class="sxs-lookup"><span data-stu-id="0dae8-181">user.surname</span></span> |
    
    <span data-ttu-id="0dae8-182">a.</span><span class="sxs-lookup"><span data-stu-id="0dae8-182">a.</span></span> <span data-ttu-id="0dae8-183">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dae8-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0dae8-186">b.</span><span class="sxs-lookup"><span data-stu-id="0dae8-186">b.</span></span> <span data-ttu-id="0dae8-187">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="0dae8-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="0dae8-188">c.</span><span class="sxs-lookup"><span data-stu-id="0dae8-188">c.</span></span> <span data-ttu-id="0dae8-189">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="0dae8-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="0dae8-190">d.</span><span class="sxs-lookup"><span data-stu-id="0dae8-190">d.</span></span> <span data-ttu-id="0dae8-191">Hallo laat **Namespace** leeg.</span><span class="sxs-lookup"><span data-stu-id="0dae8-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="0dae8-192">e.</span><span class="sxs-lookup"><span data-stu-id="0dae8-192">e.</span></span> <span data-ttu-id="0dae8-193">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-193">Click **Ok**.</span></span>

7. <span data-ttu-id="0dae8-194">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0dae8-194">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0dae8-196">tooconfigure eenmalige aanmelding op **Learningpool Act** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Learningpool Act-ondersteuningsteam](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="0dae8-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="0dae8-197">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0dae8-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0dae8-198">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="0dae8-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0dae8-199">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="0dae8-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0dae8-200">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0dae8-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dae8-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0dae8-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="0dae8-202">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0dae8-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0dae8-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0dae8-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dae8-205">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0dae8-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dae8-207">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dae8-209">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0dae8-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dae8-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0dae8-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dae8-213">a.</span><span class="sxs-lookup"><span data-stu-id="0dae8-213">a.</span></span> <span data-ttu-id="0dae8-214">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dae8-215">b.</span><span class="sxs-lookup"><span data-stu-id="0dae8-215">b.</span></span> <span data-ttu-id="0dae8-216">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0dae8-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dae8-217">c.</span><span class="sxs-lookup"><span data-stu-id="0dae8-217">c.</span></span> <span data-ttu-id="0dae8-218">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0dae8-219">d.</span><span class="sxs-lookup"><span data-stu-id="0dae8-219">d.</span></span> <span data-ttu-id="0dae8-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="0dae8-221">Maken van een testgebruiker Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="0dae8-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="0dae8-222">Azure AD tooenable gebruikers toolog in tooLearningpool Act, ze in Learningpool Act moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="0dae8-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="0dae8-223">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="0dae8-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="0dae8-224">Gebruikers moeten toobe gemaakt door uw [Learningpool Act-ondersteuningsteam](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="0dae8-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="0dae8-225">U kunt andere Learningpool Act gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Learningpool Act tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="0dae8-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0dae8-226">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dae8-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0dae8-227">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="0dae8-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0dae8-229">**tooassign Britta Simon tooLearningpool Act, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0dae8-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dae8-230">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0dae8-232">Selecteer in de lijst met de toepassingen van Hallo **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="0dae8-234">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0dae8-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0dae8-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0dae8-236">Click **Add** button.</span></span> <span data-ttu-id="0dae8-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dae8-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0dae8-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0dae8-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dae8-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dae8-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dae8-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dae8-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dae8-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0dae8-242">Testing single sign-on</span></span>

<span data-ttu-id="0dae8-243">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="0dae8-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0dae8-244">Als u op Hallo Learningpool Act-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Learningpool Act-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0dae8-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0dae8-245">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0dae8-245">Additional resources</span></span>

* [<span data-ttu-id="0dae8-246">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0dae8-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dae8-247">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0dae8-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

