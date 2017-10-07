---
title: 'Zelfstudie: Azure Active Directory-integratie met Jobscience | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jobscience.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="34f71-103">Zelfstudie: Azure Active Directory-integratie met Jobscience</span><span class="sxs-lookup"><span data-stu-id="34f71-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="34f71-104">In deze zelfstudie leert u hoe toointegrate Jobscience met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34f71-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34f71-105">Jobscience integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="34f71-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34f71-106">U kunt beheren in Azure AD die tooJobscience toegang heeft</span><span class="sxs-lookup"><span data-stu-id="34f71-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="34f71-107">U kunt uw gebruikers tooautomatically get aangemelde tooJobscience (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="34f71-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34f71-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="34f71-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34f71-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34f71-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34f71-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="34f71-110">Prerequisites</span></span>

<span data-ttu-id="34f71-111">Azure AD-integratie met Jobscience tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="34f71-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="34f71-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="34f71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34f71-113">Een Jobscience eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="34f71-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34f71-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="34f71-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34f71-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="34f71-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34f71-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="34f71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34f71-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34f71-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34f71-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="34f71-118">Scenario description</span></span>
<span data-ttu-id="34f71-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="34f71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34f71-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="34f71-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34f71-121">Het toevoegen van Jobscience van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="34f71-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="34f71-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34f71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="34f71-123">Het toevoegen van Jobscience van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="34f71-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="34f71-124">tooconfigure hello integratie van Jobscience in Azure AD, moet u tooadd Jobscience uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="34f71-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34f71-125">**tooadd Jobscience via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="34f71-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f71-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="34f71-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34f71-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34f71-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34f71-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34f71-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="34f71-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34f71-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="34f71-133">Typ in het zoekvak Hallo **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="34f71-133">In hello search box, type **Jobscience**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="34f71-135">Selecteer in het deelvenster resultaten hello, **Jobscience**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="34f71-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34f71-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34f71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34f71-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jobscience op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="34f71-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="34f71-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Jobscience is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34f71-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="34f71-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Jobscience toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="34f71-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="34f71-141">Wijs in Jobscience, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="34f71-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="34f71-142">tooconfigure en eenmalige aanmelding Azure AD-test met Jobscience, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="34f71-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34f71-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="34f71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34f71-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34f71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34f71-145">**[Maken van een testgebruiker Jobscience](#creating-a-jobscience-test-user)**  -toohave een equivalent van Britta Simon in Jobscience die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="34f71-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34f71-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="34f71-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34f71-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="34f71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34f71-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="34f71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34f71-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Jobscience configureren.</span><span class="sxs-lookup"><span data-stu-id="34f71-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="34f71-150">**Azure AD tooconfigure eenmalige aanmelding met Jobscience, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="34f71-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f71-151">In de Azure-portal op Hallo Hallo **Jobscience** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="34f71-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="34f71-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="34f71-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="34f71-155">Op Hallo **Jobscience domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="34f71-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="34f71-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="34f71-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="34f71-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="34f71-158">This value is not real.</span></span> <span data-ttu-id="34f71-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="34f71-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="34f71-160">Deze waarde krijgen door [Jobscience Client ondersteuningsteam](https://www.jobscience.com/support) of van Hallo sso-profiel maakt u die later in Hallo zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="34f71-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="34f71-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="34f71-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="34f71-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="34f71-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="34f71-165">Op Hallo **Jobscience configuratie** sectie, klikt u op **configureren Jobscience** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="34f71-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="34f71-166">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="34f71-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="34f71-168">Aanmelden tooyour Jobscience bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="34f71-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="34f71-169">Ga te**Setup**.</span><span class="sxs-lookup"><span data-stu-id="34f71-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="34f71-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="34f71-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="34f71-171">Op Hallo navigatiedeelvenster links in Hallo **beheren** sectie, klikt u op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello  **Mijn domein** pagina.</span><span class="sxs-lookup"><span data-stu-id="34f71-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="34f71-172">![Mijn domein](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="34f71-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="34f71-173">tooverify die uw domein is correct is ingesteld, zorg ervoor dat deze wordt '**stap 4 geïmplementeerd tooUsers**' en bekijk uw '**mijn domeininstellingen**'.</span><span class="sxs-lookup"><span data-stu-id="34f71-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="34f71-174">![Domein geïmplementeerd tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser domein geïmplementeerd")</span><span class="sxs-lookup"><span data-stu-id="34f71-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="34f71-175">Klik op Hallo Jobscience bedrijf site **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="34f71-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="34f71-176">![Beveiligingsmechanismen](./media/active-directory-saas-jobscience-tutorial/ic784364.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="34f71-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="34f71-177">In Hallo **instellingen voor eenmalige aanmelding** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="34f71-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="34f71-178">![Eenmalige aanmelding instellingen](./media/active-directory-saas-jobscience-tutorial/ic781026.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="34f71-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="34f71-179">a.</span><span class="sxs-lookup"><span data-stu-id="34f71-179">a.</span></span> <span data-ttu-id="34f71-180">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="34f71-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="34f71-181">b.</span><span class="sxs-lookup"><span data-stu-id="34f71-181">b.</span></span> <span data-ttu-id="34f71-182">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="34f71-182">Click **New**.</span></span>

13. <span data-ttu-id="34f71-183">Op Hallo **SAML Single Sign-On instelling bewerken** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="34f71-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="34f71-184">![Afzonderlijke SAML aanmelding instelling](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On-instelling")</span><span class="sxs-lookup"><span data-stu-id="34f71-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="34f71-185">a.</span><span class="sxs-lookup"><span data-stu-id="34f71-185">a.</span></span> <span data-ttu-id="34f71-186">In Hallo **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="34f71-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="34f71-187">b.</span><span class="sxs-lookup"><span data-stu-id="34f71-187">b.</span></span> <span data-ttu-id="34f71-188">In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="34f71-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="34f71-189">c.</span><span class="sxs-lookup"><span data-stu-id="34f71-189">c.</span></span> <span data-ttu-id="34f71-190">In Hallo **entiteit-Id** textbox type`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="34f71-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="34f71-191">d.</span><span class="sxs-lookup"><span data-stu-id="34f71-191">d.</span></span> <span data-ttu-id="34f71-192">Klik op **Bladeren** tooupload uw Azure AD-certificaat.</span><span class="sxs-lookup"><span data-stu-id="34f71-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="34f71-193">e.</span><span class="sxs-lookup"><span data-stu-id="34f71-193">e.</span></span> <span data-ttu-id="34f71-194">Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**.</span><span class="sxs-lookup"><span data-stu-id="34f71-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="34f71-195">f.</span><span class="sxs-lookup"><span data-stu-id="34f71-195">f.</span></span> <span data-ttu-id="34f71-196">Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentfier element van Hallo onderwerp instructie**.</span><span class="sxs-lookup"><span data-stu-id="34f71-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="34f71-197">g.</span><span class="sxs-lookup"><span data-stu-id="34f71-197">g.</span></span> <span data-ttu-id="34f71-198">In **identiteit Provider aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="34f71-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="34f71-199">h.</span><span class="sxs-lookup"><span data-stu-id="34f71-199">h.</span></span> <span data-ttu-id="34f71-200">In **identiteit Provider afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="34f71-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="34f71-201">ik.</span><span class="sxs-lookup"><span data-stu-id="34f71-201">i.</span></span> <span data-ttu-id="34f71-202">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="34f71-202">Click **Save**.</span></span>

14. <span data-ttu-id="34f71-203">Op Hallo navigatiedeelvenster links in Hallo **beheren** sectie, klikt u op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello  **Mijn domein** pagina.</span><span class="sxs-lookup"><span data-stu-id="34f71-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="34f71-204">![Mijn domein](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="34f71-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="34f71-205">Op Hallo **mijn domein** pagina in Hallo **aanmelding pagina huisstijl** sectie, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="34f71-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="34f71-206">![Aanmeldingspagina huisstijl](./media/active-directory-saas-jobscience-tutorial/ic767826.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="34f71-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="34f71-207">Op Hallo **aanmelding pagina huisstijl** pagina in Hallo **verificatieservice** sectie, Hallo-naam van uw **SAML SSO instellingen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="34f71-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="34f71-208">Selecteer deze en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="34f71-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="34f71-209">![Aanmeldingspagina huisstijl](./media/active-directory-saas-jobscience-tutorial/ic784366.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="34f71-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="34f71-210">tooget hello SP eenmalige gestart op de aanmeldings-URL-Klik op Hallo **instellingen voor eenmalige aanmelding** in Hallo **beveiligingsmechanismen** sectie menu.</span><span class="sxs-lookup"><span data-stu-id="34f71-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="34f71-211">![Beveiligingsmechanismen](./media/active-directory-saas-jobscience-tutorial/ic784368.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="34f71-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="34f71-212">Klik op Hallo SSO profiel die u in de bovenstaande Hallo stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34f71-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="34f71-213">Deze pagina bevat Hallo eenmalige aanmelding op de URL voor uw bedrijf (bijvoorbeeld [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="34f71-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="34f71-214">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="34f71-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34f71-215">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="34f71-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34f71-216">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34f71-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34f71-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="34f71-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="34f71-218">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="34f71-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="34f71-220">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="34f71-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f71-221">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="34f71-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34f71-223">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="34f71-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34f71-225">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="34f71-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34f71-227">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="34f71-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34f71-229">a.</span><span class="sxs-lookup"><span data-stu-id="34f71-229">a.</span></span> <span data-ttu-id="34f71-230">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34f71-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34f71-231">b.</span><span class="sxs-lookup"><span data-stu-id="34f71-231">b.</span></span> <span data-ttu-id="34f71-232">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34f71-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34f71-233">c.</span><span class="sxs-lookup"><span data-stu-id="34f71-233">c.</span></span> <span data-ttu-id="34f71-234">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="34f71-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34f71-235">d.</span><span class="sxs-lookup"><span data-stu-id="34f71-235">d.</span></span> <span data-ttu-id="34f71-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="34f71-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="34f71-237">Een testgebruiker Jobscience maken</span><span class="sxs-lookup"><span data-stu-id="34f71-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="34f71-238">In de volgorde tooenable Azure AD gebruikers toolog in tooJobscience, moeten ze worden ingericht in Jobscience.</span><span class="sxs-lookup"><span data-stu-id="34f71-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="34f71-239">In geval van Jobscience Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="34f71-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="34f71-240">U kunt andere Jobscience gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Jobscience tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="34f71-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="34f71-241">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="34f71-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f71-242">Meld u bij tooyour **Jobscience** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="34f71-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="34f71-243">Ga tooSetup.</span><span class="sxs-lookup"><span data-stu-id="34f71-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="34f71-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="34f71-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="34f71-245">Ga te**gebruikers beheren \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="34f71-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="34f71-246">![Gebruikers](./media/active-directory-saas-jobscience-tutorial/ic784369.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="34f71-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="34f71-247">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="34f71-247">Click **New User**.</span></span>
   
   <span data-ttu-id="34f71-248">![Alle gebruikers](./media/active-directory-saas-jobscience-tutorial/ic784370.png "alle gebruikers")</span><span class="sxs-lookup"><span data-stu-id="34f71-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="34f71-249">Op Hallo **-gebruiker bewerken** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="34f71-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="34f71-250">![Gebruiker bewerken](./media/active-directory-saas-jobscience-tutorial/ic784371.png "gebruiker bewerken")</span><span class="sxs-lookup"><span data-stu-id="34f71-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="34f71-251">a.</span><span class="sxs-lookup"><span data-stu-id="34f71-251">a.</span></span> <span data-ttu-id="34f71-252">In Hallo **voornaam** textbox, typ een naam van de eerste van de gebruiker Hallo zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="34f71-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="34f71-253">b.</span><span class="sxs-lookup"><span data-stu-id="34f71-253">b.</span></span> <span data-ttu-id="34f71-254">In Hallo **achternaam** textbox, typt u een achternaam van de gebruiker Hallo zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="34f71-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="34f71-255">c.</span><span class="sxs-lookup"><span data-stu-id="34f71-255">c.</span></span> <span data-ttu-id="34f71-256">In Hallo **Alias** textbox, typt u een aliasnaam van de gebruiker Hallo zoals brittas.</span><span class="sxs-lookup"><span data-stu-id="34f71-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="34f71-257">d.</span><span class="sxs-lookup"><span data-stu-id="34f71-257">d.</span></span> <span data-ttu-id="34f71-258">In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="34f71-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="34f71-259">e.</span><span class="sxs-lookup"><span data-stu-id="34f71-259">e.</span></span> <span data-ttu-id="34f71-260">In Hallo **gebruikersnaam** textbox, typ een naam van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="34f71-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="34f71-261">f.</span><span class="sxs-lookup"><span data-stu-id="34f71-261">f.</span></span> <span data-ttu-id="34f71-262">In Hallo **bijnaam** textbox, typ een naam nick van gebruiker zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="34f71-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="34f71-263">g.</span><span class="sxs-lookup"><span data-stu-id="34f71-263">g.</span></span> <span data-ttu-id="34f71-264">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="34f71-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="34f71-265">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="34f71-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34f71-266">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f71-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34f71-267">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooJobscience toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="34f71-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="34f71-269">**tooassign Britta Simon tooJobscience, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="34f71-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f71-270">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34f71-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="34f71-272">Selecteer in de lijst met de toepassingen van Hallo **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="34f71-272">In hello applications list, select **Jobscience**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="34f71-274">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="34f71-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="34f71-276">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="34f71-276">Click **Add** button.</span></span> <span data-ttu-id="34f71-277">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34f71-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="34f71-279">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="34f71-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34f71-280">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34f71-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34f71-281">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34f71-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34f71-282">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34f71-282">Testing single sign-on</span></span>

<span data-ttu-id="34f71-283">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="34f71-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="34f71-284">Als u op Hallo Jobscience tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Jobscience toepassing.</span><span class="sxs-lookup"><span data-stu-id="34f71-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="34f71-285">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34f71-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34f71-286">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="34f71-286">Additional resources</span></span>

* [<span data-ttu-id="34f71-287">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34f71-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34f71-288">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34f71-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

