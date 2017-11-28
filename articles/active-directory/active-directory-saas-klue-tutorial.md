---
title: 'Zelfstudie: Azure Active Directory-integratie met Klue | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Klue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="f0f7b-103">Zelfstudie: Azure Active Directory-integratie met Klue</span><span class="sxs-lookup"><span data-stu-id="f0f7b-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="f0f7b-104">In deze zelfstudie leert u hoe toointegrate Klue met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0f7b-104">In this tutorial, you learn how toointegrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0f7b-105">Klue integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-105">Integrating Klue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f0f7b-106">U kunt beheren in Azure AD die tooKlue toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f0f7b-106">You can control in Azure AD who has access tooKlue</span></span>
- <span data-ttu-id="f0f7b-107">U kunt uw gebruikers tooautomatically get aangemelde tooKlue (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f0f7b-107">You can enable your users tooautomatically get signed-on tooKlue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0f7b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f0f7b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f0f7b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0f7b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0f7b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f0f7b-110">Prerequisites</span></span>

<span data-ttu-id="f0f7b-111">Azure AD-integratie met Klue tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-111">tooconfigure Azure AD integration with Klue, you need hello following items:</span></span>

- <span data-ttu-id="f0f7b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f0f7b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0f7b-113">Een Klue eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f0f7b-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0f7b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0f7b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0f7b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0f7b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0f7b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0f7b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f0f7b-118">Scenario description</span></span>
<span data-ttu-id="f0f7b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0f7b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0f7b-121">Het toevoegen van Klue van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f0f7b-121">Adding Klue from hello gallery</span></span>
2. <span data-ttu-id="f0f7b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0f7b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-hello-gallery"></a><span data-ttu-id="f0f7b-123">Het toevoegen van Klue van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f0f7b-123">Adding Klue from hello gallery</span></span>
<span data-ttu-id="f0f7b-124">tooconfigure hello integratie van Klue in Azure AD, moet u tooadd Klue uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-124">tooconfigure hello integration of Klue into Azure AD, you need tooadd Klue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f0f7b-125">**tooadd Klue via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0f7b-125">**tooadd Klue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0f7b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0f7b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f0f7b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f0f7b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f0f7b-133">Typ in het zoekvak Hallo **Klue**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-133">In hello search box, type **Klue**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="f0f7b-135">Selecteer in het deelvenster resultaten hello, **Klue**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-135">In hello results panel, select **Klue**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0f7b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0f7b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0f7b-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Klue op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0f7b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Klue is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Klue is tooa user in Azure AD.</span></span> <span data-ttu-id="f0f7b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Klue toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-140">In other words, a link relationship between an Azure AD user and hello related user in Klue needs toobe established.</span></span>

<span data-ttu-id="f0f7b-141">Wijs in Klue, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-141">In Klue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f0f7b-142">tooconfigure en eenmalige aanmelding Azure AD-test met Klue, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-142">tooconfigure and test Azure AD single sign-on with Klue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f0f7b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f0f7b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0f7b-145">**[Maken van een testgebruiker Klue](#creating-a-klue-test-user)**  -toohave een equivalent van Britta Simon in Klue die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - toohave a counterpart of Britta Simon in Klue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0f7b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0f7b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0f7b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f0f7b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0f7b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Klue configureren.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="f0f7b-150">**Azure AD tooconfigure eenmalige aanmelding met Klue, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0f7b-150">**tooconfigure Azure AD single sign-on with Klue, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0f7b-151">In de Azure-portal op Hallo Hallo **Klue** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-151">In hello Azure portal, on hello **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f0f7b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="f0f7b-155">Op Hallo **Klue domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-155">On hello **Klue Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="f0f7b-157">a.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-157">a.</span></span> <span data-ttu-id="f0f7b-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="f0f7b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="f0f7b-159">b.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-159">b.</span></span> <span data-ttu-id="f0f7b-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="f0f7b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="f0f7b-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="f0f7b-162">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="f0f7b-164">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="f0f7b-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f0f7b-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-165">These values are not real.</span></span> <span data-ttu-id="f0f7b-166">Deze waarden bijwerken met Hallo werkelijke antwoord-URL, de id en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-166">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="f0f7b-167">Neem contact op met [Klue Client ondersteuningsteam](mailto:support@klue.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-167">Contact [Klue Client support team](mailto:support@klue.com) tooget these values.</span></span>

5. <span data-ttu-id="f0f7b-168">Hallo Klue toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-168">hello Klue application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="f0f7b-169">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-169">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="f0f7b-171">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="f0f7b-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f0f7b-172">Attribute Name</span></span>      | <span data-ttu-id="f0f7b-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f0f7b-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="f0f7b-174">Voornaam</span><span class="sxs-lookup"><span data-stu-id="f0f7b-174">first_name</span></span>          | <span data-ttu-id="f0f7b-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="f0f7b-175">user.givenname</span></span> |
    | <span data-ttu-id="f0f7b-176">Achternaam</span><span class="sxs-lookup"><span data-stu-id="f0f7b-176">last_name</span></span>           | <span data-ttu-id="f0f7b-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="f0f7b-177">user.surname</span></span> |
    | <span data-ttu-id="f0f7b-178">E-mail</span><span class="sxs-lookup"><span data-stu-id="f0f7b-178">email</span></span>               | <span data-ttu-id="f0f7b-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="f0f7b-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="f0f7b-180">a.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-180">a.</span></span> <span data-ttu-id="f0f7b-181">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f0f7b-184">b.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-184">b.</span></span> <span data-ttu-id="f0f7b-185">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="f0f7b-186">c.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-186">c.</span></span> <span data-ttu-id="f0f7b-187">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f0f7b-188">d.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-188">d.</span></span> <span data-ttu-id="f0f7b-189">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-189">Click **Ok**.</span></span>

7. <span data-ttu-id="f0f7b-190">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-190">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="f0f7b-192">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-192">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="f0f7b-194">Op Hallo **Klue configuratie** sectie, klikt u op **configureren Klue** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-194">On hello **Klue Configuration** section, click **Configure Klue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f0f7b-195">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f0f7b-195">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="f0f7b-197">tooconfigure eenmalige aanmelding op **Klue** zijde, moet u toosend Hallo gedownload **Certificate(Base64) SAML Single Sign-On Service-URL en SAML entiteit-ID** te[Klue ondersteuningsteam](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="f0f7b-197">tooconfigure single sign-on on **Klue** side, you need toosend hello downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** too[Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="f0f7b-198">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f0f7b-199">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f0f7b-200">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0f7b-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0f7b-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f0f7b-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0f7b-202">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f0f7b-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0f7b-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0f7b-205">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0f7b-207">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0f7b-209">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0f7b-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0f7b-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0f7b-213">a.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-213">a.</span></span> <span data-ttu-id="f0f7b-214">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0f7b-215">b.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-215">b.</span></span> <span data-ttu-id="f0f7b-216">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0f7b-217">c.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-217">c.</span></span> <span data-ttu-id="f0f7b-218">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f0f7b-219">d.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-219">d.</span></span> <span data-ttu-id="f0f7b-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="f0f7b-221">Een testgebruiker Klue maken</span><span class="sxs-lookup"><span data-stu-id="f0f7b-221">Creating a Klue test user</span></span>

<span data-ttu-id="f0f7b-222">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Klue van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-222">hello objective of this section is toocreate a user called Britta Simon in Klue.</span></span> <span data-ttu-id="f0f7b-223">Klue ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f0f7b-224">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-224">There is no action item for you in this section.</span></span> <span data-ttu-id="f0f7b-225">Een nieuwe gebruiker wordt tijdens een poging tooaccess Klue gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-225">A new user is created during an attempt tooaccess Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="f0f7b-226">Als u moet een gebruiker handmatig, neem contact op met toocreate [Klue ondersteuningsteam](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="f0f7b-226">If you need toocreate a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f0f7b-227">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0f7b-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f0f7b-228">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKlue toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKlue.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f0f7b-230">**tooassign Britta Simon tooKlue, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0f7b-230">**tooassign Britta Simon tooKlue, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0f7b-231">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f0f7b-233">Selecteer in de lijst met de toepassingen van Hallo **Klue**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-233">In hello applications list, select **Klue**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="f0f7b-235">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f0f7b-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-237">Click **Add** button.</span></span> <span data-ttu-id="f0f7b-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f0f7b-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f0f7b-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0f7b-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0f7b-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0f7b-243">Testing single sign-on</span></span>

<span data-ttu-id="f0f7b-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f0f7b-245">Als u op Hallo Klue tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Klue toepassing.</span><span class="sxs-lookup"><span data-stu-id="f0f7b-245">When you click hello Klue tile in hello Access Panel, you should get automatically signed-on tooyour Klue application.</span></span>
<span data-ttu-id="f0f7b-246">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0f7b-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0f7b-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f0f7b-247">Additional resources</span></span>

* [<span data-ttu-id="f0f7b-248">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0f7b-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0f7b-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0f7b-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

