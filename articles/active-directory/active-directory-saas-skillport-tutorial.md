---
title: 'Zelfstudie: Azure Active Directory-integratie met Skillport | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Skillport.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="dfd41-103">Zelfstudie: Azure Active Directory-integratie met Skillport</span><span class="sxs-lookup"><span data-stu-id="dfd41-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="dfd41-104">In deze zelfstudie leert u hoe toointegrate Skillport met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfd41-104">In this tutorial, you learn how toointegrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dfd41-105">Skillport integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-105">Integrating Skillport with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dfd41-106">U kunt beheren in Azure AD die tooSkillport toegang heeft</span><span class="sxs-lookup"><span data-stu-id="dfd41-106">You can control in Azure AD who has access tooSkillport</span></span>
- <span data-ttu-id="dfd41-107">U kunt uw gebruikers tooautomatically get aangemelde tooSkillport (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="dfd41-107">You can enable your users tooautomatically get signed-on tooSkillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dfd41-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="dfd41-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dfd41-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dfd41-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfd41-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dfd41-110">Prerequisites</span></span>

<span data-ttu-id="dfd41-111">Azure AD-integratie met Skillport tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="dfd41-111">tooconfigure Azure AD integration with Skillport, you need hello following items:</span></span>

- <span data-ttu-id="dfd41-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="dfd41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dfd41-113">Een Skillport eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="dfd41-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dfd41-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="dfd41-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dfd41-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dfd41-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="dfd41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dfd41-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfd41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dfd41-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="dfd41-118">Scenario description</span></span>
<span data-ttu-id="dfd41-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="dfd41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dfd41-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dfd41-121">Het toevoegen van Skillport van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dfd41-121">Adding Skillport from hello gallery</span></span>
2. <span data-ttu-id="dfd41-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dfd41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-hello-gallery"></a><span data-ttu-id="dfd41-123">Het toevoegen van Skillport van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dfd41-123">Adding Skillport from hello gallery</span></span>
<span data-ttu-id="dfd41-124">tooconfigure hello integratie van Skillport in Azure AD, moet u tooadd Skillport uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="dfd41-124">tooconfigure hello integration of Skillport into Azure AD, you need tooadd Skillport from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dfd41-125">**tooadd Skillport via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dfd41-125">**tooadd Skillport from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd41-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dfd41-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dfd41-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dfd41-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="dfd41-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="dfd41-131">Click **New Application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="dfd41-133">Typ in het zoekvak Hallo **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-133">In hello search box, type **Skillport**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="dfd41-135">Selecteer in het deelvenster resultaten hello, **Skillport**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dfd41-135">In hello results panel, select **Skillport**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dfd41-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dfd41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dfd41-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Skillport op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="dfd41-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dfd41-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Skillport is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfd41-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skillport is tooa user in Azure AD.</span></span> <span data-ttu-id="dfd41-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Skillport toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="dfd41-140">In other words, a link relationship between an Azure AD user and hello related user in Skillport needs toobe established.</span></span>

<span data-ttu-id="dfd41-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Skillport.</span><span class="sxs-lookup"><span data-stu-id="dfd41-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Skillport.</span></span>

<span data-ttu-id="dfd41-142">tooconfigure en eenmalige aanmelding Azure AD-test met Skillport, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-142">tooconfigure and test Azure AD single sign-on with Skillport, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dfd41-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="dfd41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dfd41-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dfd41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dfd41-145">**[Maken van een testgebruiker Skillport](#creating-a-skillport-test-user)**  -toohave een equivalent van Britta Simon in Skillport die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dfd41-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - toohave a counterpart of Britta Simon in Skillport that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dfd41-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dfd41-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dfd41-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="dfd41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dfd41-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="dfd41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dfd41-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Skillport configureren.</span><span class="sxs-lookup"><span data-stu-id="dfd41-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="dfd41-150">**Azure AD tooconfigure eenmalige aanmelding met Skillport, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dfd41-150">**tooconfigure Azure AD single sign-on with Skillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd41-151">In de Azure-portal op Hallo Hallo **Skillport** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-151">In hello Azure  portal, on hello **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="dfd41-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dfd41-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="dfd41-155">Op Hallo **Skillport domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-155">On hello **Skillport Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="dfd41-157">a.</span><span class="sxs-lookup"><span data-stu-id="dfd41-157">a.</span></span> <span data-ttu-id="dfd41-158">In Hallo **aanmeldings-URL** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span>
      
      <span data-ttu-id="dfd41-159">EU Datacenter:`https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="dfd41-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="dfd41-160">VS Datacenter:`https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="dfd41-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="dfd41-161">b.</span><span class="sxs-lookup"><span data-stu-id="dfd41-161">b.</span></span> <span data-ttu-id="dfd41-162">In Hallo **antwoord-URL** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span>
    
      <span data-ttu-id="dfd41-163">EU Datacenter:`https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="dfd41-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="dfd41-164">VS Datacenter:`https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="dfd41-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dfd41-165">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="dfd41-165">These values are not hello real.</span></span> <span data-ttu-id="dfd41-166">Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="dfd41-166">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="dfd41-167">Neem contact op met [Skillport Client ondersteuningsteam](https://www.skillsoft.com/contact.asp) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="dfd41-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) tooget these values.</span></span>
 
4. <span data-ttu-id="dfd41-168">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="dfd41-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="dfd41-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="dfd41-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dfd41-172">tooconfigure eenmalige aanmelding op **Skillport** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Skillport ondersteuningsteam](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="dfd41-172">tooconfigure single sign-on on **Skillport** side, you need toosend hello downloaded **Metadata XML** too[Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="dfd41-173">Ze zullen het instellen van toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="dfd41-173">They will set it up toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dfd41-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="dfd41-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="dfd41-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="dfd41-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="dfd41-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dfd41-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd41-178">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dfd41-178">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dfd41-180">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="dfd41-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dfd41-182">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dfd41-182">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dfd41-184">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dfd41-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dfd41-186">a.</span><span class="sxs-lookup"><span data-stu-id="dfd41-186">a.</span></span> <span data-ttu-id="dfd41-187">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dfd41-188">b.</span><span class="sxs-lookup"><span data-stu-id="dfd41-188">b.</span></span> <span data-ttu-id="dfd41-189">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dfd41-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dfd41-190">c.</span><span class="sxs-lookup"><span data-stu-id="dfd41-190">c.</span></span> <span data-ttu-id="dfd41-191">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dfd41-192">d.</span><span class="sxs-lookup"><span data-stu-id="dfd41-192">d.</span></span> <span data-ttu-id="dfd41-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="dfd41-194">Een testgebruiker Skillport maken</span><span class="sxs-lookup"><span data-stu-id="dfd41-194">Creating a Skillport test user</span></span>

<span data-ttu-id="dfd41-195">In de volgorde toocreate Skillport testgebruiker, moet u toocontact [Skillport ondersteuningsteam](https://www.skillsoft.com/contact.asp) als ze hebben meerdere bedrijfsscenario's op basis van de vereiste toohello van eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="dfd41-195">In order toocreate Skillport test user, you need toocontact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according toohello requirement of end user.</span></span> <span data-ttu-id="dfd41-196">Ze wordt deze na overleg met de Hallo gebruikers configureren.</span><span class="sxs-lookup"><span data-stu-id="dfd41-196">They will configure it after discussion with hello users.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dfd41-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd41-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dfd41-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSkillport toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="dfd41-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkillport.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="dfd41-200">**tooassign Britta Simon tooSkillport, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dfd41-200">**tooassign Britta Simon tooSkillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd41-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="dfd41-203">Selecteer in de lijst met de toepassingen van Hallo **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-203">In hello applications list, select **Skillport**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="dfd41-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="dfd41-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="dfd41-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="dfd41-207">Click **Add** button.</span></span> <span data-ttu-id="dfd41-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dfd41-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="dfd41-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="dfd41-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dfd41-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dfd41-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dfd41-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dfd41-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dfd41-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dfd41-213">Testing single sign-on</span></span>

<span data-ttu-id="dfd41-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="dfd41-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dfd41-215">Als u op Hallo Skillport tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Skillport toepassing.</span><span class="sxs-lookup"><span data-stu-id="dfd41-215">When you click hello Skillport tile in hello Access Panel, you should get automatically signed-on tooyour Skillport application.</span></span>
<span data-ttu-id="dfd41-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="dfd41-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dfd41-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="dfd41-217">Additional resources</span></span>

* [<span data-ttu-id="dfd41-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfd41-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dfd41-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dfd41-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

