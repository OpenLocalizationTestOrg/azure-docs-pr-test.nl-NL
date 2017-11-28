---
title: 'Zelfstudie: Azure Active Directory-integratie met PolicyStat | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PolicyStat.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="c27c6-103">Zelfstudie: Azure Active Directory-integratie met PolicyStat</span><span class="sxs-lookup"><span data-stu-id="c27c6-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="c27c6-104">In deze zelfstudie leert u hoe toointegrate PolicyStat met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c27c6-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c27c6-105">PolicyStat integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c27c6-106">U kunt beheren in Azure AD die tooPolicyStat toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c27c6-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="c27c6-107">U kunt uw gebruikers tooautomatically get aangemelde tooPolicyStat (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c27c6-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c27c6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c27c6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c27c6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c27c6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c27c6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c27c6-110">Prerequisites</span></span>

<span data-ttu-id="c27c6-111">Azure AD-integratie met PolicyStat tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c27c6-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="c27c6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c27c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c27c6-113">Een PolicyStat eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c27c6-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c27c6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c27c6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c27c6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c27c6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c27c6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c27c6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c27c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c27c6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c27c6-118">Scenario description</span></span>
<span data-ttu-id="c27c6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c27c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c27c6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c27c6-121">Het toevoegen van PolicyStat van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c27c6-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="c27c6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c27c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="c27c6-123">Het toevoegen van PolicyStat van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c27c6-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="c27c6-124">tooconfigure hello integratie van PolicyStat in Azure AD, moet u tooadd PolicyStat uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c27c6-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c27c6-125">**tooadd PolicyStat via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c27c6-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27c6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c27c6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c27c6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c27c6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c27c6-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c27c6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c27c6-133">Typ in het zoekvak Hallo **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-133">In hello search box, type **PolicyStat**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="c27c6-135">Selecteer in het deelvenster resultaten hello, **PolicyStat**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c27c6-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c27c6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c27c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c27c6-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met PolicyStat op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c27c6-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c27c6-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PolicyStat is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27c6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="c27c6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PolicyStat toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c27c6-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="c27c6-141">Wijs in PolicyStat, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c27c6-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c27c6-142">tooconfigure en eenmalige aanmelding Azure AD-test met PolicyStat, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c27c6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c27c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c27c6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c27c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c27c6-145">**[Maken van een testgebruiker PolicyStat](#creating-a-policystat-test-user)**  -toohave een equivalent van Britta Simon in PolicyStat die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c27c6-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c27c6-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c27c6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c27c6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c27c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c27c6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c27c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c27c6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing PolicyStat configureren.</span><span class="sxs-lookup"><span data-stu-id="c27c6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="c27c6-150">**Azure AD tooconfigure eenmalige aanmelding met PolicyStat, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c27c6-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27c6-151">In de Azure-portal op Hallo Hallo **PolicyStat** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c27c6-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c27c6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="c27c6-155">Op Hallo **PolicyStat domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="c27c6-157">a.</span><span class="sxs-lookup"><span data-stu-id="c27c6-157">a.</span></span> <span data-ttu-id="c27c6-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="c27c6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="c27c6-159">b.</span><span class="sxs-lookup"><span data-stu-id="c27c6-159">b.</span></span> <span data-ttu-id="c27c6-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="c27c6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c27c6-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c27c6-161">These values are not real.</span></span> <span data-ttu-id="c27c6-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="c27c6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c27c6-163">Neem contact op met [PolicyStat Client ondersteuningsteam](http://www.policystat.com/support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c27c6-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="c27c6-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c27c6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="c27c6-166">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooPolicyStat aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="c27c6-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="c27c6-167">Hallo PolicyStat toepassing hello SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **SAML-Token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="c27c6-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="c27c6-168">Hallo volgende Schermafbeelding toont een voorbeeld hiervan.</span><span class="sxs-lookup"><span data-stu-id="c27c6-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="c27c6-169">![Kenmerken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="c27c6-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="c27c6-170">Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="c27c6-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="c27c6-171">Attribute Name</span></span>    |   <span data-ttu-id="c27c6-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="c27c6-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="c27c6-173">UID</span><span class="sxs-lookup"><span data-stu-id="c27c6-173">uid</span></span> | <span data-ttu-id="c27c6-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="c27c6-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="c27c6-175">a.</span><span class="sxs-lookup"><span data-stu-id="c27c6-175">a.</span></span> <span data-ttu-id="c27c6-176">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c27c6-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="c27c6-179">b.</span><span class="sxs-lookup"><span data-stu-id="c27c6-179">b.</span></span> <span data-ttu-id="c27c6-180">In Hallo **kenmerknaam** textbox type **uid**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="c27c6-181">c.</span><span class="sxs-lookup"><span data-stu-id="c27c6-181">c.</span></span> <span data-ttu-id="c27c6-182">In Hallo **kenmerkwaarde** textbox, selecteer **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="c27c6-183">d.</span><span class="sxs-lookup"><span data-stu-id="c27c6-183">d.</span></span> <span data-ttu-id="c27c6-184">Van Hallo **Mail** selecteert **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="c27c6-185">e.</span><span class="sxs-lookup"><span data-stu-id="c27c6-185">e.</span></span> <span data-ttu-id="c27c6-186">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="c27c6-186">Click **Ok**</span></span>

7. <span data-ttu-id="c27c6-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c27c6-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c27c6-189">In een ander browservenster, meld u bij uw bedrijf PolicyStat site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c27c6-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="c27c6-190">Klik op Hallo **Admin** tabblad en klik vervolgens op **configuratie voor één aanmelding** in het navigatiedeelvenster links.</span><span class="sxs-lookup"><span data-stu-id="c27c6-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="c27c6-191">![Menu beheerder](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu beheerder")</span><span class="sxs-lookup"><span data-stu-id="c27c6-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="c27c6-192">In Hallo **Setup** sectie **inschakelen eenmalige aanmelding integratie**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="c27c6-193">![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On-configuratie")</span><span class="sxs-lookup"><span data-stu-id="c27c6-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="c27c6-194">Klik op **kenmerken configureren**, en klikt u op Hallo **kenmerken configureren** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c27c6-195">![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On-configuratie")</span><span class="sxs-lookup"><span data-stu-id="c27c6-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="c27c6-196">a.</span><span class="sxs-lookup"><span data-stu-id="c27c6-196">a.</span></span> <span data-ttu-id="c27c6-197">In Hallo **kenmerk Username** textbox type **uid**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="c27c6-198">b.</span><span class="sxs-lookup"><span data-stu-id="c27c6-198">b.</span></span> <span data-ttu-id="c27c6-199">In Hallo **voornaam kenmerk** textbox type **firstname** van gebruiker **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="c27c6-200">c.</span><span class="sxs-lookup"><span data-stu-id="c27c6-200">c.</span></span> <span data-ttu-id="c27c6-201">In Hallo **laatste naamkenmerk** textbox type **lastname** van gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="c27c6-202">d.</span><span class="sxs-lookup"><span data-stu-id="c27c6-202">d.</span></span> <span data-ttu-id="c27c6-203">In Hallo **e kenmerk** textbox type **emailaddress** van gebruiker  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c27c6-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="c27c6-204">e.</span><span class="sxs-lookup"><span data-stu-id="c27c6-204">e.</span></span> <span data-ttu-id="c27c6-205">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="c27c6-206">Klik op **uw IDP metagegevens**, en klikt u op Hallo **uw IDP metagegevens** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c27c6-207">![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On-configuratie")</span><span class="sxs-lookup"><span data-stu-id="c27c6-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="c27c6-208">a.</span><span class="sxs-lookup"><span data-stu-id="c27c6-208">a.</span></span> <span data-ttu-id="c27c6-209">Open uw gedownloade metagegevensbestand, kopie Hallo inhoud en plak deze in Hallo **uw identiteit Provider metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="c27c6-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="c27c6-210">b.</span><span class="sxs-lookup"><span data-stu-id="c27c6-210">b.</span></span> <span data-ttu-id="c27c6-211">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c27c6-212">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c27c6-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c27c6-213">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c27c6-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c27c6-214">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c27c6-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c27c6-215">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c27c6-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="c27c6-216">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c27c6-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c27c6-218">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c27c6-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27c6-219">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c27c6-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c27c6-221">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c27c6-223">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c27c6-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c27c6-225">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c27c6-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c27c6-227">a.</span><span class="sxs-lookup"><span data-stu-id="c27c6-227">a.</span></span> <span data-ttu-id="c27c6-228">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c27c6-229">b.</span><span class="sxs-lookup"><span data-stu-id="c27c6-229">b.</span></span> <span data-ttu-id="c27c6-230">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c27c6-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c27c6-231">c.</span><span class="sxs-lookup"><span data-stu-id="c27c6-231">c.</span></span> <span data-ttu-id="c27c6-232">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c27c6-233">d.</span><span class="sxs-lookup"><span data-stu-id="c27c6-233">d.</span></span> <span data-ttu-id="c27c6-234">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="c27c6-235">Een testgebruiker PolicyStat maken</span><span class="sxs-lookup"><span data-stu-id="c27c6-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="c27c6-236">In de volgorde tooenable Azure AD gebruikers toolog in PolicyStat, moeten ze worden ingericht in PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="c27c6-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="c27c6-237">PolicyStat ondersteunt alleen in de tijd van gebruikersinrichting.</span><span class="sxs-lookup"><span data-stu-id="c27c6-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="c27c6-238">Dit betekent dat, hoeft u geen tooadd Hallo gebruikers handmatig tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="c27c6-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="c27c6-239">Hallo gebruikers krijgen op hun eerste aanmelding via eenmalige aanmelding automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c27c6-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="c27c6-240">U kunt andere PolicyStat gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door PolicyStat tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c27c6-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c27c6-241">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c27c6-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c27c6-242">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPolicyStat toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c27c6-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c27c6-244">**tooassign Britta Simon tooPolicyStat, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c27c6-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27c6-245">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c27c6-247">Selecteer in de lijst met de toepassingen van Hallo **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="c27c6-249">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c27c6-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c27c6-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c27c6-251">Click **Add** button.</span></span> <span data-ttu-id="c27c6-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c27c6-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c27c6-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c27c6-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c27c6-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c27c6-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c27c6-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c27c6-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c27c6-257">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c27c6-257">Testing single sign-on</span></span>

<span data-ttu-id="c27c6-258">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c27c6-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c27c6-259">Als u op Hallo PolicyStat tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour PolicyStat toepassing.</span><span class="sxs-lookup"><span data-stu-id="c27c6-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="c27c6-260">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c27c6-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c27c6-261">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c27c6-261">Additional resources</span></span>

* [<span data-ttu-id="c27c6-262">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c27c6-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c27c6-263">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c27c6-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

