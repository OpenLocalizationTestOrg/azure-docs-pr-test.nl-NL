---
title: 'Zelfstudie: Azure Active Directory-integratie met Trello | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Trello.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="b7728-103">Zelfstudie: Azure Active Directory-integratie met Trello</span><span class="sxs-lookup"><span data-stu-id="b7728-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="b7728-104">In deze zelfstudie leert u hoe toointegrate Trello met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7728-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7728-105">Trello integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b7728-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b7728-106">U kunt beheren in Azure AD die tooTrello toegang heeft</span><span class="sxs-lookup"><span data-stu-id="b7728-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="b7728-107">U kunt uw gebruikers tooautomatically get aangemelde tooTrello (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b7728-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7728-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b7728-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b7728-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7728-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7728-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b7728-110">Prerequisites</span></span>

<span data-ttu-id="b7728-111">Azure AD-integratie met Trello tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b7728-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="b7728-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b7728-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7728-113">Een Trello eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b7728-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7728-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b7728-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7728-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b7728-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7728-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b7728-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7728-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7728-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7728-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b7728-118">Scenario description</span></span>
<span data-ttu-id="b7728-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b7728-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7728-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b7728-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7728-121">Het toevoegen van Trello van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b7728-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="b7728-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b7728-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="b7728-123">Het toevoegen van Trello van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b7728-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="b7728-124">tooconfigure hello integratie van Trello in Azure AD, moet u tooadd Trello uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b7728-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b7728-125">**tooadd Trello via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7728-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7728-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b7728-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b7728-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b7728-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b7728-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b7728-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b7728-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7728-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b7728-133">Typ in het zoekvak Hallo **Trello**.</span><span class="sxs-lookup"><span data-stu-id="b7728-133">In hello search box, type **Trello**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="b7728-135">Selecteer in het deelvenster resultaten hello, **Trello**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b7728-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b7728-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b7728-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b7728-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Trello op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b7728-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7728-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Trello is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7728-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="b7728-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Trello toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b7728-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="b7728-141">Wijs in Trello, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="b7728-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b7728-142">tooconfigure en eenmalige aanmelding Azure AD-test met Trello, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7728-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b7728-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b7728-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b7728-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7728-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7728-145">**[Maken van een testgebruiker Trello](#creating-a-trello-test-user)**  -toohave een equivalent van Britta Simon in Trello die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b7728-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7728-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b7728-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7728-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b7728-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b7728-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b7728-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b7728-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Trello configureren.</span><span class="sxs-lookup"><span data-stu-id="b7728-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="b7728-150">**Azure AD tooconfigure eenmalige aanmelding met Trello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7728-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7728-151">In de Azure-portal op Hallo Hallo **Trello** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b7728-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b7728-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b7728-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="b7728-155">Op Hallo **Trello domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="b7728-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="b7728-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="b7728-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="b7728-158">Op Hallo **Trello domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="b7728-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="b7728-160">a.</span><span class="sxs-lookup"><span data-stu-id="b7728-160">a.</span></span> <span data-ttu-id="b7728-161">Klik op Hallo **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="b7728-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="b7728-162">b.</span><span class="sxs-lookup"><span data-stu-id="b7728-162">b.</span></span> <span data-ttu-id="b7728-163">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="b7728-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="b7728-164">Krijgt u Hallo  **\<enterprise\>**  slug van Trello.</span><span class="sxs-lookup"><span data-stu-id="b7728-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="b7728-165">Als u geen Hallo slug waarde, neem dan contact op met [Trello ondersteuningsteam](mailto:support@trello.com) tooget Hallo slug voor u enterprise.</span><span class="sxs-lookup"><span data-stu-id="b7728-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="b7728-166">Trello toepassing verwacht hello SAML asserties toocontain specifieke kenmerken.</span><span class="sxs-lookup"><span data-stu-id="b7728-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="b7728-167">Configureer Hallo kenmerken voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="b7728-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="b7728-168">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerken'** van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b7728-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="b7728-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="b7728-169">hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="b7728-171">Op Hallo **SAML-token kenmerken** dialoogvenster uitvoeren Hallo volgende stappen uit voor elke rij in Hallo tabel hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b7728-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="b7728-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b7728-172">Attribute Name</span></span> | <span data-ttu-id="b7728-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b7728-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="b7728-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="b7728-174">User.Email</span></span> | <span data-ttu-id="b7728-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="b7728-175">user.mail</span></span> |
    | <span data-ttu-id="b7728-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="b7728-176">User.FirstName</span></span> | <span data-ttu-id="b7728-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="b7728-177">user.givenname</span></span> |
    | <span data-ttu-id="b7728-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="b7728-178">User.LastName</span></span> | <span data-ttu-id="b7728-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="b7728-179">user.surname</span></span> |

    <span data-ttu-id="b7728-180">a.</span><span class="sxs-lookup"><span data-stu-id="b7728-180">a.</span></span> <span data-ttu-id="b7728-181">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7728-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="b7728-184">b.</span><span class="sxs-lookup"><span data-stu-id="b7728-184">b.</span></span> <span data-ttu-id="b7728-185">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b7728-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="b7728-186">c.</span><span class="sxs-lookup"><span data-stu-id="b7728-186">c.</span></span> <span data-ttu-id="b7728-187">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b7728-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b7728-188">d.</span><span class="sxs-lookup"><span data-stu-id="b7728-188">d.</span></span> <span data-ttu-id="b7728-189">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7728-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="b7728-190">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b7728-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="b7728-192">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b7728-192">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b7728-194">Op Hallo **Trello configuratie** sectie, klikt u op **configureren Trello** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b7728-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b7728-195">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b7728-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="b7728-197">tooget SSO is geconfigureerd voor uw toepassing gaat te[Trello SSO Ondernemingsconfiguratie](https://trello.com/sso-configuration) pagina toosend [Trello ondersteuningsteam](mailto:support@trello.com) hello **SAML Single Sign-On Service-URL** en Hallo koppelen **certificaat (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="b7728-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="b7728-198">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b7728-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b7728-199">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b7728-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b7728-200">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b7728-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b7728-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b7728-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="b7728-202">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b7728-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b7728-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7728-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7728-205">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b7728-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b7728-207">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b7728-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b7728-209">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b7728-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7728-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7728-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b7728-213">a.</span><span class="sxs-lookup"><span data-stu-id="b7728-213">a.</span></span> <span data-ttu-id="b7728-214">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7728-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7728-215">b.</span><span class="sxs-lookup"><span data-stu-id="b7728-215">b.</span></span> <span data-ttu-id="b7728-216">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b7728-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b7728-217">c.</span><span class="sxs-lookup"><span data-stu-id="b7728-217">c.</span></span> <span data-ttu-id="b7728-218">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b7728-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b7728-219">d.</span><span class="sxs-lookup"><span data-stu-id="b7728-219">d.</span></span> <span data-ttu-id="b7728-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b7728-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="b7728-221">Een testgebruiker Trello maken</span><span class="sxs-lookup"><span data-stu-id="b7728-221">Creating a Trello test user</span></span>

<span data-ttu-id="b7728-222">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Trello maken.</span><span class="sxs-lookup"><span data-stu-id="b7728-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="b7728-223">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Trello maken.</span><span class="sxs-lookup"><span data-stu-id="b7728-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="b7728-224">Trello ondersteuning biedt voor just-in-time-inrichting en een nieuw account is gemaakt Hallo eerste keer dat u zich aanmeldt vanuit Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7728-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b7728-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7728-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b7728-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTrello toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="b7728-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b7728-228">**tooassign Britta Simon tooTrello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7728-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7728-229">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b7728-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b7728-231">Selecteer in de lijst met de toepassingen van Hallo **Trello**.</span><span class="sxs-lookup"><span data-stu-id="b7728-231">In hello applications list, select **Trello**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="b7728-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b7728-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b7728-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b7728-235">Click **Add** button.</span></span> <span data-ttu-id="b7728-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7728-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b7728-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7728-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b7728-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7728-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7728-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7728-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b7728-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b7728-241">Testing single sign-on</span></span>

<span data-ttu-id="b7728-242">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b7728-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b7728-243">Als u op Hallo Trello tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Trello toepassing.</span><span class="sxs-lookup"><span data-stu-id="b7728-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7728-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b7728-244">Additional resources</span></span>

* [<span data-ttu-id="b7728-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7728-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7728-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7728-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

