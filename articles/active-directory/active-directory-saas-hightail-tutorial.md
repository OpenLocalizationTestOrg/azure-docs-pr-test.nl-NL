---
title: 'Zelfstudie: Azure Active Directory-integratie met Hightail | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="7cf6f-103">Zelfstudie: Azure Active Directory-integratie met Hightail</span><span class="sxs-lookup"><span data-stu-id="7cf6f-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="7cf6f-104">In deze zelfstudie leert u hoe toointegrate Hightail met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7cf6f-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cf6f-105">Hightail integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7cf6f-106">U kunt beheren in Azure AD die tooHightail toegang heeft</span><span class="sxs-lookup"><span data-stu-id="7cf6f-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="7cf6f-107">U kunt uw gebruikers tooautomatically get aangemelde tooHightail (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7cf6f-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7cf6f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7cf6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7cf6f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7cf6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cf6f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7cf6f-110">Prerequisites</span></span>

<span data-ttu-id="7cf6f-111">Azure AD-integratie met Hightail tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="7cf6f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7cf6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7cf6f-113">Een Hightail eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7cf6f-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cf6f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cf6f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cf6f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cf6f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7cf6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cf6f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7cf6f-118">Scenario description</span></span>
<span data-ttu-id="7cf6f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cf6f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cf6f-121">Het toevoegen van Hightail van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7cf6f-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="7cf6f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cf6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="7cf6f-123">Het toevoegen van Hightail van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7cf6f-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="7cf6f-124">tooconfigure hello integratie van Hightail in Azure AD, moet u tooadd Hightail uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7cf6f-125">**tooadd Hightail via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7cf6f-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cf6f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7cf6f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7cf6f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7cf6f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7cf6f-133">Typ in het zoekvak Hallo **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-133">In hello search box, type **Hightail**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="7cf6f-135">Selecteer in het deelvenster resultaten hello, **Hightail**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7cf6f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cf6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7cf6f-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Hightail op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7cf6f-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Hightail is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="7cf6f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Hightail toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="7cf6f-141">Wijs in Hightail, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7cf6f-142">tooconfigure en eenmalige aanmelding Azure AD-test met Hightail, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7cf6f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7cf6f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7cf6f-145">**[Maken van een testgebruiker Hightail](#creating-a-hightail-test-user)**  -toohave een equivalent van Britta Simon in Hightail die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7cf6f-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7cf6f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7cf6f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7cf6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7cf6f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Hightail configureren.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="7cf6f-150">**Azure AD tooconfigure eenmalige aanmelding met Hightail, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7cf6f-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cf6f-151">In de Azure-portal op Hallo Hallo **Hightail** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7cf6f-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="7cf6f-155">Op Hallo **Hightail domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="7cf6f-157">In Hallo **antwoord-URL** textbox type Hallo URL als:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="7cf6f-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7cf6f-158">Hallo voorgaande waarde is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-158">hello preceding value is not real value.</span></span> <span data-ttu-id="7cf6f-159">Hallo-waarde wordt bijgewerkt met Hallo werkelijke antwoord-URL, die verderop in Hallo zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="7cf6f-160">Op Hallo **Hightail domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="7cf6f-162">a.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-162">a.</span></span> <span data-ttu-id="7cf6f-163">Klik op Hallo **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="7cf6f-164">b.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-164">b.</span></span> <span data-ttu-id="7cf6f-165">In Hallo **aanmelding op URL** textbox type Hallo URL als:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="7cf6f-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="7cf6f-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="7cf6f-168">Hightail toepassing hello SAML asserties verwacht in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7cf6f-169">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="7cf6f-170">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Atrribute'** tabblad van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="7cf6f-171">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-171">hello following screenshot shows an example for this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="7cf6f-173">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7cf6f-174">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7cf6f-174">Attribute Name</span></span> | <span data-ttu-id="7cf6f-175">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7cf6f-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="7cf6f-176">Voornaam</span><span class="sxs-lookup"><span data-stu-id="7cf6f-176">FirstName</span></span> | <span data-ttu-id="7cf6f-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="7cf6f-177">user.givenname</span></span> |
    | <span data-ttu-id="7cf6f-178">Achternaam</span><span class="sxs-lookup"><span data-stu-id="7cf6f-178">LastName</span></span> | <span data-ttu-id="7cf6f-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="7cf6f-179">user.surname</span></span> |
    | <span data-ttu-id="7cf6f-180">E-mail</span><span class="sxs-lookup"><span data-stu-id="7cf6f-180">Email</span></span> | <span data-ttu-id="7cf6f-181">User.mail</span><span class="sxs-lookup"><span data-stu-id="7cf6f-181">user.mail</span></span> |    
    | <span data-ttu-id="7cf6f-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="7cf6f-182">UserIdentity</span></span> | <span data-ttu-id="7cf6f-183">User.mail</span><span class="sxs-lookup"><span data-stu-id="7cf6f-183">user.mail</span></span> |
    
    <span data-ttu-id="7cf6f-184">a.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-184">a.</span></span> <span data-ttu-id="7cf6f-185">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="7cf6f-188">b.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-188">b.</span></span> <span data-ttu-id="7cf6f-189">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7cf6f-190">c.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-190">c.</span></span> <span data-ttu-id="7cf6f-191">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="7cf6f-192">d.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-192">d.</span></span> <span data-ttu-id="7cf6f-193">Hallo laat **Namespace** leeg.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="7cf6f-194">e.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-194">e.</span></span> <span data-ttu-id="7cf6f-195">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-195">Click **Ok**.</span></span>

7. <span data-ttu-id="7cf6f-196">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-196">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7cf6f-198">Op Hallo **Hightail configuratie** sectie, klikt u op **configureren Hightail** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7cf6f-199">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7cf6f-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="7cf6f-201">Voordat u configureert Hallo eenmalige aanmelding op Hightail app, kunt witte lijst uw e-maildomein met Hightail team, zodat alle gebruikers met dit domein Hallo gebruik functionaliteit voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="7cf6f-202">tooget SSO is geconfigureerd voor uw toepassing, moet u toosign op tooyour Hightail tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="7cf6f-203">a.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-203">a.</span></span> <span data-ttu-id="7cf6f-204">Klik op Hallo in het menu bovenaan Hallo Hallo **Account** tabblad en selecteer **SAML configureren**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="7cf6f-206">b.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-206">b.</span></span> <span data-ttu-id="7cf6f-207">Schakel dit selectievakje in Hallo van **SAML-verificatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="7cf6f-209">c.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-209">c.</span></span> <span data-ttu-id="7cf6f-210">De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **handtekeningcertificaat van SAML-Token** textbox.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="7cf6f-212">d.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-212">d.</span></span> <span data-ttu-id="7cf6f-213">In Hallo **SAML-instantie (id-Provider)** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="7cf6f-215">e.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-215">e.</span></span> <span data-ttu-id="7cf6f-216">Als u wilt dat tooconfigure Hallo toepassing in **IDP geïnitieerd modus** selecteren **'Identiteitsprovider (IdP) geïnitieerd aanmelden'**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="7cf6f-217">Als **SP geïnitieerd modus** Selecteer **'Serviceprovider (SP) geïnitieerd aanmelden'**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="7cf6f-219">f.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-219">f.</span></span> <span data-ttu-id="7cf6f-220">Hallo SAML consumer-URL voor uw exemplaar Kopieer en plak deze in **antwoord-URL** textbox in **Hightail domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="7cf6f-221">g.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-221">g.</span></span> <span data-ttu-id="7cf6f-222">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7cf6f-223">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7cf6f-224">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7cf6f-225">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7cf6f-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7cf6f-226">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7cf6f-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="7cf6f-227">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7cf6f-229">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7cf6f-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cf6f-230">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7cf6f-232">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7cf6f-234">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7cf6f-236">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7cf6f-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7cf6f-238">a.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-238">a.</span></span> <span data-ttu-id="7cf6f-239">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cf6f-240">b.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-240">b.</span></span> <span data-ttu-id="7cf6f-241">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7cf6f-242">c.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-242">c.</span></span> <span data-ttu-id="7cf6f-243">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7cf6f-244">d.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-244">d.</span></span> <span data-ttu-id="7cf6f-245">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="7cf6f-246">Een testgebruiker Hightail maken</span><span class="sxs-lookup"><span data-stu-id="7cf6f-246">Creating a Hightail test user</span></span>

<span data-ttu-id="7cf6f-247">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Hightail van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="7cf6f-248">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-248">There is no action item for you in this section.</span></span> <span data-ttu-id="7cf6f-249">Hightail ondersteunt just in time gebruikers inrichten op basis van Hallo aangepaste claims.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="7cf6f-250">Als u aangepaste claims Hallo hebt geconfigureerd, zoals wordt weergegeven in de sectie Hallo  **[eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on)**  , een gebruiker is gemaakt in Hallo toepassing nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="7cf6f-251">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Hightail ondersteuningsteam](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="7cf6f-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7cf6f-252">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cf6f-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7cf6f-253">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHightail toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7cf6f-255">**tooassign Britta Simon tooHightail, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7cf6f-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cf6f-256">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7cf6f-258">Selecteer in de lijst met de toepassingen van Hallo **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-258">In hello applications list, select **Hightail**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="7cf6f-260">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7cf6f-262">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-262">Click **Add** button.</span></span> <span data-ttu-id="7cf6f-263">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7cf6f-265">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7cf6f-266">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cf6f-267">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7cf6f-268">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7cf6f-268">Testing single sign-on</span></span>

<span data-ttu-id="7cf6f-269">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7cf6f-270">Als u op Hallo Hightail tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Hightail toepassing.</span><span class="sxs-lookup"><span data-stu-id="7cf6f-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7cf6f-271">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7cf6f-271">Additional resources</span></span>

* [<span data-ttu-id="7cf6f-272">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cf6f-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7cf6f-273">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7cf6f-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

