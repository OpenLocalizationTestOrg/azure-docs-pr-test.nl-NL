---
title: 'Zelfstudie: Azure Active Directory-integratie met Ceridian Dayforce HCM | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Ceridian Dayforce HCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="b5743-103">Zelfstudie: Azure Active Directory-integratie met Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="b5743-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="b5743-104">In deze zelfstudie leert u hoe toointegrate Ceridian Dayforce HCM met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5743-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5743-105">Ceridian Dayforce HCM integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b5743-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5743-106">U kunt beheren in Azure AD die toegang tooCeridian Dayforce HCM heeft.</span><span class="sxs-lookup"><span data-stu-id="b5743-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="b5743-107">U kunt uw gebruikers tooautomatically get aangemelde tooCeridian Dayforce HCM (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="b5743-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b5743-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="b5743-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b5743-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5743-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5743-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b5743-110">Prerequisites</span></span>

<span data-ttu-id="b5743-111">Azure AD-integratie met Ceridian Dayforce HCM tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b5743-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="b5743-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b5743-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5743-113">Een Ceridian Dayforce HCM eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b5743-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5743-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b5743-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5743-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b5743-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5743-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b5743-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5743-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5743-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5743-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b5743-118">Scenario description</span></span>
<span data-ttu-id="b5743-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b5743-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5743-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b5743-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5743-121">Het toevoegen van Ceridian Dayforce HCM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b5743-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="b5743-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5743-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="b5743-123">Het toevoegen van Ceridian Dayforce HCM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b5743-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="b5743-124">tooconfigure hello integratie van Ceridian Dayforce HCM in Azure AD, moet u tooadd Ceridian Dayforce HCM uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b5743-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5743-125">**tooadd Ceridian Dayforce HCM via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b5743-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5743-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b5743-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="b5743-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5743-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b5743-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5743-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="b5743-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="b5743-133">Typ in het zoekvak Hallo **Ceridian Dayforce HCM**, selecteer **Ceridian Dayforce HCM** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5743-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ceridian Dayforce HCM in de lijst met resultaten Hallo](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b5743-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5743-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b5743-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Ceridian Dayforce HCM op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b5743-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5743-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Ceridian Dayforce HCM is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5743-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="b5743-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Ceridian Dayforce HCM toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b5743-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="b5743-139">Wijs in Ceridian Dayforce HCM, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="b5743-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b5743-140">tooconfigure en eenmalige aanmelding Azure AD-test met Ceridian Dayforce HCM, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5743-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5743-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b5743-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5743-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5743-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5743-143">**[Maak een testgebruiker Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave een equivalent van Britta Simon in Ceridian Dayforce HCM die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b5743-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5743-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b5743-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5743-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b5743-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b5743-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b5743-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b5743-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Ceridian Dayforce HCM configureren.</span><span class="sxs-lookup"><span data-stu-id="b5743-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="b5743-148">**tooconfigure eenmalige aanmelding Azure AD met Ceridian Dayforce HCM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b5743-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5743-149">In de Azure-portal op Hallo Hallo **Ceridian Dayforce HCM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b5743-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b5743-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b5743-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="b5743-153">Op Hallo **Ceridian Dayforce HCM domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5743-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="b5743-155">a.</span><span class="sxs-lookup"><span data-stu-id="b5743-155">a.</span></span> <span data-ttu-id="b5743-156">In Hallo **aanmelding op URL** textbox type Hallo-URL die door uw gebruikers toosign op tooyour Ceridian Dayforce HCM toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b5743-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="b5743-157">Omgeving</span><span class="sxs-lookup"><span data-stu-id="b5743-157">Environment</span></span> | <span data-ttu-id="b5743-158">URL</span><span class="sxs-lookup"><span data-stu-id="b5743-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b5743-159">Voor productie</span><span class="sxs-lookup"><span data-stu-id="b5743-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="b5743-160">Voor de tests voor</span><span class="sxs-lookup"><span data-stu-id="b5743-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="b5743-161">b.</span><span class="sxs-lookup"><span data-stu-id="b5743-161">b.</span></span> <span data-ttu-id="b5743-162">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="b5743-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="b5743-163">Omgeving</span><span class="sxs-lookup"><span data-stu-id="b5743-163">Environment</span></span> | <span data-ttu-id="b5743-164">URL</span><span class="sxs-lookup"><span data-stu-id="b5743-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b5743-165">Voor productie</span><span class="sxs-lookup"><span data-stu-id="b5743-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="b5743-166">Voor de tests voor</span><span class="sxs-lookup"><span data-stu-id="b5743-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="b5743-167">c.</span><span class="sxs-lookup"><span data-stu-id="b5743-167">c.</span></span> <span data-ttu-id="b5743-168">In Hallo **antwoord-URL** textbox type Hallo-URL die door Azure AD toopost Hallo antwoord gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b5743-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="b5743-169">Omgeving</span><span class="sxs-lookup"><span data-stu-id="b5743-169">Environment</span></span> | <span data-ttu-id="b5743-170">URL</span><span class="sxs-lookup"><span data-stu-id="b5743-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b5743-171">Voor productie</span><span class="sxs-lookup"><span data-stu-id="b5743-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="b5743-172">Voor de tests voor</span><span class="sxs-lookup"><span data-stu-id="b5743-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="b5743-173">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b5743-173">These values are not real.</span></span> <span data-ttu-id="b5743-174">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="b5743-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="b5743-175">Neem contact op met [Ceridian Dayforce HCM Client ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b5743-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="b5743-176">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b5743-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="b5743-178">Uw toepassing Ceridian Dayforce HCM verwacht Hallo SAML asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="b5743-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b5743-179">Werken met [Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) eerste tooidentify Hallo juiste gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="b5743-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="b5743-180">Microsoft raadt u Hallo **'name'** kenmerk als gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="b5743-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="b5743-181">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="b5743-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="b5743-182">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="b5743-182">hello following screenshot shows an example for this.</span></span>  

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="b5743-184">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5743-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b5743-185">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b5743-185">Attribute Name</span></span>  | <span data-ttu-id="b5743-186">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b5743-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="b5743-187">naam</span><span class="sxs-lookup"><span data-stu-id="b5743-187">name</span></span>  | <span data-ttu-id="b5743-188">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="b5743-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="b5743-189">a.</span><span class="sxs-lookup"><span data-stu-id="b5743-189">a.</span></span> <span data-ttu-id="b5743-190">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b5743-193">b.</span><span class="sxs-lookup"><span data-stu-id="b5743-193">b.</span></span> <span data-ttu-id="b5743-194">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b5743-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b5743-195">c.</span><span class="sxs-lookup"><span data-stu-id="b5743-195">c.</span></span> <span data-ttu-id="b5743-196">In Hallo **waarde** lijst, selecteer Hallo gebruikerskenmerk gewenste toouse voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="b5743-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="b5743-197">Bijvoorbeeld, als u wilt dat toouse Hallo werknemer-id als unieke gebruikers-id en u Hallo-kenmerkwaarde in Hallo ExtensionAttribute2 hebt opgeslagen, selecteert u **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="b5743-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="b5743-198">d.</span><span class="sxs-lookup"><span data-stu-id="b5743-198">d.</span></span> <span data-ttu-id="b5743-199">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5743-199">Click **Ok**.</span></span>

7. <span data-ttu-id="b5743-200">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b5743-200">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="b5743-202">Op Hallo **Ceridian Dayforce HCM configuratie** sectie, klikt u op **configureren Ceridian Dayforce HCM** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b5743-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b5743-203">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b5743-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM configuratie](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="b5743-205">tooconfigure eenmalige aanmelding op **Ceridian Dayforce HCM** zijde, moet u toosend Hallo gedownload **Metadata XML** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="b5743-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="b5743-206">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b5743-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5743-207">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b5743-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5743-208">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5743-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b5743-209">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b5743-209">Create an Azure AD test user</span></span>

<span data-ttu-id="b5743-210">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b5743-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b5743-212">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b5743-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5743-213">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="b5743-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b5743-215">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b5743-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b5743-217">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b5743-219">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5743-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b5743-221">a.</span><span class="sxs-lookup"><span data-stu-id="b5743-221">a.</span></span> <span data-ttu-id="b5743-222">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5743-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5743-223">b.</span><span class="sxs-lookup"><span data-stu-id="b5743-223">b.</span></span> <span data-ttu-id="b5743-224">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="b5743-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b5743-225">c.</span><span class="sxs-lookup"><span data-stu-id="b5743-225">c.</span></span> <span data-ttu-id="b5743-226">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="b5743-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b5743-227">d.</span><span class="sxs-lookup"><span data-stu-id="b5743-227">d.</span></span> <span data-ttu-id="b5743-228">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b5743-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="b5743-229">Een testgebruiker Ceridian Dayforce HCM maken</span><span class="sxs-lookup"><span data-stu-id="b5743-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="b5743-230">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Ceridian Dayforce HCM van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b5743-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="b5743-231">Werken met Hallo [Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) tooget gebruikers toegevoegd in Hallo Ceridian Dayforce HCM toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5743-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b5743-232">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5743-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b5743-233">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="b5743-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b5743-235">**tooassign Britta Simon tooCeridian Dayforce HCM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b5743-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5743-236">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5743-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b5743-238">Selecteer in de lijst met de toepassingen van Hallo **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="b5743-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="b5743-240">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b5743-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b5743-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b5743-242">Click **Add** button.</span></span> <span data-ttu-id="b5743-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b5743-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b5743-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5743-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5743-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b5743-248">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5743-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b5743-249">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="b5743-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="b5743-251">**tooassign Britta Simon tooCeridian Dayforce HCM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b5743-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5743-252">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5743-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b5743-254">Selecteer in de lijst met de toepassingen van Hallo **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="b5743-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Hallo Ceridian Dayforce HCM koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="b5743-256">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b5743-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="b5743-258">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b5743-258">Click **Add** button.</span></span> <span data-ttu-id="b5743-259">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="b5743-261">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b5743-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5743-262">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5743-263">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b5743-264">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5743-264">Test single sign-on</span></span>

<span data-ttu-id="b5743-265">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b5743-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="b5743-266">Als u op Hallo Ceridian Dayforce HCM tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Ceridian Dayforce HCM toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5743-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b5743-267">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b5743-267">Additional resources</span></span>

* [<span data-ttu-id="b5743-268">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5743-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5743-269">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b5743-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

