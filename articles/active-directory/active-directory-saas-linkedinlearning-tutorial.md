---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn Learning | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LinkedIn daarvan te leren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="d2051-103">Zelfstudie: Azure Active Directory-integratie met LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="d2051-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="d2051-104">In deze zelfstudie leert u hoe toointegrate LinkedIn Learning met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2051-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2051-105">LinkedIn Learning integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d2051-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d2051-106">U kunt beheren in Azure AD wie toegang tot tooLinkedIn heeft leren</span><span class="sxs-lookup"><span data-stu-id="d2051-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="d2051-107">U kunt uw gebruikers tooautomatically get aangemelde tooLinkedIn inschakelen Learning (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="d2051-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2051-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d2051-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d2051-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2051-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2051-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d2051-110">Prerequisites</span></span>

<span data-ttu-id="d2051-111">Azure AD-integratie met LinkedIn Learning tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d2051-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="d2051-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d2051-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2051-113">Een LinkedIn Learning eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d2051-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d2051-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d2051-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d2051-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d2051-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2051-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d2051-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d2051-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2051-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2051-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d2051-118">Scenario description</span></span>
<span data-ttu-id="d2051-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d2051-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2051-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d2051-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2051-121">Het toevoegen van LinkedIn Learning van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d2051-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="d2051-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d2051-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="d2051-123">Het toevoegen van LinkedIn Learning van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d2051-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="d2051-124">tooconfigure hello integratie van LinkedIn Learning in Azure AD, moet u tooadd LinkedIn Learning uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d2051-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d2051-125">**tooadd LinkedIn leren van Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d2051-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2051-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d2051-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d2051-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d2051-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d2051-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d2051-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d2051-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d2051-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d2051-133">Typ in het zoekvak Hallo **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="d2051-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="d2051-134">Klik in het deelvenster met resultaten, op **LinkedIn Learning** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d2051-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d2051-136">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d2051-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d2051-137">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met LinkedIn Learning op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d2051-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d2051-138">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LinkedIn Learning is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2051-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="d2051-139">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in LinkedIn Learning toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d2051-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="d2051-140">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** LinkedIn weten.</span><span class="sxs-lookup"><span data-stu-id="d2051-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="d2051-141">tooconfigure en test eenmalige aanmelding Azure AD met LinkedIn Learning, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2051-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d2051-142">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d2051-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d2051-143">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2051-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2051-144">**[Maken van een testgebruiker LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2051-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="d2051-145">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d2051-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2051-146">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d2051-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d2051-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d2051-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d2051-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="d2051-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="d2051-149">**Voer tooconfigure Azure AD eenmalige aanmelding met LinkedIn-Learning Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d2051-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2051-150">In de Azure-portal op Hallo Hallo **LinkedIn Learning** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d2051-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d2051-152">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d2051-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="d2051-154">In een ander browservenster, aanmelding tooyour LinkedIn Learning tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d2051-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="d2051-155">In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d2051-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="d2051-156">Schakel ook **Learning - standaard** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2051-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="d2051-158">Klik op **of Klik hier tooload en kopieert u afzonderlijke velden uit Hallo formulier** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**</span><span class="sxs-lookup"><span data-stu-id="d2051-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="d2051-160">Op de Azure-portal onder **LinkedIn Learning domein en de URL's**, uitvoeren van de volgende stappen uit als u wilt dat tooconfigure SSO Hallo in **IdP geïnitieerd** modus</span><span class="sxs-lookup"><span data-stu-id="d2051-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="d2051-162">a.</span><span class="sxs-lookup"><span data-stu-id="d2051-162">a.</span></span> <span data-ttu-id="d2051-163">In Hallo **id** textbox Voer Hallo **entiteit-ID** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="d2051-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="d2051-164">b.</span><span class="sxs-lookup"><span data-stu-id="d2051-164">b.</span></span> <span data-ttu-id="d2051-165">In Hallo **antwoord-URL** textbox Voer Hallo **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="d2051-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="d2051-166">Als u wilt dat tooconfigure SSO in **SP geïnitieerd**, klikt u op geavanceerde URL weergeven instelling optie in de configuratiesectie Hallo en Hallo aanmeldings-URL configureren met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="d2051-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="d2051-168">Uw toepassing LinkedIn Learning verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="d2051-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="d2051-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="d2051-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="d2051-170">Hallo standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn Learning deze toobe toegewezen met e-mailadres van de gebruiker Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="d2051-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="d2051-171">Die u kunt **user.mail** kenmerk uit de lijst Hallo of Hallo juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2051-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="d2051-173">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="d2051-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="d2051-174">Hallo-gebruiker moet vier tooadd-claims met de naam **e**, **afdeling**, **firstname**, en **lastname** en Hallo-waarde is toegewezen met toobe **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk</span><span class="sxs-lookup"><span data-stu-id="d2051-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="d2051-175">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="d2051-175">Attribute Name</span></span> | <span data-ttu-id="d2051-176">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="d2051-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d2051-177">E-mail</span><span class="sxs-lookup"><span data-stu-id="d2051-177">email</span></span>| <span data-ttu-id="d2051-178">User.mail</span><span class="sxs-lookup"><span data-stu-id="d2051-178">user.mail</span></span> |    
    | <span data-ttu-id="d2051-179">Afdeling</span><span class="sxs-lookup"><span data-stu-id="d2051-179">department</span></span>| <span data-ttu-id="d2051-180">User.Department</span><span class="sxs-lookup"><span data-stu-id="d2051-180">user.department</span></span> |
    | <span data-ttu-id="d2051-181">Voornaam</span><span class="sxs-lookup"><span data-stu-id="d2051-181">firstname</span></span>| <span data-ttu-id="d2051-182">User.givenName</span><span class="sxs-lookup"><span data-stu-id="d2051-182">user.givenname</span></span> |
    | <span data-ttu-id="d2051-183">Achternaam</span><span class="sxs-lookup"><span data-stu-id="d2051-183">lastname</span></span>| <span data-ttu-id="d2051-184">User.surname</span><span class="sxs-lookup"><span data-stu-id="d2051-184">user.surname</span></span> |
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="d2051-186">a.</span><span class="sxs-lookup"><span data-stu-id="d2051-186">a.</span></span> <span data-ttu-id="d2051-187">Klik op **kenmerk toevoegen** dialoogvenster tooopen Hallo-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d2051-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="d2051-190">b.</span><span class="sxs-lookup"><span data-stu-id="d2051-190">b.</span></span> <span data-ttu-id="d2051-191">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="d2051-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d2051-192">c.</span><span class="sxs-lookup"><span data-stu-id="d2051-192">c.</span></span> <span data-ttu-id="d2051-193">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="d2051-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d2051-194">d.</span><span class="sxs-lookup"><span data-stu-id="d2051-194">d.</span></span> <span data-ttu-id="d2051-195">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="d2051-195">Click **Ok**</span></span>

10. <span data-ttu-id="d2051-196">Uitvoeren van de volgende stappen uit op Hallo Hallo **naam** kenmerk -</span><span class="sxs-lookup"><span data-stu-id="d2051-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="d2051-197">a.</span><span class="sxs-lookup"><span data-stu-id="d2051-197">a.</span></span> <span data-ttu-id="d2051-198">Klik op Hallo kenmerk tooopen hello **kenmerk bewerken** venster.</span><span class="sxs-lookup"><span data-stu-id="d2051-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="d2051-200">b.</span><span class="sxs-lookup"><span data-stu-id="d2051-200">b.</span></span> <span data-ttu-id="d2051-201">Hallo URL waarde verwijderen uit Hallo **naamruimte**.</span><span class="sxs-lookup"><span data-stu-id="d2051-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="d2051-202">c.</span><span class="sxs-lookup"><span data-stu-id="d2051-202">c.</span></span> <span data-ttu-id="d2051-203">Klik op **Ok** toosave Hallo-instelling.</span><span class="sxs-lookup"><span data-stu-id="d2051-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="d2051-204">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d2051-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="d2051-206">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d2051-206">Click **Save**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="d2051-208">Ga te**LinkedIn beheerdersinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="d2051-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="d2051-209">Hallo XML-bestand die u hebt gedownload van hello Azure-portal door te klikken op de optie Hallo uploaden XML-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="d2051-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="d2051-211">Klik op **op** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d2051-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="d2051-212">Status SSO wordt gewijzigd van **niet verbonden** te**verbonden**</span><span class="sxs-lookup"><span data-stu-id="d2051-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d2051-214">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d2051-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="d2051-215">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d2051-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d2051-217">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d2051-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2051-218">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d2051-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2051-220">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d2051-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2051-222">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d2051-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2051-224">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2051-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2051-226">a.</span><span class="sxs-lookup"><span data-stu-id="d2051-226">a.</span></span> <span data-ttu-id="d2051-227">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2051-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2051-228">b.</span><span class="sxs-lookup"><span data-stu-id="d2051-228">b.</span></span> <span data-ttu-id="d2051-229">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d2051-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2051-230">c.</span><span class="sxs-lookup"><span data-stu-id="d2051-230">c.</span></span> <span data-ttu-id="d2051-231">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d2051-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d2051-232">d.</span><span class="sxs-lookup"><span data-stu-id="d2051-232">d.</span></span> <span data-ttu-id="d2051-233">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2051-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="d2051-234">Een testgebruiker LinkedIn Learning maken</span><span class="sxs-lookup"><span data-stu-id="d2051-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="d2051-235">Gekoppelde Learning toepassing ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="d2051-235">Linked Learning Application supports.</span></span> <span data-ttu-id="d2051-236">Alleen bij tijd gebruikers inrichten en na verificatie zijn gebruikers in de toepassing hello automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d2051-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="d2051-237">Op Hallo beheerder instellingenpagina op Hallo LinkedIn Learning portal spiegelen Hallo switch **automatisch toewijzen van licenties** tooactive tooenable NET tijd inrichten en dit wordt ook een licentie toohello gebruiker toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d2051-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d2051-239">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2051-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d2051-240">In deze sectie u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLinkedIn leren.</span><span class="sxs-lookup"><span data-stu-id="d2051-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d2051-242">**tooassign Britta Simon tooLinkedIn leren, Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d2051-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2051-243">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d2051-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d2051-245">Selecteer in de lijst met de toepassingen van Hallo **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="d2051-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="d2051-247">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d2051-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d2051-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d2051-249">Click **Add** button.</span></span> <span data-ttu-id="d2051-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2051-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d2051-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2051-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d2051-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2051-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2051-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2051-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d2051-255">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d2051-255">Testing single sign-on</span></span>

<span data-ttu-id="d2051-256">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d2051-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d2051-257">Als u op Hallo LinkedIn Learning tegel in Hallo Toegangsvenster, krijgt u hello Azure aanmelding pagina en op na geslaagde aanmelding, krijgt u in uw toepassing LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="d2051-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2051-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d2051-258">Additional resources</span></span>

* [<span data-ttu-id="d2051-259">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2051-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2051-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d2051-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png