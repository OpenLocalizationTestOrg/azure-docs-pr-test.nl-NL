---
title: 'Zelfstudie: Azure Active Directory-integratie met Clever | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Clever.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="da9aa-103">Zelfstudie: Azure Active Directory-integratie met Clever</span><span class="sxs-lookup"><span data-stu-id="da9aa-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="da9aa-104">In deze zelfstudie leert u hoe toointegrate Clever met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da9aa-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da9aa-105">Clever integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="da9aa-106">U kunt beheren in Azure AD die tooClever toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="da9aa-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="da9aa-107">U kunt uw gebruikers tooautomatically get aangemelde tooClever (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="da9aa-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="da9aa-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="da9aa-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="da9aa-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da9aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da9aa-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="da9aa-110">Prerequisites</span></span>

<span data-ttu-id="da9aa-111">Azure AD-integratie met Clever tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="da9aa-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="da9aa-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="da9aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da9aa-113">Een slimme eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="da9aa-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da9aa-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="da9aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da9aa-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da9aa-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="da9aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da9aa-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da9aa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da9aa-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="da9aa-118">Scenario description</span></span>
<span data-ttu-id="da9aa-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="da9aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da9aa-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da9aa-121">Het toevoegen van Clever van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="da9aa-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="da9aa-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da9aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="da9aa-123">Het toevoegen van Clever van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="da9aa-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="da9aa-124">tooconfigure hello integratie van Clever in Azure AD, moet u tooadd Clever uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="da9aa-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="da9aa-125">**tooadd Clever via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da9aa-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="da9aa-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="da9aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="da9aa-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="da9aa-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="da9aa-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da9aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="da9aa-133">Typ in het zoekvak Hallo **Clever**, selecteer **Clever** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="da9aa-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![In de lijst met resultaten Hallo slimme](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="da9aa-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="da9aa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="da9aa-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Clever op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="da9aa-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da9aa-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Clever is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da9aa-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="da9aa-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Clever toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="da9aa-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="da9aa-139">Wijs in Clever, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="da9aa-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="da9aa-140">tooconfigure en eenmalige aanmelding Azure AD-test met Clever, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="da9aa-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="da9aa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="da9aa-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da9aa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da9aa-143">**[Maak een slimme testgebruiker](#create-a-clever-test-user)**  -toohave een equivalent van Britta Simon in Clever die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="da9aa-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="da9aa-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="da9aa-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da9aa-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="da9aa-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="da9aa-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="da9aa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="da9aa-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing slimme configureren.</span><span class="sxs-lookup"><span data-stu-id="da9aa-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="da9aa-148">**Azure AD tooconfigure eenmalige aanmelding met Clever, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da9aa-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="da9aa-149">In de Azure-portal op Hallo Hallo **Clever** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="da9aa-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="da9aa-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="da9aa-153">Op Hallo **slimme domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Slimme domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="da9aa-155">a.</span><span class="sxs-lookup"><span data-stu-id="da9aa-155">a.</span></span> <span data-ttu-id="da9aa-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="da9aa-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="da9aa-157">b.</span><span class="sxs-lookup"><span data-stu-id="da9aa-157">b.</span></span> <span data-ttu-id="da9aa-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="da9aa-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="da9aa-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="da9aa-159">These values are not real.</span></span> <span data-ttu-id="da9aa-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="da9aa-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="da9aa-161">Neem contact op met [slimme Client ondersteuningsteam](https://clever.com/about/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="da9aa-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="da9aa-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="da9aa-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="da9aa-164">Hallo slimme toepassing hello SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **SAML-Token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="da9aa-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="da9aa-165">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="da9aa-165">hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="da9aa-167">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="da9aa-168">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="da9aa-168">Attribute Name</span></span>  | <span data-ttu-id="da9aa-169">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="da9aa-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="da9aa-170">clever.student.credentials.district\_gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="da9aa-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="da9aa-171">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="da9aa-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="da9aa-172">Voornaam</span><span class="sxs-lookup"><span data-stu-id="da9aa-172">Firstname</span></span>  | <span data-ttu-id="da9aa-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="da9aa-173">user.givenname</span></span> |
    | <span data-ttu-id="da9aa-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="da9aa-174">Lastname</span></span>  | <span data-ttu-id="da9aa-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="da9aa-175">user.surname</span></span> |    

    <span data-ttu-id="da9aa-176">a.</span><span class="sxs-lookup"><span data-stu-id="da9aa-176">a.</span></span> <span data-ttu-id="da9aa-177">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da9aa-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="da9aa-180">b.</span><span class="sxs-lookup"><span data-stu-id="da9aa-180">b.</span></span> <span data-ttu-id="da9aa-181">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="da9aa-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="da9aa-182">c.</span><span class="sxs-lookup"><span data-stu-id="da9aa-182">c.</span></span> <span data-ttu-id="da9aa-183">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="da9aa-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="da9aa-184">d.</span><span class="sxs-lookup"><span data-stu-id="da9aa-184">d.</span></span> <span data-ttu-id="da9aa-185">Hallo laat **Namespace** textbox leeg.</span><span class="sxs-lookup"><span data-stu-id="da9aa-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="da9aa-186">d.</span><span class="sxs-lookup"><span data-stu-id="da9aa-186">d.</span></span> <span data-ttu-id="da9aa-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="da9aa-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="da9aa-188">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="da9aa-190">Hallo toogenerate **metagegevens** -url, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="da9aa-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="da9aa-191">a.</span><span class="sxs-lookup"><span data-stu-id="da9aa-191">a.</span></span> <span data-ttu-id="da9aa-192">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-192">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="da9aa-194">b.</span><span class="sxs-lookup"><span data-stu-id="da9aa-194">b.</span></span> <span data-ttu-id="da9aa-195">Klik op **eindpunten** tooopen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da9aa-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="da9aa-197">c.</span><span class="sxs-lookup"><span data-stu-id="da9aa-197">c.</span></span> <span data-ttu-id="da9aa-198">Klik op Hallo kopie knop toocopy **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="da9aa-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="da9aa-200">d.</span><span class="sxs-lookup"><span data-stu-id="da9aa-200">d.</span></span> <span data-ttu-id="da9aa-201">Ga nu toohello eigenschappenpagina van **Clever** en kopiëren Hallo **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="da9aa-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="da9aa-203">e.</span><span class="sxs-lookup"><span data-stu-id="da9aa-203">e.</span></span> <span data-ttu-id="da9aa-204">Hallo genereren **metagegevens-URL** met Hallo patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="da9aa-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="da9aa-205">In een ander browservenster, meld u aan tooyour slimme bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="da9aa-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="da9aa-206">Klik in de werkbalk Hallo op **directe aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="da9aa-207">![Directe aanmelding](./media/active-directory-saas-clever-tutorial/ic798984.png "directe aanmelding")</span><span class="sxs-lookup"><span data-stu-id="da9aa-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="da9aa-208">Op Hallo **directe aanmelding** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="da9aa-209">![Directe aanmelding](./media/active-directory-saas-clever-tutorial/ic798985.png "directe aanmelding")</span><span class="sxs-lookup"><span data-stu-id="da9aa-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="da9aa-210">a.</span><span class="sxs-lookup"><span data-stu-id="da9aa-210">a.</span></span> <span data-ttu-id="da9aa-211">Type Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="da9aa-212">Hallo **aanmeldings-URL** is een aangepaste waarde.</span><span class="sxs-lookup"><span data-stu-id="da9aa-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="da9aa-213">Neem contact op met [slimme Client ondersteuningsteam](https://clever.com/about/contact/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="da9aa-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="da9aa-214">b.</span><span class="sxs-lookup"><span data-stu-id="da9aa-214">b.</span></span> <span data-ttu-id="da9aa-215">Als **identiteitsbeheersysteem**, selecteer **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="da9aa-216">c.</span><span class="sxs-lookup"><span data-stu-id="da9aa-216">c.</span></span> <span data-ttu-id="da9aa-217">Type Hallo **metagegevens-URL** in Hallo **metagegevens-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="da9aa-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="da9aa-218">d.</span><span class="sxs-lookup"><span data-stu-id="da9aa-218">d.</span></span> <span data-ttu-id="da9aa-219">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="da9aa-220">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="da9aa-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="da9aa-221">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="da9aa-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="da9aa-222">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="da9aa-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="da9aa-223">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="da9aa-223">Create an Azure AD test user</span></span>

<span data-ttu-id="da9aa-224">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="da9aa-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="da9aa-226">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da9aa-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="da9aa-227">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="da9aa-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="da9aa-229">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="da9aa-231">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da9aa-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="da9aa-233">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da9aa-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="da9aa-235">a.</span><span class="sxs-lookup"><span data-stu-id="da9aa-235">a.</span></span> <span data-ttu-id="da9aa-236">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da9aa-237">b.</span><span class="sxs-lookup"><span data-stu-id="da9aa-237">b.</span></span> <span data-ttu-id="da9aa-238">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="da9aa-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="da9aa-239">c.</span><span class="sxs-lookup"><span data-stu-id="da9aa-239">c.</span></span> <span data-ttu-id="da9aa-240">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="da9aa-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="da9aa-241">d.</span><span class="sxs-lookup"><span data-stu-id="da9aa-241">d.</span></span> <span data-ttu-id="da9aa-242">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="da9aa-243">Een slimme testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="da9aa-243">Create a Clever test user</span></span>

<span data-ttu-id="da9aa-244">Azure AD tooenable gebruikers toolog in tooClever, ze in Clever moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="da9aa-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="da9aa-245">In geval van een Clever, werken met [slimme Client ondersteuningsteam](https://clever.com/about/contact/) Hallo gebruikers toevoegen in slimme Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="da9aa-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="da9aa-246">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="da9aa-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="da9aa-247">U kunt een andere gebruiker slimme account hulpmiddelen voor het maken of API's die worden geleverd door slimme tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="da9aa-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="da9aa-248">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="da9aa-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="da9aa-249">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooClever toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="da9aa-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="da9aa-251">**tooassign Britta Simon tooClever, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da9aa-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="da9aa-252">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="da9aa-254">Selecteer in de lijst met de toepassingen van Hallo **Clever**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-254">In hello applications list, select **Clever**.</span></span>

    ![Hallo Clever koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="da9aa-256">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="da9aa-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="da9aa-258">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="da9aa-258">Click **Add** button.</span></span> <span data-ttu-id="da9aa-259">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da9aa-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="da9aa-261">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="da9aa-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="da9aa-262">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da9aa-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da9aa-263">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da9aa-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="da9aa-264">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da9aa-264">Test single sign-on</span></span>

<span data-ttu-id="da9aa-265">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="da9aa-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="da9aa-266">Wanneer u klikt op Hallo slimme tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour slimme toepassing.</span><span class="sxs-lookup"><span data-stu-id="da9aa-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="da9aa-267">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da9aa-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="da9aa-268">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="da9aa-268">Additional resources</span></span>

* [<span data-ttu-id="da9aa-269">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da9aa-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da9aa-270">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da9aa-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

