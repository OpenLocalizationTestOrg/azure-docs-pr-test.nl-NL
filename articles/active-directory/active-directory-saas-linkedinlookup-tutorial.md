---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LinkedIn opzoeken.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="b43ee-103">Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="b43ee-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="b43ee-104">In deze zelfstudie leert u hoe toointegrate LinkedIn Lookup met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b43ee-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b43ee-105">LinkedIn Lookup integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b43ee-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b43ee-106">U kunt beheren in Azure AD wie toegang tot tooLinkedIn Lookup heeft</span><span class="sxs-lookup"><span data-stu-id="b43ee-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="b43ee-107">U kunt uw gebruikers tooautomatically get aangemelde tooLinkedIn Lookup (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b43ee-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b43ee-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b43ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b43ee-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b43ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b43ee-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b43ee-110">Prerequisites</span></span>

<span data-ttu-id="b43ee-111">Azure AD-integratie met LinkedIn Lookup tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b43ee-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="b43ee-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b43ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b43ee-113">Een LinkedIn Lookup eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b43ee-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b43ee-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b43ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b43ee-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b43ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b43ee-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b43ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b43ee-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b43ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b43ee-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b43ee-118">Scenario description</span></span>
<span data-ttu-id="b43ee-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b43ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b43ee-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b43ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b43ee-121">Het toevoegen van LinkedIn Lookup van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b43ee-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="b43ee-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b43ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="b43ee-123">Het toevoegen van LinkedIn Lookup van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b43ee-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="b43ee-124">tooconfigure hello integratie van LinkedIn zoeken in Azure AD, moet u tooadd LinkedIn Lookup uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b43ee-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b43ee-125">**tooadd LinkedIn Lookup via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b43ee-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b43ee-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b43ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b43ee-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b43ee-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b43ee-131">Klik op **nieuwe toepassing** knop bovenaan Hallo van Hallo dialoogvenster tooadd nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="b43ee-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b43ee-133">Typ in het zoekvak Hallo **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="b43ee-135">Selecteer in het deelvenster resultaten hello, **LinkedIn Lookup**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b43ee-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b43ee-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b43ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b43ee-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met LinkedIn opzoeken op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b43ee-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b43ee-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LinkedIn Lookup is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="b43ee-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in LinkedIn Lookup toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b43ee-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="b43ee-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in LinkedIn opzoeken.</span><span class="sxs-lookup"><span data-stu-id="b43ee-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="b43ee-142">tooconfigure en eenmalige aanmelding Azure AD-test met LinkedIn opzoeken, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b43ee-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b43ee-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b43ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b43ee-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b43ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b43ee-145">**[Maken van een testgebruiker LinkedIn Lookup](#creating-an-linkedin-lookup-test-user)**  -toohave een equivalent van Britta Simon in LinkedIn Lookup die is gekoppeld toohello Azure AD-weergave.</span><span class="sxs-lookup"><span data-stu-id="b43ee-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="b43ee-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b43ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b43ee-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b43ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b43ee-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b43ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b43ee-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LinkedIn Lookup configureren.</span><span class="sxs-lookup"><span data-stu-id="b43ee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="b43ee-150">**Voer tooconfigure Azure AD eenmalige aanmelding met LinkedIn-Lookup, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b43ee-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="b43ee-151">In de Azure-portal op Hallo Hallo **LinkedIn Lookup** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b43ee-153">Op Hallo **eenmalige aanmelding** dialoogvenster in **modus** Selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b43ee-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="b43ee-155">In een andere web-browservenster aanmelding tooyour **LinkedIn Lookup** website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b43ee-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="b43ee-156">In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="b43ee-157">Schakel ook **Lookup** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="b43ee-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="b43ee-159">Klik op **of Klik hier tooload en kopieert u afzonderlijke velden uit Hallo formulier** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**</span><span class="sxs-lookup"><span data-stu-id="b43ee-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="b43ee-161">Op de Azure-portal onder **LinkedIn Lookup domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="b43ee-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="b43ee-163">a.</span><span class="sxs-lookup"><span data-stu-id="b43ee-163">a.</span></span> <span data-ttu-id="b43ee-164">In Hallo **id** textbox Voer Hallo **entiteit-ID** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="b43ee-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="b43ee-165">b.</span><span class="sxs-lookup"><span data-stu-id="b43ee-165">b.</span></span> <span data-ttu-id="b43ee-166">In Hallo **antwoord-URL** textbox Voer Hallo **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="b43ee-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="b43ee-167">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="b43ee-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="b43ee-169">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="b43ee-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b43ee-170">Dit is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="b43ee-170">This is not real value.</span></span> <span data-ttu-id="b43ee-171">Hallo gebruiker heeft tooupdate deze waarden Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="b43ee-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="b43ee-172">Neem contact op met [LinkedIn Lookup Client ondersteuningsteam](https://business.LinkedIn.com/lookup) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="b43ee-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="b43ee-173">Uw **LinkedIn Lookup** toepassing hello SAML asserties verwacht in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="b43ee-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b43ee-174">Hallo gebruiker heeft tooadd aangepast kenmerk toewijzingen toohello SAML-token kenmerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="b43ee-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="b43ee-175">Hallo volgende Schermafbeelding toont een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b43ee-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="b43ee-176">Hallo standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn Lookup deze toobe toegewezen met e-mailadres van de gebruiker Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="b43ee-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="b43ee-177">U kunt **user.mail** kenmerk uit de lijst Hallo of Hallo juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b43ee-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="b43ee-179">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="b43ee-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="b43ee-180">Hallo-gebruiker moet vier tooadd-claims met de naam **e**, **afdeling**, **firstname**, en **lastname** en Hallo-waarde is toegewezen met toobe **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk</span><span class="sxs-lookup"><span data-stu-id="b43ee-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="b43ee-181">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b43ee-181">Attribute Name</span></span> | <span data-ttu-id="b43ee-182">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b43ee-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="b43ee-183">E-mail</span><span class="sxs-lookup"><span data-stu-id="b43ee-183">email</span></span>| <span data-ttu-id="b43ee-184">User.mail</span><span class="sxs-lookup"><span data-stu-id="b43ee-184">user.mail</span></span> |    
    | <span data-ttu-id="b43ee-185">Afdeling</span><span class="sxs-lookup"><span data-stu-id="b43ee-185">department</span></span>| <span data-ttu-id="b43ee-186">User.Department</span><span class="sxs-lookup"><span data-stu-id="b43ee-186">user.department</span></span> |
    | <span data-ttu-id="b43ee-187">Voornaam</span><span class="sxs-lookup"><span data-stu-id="b43ee-187">firstname</span></span>| <span data-ttu-id="b43ee-188">User.givenName</span><span class="sxs-lookup"><span data-stu-id="b43ee-188">user.givenname</span></span> |
    | <span data-ttu-id="b43ee-189">Achternaam</span><span class="sxs-lookup"><span data-stu-id="b43ee-189">lastname</span></span>| <span data-ttu-id="b43ee-190">User.surname</span><span class="sxs-lookup"><span data-stu-id="b43ee-190">user.surname</span></span> |

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="b43ee-192">a.</span><span class="sxs-lookup"><span data-stu-id="b43ee-192">a.</span></span> <span data-ttu-id="b43ee-193">Klik op **kenmerk toevoegen** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43ee-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="b43ee-196">b.</span><span class="sxs-lookup"><span data-stu-id="b43ee-196">b.</span></span> <span data-ttu-id="b43ee-197">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b43ee-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b43ee-198">c.</span><span class="sxs-lookup"><span data-stu-id="b43ee-198">c.</span></span> <span data-ttu-id="b43ee-199">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b43ee-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b43ee-200">d.</span><span class="sxs-lookup"><span data-stu-id="b43ee-200">d.</span></span> <span data-ttu-id="b43ee-201">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="b43ee-201">Click **Ok**</span></span>

10. <span data-ttu-id="b43ee-202">Uitvoeren van de volgende stappen uit op Hallo Hallo **naam** kenmerk -</span><span class="sxs-lookup"><span data-stu-id="b43ee-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="b43ee-203">a.</span><span class="sxs-lookup"><span data-stu-id="b43ee-203">a.</span></span> <span data-ttu-id="b43ee-204">Klik op Hallo kenmerk tooopen hello **kenmerk bewerken** venster.</span><span class="sxs-lookup"><span data-stu-id="b43ee-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="b43ee-206">b.</span><span class="sxs-lookup"><span data-stu-id="b43ee-206">b.</span></span> <span data-ttu-id="b43ee-207">Hallo URL waarde verwijderen uit Hallo **naamruimte**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="b43ee-208">c.</span><span class="sxs-lookup"><span data-stu-id="b43ee-208">c.</span></span> <span data-ttu-id="b43ee-209">Klik op **Ok** toosave Hallo-instelling.</span><span class="sxs-lookup"><span data-stu-id="b43ee-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="b43ee-210">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b43ee-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="b43ee-212">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b43ee-212">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="b43ee-214">Ga te**LinkedIn beheerdersinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="b43ee-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="b43ee-215">U hebt gedownload van hello Azure-portal door te klikken op Hallo van uploaden Hallo XML-bestand **uploaden XML-bestand** optie.</span><span class="sxs-lookup"><span data-stu-id="b43ee-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="b43ee-217">Klik op **op** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b43ee-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="b43ee-218">Status SSO wordt gewijzigd van **niet verbonden** te**verbonden**</span><span class="sxs-lookup"><span data-stu-id="b43ee-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="b43ee-220">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b43ee-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b43ee-221">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b43ee-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b43ee-222">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b43ee-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b43ee-223">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b43ee-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="b43ee-224">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b43ee-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b43ee-226">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b43ee-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b43ee-227">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b43ee-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b43ee-229">Ga te**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b43ee-231">Klik op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43ee-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b43ee-233">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b43ee-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b43ee-235">a.</span><span class="sxs-lookup"><span data-stu-id="b43ee-235">a.</span></span> <span data-ttu-id="b43ee-236">In Hallo **naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b43ee-237">b.</span><span class="sxs-lookup"><span data-stu-id="b43ee-237">b.</span></span> <span data-ttu-id="b43ee-238">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b43ee-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b43ee-239">c.</span><span class="sxs-lookup"><span data-stu-id="b43ee-239">c.</span></span> <span data-ttu-id="b43ee-240">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b43ee-241">d.</span><span class="sxs-lookup"><span data-stu-id="b43ee-241">d.</span></span> <span data-ttu-id="b43ee-242">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="b43ee-243">Maken van een testgebruiker LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="b43ee-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="b43ee-244">Gekoppelde Lookup toepassing ondersteunt Just in Time (Just in time) gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="b43ee-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="b43ee-245">Activeren **automatisch toewijzen van licenties** tooassign een licentie toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b43ee-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b43ee-247">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43ee-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b43ee-248">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLinkedIn opzoeken.</span><span class="sxs-lookup"><span data-stu-id="b43ee-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b43ee-250">**tooassign Britta Simon tooLinkedIn-Lookup, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b43ee-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="b43ee-251">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b43ee-253">Selecteer in de lijst met de toepassingen van Hallo **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="b43ee-255">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b43ee-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b43ee-257">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b43ee-257">Click **Add** button.</span></span> <span data-ttu-id="b43ee-258">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43ee-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b43ee-260">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b43ee-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b43ee-261">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43ee-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b43ee-262">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43ee-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b43ee-263">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b43ee-263">Testing single sign-on</span></span>

<span data-ttu-id="b43ee-264">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b43ee-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b43ee-265">Wanneer u op Hallo LinkedIn Lookup-tegel in Hallo toegangsvenster klikt, moet u omgeleide tooOrganizational pagina waar u tooprovide de details van uw persoonlijke LinkedIn hebt.</span><span class="sxs-lookup"><span data-stu-id="b43ee-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="b43ee-266">Uw persoonlijke account aan uw LinkedIn business-account worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="b43ee-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="b43ee-267">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b43ee-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b43ee-268">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b43ee-268">Additional resources</span></span>

* [<span data-ttu-id="b43ee-269">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b43ee-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b43ee-270">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b43ee-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

