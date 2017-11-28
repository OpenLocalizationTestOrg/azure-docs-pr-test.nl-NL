---
title: 'Zelfstudie: Azure Active Directory-integratie met ServiceNow | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ServiceNow en ServiceNow Express.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="88e1a-103">Zelfstudie: Azure Active Directory-integratie met ServiceNow</span><span class="sxs-lookup"><span data-stu-id="88e1a-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="88e1a-104">In deze zelfstudie leert u hoe toointegrate ServiceNow en ServiceNow Express met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88e1a-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88e1a-105">ServiceNow en ServiceNow Express integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="88e1a-106">U kunt beheren in Azure AD wie toegang tot tooServiceNow heeft en ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="88e1a-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="88e1a-107">U kunt uw gebruikers tooautomatically get aangemelde tooServiceNow en ServiceNow Express (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="88e1a-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="88e1a-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="88e1a-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="88e1a-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88e1a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88e1a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88e1a-110">Prerequisites</span></span>
<span data-ttu-id="88e1a-111">Azure AD-integratie met ServiceNow en ServiceNow Express tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="88e1a-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="88e1a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="88e1a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="88e1a-113">Voor ServiceNow, een exemplaar of de tenant van ServiceNow, Calgary versie of hoger</span><span class="sxs-lookup"><span data-stu-id="88e1a-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="88e1a-114">Voor ServiceNow snelle, een exemplaar van ServiceNow Express, Helsinki versie of hoger</span><span class="sxs-lookup"><span data-stu-id="88e1a-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="88e1a-115">Hallo ServiceNow-tenant moet hebben Hallo [meerdere Provider eenmalige aanmelding op invoegtoepassing](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="88e1a-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="88e1a-116">Dit kan worden gedaan door [indienen van een serviceaanvraag](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="88e1a-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="88e1a-117">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="88e1a-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="88e1a-118">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="88e1a-119">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="88e1a-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="88e1a-120">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88e1a-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88e1a-121">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="88e1a-121">Scenario description</span></span>
<span data-ttu-id="88e1a-122">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="88e1a-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88e1a-123">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88e1a-124">Het toevoegen van ServiceNow van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="88e1a-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="88e1a-125">Configureren en testen van Azure AD eenmalige aanmelding voor ServiceNow of ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="88e1a-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="88e1a-126">Het toevoegen van ServiceNow van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="88e1a-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="88e1a-127">tooconfigure hello integratie van ServiceNow of ServiceNow Express in Azure AD, moet u tooadd ServiceNow uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="88e1a-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="88e1a-128">**tooadd ServiceNow via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="88e1a-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e1a-129">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="88e1a-131">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="88e1a-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="88e1a-132">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="88e1a-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Toepassingen][2]
4. <span data-ttu-id="88e1a-134">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="88e1a-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3]
5. <span data-ttu-id="88e1a-136">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Toepassingen][4]
6. <span data-ttu-id="88e1a-138">Typ in het zoekvak Hallo **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="88e1a-140">Selecteer in het deelvenster met resultaten Hallo **ServiceNow**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="88e1a-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88e1a-142">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88e1a-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88e1a-143">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met ServiceNow of ServiceNow snelle op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="88e1a-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88e1a-144">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ServiceNow is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e1a-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="88e1a-145">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in ServiceNow toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="88e1a-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="88e1a-146">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="88e1a-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="88e1a-147">tooconfigure en eenmalige aanmelding Azure AD-test met ServiceNow, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88e1a-148">**[Azure AD eenmalige aanmelding configureren voor ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="88e1a-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88e1a-149">**[Configureren van Azure AD eenmalige aanmelding voor snelle ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="88e1a-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="88e1a-150">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88e1a-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="88e1a-151">**[Maken van een testgebruiker ServiceNow](#creating-a-servicenow-test-user)**  -toohave een equivalent van Britta Simon in ServiceNow die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="88e1a-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="88e1a-152">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="88e1a-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="88e1a-153">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="88e1a-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="88e1a-154">Als u wilt weglaten tooconfigure ServiceNow stap 2.</span><span class="sxs-lookup"><span data-stu-id="88e1a-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="88e1a-155">Op dezelfde manier als u wilt dat tooconfigure weglaten ServiceNow snelle stap 1.</span><span class="sxs-lookup"><span data-stu-id="88e1a-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="88e1a-156">Azure AD voor eenmalige aanmelding configureren voor ServiceNow</span><span class="sxs-lookup"><span data-stu-id="88e1a-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="88e1a-157">In de klassieke portal hello Azure AD op Hallo **ServiceNow** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster .</span><span class="sxs-lookup"><span data-stu-id="88e1a-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="88e1a-158">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="88e1a-159">Op Hallo **wilt u hoe gebruikers toosign op tooServiceNow** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="88e1a-160">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749324.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="88e1a-161">Op Hallo **App-instellingen configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="88e1a-162">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC769497.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="88e1a-163">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-163">a.</span></span> <span data-ttu-id="88e1a-164">in Hallo **ServiceNow aanmelding op URL** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="88e1a-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="88e1a-165">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-165">b.</span></span> <span data-ttu-id="88e1a-166">In Hallo **id** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="88e1a-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="88e1a-167">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-167">c.</span></span> <span data-ttu-id="88e1a-168">Klik op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="88e1a-168">Click **Next**</span></span>

4. <span data-ttu-id="88e1a-169">toohave Azure AD automatisch ServiceNow configureren voor verificatie op basis van SAML, Voer uw ServiceNow-instantienaam, beheerdersgebruikersnaam en beheerderswachtwoord in Hallo **automatisch eenmalige aanmelding configureren** vormen en klikt u op  *Configureer*.</span><span class="sxs-lookup"><span data-stu-id="88e1a-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="88e1a-170">Opmerking die Hallo beheerder opgegeven gebruikersnaam moet hebben Hallo **security_admin** rol die is toegewezen in ServiceNow voor deze toowork.</span><span class="sxs-lookup"><span data-stu-id="88e1a-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="88e1a-171">Anders toomanually ServiceNow toouse Azure AD als SAML-identiteitsprovider configureren, klikt u op **handmatig Hallo-toepassing voor eenmalige aanmelding configureren**, klikt u vervolgens op **volgende** en volledige Hallo volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="88e1a-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="88e1a-172">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="88e1a-173">Op Hallo **eenmalige aanmelding configureren op ServiceNow** pagina, klikt u op **certificaat downloaden**, slaat u Hallo certificaatbestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="88e1a-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="88e1a-174">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749325.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="88e1a-175">Eenmalige aanmelding tooyour ServiceNow-toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="88e1a-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="88e1a-176">Hallo activeren *integratie - meerdere Provider Single Sign-On-installatieprogramma* invoegtoepassing door Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="88e1a-177">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-177">a.</span></span> <span data-ttu-id="88e1a-178">In het navigatievenster aan de linkerkant Hallo Hallo gaat te**System Definition** sectie en klik vervolgens op **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="88e1a-179">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "invoegtoepassing activeren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="88e1a-180">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-180">b.</span></span> <span data-ttu-id="88e1a-181">Zoeken naar *integratie - meerdere Provider Single Sign-On-installatieprogramma*.</span><span class="sxs-lookup"><span data-stu-id="88e1a-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="88e1a-182">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "invoegtoepassing activeren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="88e1a-183">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-183">c.</span></span> <span data-ttu-id="88e1a-184">Selecteer Hallo-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="88e1a-184">Select hello plugin.</span></span> <span data-ttu-id="88e1a-185">Rigth op en selecteer **activeren/Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="88e1a-186">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-186">d.</span></span> <span data-ttu-id="88e1a-187">Klik op Hallo **activeren** knop.</span><span class="sxs-lookup"><span data-stu-id="88e1a-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="88e1a-188">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="88e1a-189">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="88e1a-190">Op Hallo **meerdere eigenschappen van de Provider SSO** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="88e1a-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="88e1a-191">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="88e1a-192">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-192">a.</span></span> <span data-ttu-id="88e1a-193">Als **provider voor meervoudige eenmalige aanmelding inschakelen**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="88e1a-194">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-194">b.</span></span> <span data-ttu-id="88e1a-195">Als **inschakelen, hebt u logboekregistratie voor foutopsporing Hallo provider voor meervoudige SSO-integratie**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="88e1a-196">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-196">c.</span></span> <span data-ttu-id="88e1a-197">In **Hallo veld op Hallo gebruiker tabel die...**  textbox type **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="88e1a-198">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-198">d.</span></span> <span data-ttu-id="88e1a-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-199">Click **Save**.</span></span>

10. <span data-ttu-id="88e1a-200">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **x509 certificaten**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="88e1a-201">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="88e1a-202">Op Hallo **X.509-certificaten** dialoogvenster, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="88e1a-203">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="88e1a-204">Op Hallo **X.509-certificaten** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="88e1a-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="88e1a-205">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="88e1a-206">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-206">a.</span></span> <span data-ttu-id="88e1a-207">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-207">Click **New**.</span></span>
    
     <span data-ttu-id="88e1a-208">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-208">b.</span></span> <span data-ttu-id="88e1a-209">In Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="88e1a-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="88e1a-210">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-210">c.</span></span> <span data-ttu-id="88e1a-211">Selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-211">Select **Active**.</span></span>
    
     <span data-ttu-id="88e1a-212">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-212">d.</span></span> <span data-ttu-id="88e1a-213">Als **indeling**, selecteer **PEM**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="88e1a-214">e.</span><span class="sxs-lookup"><span data-stu-id="88e1a-214">e.</span></span> <span data-ttu-id="88e1a-215">Als **Type**, selecteer **vertrouwen Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="88e1a-216">f.</span><span class="sxs-lookup"><span data-stu-id="88e1a-216">f.</span></span> <span data-ttu-id="88e1a-217">De met Base64 versleuteld certificaat openen in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **PEM certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="88e1a-218">g.</span><span class="sxs-lookup"><span data-stu-id="88e1a-218">g.</span></span> <span data-ttu-id="88e1a-219">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-219">Click **Update**.</span></span>

13. <span data-ttu-id="88e1a-220">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="88e1a-221">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="88e1a-222">Op Hallo **identiteitsproviders** dialoogvenster, klikt u op **nieuw**:</span><span class="sxs-lookup"><span data-stu-id="88e1a-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="88e1a-223">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="88e1a-224">Op Hallo **identiteitsproviders** dialoogvenster, klikt u op **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="88e1a-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="88e1a-225">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="88e1a-226">Op eigenschappenvenster Hallo SAML2 Update1, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="88e1a-227">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="88e1a-228">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-228">a.</span></span> <span data-ttu-id="88e1a-229">in Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="88e1a-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="88e1a-230">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-230">b.</span></span> <span data-ttu-id="88e1a-231">In Hallo **Gebruikersveld** textbox type **e** of **gebruikersnaam**, afhankelijk van welk veld wordt gebruikt toouniquely gebruikers in uw ServiceNow-implementatie identificeren.</span><span class="sxs-lookup"><span data-stu-id="88e1a-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="88e1a-232">U kunt configue Azure AD tooemit beide hello Azure AD-gebruikers-ID (UPN) of Hallo e-mailadres als unieke id in het SAML-token Hallo Hallo door te gaan toohello **ServiceNow > kenmerken > eenmalige aanmelding** sectie klassieke Azure portal en toewijzing Hallo gewenst veld toohello Hallo **nameidentifier** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="88e1a-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="88e1a-233">Hallo-waarde voor het geselecteerde kenmerk Hallo opgeslagen in Azure AD (bijvoorbeeld gebruiker principal name) moet overeenkomen met de Hallo opgeslagen in ServiceNow voor Hallo ingevoerd veld (bijvoorbeeld gebruikersnaam)</span><span class="sxs-lookup"><span data-stu-id="88e1a-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="88e1a-234">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-234">c.</span></span> <span data-ttu-id="88e1a-235">Kopieer in de klassieke portal hello Azure AD, Hallo **identiteit Provider-ID** waarde en plak deze in Hallo **identiteit Provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="88e1a-236">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-236">d.</span></span> <span data-ttu-id="88e1a-237">Kopieer in de klassieke portal hello Azure AD, Hallo **aanvraag-URL voor webverificatie** waarde en plak deze in Hallo **van de identiteitsprovider AuthnRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="88e1a-238">e.</span><span class="sxs-lookup"><span data-stu-id="88e1a-238">e.</span></span> <span data-ttu-id="88e1a-239">Kopieer in de klassieke portal hello Azure AD, Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **van de identiteitsprovider SingleLogoutRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="88e1a-240">f.</span><span class="sxs-lookup"><span data-stu-id="88e1a-240">f.</span></span> <span data-ttu-id="88e1a-241">In Hallo **ServiceNow Homepage** textbox type Hallo-URL van de startpagina van uw ServiceNow-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="88e1a-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88e1a-242">startpagina van Hallo ServiceNow-exemplaar is een samenvoeging van uw **ServieNow tenant-URL** en **/navpage.do** (bijvoorbeeld:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="88e1a-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="88e1a-243">g.</span><span class="sxs-lookup"><span data-stu-id="88e1a-243">g.</span></span> <span data-ttu-id="88e1a-244">In Hallo **entiteit-ID / verlener** textbox type Hallo-URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="88e1a-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="88e1a-245">h.</span><span class="sxs-lookup"><span data-stu-id="88e1a-245">h.</span></span> <span data-ttu-id="88e1a-246">In Hallo **doelgroep URL** textbox type Hallo-URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="88e1a-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="88e1a-247">ik.</span><span class="sxs-lookup"><span data-stu-id="88e1a-247">i.</span></span> <span data-ttu-id="88e1a-248">In Hallo **Protocol Binding voor Hallo van IDP SingleLogoutRequest** textbox type **urn: oasis: namen: tc: SAML:2.0:bindings:HTTP-omleiden**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="88e1a-249">j.</span><span class="sxs-lookup"><span data-stu-id="88e1a-249">j.</span></span> <span data-ttu-id="88e1a-250">Typ in het tekstvak NameID beleid hello, **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: niet-gespecificeerde**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="88e1a-251">k.</span><span class="sxs-lookup"><span data-stu-id="88e1a-251">k.</span></span> <span data-ttu-id="88e1a-252">Hef de selectie **maken van een AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="88e1a-253">l.</span><span class="sxs-lookup"><span data-stu-id="88e1a-253">l.</span></span> <span data-ttu-id="88e1a-254">In Hallo **AuthnContextClassRef methode**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="88e1a-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="88e1a-255">Dit is alleen nodig als u alleen cloud-organisatie.</span><span class="sxs-lookup"><span data-stu-id="88e1a-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="88e1a-256">Als u werkt met on-premises AD FS of MFA voor verificatie en vervolgens moet u deze waarde niet configureren.</span><span class="sxs-lookup"><span data-stu-id="88e1a-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="88e1a-257">m.</span><span class="sxs-lookup"><span data-stu-id="88e1a-257">m.</span></span> <span data-ttu-id="88e1a-258">In **klok leiden tot onjuiste** textbox type **60**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="88e1a-259">n.</span><span class="sxs-lookup"><span data-stu-id="88e1a-259">n.</span></span> <span data-ttu-id="88e1a-260">Als **eenmalige aanmelding op Script**, selecteer **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="88e1a-261">o.</span><span class="sxs-lookup"><span data-stu-id="88e1a-261">o.</span></span> <span data-ttu-id="88e1a-262">Als **x509 certificaat**, selecteert u hebt gemaakt in de vorige stap Hallo Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="88e1a-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="88e1a-263">p.</span><span class="sxs-lookup"><span data-stu-id="88e1a-263">p.</span></span> <span data-ttu-id="88e1a-264">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="88e1a-265">In de klassieke portal hello Azure AD, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="88e1a-266">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="88e1a-267">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="88e1a-268">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="88e1a-269">Configureren van Azure AD voor eenmalige aanmelding voor snelle ServiceNow</span><span class="sxs-lookup"><span data-stu-id="88e1a-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="88e1a-270">In de klassieke portal hello Azure AD op Hallo **ServiceNow** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster .</span><span class="sxs-lookup"><span data-stu-id="88e1a-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="88e1a-271">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="88e1a-272">Op Hallo **wilt u hoe gebruikers toosign op tooServiceNow** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="88e1a-273">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749324.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="88e1a-274">Op Hallo **App-instellingen configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="88e1a-275">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC769497.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="88e1a-276">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-276">a.</span></span> <span data-ttu-id="88e1a-277">in Hallo **ServiceNow aanmelding op URL** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="88e1a-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="88e1a-278">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-278">b.</span></span> <span data-ttu-id="88e1a-279">In Hallo **URL-verlener** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="88e1a-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="88e1a-280">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-280">c.</span></span> <span data-ttu-id="88e1a-281">Klik op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="88e1a-281">Click **Next**</span></span>

4. <span data-ttu-id="88e1a-282">Klik op **handmatig Hallo-toepassing voor eenmalige aanmelding configureren**, klikt u vervolgens op **volgende** en volledige Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="88e1a-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="88e1a-283">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="88e1a-284">Op Hallo **eenmalige aanmelding configureren op ServiceNow** pagina, klikt u op **certificaat downloaden**Hallo certificaatbestand lokaal op uw computer opgeslagen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="88e1a-285">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749325.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="88e1a-286">Eenmalige aanmelding tooyour ServiceNow Express-toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="88e1a-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="88e1a-287">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="88e1a-288">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="88e1a-289">Op Hallo **Single Sign-On** dialoogvenster, klikt u op Hallo configuratiepictogram op Hallo rechterbovenhoek rechts en stel hello volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="88e1a-290">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="88e1a-291">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-291">a.</span></span> <span data-ttu-id="88e1a-292">Wisselknop **provider voor meervoudige eenmalige aanmelding inschakelen** toohello rechts.</span><span class="sxs-lookup"><span data-stu-id="88e1a-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="88e1a-293">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-293">b.</span></span> <span data-ttu-id="88e1a-294">Wisselknop **logboekregistratie voor Hallo provider voor meervoudige SSO-integratie voor het inschakelen van foutopsporing** toohello rechts.</span><span class="sxs-lookup"><span data-stu-id="88e1a-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="88e1a-295">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-295">c.</span></span> <span data-ttu-id="88e1a-296">In **Hallo veld op Hallo gebruiker tabel die...**  textbox type **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="88e1a-297">Op Hallo **Single Sign-On** dialoogvenster, klikt u op **nieuw certificaat toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="88e1a-298">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="88e1a-299">Op Hallo **X.509-certificaten** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="88e1a-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="88e1a-300">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="88e1a-301">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-301">a.</span></span> <span data-ttu-id="88e1a-302">In Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="88e1a-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="88e1a-303">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-303">b.</span></span> <span data-ttu-id="88e1a-304">Selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-304">Select **Active**.</span></span>
    
    <span data-ttu-id="88e1a-305">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-305">c.</span></span> <span data-ttu-id="88e1a-306">Als **indeling**, selecteer **PEM**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="88e1a-307">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-307">d.</span></span> <span data-ttu-id="88e1a-308">Als **Type**, selecteer **vertrouwen Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="88e1a-309">e.</span><span class="sxs-lookup"><span data-stu-id="88e1a-309">e.</span></span> <span data-ttu-id="88e1a-310">Maak een Base64-gecodeerde bestand uit het gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="88e1a-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="88e1a-311">Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="88e1a-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="88e1a-312">f.</span><span class="sxs-lookup"><span data-stu-id="88e1a-312">f.</span></span> <span data-ttu-id="88e1a-313">De met Base64 versleuteld certificaat openen in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **PEM certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="88e1a-314">g.</span><span class="sxs-lookup"><span data-stu-id="88e1a-314">g.</span></span> <span data-ttu-id="88e1a-315">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-315">Click **Update**.</span></span>
11. <span data-ttu-id="88e1a-316">Op Hallo **Single Sign-On** dialoogvenster, klikt u op **toevoegen van nieuwe IdP**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="88e1a-317">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="88e1a-318">Op Hallo **identiteitsprovider toevoegen** dialoogvenster onder **id-Provider configureren**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="88e1a-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="88e1a-319">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="88e1a-320">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-320">a.</span></span> <span data-ttu-id="88e1a-321">in Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="88e1a-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="88e1a-322">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-322">b.</span></span> <span data-ttu-id="88e1a-323">Kopieer in de klassieke portal hello Azure AD, Hallo **identiteit Provider-ID** waarde en plak deze in Hallo **identiteit Provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="88e1a-324">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-324">c.</span></span> <span data-ttu-id="88e1a-325">Kopieer in de klassieke portal hello Azure AD, Hallo **aanvraag-URL voor webverificatie** waarde en plak deze in Hallo **van de identiteitsprovider AuthnRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="88e1a-326">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-326">d.</span></span> <span data-ttu-id="88e1a-327">Kopieer in de klassieke portal hello Azure AD, Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **van de identiteitsprovider SingleLogoutRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="88e1a-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="88e1a-328">e.</span><span class="sxs-lookup"><span data-stu-id="88e1a-328">e.</span></span> <span data-ttu-id="88e1a-329">Als **Provider identiteitscertificaat**, selecteert u hebt gemaakt in de vorige stap Hallo Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="88e1a-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="88e1a-330">Klik op **geavanceerde instellingen**, en klikt u onder **extra identiteitseigenschappen Provider**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="88e1a-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="88e1a-331">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="88e1a-332">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-332">a.</span></span> <span data-ttu-id="88e1a-333">In Hallo **Protocol Binding voor Hallo van IDP SingleLogoutRequest** textbox type **urn: oasis: namen: tc: SAML:2.0:bindings:HTTP-omleiden**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="88e1a-334">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-334">b.</span></span> <span data-ttu-id="88e1a-335">In Hallo **NameID beleid** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: niet-gespecificeerde**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="88e1a-336">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-336">c.</span></span> <span data-ttu-id="88e1a-337">In Hallo **AuthnContextClassRef methode**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="88e1a-338">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-338">d.</span></span> <span data-ttu-id="88e1a-339">Hef de selectie **maken van een AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="88e1a-340">Onder **extra eigenschappen van de Service Provider**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="88e1a-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="88e1a-341">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="88e1a-342">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-342">a.</span></span> <span data-ttu-id="88e1a-343">In Hallo **ServiceNow Homepage** textbox type Hallo-URL van de startpagina van uw ServiceNow-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="88e1a-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="88e1a-344">startpagina van Hallo ServiceNow-exemplaar is een samenvoeging van uw **ServieNow tenant-URL** en **/navpage.do** (bijvoorbeeld: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="88e1a-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="88e1a-345">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-345">b.</span></span> <span data-ttu-id="88e1a-346">In Hallo **entiteit-ID / verlener** textbox type Hallo-URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="88e1a-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="88e1a-347">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-347">c.</span></span> <span data-ttu-id="88e1a-348">In Hallo **doelgroep-URI** textbox type Hallo-URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="88e1a-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="88e1a-349">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-349">d.</span></span> <span data-ttu-id="88e1a-350">In **klok leiden tot onjuiste** textbox type **60**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="88e1a-351">e.</span><span class="sxs-lookup"><span data-stu-id="88e1a-351">e.</span></span> <span data-ttu-id="88e1a-352">In Hallo **Gebruikersveld** textbox type **e** of **gebruikersnaam**, afhankelijk van welk veld wordt gebruikt toouniquely gebruikers in uw ServiceNow-implementatie identificeren.</span><span class="sxs-lookup"><span data-stu-id="88e1a-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="88e1a-353">U kunt configue Azure AD tooemit beide hello Azure AD-gebruikers-ID (UPN) of Hallo e-mailadres als unieke id in het SAML-token Hallo Hallo door te gaan toohello **ServiceNow > kenmerken > eenmalige aanmelding** sectie klassieke Azure portal en toewijzing Hallo gewenst veld toohello Hallo **nameidentifier** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="88e1a-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="88e1a-354">Hallo-waarde voor het geselecteerde kenmerk Hallo opgeslagen in Azure AD (bijvoorbeeld gebruiker principal name) moet overeenkomen met de Hallo opgeslagen in ServiceNow voor Hallo ingevoerd veld (bijvoorbeeld gebruikersnaam)</span><span class="sxs-lookup"><span data-stu-id="88e1a-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="88e1a-355">f.</span><span class="sxs-lookup"><span data-stu-id="88e1a-355">f.</span></span> <span data-ttu-id="88e1a-356">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-356">Click **Save**.</span></span> 

3. <span data-ttu-id="88e1a-357">In de klassieke portal hello Azure AD, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="88e1a-358">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="88e1a-359">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="88e1a-360">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="88e1a-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="88e1a-361">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="88e1a-361">Configuring user provisioning</span></span>
<span data-ttu-id="88e1a-362">Hallo-doel van deze sectie is het toooutline hoe tooServiceNow tooenable gebruikers inrichten van Active Directory-gebruiker accounts.</span><span class="sxs-lookup"><span data-stu-id="88e1a-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="88e1a-363">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="88e1a-364">In hello Azure Management klassieke portal op Hallo **ServiceNow** toepassing Integratiepagina, klikt u op **configureren gebruikersaanvragen**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="88e1a-365">![Gebruikers inrichten](./media/active-directory-saas-servicenow-tutorial/IC769498.png "gebruikers inrichten")</span><span class="sxs-lookup"><span data-stu-id="88e1a-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="88e1a-366">Op Hallo **Voer uw ServiceNow referenties tooenable automatisch gebruikers inrichten** pagina, bieden Hallo na configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="88e1a-367">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-367">a.</span></span> <span data-ttu-id="88e1a-368">In Hallo **ServiceNow-exemplaarnaam** textbox typenaam Hallo ServiceNow-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="88e1a-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="88e1a-369">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-369">b.</span></span> <span data-ttu-id="88e1a-370">In Hallo **ServiceNow-Beheerdersgebruikersnaam** textbox Hallo typenaam Hallo ServiceNow-beheeraccount.</span><span class="sxs-lookup"><span data-stu-id="88e1a-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="88e1a-371">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-371">c.</span></span> <span data-ttu-id="88e1a-372">In Hallo **ServiceNow-beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.</span><span class="sxs-lookup"><span data-stu-id="88e1a-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="88e1a-373">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-373">d.</span></span> <span data-ttu-id="88e1a-374">Klik op **valideren** tooverify uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="88e1a-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="88e1a-375">e.</span><span class="sxs-lookup"><span data-stu-id="88e1a-375">e.</span></span> <span data-ttu-id="88e1a-376">Klik op Hallo **volgende** knop tooopen hello **Vervolgstappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="88e1a-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="88e1a-377">f.</span><span class="sxs-lookup"><span data-stu-id="88e1a-377">f.</span></span> <span data-ttu-id="88e1a-378">Als u wilt dat tooprovision alle gebruikers toothis toepassing, selecteert u '**automatisch inrichten van alle gebruikersaccounts in de directory toothis-toepassing hello**'.</span><span class="sxs-lookup"><span data-stu-id="88e1a-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="88e1a-379">![Volgende stappen](./media/active-directory-saas-servicenow-tutorial/IC698804.png "volgende stappen")</span><span class="sxs-lookup"><span data-stu-id="88e1a-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="88e1a-380">g.</span><span class="sxs-lookup"><span data-stu-id="88e1a-380">g.</span></span> <span data-ttu-id="88e1a-381">Op Hallo **Vervolgstappen** pagina, klikt u op **Complete** toosave uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="88e1a-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88e1a-382">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="88e1a-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="88e1a-383">In deze sectie kunt u een testgebruiker maken in de klassieke portal Hallo Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="88e1a-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="88e1a-385">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="88e1a-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e1a-386">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="88e1a-388">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="88e1a-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="88e1a-389">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88e1a-391">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="88e1a-393">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="88e1a-395">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-395">a.</span></span> <span data-ttu-id="88e1a-396">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="88e1a-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="88e1a-397">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-397">b.</span></span> <span data-ttu-id="88e1a-398">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="88e1a-399">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-399">c.</span></span> <span data-ttu-id="88e1a-400">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-400">Click **Next**.</span></span>

6. <span data-ttu-id="88e1a-401">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="88e1a-403">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-403">a.</span></span> <span data-ttu-id="88e1a-404">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="88e1a-405">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-405">b.</span></span> <span data-ttu-id="88e1a-406">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="88e1a-407">c.</span><span class="sxs-lookup"><span data-stu-id="88e1a-407">c.</span></span> <span data-ttu-id="88e1a-408">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="88e1a-409">d.</span><span class="sxs-lookup"><span data-stu-id="88e1a-409">d.</span></span> <span data-ttu-id="88e1a-410">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="88e1a-411">e.</span><span class="sxs-lookup"><span data-stu-id="88e1a-411">e.</span></span> <span data-ttu-id="88e1a-412">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-412">Click **Next**.</span></span>

7. <span data-ttu-id="88e1a-413">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="88e1a-415">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88e1a-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="88e1a-417">a.</span><span class="sxs-lookup"><span data-stu-id="88e1a-417">a.</span></span> <span data-ttu-id="88e1a-418">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="88e1a-419">b.</span><span class="sxs-lookup"><span data-stu-id="88e1a-419">b.</span></span> <span data-ttu-id="88e1a-420">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="88e1a-421">Maken van een testgebruiker ServiceNow</span><span class="sxs-lookup"><span data-stu-id="88e1a-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="88e1a-422">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="88e1a-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="88e1a-423">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="88e1a-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="88e1a-424">Als u niet hoe tooadd een gebruiker in uw ServiceNow of ServiceNow Express-account weet, moet u contact op met ServiceNow-ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="88e1a-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="88e1a-425">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e1a-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="88e1a-426">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooServiceNow toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="88e1a-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="88e1a-428">**tooassign Britta Simon tooServiceNow, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="88e1a-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e1a-429">Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="88e1a-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="88e1a-431">Selecteer in de lijst met de toepassingen van Hallo **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="88e1a-433">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203] 

4. <span data-ttu-id="88e1a-435">Selecteer in de lijst met alle gebruikers van hello, **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="88e1a-436">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="88e1a-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="88e1a-438">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88e1a-438">Testing single sign-on</span></span>
<span data-ttu-id="88e1a-439">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="88e1a-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88e1a-440">Als u op Hallo ServiceNow-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ServiceNow-toepassing.</span><span class="sxs-lookup"><span data-stu-id="88e1a-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88e1a-441">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="88e1a-441">Additional resources</span></span>
* [<span data-ttu-id="88e1a-442">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88e1a-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88e1a-443">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88e1a-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
