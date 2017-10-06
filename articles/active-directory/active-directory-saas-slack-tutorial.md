---
title: 'Zelfstudie: Azure Active Directory-integratie met Slack | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en de toegestane vertraging.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="cf119-103">Zelfstudie: Azure Active Directory-integratie met Slack</span><span class="sxs-lookup"><span data-stu-id="cf119-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="cf119-104">In deze zelfstudie leert u hoe toointegrate vertraging bij Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf119-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf119-105">Vertraging integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="cf119-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cf119-106">U kunt beheren in Azure AD die tooSlack toegang heeft</span><span class="sxs-lookup"><span data-stu-id="cf119-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="cf119-107">U kunt uw gebruikers tooautomatically get aangemelde tooSlack (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="cf119-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf119-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="cf119-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cf119-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf119-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf119-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cf119-110">Prerequisites</span></span>

<span data-ttu-id="cf119-111">Azure AD-integratie met Slack tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="cf119-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="cf119-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="cf119-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf119-113">Een toegestane eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="cf119-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf119-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cf119-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf119-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="cf119-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf119-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="cf119-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf119-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf119-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf119-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cf119-118">Scenario description</span></span>
<span data-ttu-id="cf119-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="cf119-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf119-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="cf119-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf119-121">Het toevoegen van vertraging van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cf119-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="cf119-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf119-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="cf119-123">Het toevoegen van vertraging van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cf119-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="cf119-124">Hallo-integratie tooconfigure vertraging met Azure AD, moet u tooadd Slack uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="cf119-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cf119-125">**tooadd Slack via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cf119-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf119-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cf119-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf119-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf119-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cf119-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf119-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="cf119-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf119-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="cf119-133">Typ in het zoekvak Hallo **Slack**.</span><span class="sxs-lookup"><span data-stu-id="cf119-133">In hello search box, type **Slack**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="cf119-135">Selecteer in het deelvenster resultaten hello, **Slack**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cf119-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf119-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf119-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf119-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Slack op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="cf119-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf119-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Slack is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf119-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="cf119-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Slack toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="cf119-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="cf119-141">In Slack, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="cf119-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cf119-142">tooconfigure en eenmalige aanmelding Azure AD-test met Slack, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf119-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cf119-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="cf119-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cf119-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf119-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf119-145">**[Maken van een toegestane testgebruiker](#creating-a-slack-test-user)**  -toohave een equivalent van Britta Simon in Slack die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cf119-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf119-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cf119-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf119-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="cf119-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf119-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="cf119-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf119-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing toegestane configureren.</span><span class="sxs-lookup"><span data-stu-id="cf119-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="cf119-150">**Voer tooconfigure Azure AD eenmalige aanmelding met vertraging Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cf119-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf119-151">In de Azure-portal op Hallo Hallo **Slack** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="cf119-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="cf119-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cf119-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="cf119-155">Op Hallo **Slack-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf119-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="cf119-157">a.</span><span class="sxs-lookup"><span data-stu-id="cf119-157">a.</span></span> <span data-ttu-id="cf119-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="cf119-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="cf119-159">b.</span><span class="sxs-lookup"><span data-stu-id="cf119-159">b.</span></span> <span data-ttu-id="cf119-160">In Hallo **id** textbox type Hallo URL:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="cf119-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cf119-161">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="cf119-161">hello value is not real.</span></span> <span data-ttu-id="cf119-162">U hebt tooupdate de waarde Hallo met Hallo werkelijke aanmelding op URL.</span><span class="sxs-lookup"><span data-stu-id="cf119-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="cf119-163">Neem contact op met [toegestane ondersteuningsteam](https://slack.com/help/contact) tooget Hallo waarde</span><span class="sxs-lookup"><span data-stu-id="cf119-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="cf119-164">Toegestane toepassing verwacht Hallo SAML asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="cf119-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="cf119-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="cf119-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="cf119-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="cf119-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="cf119-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="cf119-167">hello following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="cf119-169">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **user.mail** als **gebruikers-id** en voor elke rij die wordt weergegeven Voer in Hallo onderstaande tabel Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf119-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="cf119-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="cf119-170">Attribute Name</span></span> | <span data-ttu-id="cf119-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="cf119-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="cf119-172">Voornaam</span><span class="sxs-lookup"><span data-stu-id="cf119-172">first_name</span></span> | <span data-ttu-id="cf119-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="cf119-173">user.givenname</span></span> |
    | <span data-ttu-id="cf119-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="cf119-174">last_name</span></span> | <span data-ttu-id="cf119-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="cf119-175">user.surname</span></span> |
    | <span data-ttu-id="cf119-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="cf119-176">User.Email</span></span> | <span data-ttu-id="cf119-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="cf119-177">user.mail</span></span> |  
    | <span data-ttu-id="cf119-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="cf119-178">User.Username</span></span> | <span data-ttu-id="cf119-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="cf119-179">user.userprincipalname</span></span> |

    <span data-ttu-id="cf119-180">a.</span><span class="sxs-lookup"><span data-stu-id="cf119-180">a.</span></span> <span data-ttu-id="cf119-181">Klik op **kenmerk** tooopen **kenmerk bewerken** dialoogvenster vak en Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="cf119-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="cf119-183">a.</span><span class="sxs-lookup"><span data-stu-id="cf119-183">a.</span></span> <span data-ttu-id="cf119-184">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="cf119-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cf119-185">b.</span><span class="sxs-lookup"><span data-stu-id="cf119-185">b.</span></span> <span data-ttu-id="cf119-186">Van Hallo **waarde** wilt weergeven, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="cf119-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cf119-187">c.</span><span class="sxs-lookup"><span data-stu-id="cf119-187">c.</span></span> <span data-ttu-id="cf119-188">Klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="cf119-188">Click **OK**</span></span>

6. <span data-ttu-id="cf119-189">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cf119-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="cf119-191">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="cf119-191">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cf119-193">Op Hallo **Slack configuratie** sectie, klikt u op **Slack configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="cf119-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cf119-194">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="cf119-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="cf119-196">In een ander browservenster, meld u aan tooyour toegestane bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="cf119-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="cf119-197">Navigeer te**Microsoft Azure AD** gaat u verder te**instellingen Team**.</span><span class="sxs-lookup"><span data-stu-id="cf119-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="cf119-199">In Hallo **instellingen Team** sectie, klikt u op Hallo **verificatie** tabblad en klik vervolgens op **Wijzigingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="cf119-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="cf119-201">Op Hallo **SAML-verificatie-instellingen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="cf119-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="cf119-203">a.</span><span class="sxs-lookup"><span data-stu-id="cf119-203">a.</span></span>  <span data-ttu-id="cf119-204">In Hallo **SAML 2.0-eindpunt (HTTP)** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cf119-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cf119-205">b.</span><span class="sxs-lookup"><span data-stu-id="cf119-205">b.</span></span>  <span data-ttu-id="cf119-206">In Hallo **identiteit Provider verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cf119-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cf119-207">c.</span><span class="sxs-lookup"><span data-stu-id="cf119-207">c.</span></span>  <span data-ttu-id="cf119-208">Open uw gedownloade certificaat-bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **openbaar certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="cf119-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="cf119-209">d.</span><span class="sxs-lookup"><span data-stu-id="cf119-209">d.</span></span> <span data-ttu-id="cf119-210">Hallo bovenstaande drie instellingen geschikt is voor uw team toegestane configureren.</span><span class="sxs-lookup"><span data-stu-id="cf119-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="cf119-211">Vinden voor meer informatie over instellingen voor Hallo Hallo **vertraging van SSO configuratiehandleiding** hier.</span><span class="sxs-lookup"><span data-stu-id="cf119-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="cf119-212">e.</span><span class="sxs-lookup"><span data-stu-id="cf119-212">e.</span></span>  <span data-ttu-id="cf119-213">Klik op **configuratie op te slaan**.</span><span class="sxs-lookup"><span data-stu-id="cf119-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="cf119-214">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="cf119-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cf119-215">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="cf119-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cf119-216">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf119-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf119-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cf119-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf119-218">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cf119-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="cf119-220">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cf119-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf119-221">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cf119-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf119-223">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cf119-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf119-225">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="cf119-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf119-227">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf119-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf119-229">a.</span><span class="sxs-lookup"><span data-stu-id="cf119-229">a.</span></span> <span data-ttu-id="cf119-230">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf119-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf119-231">b.</span><span class="sxs-lookup"><span data-stu-id="cf119-231">b.</span></span> <span data-ttu-id="cf119-232">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf119-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf119-233">c.</span><span class="sxs-lookup"><span data-stu-id="cf119-233">c.</span></span> <span data-ttu-id="cf119-234">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="cf119-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cf119-235">d.</span><span class="sxs-lookup"><span data-stu-id="cf119-235">d.</span></span> <span data-ttu-id="cf119-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cf119-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="cf119-237">Een toegestane testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cf119-237">Creating a Slack test user</span></span>

<span data-ttu-id="cf119-238">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Slack van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cf119-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="cf119-239">Vertraging ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cf119-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cf119-240">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="cf119-240">There is no action item for you in this section.</span></span> <span data-ttu-id="cf119-241">Een nieuwe gebruiker wordt tijdens een poging tooaccess Slack gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="cf119-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="cf119-242">Als u een gebruiker toocreate handmatig nodig hebt, moet u tooContact [toegestane ondersteuningsteam](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="cf119-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cf119-243">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf119-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cf119-244">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSlack toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="cf119-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="cf119-246">**tooassign Britta Simon tooSlack, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cf119-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf119-247">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf119-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="cf119-249">Selecteer in de lijst met de toepassingen van Hallo **Slack**.</span><span class="sxs-lookup"><span data-stu-id="cf119-249">In hello applications list, select **Slack**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="cf119-251">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="cf119-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="cf119-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="cf119-253">Click **Add** button.</span></span> <span data-ttu-id="cf119-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf119-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="cf119-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="cf119-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cf119-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf119-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf119-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf119-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf119-259">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf119-259">Testing single sign-on</span></span>

<span data-ttu-id="cf119-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="cf119-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cf119-261">Wanneer u klikt op Hallo toegestane tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour toegestane toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cf119-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf119-262">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cf119-262">Additional resources</span></span>

* [<span data-ttu-id="cf119-263">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf119-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf119-264">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf119-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

