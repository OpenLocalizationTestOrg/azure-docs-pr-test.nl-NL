---
title: 'Zelfstudie: Azure Active Directory-integratie met TimeOffManager | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="f61a6-103">Zelfstudie: Azure Active Directory-integratie met TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="f61a6-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="f61a6-104">In deze zelfstudie leert u hoe toointegrate TimeOffManager met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f61a6-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f61a6-105">TimeOffManager integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f61a6-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f61a6-106">U kunt beheren in Azure AD die tooTimeOffManager toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f61a6-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="f61a6-107">U kunt uw gebruikers tooautomatically get aangemelde tooTimeOffManager (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f61a6-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f61a6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f61a6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f61a6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f61a6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f61a6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f61a6-110">Prerequisites</span></span>

<span data-ttu-id="f61a6-111">Azure AD-integratie met TimeOffManager tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f61a6-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="f61a6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f61a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f61a6-113">Een TimeOffManager eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f61a6-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f61a6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f61a6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f61a6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f61a6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f61a6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f61a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f61a6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f61a6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f61a6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f61a6-118">Scenario description</span></span>
<span data-ttu-id="f61a6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f61a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f61a6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f61a6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f61a6-121">TimeOffManager van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f61a6-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="f61a6-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f61a6-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="f61a6-123">TimeOffManager van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f61a6-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="f61a6-124">tooconfigure hello integratie van TimeOffManager in Azure AD, moet u tooadd TimeOffManager uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f61a6-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f61a6-125">**tooadd TimeOffManager via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f61a6-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f61a6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f61a6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f61a6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f61a6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f61a6-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f61a6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f61a6-133">Typ in het zoekvak Hallo **TimeOffManager**, selecteer **TimeOffManager** van resultaat deelvenster en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f61a6-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Uit de galerie toevoegen](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f61a6-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f61a6-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f61a6-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met TimeOffManager op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f61a6-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f61a6-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TimeOffManager is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f61a6-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="f61a6-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TimeOffManager toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f61a6-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="f61a6-139">Wijs in TimeOffManager, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f61a6-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f61a6-140">tooconfigure en eenmalige aanmelding Azure AD-test met TimeOffManager, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f61a6-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f61a6-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f61a6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f61a6-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f61a6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f61a6-143">**[Maak een testgebruiker TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave een equivalent van Britta Simon in TimeOffManager die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f61a6-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f61a6-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f61a6-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f61a6-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f61a6-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f61a6-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f61a6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f61a6-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TimeOffManager configureren.</span><span class="sxs-lookup"><span data-stu-id="f61a6-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="f61a6-148">**Azure AD tooconfigure eenmalige aanmelding met TimeOffManager, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f61a6-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="f61a6-149">In de Azure-portal op Hallo Hallo **TimeOffManager** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f61a6-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f61a6-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML op basis van eenmalige aanmelding](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="f61a6-153">Op Hallo **TimeOffManager domein en de URL's** sectie, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="f61a6-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Sectie TimeOffManager domein en URL 's](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="f61a6-155">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="f61a6-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f61a6-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f61a6-156">This value is not real.</span></span> <span data-ttu-id="f61a6-157">Deze waarde met de werkelijke antwoord-URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f61a6-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="f61a6-158">U krijgt deze waarde van **voor eenmalige aanmelding instellingenpagina** die wordt uitgelegd later in de zelfstudie Hallo of neem contact op met [TimeOffManager ondersteuningsteam](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="f61a6-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="f61a6-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f61a6-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="f61a6-161">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooTimeOffManger aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="f61a6-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="f61a6-162">Uw toepassing TimeOffManger verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="f61a6-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="f61a6-163">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="f61a6-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="f61a6-164">![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml-token kenmerken")</span><span class="sxs-lookup"><span data-stu-id="f61a6-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="f61a6-165">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f61a6-165">Attribute Name</span></span> | <span data-ttu-id="f61a6-166">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f61a6-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f61a6-167">Voornaam</span><span class="sxs-lookup"><span data-stu-id="f61a6-167">Firstname</span></span> |<span data-ttu-id="f61a6-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="f61a6-168">User.givenname</span></span> |
    | <span data-ttu-id="f61a6-169">Achternaam</span><span class="sxs-lookup"><span data-stu-id="f61a6-169">Lastname</span></span> |<span data-ttu-id="f61a6-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="f61a6-170">User.surname</span></span> |
    | <span data-ttu-id="f61a6-171">E-mail</span><span class="sxs-lookup"><span data-stu-id="f61a6-171">Email</span></span> |<span data-ttu-id="f61a6-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="f61a6-172">User.mail</span></span> |
    
    <span data-ttu-id="f61a6-173">a.</span><span class="sxs-lookup"><span data-stu-id="f61a6-173">a.</span></span>  <span data-ttu-id="f61a6-174">Klik voor elke gegevensrij in bovenstaande tabel voor Hallo **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="f61a6-175">![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml-token kenmerken")</span><span class="sxs-lookup"><span data-stu-id="f61a6-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="f61a6-176">![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml-token kenmerken")</span><span class="sxs-lookup"><span data-stu-id="f61a6-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="f61a6-177">b.</span><span class="sxs-lookup"><span data-stu-id="f61a6-177">b.</span></span>  <span data-ttu-id="f61a6-178">In Hallo **kenmerknaam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f61a6-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f61a6-179">c.</span><span class="sxs-lookup"><span data-stu-id="f61a6-179">c.</span></span>  <span data-ttu-id="f61a6-180">In Hallo **kenmerkwaarde** textbox, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f61a6-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="f61a6-181">d.</span><span class="sxs-lookup"><span data-stu-id="f61a6-181">d.</span></span>  <span data-ttu-id="f61a6-182">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="f61a6-183">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f61a6-183">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f61a6-185">Op Hallo **TimeOffManager configuratie** sectie, klikt u op **configureren TimeOffManager** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f61a6-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f61a6-186">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f61a6-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuratiesectie TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="f61a6-188">In een ander browservenster, meld u bij uw bedrijf TimeOffManager site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f61a6-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="f61a6-189">Ga te**Account \> accountopties \> instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="f61a6-190">![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="f61a6-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="f61a6-191">In Hallo **instellingen voor eenmalige aanmelding** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f61a6-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f61a6-192">![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="f61a6-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="f61a6-193">a.</span><span class="sxs-lookup"><span data-stu-id="f61a6-193">a.</span></span> <span data-ttu-id="f61a6-194">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak Hallo gehele certificaat in **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="f61a6-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="f61a6-195">b.</span><span class="sxs-lookup"><span data-stu-id="f61a6-195">b.</span></span> <span data-ttu-id="f61a6-196">In **Idp verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f61a6-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="f61a6-197">c.</span><span class="sxs-lookup"><span data-stu-id="f61a6-197">c.</span></span> <span data-ttu-id="f61a6-198">In **IdP eindpunt-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f61a6-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="f61a6-199">d.</span><span class="sxs-lookup"><span data-stu-id="f61a6-199">d.</span></span> <span data-ttu-id="f61a6-200">Als **afdwingen SAML**, selecteer **Nee**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="f61a6-201">e.</span><span class="sxs-lookup"><span data-stu-id="f61a6-201">e.</span></span> <span data-ttu-id="f61a6-202">Als **gebruikers automatisch maken**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="f61a6-203">f.</span><span class="sxs-lookup"><span data-stu-id="f61a6-203">f.</span></span> <span data-ttu-id="f61a6-204">In **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f61a6-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="f61a6-205">g.</span><span class="sxs-lookup"><span data-stu-id="f61a6-205">g.</span></span> <span data-ttu-id="f61a6-206">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="f61a6-207">In **voor eenmalige aanmelding instellingen** pagina kopiëren Hallo-waarde van **Assertion Consumer Service-URL** en plak deze in Hallo **antwoord-URL** in het tekstvak onder **TimeOffManager Domein- en URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f61a6-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="f61a6-208">![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="f61a6-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="f61a6-209">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f61a6-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f61a6-210">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f61a6-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f61a6-211">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f61a6-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f61a6-212">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f61a6-212">Create an Azure AD test user</span></span>
<span data-ttu-id="f61a6-213">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f61a6-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f61a6-215">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f61a6-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f61a6-216">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f61a6-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f61a6-218">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Gebruikers en groepen--> alle gebruikers](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f61a6-220">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f61a6-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Knop toevoegen](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f61a6-222">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f61a6-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f61a6-224">a.</span><span class="sxs-lookup"><span data-stu-id="f61a6-224">a.</span></span> <span data-ttu-id="f61a6-225">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f61a6-226">b.</span><span class="sxs-lookup"><span data-stu-id="f61a6-226">b.</span></span> <span data-ttu-id="f61a6-227">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f61a6-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f61a6-228">c.</span><span class="sxs-lookup"><span data-stu-id="f61a6-228">c.</span></span> <span data-ttu-id="f61a6-229">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f61a6-230">d.</span><span class="sxs-lookup"><span data-stu-id="f61a6-230">d.</span></span> <span data-ttu-id="f61a6-231">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="f61a6-232">Een testgebruiker TimeOffManager maken</span><span class="sxs-lookup"><span data-stu-id="f61a6-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="f61a6-233">In de volgorde tooenable Azure AD gebruikers toolog in TimeOffManager, moeten ze ingerichte tooTimeOffManager zijn.</span><span class="sxs-lookup"><span data-stu-id="f61a6-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="f61a6-234">TimeOffManager ondersteunt alleen in de tijd van gebruikersinrichting.</span><span class="sxs-lookup"><span data-stu-id="f61a6-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="f61a6-235">Er is geen actie-item voor u.</span><span class="sxs-lookup"><span data-stu-id="f61a6-235">There is no action item for you.</span></span>  

<span data-ttu-id="f61a6-236">Hallo gebruikers worden automatisch toegevoegd tijdens de eerste aanmelding Hallo met eenmalige aanmelding op.</span><span class="sxs-lookup"><span data-stu-id="f61a6-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="f61a6-237">U kunt andere TimeOffManager gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TimeOffManager tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="f61a6-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f61a6-238">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f61a6-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f61a6-239">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTimeOffManager toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f61a6-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f61a6-241">**tooassign Britta Simon tooTimeOffManager, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f61a6-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="f61a6-242">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f61a6-244">Selecteer in de lijst met de toepassingen van Hallo **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager in lijst met Apps](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="f61a6-246">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f61a6-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f61a6-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f61a6-248">Click **Add** button.</span></span> <span data-ttu-id="f61a6-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f61a6-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f61a6-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f61a6-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f61a6-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f61a6-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f61a6-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f61a6-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f61a6-254">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f61a6-254">Test single sign-on</span></span>

<span data-ttu-id="f61a6-255">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f61a6-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f61a6-256">Als u op Hallo TimeOffManager tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TimeOffManager toepassing.</span><span class="sxs-lookup"><span data-stu-id="f61a6-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="f61a6-257">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f61a6-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f61a6-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f61a6-258">Additional resources</span></span>

* [<span data-ttu-id="f61a6-259">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f61a6-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f61a6-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f61a6-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

