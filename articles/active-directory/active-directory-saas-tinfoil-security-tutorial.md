---
title: 'Zelfstudie: Azure Active Directory-integratie met TINFOIL SECURITY | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TINFOIL SECURITY.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="b52b2-103">Zelfstudie: Azure Active Directory-integratie met TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="b52b2-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="b52b2-104">In deze zelfstudie leert u hoe toointegrate TINFOIL SECURITY met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b52b2-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b52b2-105">TINFOIL SECURITY integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b52b2-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b52b2-106">U kunt beheren in Azure AD wie toegang tot tooTINFOIL beveiliging heeft</span><span class="sxs-lookup"><span data-stu-id="b52b2-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="b52b2-107">U kunt uw gebruikers tooautomatically get aangemelde tooTINFOIL beveiliging (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b52b2-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b52b2-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b52b2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b52b2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b52b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b52b2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b52b2-110">Prerequisites</span></span>

<span data-ttu-id="b52b2-111">Azure AD-integratie met TINFOIL SECURITY tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b52b2-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="b52b2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b52b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b52b2-113">Een TINFOIL SECURITY eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b52b2-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b52b2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b52b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b52b2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b52b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b52b2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b52b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b52b2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b52b2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b52b2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b52b2-118">Scenario description</span></span>
<span data-ttu-id="b52b2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b52b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b52b2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b52b2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b52b2-121">TINFOIL SECURITY van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b52b2-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="b52b2-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b52b2-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="b52b2-123">TINFOIL SECURITY van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b52b2-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="b52b2-124">tooconfigure hello integratie van TINFOIL SECURITY in Azure AD, moet u tooadd TINFOIL SECURITY uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b52b2-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b52b2-125">**TINFOIL SECURITY via Hallo gallery tooadd uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b52b2-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b52b2-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b52b2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b52b2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b52b2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b52b2-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b52b2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b52b2-133">Typ in het zoekvak Hallo **TINFOIL SECURITY**, selecteer **TINFOIL SECURITY** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b52b2-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TINFOIL SECURITY vanuit galerie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b52b2-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b52b2-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b52b2-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met TINFOIL SECURITY op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b52b2-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b52b2-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TINFOIL SECURITY is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b52b2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="b52b2-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TINFOIL SECURITY toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b52b2-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="b52b2-139">Wijs in TINFOIL SECURITY Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="b52b2-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b52b2-140">tooconfigure en test eenmalige aanmelding Azure AD met behulp van TINFOIL SECURITY, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b52b2-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b52b2-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b52b2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b52b2-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b52b2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b52b2-143">**[Maak een testgebruiker TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave een equivalent van Britta Simon in TINFOIL SECURITY die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b52b2-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b52b2-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b52b2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b52b2-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b52b2-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b52b2-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b52b2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b52b2-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TINFOIL SECURITY configureren.</span><span class="sxs-lookup"><span data-stu-id="b52b2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="b52b2-148">**Voer tooconfigure Azure AD eenmalige aanmelding met TINFOIL SECURITY Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b52b2-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="b52b2-149">In de Azure-portal op Hallo Hallo **TINFOIL SECURITY** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b52b2-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b52b2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML op basis van eenmalige aanmelding](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="b52b2-153">Op Hallo **TINFOIL SECURITY domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="b52b2-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="b52b2-155">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde.</span><span class="sxs-lookup"><span data-stu-id="b52b2-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="b52b2-157">Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b52b2-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="b52b2-158">![Kenmerken](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b52b2-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="b52b2-159">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b52b2-159">Attribute Name</span></span>    |   <span data-ttu-id="b52b2-160">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b52b2-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="b52b2-161">AccountId</span><span class="sxs-lookup"><span data-stu-id="b52b2-161">accountid</span></span> | <span data-ttu-id="b52b2-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="b52b2-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="b52b2-163">a.</span><span class="sxs-lookup"><span data-stu-id="b52b2-163">a.</span></span> <span data-ttu-id="b52b2-164">Klik op **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="b52b2-165">![Kenmerk toevoegen](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b52b2-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="b52b2-166">![Kenmerk toevoegen](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b52b2-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="b52b2-167">b.</span><span class="sxs-lookup"><span data-stu-id="b52b2-167">b.</span></span> <span data-ttu-id="b52b2-168">In Hallo **kenmerknaam** textbox type **accountid**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="b52b2-169">c.</span><span class="sxs-lookup"><span data-stu-id="b52b2-169">c.</span></span> <span data-ttu-id="b52b2-170">In Hallo **kenmerkwaarde** textbox plakken Hallo account id-waarde die u later op Hallo zelfstudie krijgt.</span><span class="sxs-lookup"><span data-stu-id="b52b2-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="b52b2-171">d.</span><span class="sxs-lookup"><span data-stu-id="b52b2-171">d.</span></span> <span data-ttu-id="b52b2-172">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="b52b2-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b52b2-173">Click **Save** button.</span></span>

    ![knop Opslaan](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b52b2-175">Op Hallo **TINFOIL SECURITY Configuration** sectie, klikt u op **TINFOIL SECURITY configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b52b2-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b52b2-176">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b52b2-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TINFOIL SECURITY Configuration](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="b52b2-178">In een ander browservenster, meld u bij uw bedrijf TINFOIL SECURITY site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b52b2-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="b52b2-179">Klik in de werkbalk bovenaan Hallo Hallo op **Mijn Account**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="b52b2-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="b52b2-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="b52b2-181">Klik op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-181">Click **Security**.</span></span>
   
    <span data-ttu-id="b52b2-182">![Beveiliging](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="b52b2-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="b52b2-183">Op Hallo **Single Sign-On** configuratie pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b52b2-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b52b2-184">![Eenmalige aanmelding](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="b52b2-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="b52b2-185">a.</span><span class="sxs-lookup"><span data-stu-id="b52b2-185">a.</span></span> <span data-ttu-id="b52b2-186">Selecteer **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="b52b2-187">b.</span><span class="sxs-lookup"><span data-stu-id="b52b2-187">b.</span></span> <span data-ttu-id="b52b2-188">Klik op **handmatige configuratie**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="b52b2-189">c.</span><span class="sxs-lookup"><span data-stu-id="b52b2-189">c.</span></span> <span data-ttu-id="b52b2-190">In **SAML Post URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b52b2-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="b52b2-191">d.</span><span class="sxs-lookup"><span data-stu-id="b52b2-191">d.</span></span> <span data-ttu-id="b52b2-192">In **SAML certificaat vingerafdruk** textbox plakken Hallo-waarde van **vingerafdruk** die u hebt gekopieerd uit **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="b52b2-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="b52b2-193">e.</span><span class="sxs-lookup"><span data-stu-id="b52b2-193">e.</span></span> <span data-ttu-id="b52b2-194">Kopiëren **uw Account-ID** waarde en plak Hallo-waarde in **kenmerkwaarde** textbox onder **kenmerk toevoegen** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b52b2-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="b52b2-195">f.</span><span class="sxs-lookup"><span data-stu-id="b52b2-195">f.</span></span> <span data-ttu-id="b52b2-196">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b52b2-197">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b52b2-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b52b2-198">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b52b2-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b52b2-199">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b52b2-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b52b2-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b52b2-200">Create an Azure AD test user</span></span>
<span data-ttu-id="b52b2-201">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b52b2-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b52b2-203">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b52b2-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b52b2-204">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b52b2-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b52b2-206">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="b52b2-207">Gebruikers en groepen -> alle gebruikers</span><span class="sxs-lookup"><span data-stu-id="b52b2-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b52b2-208">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b52b2-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Gebruiker](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b52b2-210">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b52b2-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b52b2-212">a.</span><span class="sxs-lookup"><span data-stu-id="b52b2-212">a.</span></span> <span data-ttu-id="b52b2-213">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b52b2-214">b.</span><span class="sxs-lookup"><span data-stu-id="b52b2-214">b.</span></span> <span data-ttu-id="b52b2-215">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b52b2-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b52b2-216">c.</span><span class="sxs-lookup"><span data-stu-id="b52b2-216">c.</span></span> <span data-ttu-id="b52b2-217">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b52b2-218">d.</span><span class="sxs-lookup"><span data-stu-id="b52b2-218">d.</span></span> <span data-ttu-id="b52b2-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="b52b2-220">Een testgebruiker TINFOIL SECURITY maken</span><span class="sxs-lookup"><span data-stu-id="b52b2-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="b52b2-221">In volgorde tooenable Azure AD gebruikers toolog in TINFOIL SECURITY, moeten ze worden ingericht in TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="b52b2-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="b52b2-222">In geval van TINFOIL SECURITY Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b52b2-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="b52b2-223">**een gebruiker die zijn ingericht, tooget uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b52b2-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="b52b2-224">Als het Hallo-gebruiker deel uitmaakt van een Enterprise-account, moet u deze te[Neem contact op met het ondersteuningsteam van Hallo TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact) tooget Hallo-gebruikersaccount is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b52b2-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="b52b2-225">Als Hallo gebruiker een gewone TINFOIL SECURITY SaaS-gebruiker, kan Hallo gebruiker een tooany medewerker van de gebruiker van het Hallo-sites toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b52b2-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="b52b2-226">Deze triggers een proces toosend een uitnodiging toohello opgegeven e-toocreate een nieuw TINFOIL SECURITY-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="b52b2-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="b52b2-227">U kunt andere TINFOIL SECURITY gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TINFOIL SECURITY tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="b52b2-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b52b2-228">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b52b2-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b52b2-229">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTINFOIL beveiliging.</span><span class="sxs-lookup"><span data-stu-id="b52b2-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b52b2-231">**tooassign Britta Simon tooTINFOIL beveiliging, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b52b2-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="b52b2-232">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b52b2-234">Selecteer in de lijst met de toepassingen van Hallo **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![TINFOIL SECURITY selecteren](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="b52b2-236">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b52b2-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b52b2-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b52b2-238">Click **Add** button.</span></span> <span data-ttu-id="b52b2-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b52b2-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b52b2-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b52b2-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b52b2-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b52b2-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b52b2-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b52b2-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b52b2-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b52b2-244">Test single sign-on</span></span>

<span data-ttu-id="b52b2-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b52b2-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b52b2-246">Als u op Hallo TINFOIL SECURITY-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TINFOIL SECURITY-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b52b2-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="b52b2-247">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b52b2-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b52b2-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b52b2-248">Additional resources</span></span>

* [<span data-ttu-id="b52b2-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b52b2-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b52b2-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b52b2-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

