---
title: 'Zelfstudie: Azure Active Directory-integratie met etouches | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en etouches.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="79e08-103">Zelfstudie: Azure Active Directory-integratie met etouches</span><span class="sxs-lookup"><span data-stu-id="79e08-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="79e08-104">In deze zelfstudie leert u hoe toointegrate etouches met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79e08-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79e08-105">Etouches integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="79e08-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79e08-106">U kunt beheren in Azure AD die tooetouches toegang heeft</span><span class="sxs-lookup"><span data-stu-id="79e08-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="79e08-107">U kunt uw gebruikers tooautomatically get aangemelde tooetouches (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="79e08-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79e08-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="79e08-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79e08-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79e08-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79e08-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="79e08-110">Prerequisites</span></span>

<span data-ttu-id="79e08-111">Azure AD-integratie met etouches tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="79e08-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="79e08-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="79e08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79e08-113">Een etouches eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="79e08-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79e08-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="79e08-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79e08-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="79e08-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79e08-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="79e08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79e08-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79e08-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79e08-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="79e08-118">Scenario description</span></span>
<span data-ttu-id="79e08-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="79e08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79e08-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="79e08-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79e08-121">Het toevoegen van etouches van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="79e08-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="79e08-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79e08-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="79e08-123">Het toevoegen van etouches van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="79e08-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="79e08-124">tooconfigure hello integratie van etouches in Azure AD, moet u tooadd etouches uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="79e08-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79e08-125">**tooadd etouches via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79e08-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79e08-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="79e08-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="79e08-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79e08-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79e08-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79e08-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="79e08-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79e08-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="79e08-133">Typ in het zoekvak Hallo **etouches**, selecteer **etouches** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="79e08-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![etouches in de lijst met resultaten Hallo](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="79e08-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="79e08-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="79e08-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met etouches op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="79e08-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79e08-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in etouches is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79e08-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="79e08-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in etouches toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="79e08-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="79e08-139">Wijs in etouches, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="79e08-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79e08-140">tooconfigure en eenmalige aanmelding Azure AD-test met etouches, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79e08-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79e08-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="79e08-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79e08-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79e08-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79e08-143">**[Maken van een testgebruiker etouches](#create-an-etouches-test-user)**  -toohave een equivalent van Britta Simon in etouches die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="79e08-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79e08-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="79e08-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79e08-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="79e08-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="79e08-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="79e08-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="79e08-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing etouches configureren.</span><span class="sxs-lookup"><span data-stu-id="79e08-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="79e08-148">**Azure AD tooconfigure eenmalige aanmelding met etouches, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79e08-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="79e08-149">In de Azure-portal op Hallo Hallo **etouches** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="79e08-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="79e08-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="79e08-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="79e08-153">Op Hallo **etouches domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79e08-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![etouches domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="79e08-155">a.</span><span class="sxs-lookup"><span data-stu-id="79e08-155">a.</span></span> <span data-ttu-id="79e08-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="79e08-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="79e08-157">b.</span><span class="sxs-lookup"><span data-stu-id="79e08-157">b.</span></span> <span data-ttu-id="79e08-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="79e08-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79e08-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="79e08-159">These values are not real.</span></span> <span data-ttu-id="79e08-160">U Hallo waarde bijwerken met de werkelijke Hallo Meld u aan bij de URL en de id, die verderop in Hallo zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="79e08-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="79e08-161">Hallo SAML asserties verwacht etouches toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="79e08-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="79e08-162">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="79e08-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="79e08-163">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerk** van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="79e08-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="79e08-164">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="79e08-164">hello following screenshot shows an example for this.</span></span> 

    ![Gebruikerskenmerk](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="79e08-166">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79e08-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="79e08-167">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="79e08-167">Attribute Name</span></span> | <span data-ttu-id="79e08-168">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="79e08-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="79e08-169">E-mail</span><span class="sxs-lookup"><span data-stu-id="79e08-169">Email</span></span> | <span data-ttu-id="79e08-170">User.mail</span><span class="sxs-lookup"><span data-stu-id="79e08-170">user.mail</span></span> |    
    
    <span data-ttu-id="79e08-171">a.</span><span class="sxs-lookup"><span data-stu-id="79e08-171">a.</span></span> <span data-ttu-id="79e08-172">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79e08-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Kenmerk toevoegen](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Dialoogvenster kenmerk toevoegen](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="79e08-175">b.</span><span class="sxs-lookup"><span data-stu-id="79e08-175">b.</span></span> <span data-ttu-id="79e08-176">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="79e08-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="79e08-177">c.</span><span class="sxs-lookup"><span data-stu-id="79e08-177">c.</span></span> <span data-ttu-id="79e08-178">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="79e08-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="79e08-179">d.</span><span class="sxs-lookup"><span data-stu-id="79e08-179">d.</span></span> <span data-ttu-id="79e08-180">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="79e08-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="79e08-181">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="79e08-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="79e08-183">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="79e08-183">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="79e08-185">tooget SSO is geconfigureerd voor uw toepassing hello stappen te volgen in Hallo etouches toepassing uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="79e08-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![etouches configuratie](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="79e08-187">a.</span><span class="sxs-lookup"><span data-stu-id="79e08-187">a.</span></span> <span data-ttu-id="79e08-188">Aanmelding te**etouches** toepassing met behulp van Hallo-beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="79e08-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="79e08-189">b.</span><span class="sxs-lookup"><span data-stu-id="79e08-189">b.</span></span> <span data-ttu-id="79e08-190">Ga toohello **SAML** configuratie.</span><span class="sxs-lookup"><span data-stu-id="79e08-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="79e08-191">c.</span><span class="sxs-lookup"><span data-stu-id="79e08-191">c.</span></span> <span data-ttu-id="79e08-192">In Hallo **algemene instellingen** sectie en opent u het gedownloade certificaat vanuit Azure-portal in Kladblok, kopieer Hallo inhoud, plakt u deze in Hallo IDP metagegevens textbox.</span><span class="sxs-lookup"><span data-stu-id="79e08-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="79e08-193">d.</span><span class="sxs-lookup"><span data-stu-id="79e08-193">d.</span></span> <span data-ttu-id="79e08-194">Klik op Hallo **opslaan & blijven** knop.</span><span class="sxs-lookup"><span data-stu-id="79e08-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="79e08-195">e.</span><span class="sxs-lookup"><span data-stu-id="79e08-195">e.</span></span> <span data-ttu-id="79e08-196">Klik op Hallo **updatemetagegevens** knop in Hallo sectie SAML-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="79e08-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="79e08-197">f.</span><span class="sxs-lookup"><span data-stu-id="79e08-197">f.</span></span> <span data-ttu-id="79e08-198">Deze wordt geopend pagina Hallo en SSO worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="79e08-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="79e08-199">Eenmaal Hallo SSO werkt u Hallo gebruikersnaam kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="79e08-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="79e08-200">g.</span><span class="sxs-lookup"><span data-stu-id="79e08-200">g.</span></span> <span data-ttu-id="79e08-201">Selecteer in het veld Username hello, Hallo **emailaddress** zoals weergegeven in onderstaande Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="79e08-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="79e08-202">h.</span><span class="sxs-lookup"><span data-stu-id="79e08-202">h.</span></span> <span data-ttu-id="79e08-203">Kopiëren Hallo **SP entiteit-ID** waarde en plak deze in Hallo **id** textbox in **etouches domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="79e08-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="79e08-204">ik.</span><span class="sxs-lookup"><span data-stu-id="79e08-204">i.</span></span> <span data-ttu-id="79e08-205">Kopiëren Hallo **SSO URL / ACS** waarde en plak deze in Hallo **URL aanmelden** textbox in **etouches domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="79e08-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="79e08-206">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="79e08-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79e08-207">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="79e08-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79e08-208">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79e08-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79e08-209">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="79e08-209">Create an Azure AD test user</span></span>
<span data-ttu-id="79e08-210">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="79e08-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="79e08-212">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79e08-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79e08-213">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="79e08-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79e08-215">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="79e08-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79e08-217">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="79e08-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79e08-219">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79e08-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79e08-221">a.</span><span class="sxs-lookup"><span data-stu-id="79e08-221">a.</span></span> <span data-ttu-id="79e08-222">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79e08-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79e08-223">b.</span><span class="sxs-lookup"><span data-stu-id="79e08-223">b.</span></span> <span data-ttu-id="79e08-224">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79e08-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79e08-225">c.</span><span class="sxs-lookup"><span data-stu-id="79e08-225">c.</span></span> <span data-ttu-id="79e08-226">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="79e08-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79e08-227">d.</span><span class="sxs-lookup"><span data-stu-id="79e08-227">d.</span></span> <span data-ttu-id="79e08-228">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="79e08-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="79e08-229">Een testgebruiker etouches maken</span><span class="sxs-lookup"><span data-stu-id="79e08-229">Create an etouches test user</span></span>

<span data-ttu-id="79e08-230">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in etouches maken.</span><span class="sxs-lookup"><span data-stu-id="79e08-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="79e08-231">Werken met [etouches Client ondersteuningsteam](https://www.etouches.com/event-software/support/customer-support/) tooadd Hallo gebruikers in Hallo etouches platform.</span><span class="sxs-lookup"><span data-stu-id="79e08-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="79e08-232">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="79e08-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="79e08-233">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooetouches toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="79e08-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="79e08-235">**tooassign Britta Simon tooetouches, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79e08-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="79e08-236">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79e08-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="79e08-238">Selecteer in de lijst met de toepassingen van Hallo **etouches**.</span><span class="sxs-lookup"><span data-stu-id="79e08-238">In hello applications list, select **etouches**.</span></span>

    ![Hallo etouches koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="79e08-240">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="79e08-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="79e08-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="79e08-242">Click **Add** button.</span></span> <span data-ttu-id="79e08-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79e08-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="79e08-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="79e08-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79e08-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79e08-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79e08-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79e08-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="79e08-248">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79e08-248">Test single sign-on</span></span>


<span data-ttu-id="79e08-249">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="79e08-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79e08-250">Als u op Hallo etouches-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour etouches toepassing.</span><span class="sxs-lookup"><span data-stu-id="79e08-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79e08-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="79e08-251">Additional resources</span></span>

* [<span data-ttu-id="79e08-252">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79e08-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79e08-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79e08-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

