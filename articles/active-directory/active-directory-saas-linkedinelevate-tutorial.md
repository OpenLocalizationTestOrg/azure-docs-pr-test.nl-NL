---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn uitbreiden | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LinkedIn uitbreiden.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="89103-103">Zelfstudie: Azure Active Directory-integratie met LinkedIn uitbreiden</span><span class="sxs-lookup"><span data-stu-id="89103-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="89103-104">In deze zelfstudie leert u hoe toointegrate LinkedIn uitbreiden met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89103-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89103-105">LinkedIn bevoegdheden integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="89103-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89103-106">U kunt beheren in Azure AD wie toegang tot tooLinkedIn uitbreiden heeft</span><span class="sxs-lookup"><span data-stu-id="89103-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="89103-107">U kunt uw gebruikers tooautomatically get aangemelde tooLinkedIn uitbreiden (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="89103-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89103-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="89103-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="89103-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89103-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89103-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="89103-110">Prerequisites</span></span>

<span data-ttu-id="89103-111">tooconfigure Azure AD-integratie met LinkedIn uitbreiden, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="89103-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="89103-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="89103-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89103-113">Een LinkedIn bevoegdheden eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="89103-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89103-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="89103-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89103-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="89103-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89103-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="89103-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="89103-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89103-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89103-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="89103-118">Scenario description</span></span>
<span data-ttu-id="89103-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="89103-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89103-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="89103-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89103-121">Het toevoegen van LinkedIn worden de bevoegdheden van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="89103-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="89103-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89103-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="89103-123">Het toevoegen van LinkedIn worden de bevoegdheden van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="89103-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="89103-124">tooconfigure hello integratie van LinkedIn bevoegdheden in Azure AD, moet u tooadd LinkedIn worden de bevoegdheden van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="89103-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89103-125">**tooadd LinkedIn bevoegdheden uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89103-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89103-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89103-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89103-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89103-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89103-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89103-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="89103-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="89103-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="89103-133">Typ in het zoekvak Hallo **LinkedIn bevoegdheden**.</span><span class="sxs-lookup"><span data-stu-id="89103-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="89103-134">Klik in het deelvenster met resultaten, op **LinkedIn bevoegdheden** tooadd Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="89103-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89103-136">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89103-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89103-137">In deze sectie configureert en test eenmalige aanmelding Azure AD met LinkedIn worden de bevoegdheden op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="89103-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89103-138">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LinkedIn worden de bevoegdheden is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89103-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="89103-139">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in LinkedIn bevoegdheden toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="89103-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="89103-140">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in LinkedIn uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="89103-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="89103-141">tooconfigure en eenmalige aanmelding Azure AD-test met LinkedIn uitbreiden, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89103-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89103-142">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="89103-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89103-143">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89103-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89103-144">**[Maken van een testgebruiker LinkedIn bevoegdheden](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89103-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="89103-145">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89103-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89103-146">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="89103-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89103-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="89103-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89103-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing LinkedIn uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="89103-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="89103-149">**Voer tooconfigure Azure AD eenmalige aanmelding met de bevoegdheden LinkedIn, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89103-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="89103-150">In hello Azure Management portal op Hallo **LinkedIn bevoegdheden** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="89103-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="89103-152">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89103-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="89103-154">In een ander browservenster, aanmelding tooyour tenant LinkedIn bevoegdheden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="89103-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="89103-155">In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="89103-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="89103-156">Schakel ook **uitbreiden - AAD-Test worden de bevoegdheden** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="89103-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="89103-158">Klik op **of Klik hier tooload en kopieert u afzonderlijke velden uit Hallo formulier** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**</span><span class="sxs-lookup"><span data-stu-id="89103-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="89103-160">Op de Azure-Portal onder **LinkedIn bevoegdheden domein en de URL's**, uitvoeren van de volgende stappen uit als u wilt dat tooconfigure SSO Hallo in **IdP geïnitieerd** modus</span><span class="sxs-lookup"><span data-stu-id="89103-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="89103-162">a.</span><span class="sxs-lookup"><span data-stu-id="89103-162">a.</span></span> <span data-ttu-id="89103-163">In Hallo **id** textbox Voer Hallo **entiteit-ID** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="89103-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="89103-164">b.</span><span class="sxs-lookup"><span data-stu-id="89103-164">b.</span></span> <span data-ttu-id="89103-165">In Hallo **antwoord-URL** textbox Voer Hallo **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="89103-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="89103-166">Als u wilt dat tooconfigure SSO in **SP geïnitieerd**, klikt u op geavanceerde URL weergeven instelling optie in de configuratiesectie Hallo en Hallo aanmeldingsopties configureren op de URL voor Hello patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="89103-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="89103-168">Uw toepassing LinkedIn bevoegdheden verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="89103-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="89103-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="89103-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="89103-170">de standaardwaarde van Hallo **gebruikers-id** is **user.userprincipalname** , maar deze toobe toegewezen met e-mailadres van de gebruiker Hallo LinkedIn bevoegdheden verwacht.</span><span class="sxs-lookup"><span data-stu-id="89103-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="89103-171">Die u kunt **user.mail** kenmerk uit de lijst Hallo of Hallo juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="89103-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="89103-173">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="89103-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="89103-174">U moet tooadd een andere claim met de naam **afdeling** en Hallo-waarde moet toobe te toegewezen**user.department**.</span><span class="sxs-lookup"><span data-stu-id="89103-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="89103-175">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="89103-175">Attribute Name</span></span> | <span data-ttu-id="89103-176">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="89103-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="89103-177">Afdeling</span><span class="sxs-lookup"><span data-stu-id="89103-177">department</span></span>| <span data-ttu-id="89103-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="89103-178">user.department</span></span> |

      ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="89103-180">a.</span><span class="sxs-lookup"><span data-stu-id="89103-180">a.</span></span> <span data-ttu-id="89103-181">Klik op de detailpagina toevoegen kenmerk tooopen Hallo kenmerk Hallo afdeling kenmerk toevoegen, zoals hieronder-</span><span class="sxs-lookup"><span data-stu-id="89103-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="89103-183">b.</span><span class="sxs-lookup"><span data-stu-id="89103-183">b.</span></span> <span data-ttu-id="89103-184">Klik op **Ok** toosave Hallo-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="89103-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="89103-185">c.</span><span class="sxs-lookup"><span data-stu-id="89103-185">c.</span></span> <span data-ttu-id="89103-186">Hallo naam wijzigen van Hallo kenmerk **emailaddress** te**e**.</span><span class="sxs-lookup"><span data-stu-id="89103-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="89103-187">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="89103-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="89103-189">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="89103-189">Click **Save**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="89103-191">Ga te**LinkedIn beheerdersinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="89103-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="89103-192">Hallo XML-bestand die u zojuist hebt gedownload van hello Azure-portal door te klikken op Hallo optie uploaden XML-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="89103-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="89103-194">Klik op **op** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89103-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="89103-195">Status SSO wordt gewijzigd van **niet verbonden** te**verbonden**</span><span class="sxs-lookup"><span data-stu-id="89103-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89103-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="89103-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="89103-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="89103-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="89103-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89103-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89103-201">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89103-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89103-203">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="89103-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89103-205">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89103-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89103-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89103-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89103-209">a.</span><span class="sxs-lookup"><span data-stu-id="89103-209">a.</span></span> <span data-ttu-id="89103-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89103-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89103-211">b.</span><span class="sxs-lookup"><span data-stu-id="89103-211">b.</span></span> <span data-ttu-id="89103-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="89103-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89103-213">c.</span><span class="sxs-lookup"><span data-stu-id="89103-213">c.</span></span> <span data-ttu-id="89103-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="89103-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="89103-215">d.</span><span class="sxs-lookup"><span data-stu-id="89103-215">d.</span></span> <span data-ttu-id="89103-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="89103-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="89103-217">Maken van een testgebruiker LinkedIn uitbreiden</span><span class="sxs-lookup"><span data-stu-id="89103-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="89103-218">Gekoppelde bevoegdheden toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="89103-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="89103-219">Op Hallo beheerder instellingenpagina op Hallo LinkedIn bevoegdheden portal spiegelen Hallo switch **automatisch toewijzen van licenties** tooactive tooenable NET tijd inrichten en dit wordt ook een licentie toohello gebruiker toewijzen.</span><span class="sxs-lookup"><span data-stu-id="89103-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="89103-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="89103-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="89103-222">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door toe te kennen haar toegang tooLinkedIn uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="89103-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="89103-224">**tooassign Britta Simon tooLinkedIn uitbreiden, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89103-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="89103-225">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89103-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="89103-227">Selecteer in de lijst met de toepassingen van Hallo **LinkedIn bevoegdheden**.</span><span class="sxs-lookup"><span data-stu-id="89103-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="89103-229">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="89103-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="89103-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="89103-231">Click **Add** button.</span></span> <span data-ttu-id="89103-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89103-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="89103-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="89103-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89103-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89103-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89103-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89103-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89103-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89103-237">Testing single sign-on</span></span>

<span data-ttu-id="89103-238">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="89103-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89103-239">Als u op Hallo LinkedIn bevoegdheden tegel in Hallo Toegangsvenster, krijgt u hello Azure aanmelding pagina en op na geslaagde aanmelding, krijgt u in uw toepassing LinkedIn uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="89103-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89103-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="89103-240">Additional resources</span></span>

* [<span data-ttu-id="89103-241">Zelfstudie: LinkedIn bevoegdheden configureren voor automatisch gebruikers inrichten met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89103-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="89103-242">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89103-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89103-243">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89103-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
