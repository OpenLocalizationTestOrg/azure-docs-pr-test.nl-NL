---
title: 'Zelfstudie: Azure Active Directory-integratie met Druva | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Druva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="7ea65-103">Zelfstudie: Azure Active Directory-integratie met Druva</span><span class="sxs-lookup"><span data-stu-id="7ea65-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="7ea65-104">In deze zelfstudie leert u hoe toointegrate Druva met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ea65-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ea65-105">Druva integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ea65-106">U kunt beheren in Azure AD die tooDruva toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="7ea65-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="7ea65-107">U kunt uw gebruikers tooautomatically get aangemelde tooDruva (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7ea65-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7ea65-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="7ea65-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7ea65-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ea65-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ea65-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7ea65-110">Prerequisites</span></span>

<span data-ttu-id="7ea65-111">Azure AD-integratie met Druva tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7ea65-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="7ea65-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7ea65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ea65-113">Een Druva eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7ea65-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ea65-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7ea65-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ea65-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ea65-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7ea65-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ea65-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ea65-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ea65-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7ea65-118">Scenario description</span></span>
<span data-ttu-id="7ea65-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7ea65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ea65-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ea65-121">Het toevoegen van Druva van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7ea65-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="7ea65-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7ea65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="7ea65-123">Het toevoegen van Druva van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7ea65-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="7ea65-124">tooconfigure hello integratie van Druva in Azure AD, moet u tooadd Druva uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7ea65-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ea65-125">**tooadd Druva via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7ea65-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea65-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7ea65-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="7ea65-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ea65-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="7ea65-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ea65-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="7ea65-133">Typ in het zoekvak Hallo **Druva**, selecteer **Druva** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ea65-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Druva in de lijst met resultaten Hallo](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7ea65-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ea65-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7ea65-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Druva op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7ea65-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ea65-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Druva is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ea65-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="7ea65-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Druva toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7ea65-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="7ea65-139">Wijs in Druva, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7ea65-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7ea65-140">tooconfigure en eenmalige aanmelding Azure AD-test met Druva, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ea65-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7ea65-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ea65-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ea65-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ea65-143">**[Maak een testgebruiker Druva](#create-a-druva-test-user)**  -toohave een equivalent van Britta Simon in Druva die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7ea65-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ea65-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7ea65-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ea65-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7ea65-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7ea65-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7ea65-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7ea65-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Druva configureren.</span><span class="sxs-lookup"><span data-stu-id="7ea65-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="7ea65-148">**Azure AD tooconfigure eenmalige aanmelding met Druva, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7ea65-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea65-149">In de Azure-portal op Hallo Hallo **Druva** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7ea65-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7ea65-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="7ea65-153">Op Hallo **Druva domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="7ea65-155">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="7ea65-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="7ea65-156">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7ea65-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="7ea65-158">Uw toepassing Druva Hallo SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **SAML-Token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="7ea65-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="7ea65-160">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="7ea65-161">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7ea65-161">Attribute Name</span></span>      | <span data-ttu-id="7ea65-162">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7ea65-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="7ea65-163">synchroon\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="7ea65-163">insync\_auth\_token</span></span> |<span data-ttu-id="7ea65-164">Voer Hallo token gegenereerde waarde</span><span class="sxs-lookup"><span data-stu-id="7ea65-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="7ea65-165">a.</span><span class="sxs-lookup"><span data-stu-id="7ea65-165">a.</span></span> <span data-ttu-id="7ea65-166">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ea65-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="7ea65-169">b.</span><span class="sxs-lookup"><span data-stu-id="7ea65-169">b.</span></span> <span data-ttu-id="7ea65-170">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7ea65-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7ea65-171">c.</span><span class="sxs-lookup"><span data-stu-id="7ea65-171">c.</span></span> <span data-ttu-id="7ea65-172">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7ea65-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="7ea65-173">Hallo token gegenereerde waarde wordt verderop in de zelfstudie beschreven.</span><span class="sxs-lookup"><span data-stu-id="7ea65-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="7ea65-174">d.</span><span class="sxs-lookup"><span data-stu-id="7ea65-174">d.</span></span> <span data-ttu-id="7ea65-175">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="7ea65-176">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7ea65-176">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7ea65-178">Op Hallo **Druva configuratie** sectie, klikt u op **configureren Druva** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7ea65-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7ea65-179">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7ea65-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="7ea65-181">In een ander browservenster, meld u aan tooyour Druva bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="7ea65-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="7ea65-182">Ga te**beheren \> instellingen**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="7ea65-183">![Instellingen](./media/active-directory-saas-druva-tutorial/ic795091.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="7ea65-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="7ea65-184">Voer in het dialoogvenster van de instellingen voor eenmalige aanmelding hello, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="7ea65-185">![Eenmalige aanmelding instellingen](./media/active-directory-saas-druva-tutorial/ic795092.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="7ea65-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="7ea65-186">a.</span><span class="sxs-lookup"><span data-stu-id="7ea65-186">a.</span></span> <span data-ttu-id="7ea65-187">Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **ID-Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="7ea65-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="7ea65-188">b.</span><span class="sxs-lookup"><span data-stu-id="7ea65-188">b.</span></span> <span data-ttu-id="7ea65-189">Plakken **Sign-Out URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **ID-Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="7ea65-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="7ea65-190">c.</span><span class="sxs-lookup"><span data-stu-id="7ea65-190">c.</span></span> <span data-ttu-id="7ea65-191">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **ID-Provider certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="7ea65-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="7ea65-192">d.</span><span class="sxs-lookup"><span data-stu-id="7ea65-192">d.</span></span> <span data-ttu-id="7ea65-193">Hallo tooopen **instellingen** pagina, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="7ea65-194">Op Hallo **instellingen** pagina, klikt u op **SSO-Token genereren**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="7ea65-195">![Instellingen](./media/active-directory-saas-druva-tutorial/ic795093.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="7ea65-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="7ea65-196">Op Hallo **Single Sign-on-verificatietoken** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7ea65-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="7ea65-197">![SSO-Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO-Token")</span><span class="sxs-lookup"><span data-stu-id="7ea65-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="7ea65-198">a.</span><span class="sxs-lookup"><span data-stu-id="7ea65-198">a.</span></span> <span data-ttu-id="7ea65-199">Klik op **kopie**, plakken waarde gekopieerd in Hallo **waarde** textbox in Hallo **kenmerk toevoegen** sectie.</span><span class="sxs-lookup"><span data-stu-id="7ea65-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="7ea65-200">b.</span><span class="sxs-lookup"><span data-stu-id="7ea65-200">b.</span></span> <span data-ttu-id="7ea65-201">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="7ea65-202">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7ea65-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7ea65-203">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7ea65-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7ea65-204">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ea65-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7ea65-205">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7ea65-205">Create an Azure AD test user</span></span>

<span data-ttu-id="7ea65-206">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7ea65-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="7ea65-208">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7ea65-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea65-209">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="7ea65-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7ea65-211">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7ea65-213">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ea65-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7ea65-215">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7ea65-217">a.</span><span class="sxs-lookup"><span data-stu-id="7ea65-217">a.</span></span> <span data-ttu-id="7ea65-218">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ea65-219">b.</span><span class="sxs-lookup"><span data-stu-id="7ea65-219">b.</span></span> <span data-ttu-id="7ea65-220">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="7ea65-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7ea65-221">c.</span><span class="sxs-lookup"><span data-stu-id="7ea65-221">c.</span></span> <span data-ttu-id="7ea65-222">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="7ea65-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7ea65-223">d.</span><span class="sxs-lookup"><span data-stu-id="7ea65-223">d.</span></span> <span data-ttu-id="7ea65-224">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="7ea65-225">Een testgebruiker Druva maken</span><span class="sxs-lookup"><span data-stu-id="7ea65-225">Create a Druva test user</span></span>

<span data-ttu-id="7ea65-226">In de volgorde tooenable Azure AD gebruikers toolog in tooDruva, moeten ze worden ingericht in Druva.</span><span class="sxs-lookup"><span data-stu-id="7ea65-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="7ea65-227">In geval van Druva Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="7ea65-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="7ea65-228">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7ea65-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea65-229">Meld u bij tooyour **Druva** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="7ea65-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="7ea65-230">Ga te**beheren \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="7ea65-231">![Gebruikers beheren](./media/active-directory-saas-druva-tutorial/ic795097.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="7ea65-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="7ea65-232">Klik op **maken van nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="7ea65-233">![Gebruikers beheren](./media/active-directory-saas-druva-tutorial/ic795098.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="7ea65-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="7ea65-234">Voer in het dialoogvenster van de nieuwe gebruiker maken hello, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea65-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="7ea65-235">![Maken van nieuwegebruiker](./media/active-directory-saas-druva-tutorial/ic795099.png "nieuwegebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="7ea65-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="7ea65-236">a.</span><span class="sxs-lookup"><span data-stu-id="7ea65-236">a.</span></span> <span data-ttu-id="7ea65-237">In Hallo **e-mailadres** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="7ea65-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="7ea65-238">b.</span><span class="sxs-lookup"><span data-stu-id="7ea65-238">b.</span></span> <span data-ttu-id="7ea65-239">In Hallo **naam** textbox Voer Hallo-naam van gebruiker zoals **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="7ea65-240">c.</span><span class="sxs-lookup"><span data-stu-id="7ea65-240">c.</span></span> <span data-ttu-id="7ea65-241">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="7ea65-242">U kunt andere Druva gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Druva tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="7ea65-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7ea65-243">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ea65-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7ea65-244">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDruva toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="7ea65-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="7ea65-246">**tooassign Britta Simon tooDruva, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7ea65-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea65-247">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7ea65-249">Selecteer in de lijst met de toepassingen van Hallo **Druva**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-249">In hello applications list, select **Druva**.</span></span>

    ![Hallo Druva koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="7ea65-251">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7ea65-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="7ea65-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7ea65-253">Click **Add** button.</span></span> <span data-ttu-id="7ea65-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ea65-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="7ea65-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ea65-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ea65-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ea65-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ea65-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ea65-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7ea65-259">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7ea65-259">Test single sign-on</span></span>

<span data-ttu-id="7ea65-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7ea65-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7ea65-261">Als u op Hallo Druva tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Druva toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ea65-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="7ea65-262">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7ea65-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7ea65-263">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7ea65-263">Additional resources</span></span>

* [<span data-ttu-id="7ea65-264">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ea65-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ea65-265">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ea65-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

