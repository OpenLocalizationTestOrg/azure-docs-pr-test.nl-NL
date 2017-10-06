---
title: 'Zelfstudie: Azure Active Directory-integratie met @Task| Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en @Task.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="6aff0-103">Zelfstudie: Azure Active Directory-integratie met@Task</span><span class="sxs-lookup"><span data-stu-id="6aff0-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="6aff0-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate @Task met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6aff0-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="6aff0-105">Integratie van @Task met Azure AD biedt u Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="6aff0-106">U kunt beheren in Azure AD die toegang heefttoo@Task</span><span class="sxs-lookup"><span data-stu-id="6aff0-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="6aff0-107">U kunt uw tooautomatically ophalen aangemelde gebruikers inschakelen too@Task (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="6aff0-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="6aff0-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-Portal beheren</span><span class="sxs-lookup"><span data-stu-id="6aff0-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="6aff0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6aff0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aff0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6aff0-110">Prerequisites</span></span>
<span data-ttu-id="6aff0-111">tooconfigure Azure AD-integratie met @Task, moet u de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="6aff0-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="6aff0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6aff0-112">An Azure AD subscription</span></span>
* <span data-ttu-id="6aff0-113">Een @Task eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6aff0-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6aff0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6aff0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="6aff0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6aff0-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6aff0-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6aff0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6aff0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="6aff0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6aff0-118">Scenario Description</span></span>
<span data-ttu-id="6aff0-119">Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6aff0-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="6aff0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit drie belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="6aff0-121">Toe te voegen @Task uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6aff0-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="6aff0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6aff0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="6aff0-123">Toe te voegen @Task uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6aff0-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="6aff0-124">tooconfigure hello integratie van @Task in Azure AD, moet u tooadd @Task uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6aff0-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6aff0-125">**tooadd @Task uitvoeren via Hallo gallery Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6aff0-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6aff0-126">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="6aff0-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="6aff0-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6aff0-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="6aff0-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Toepassingen][2] 
4. <span data-ttu-id="6aff0-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="6aff0-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3] 
5. <span data-ttu-id="6aff0-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Toepassingen][4] 
6. <span data-ttu-id="6aff0-135">Typ in het zoekvak Hallo  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="6aff0-135">In hello search box, type **@Task**.</span></span>
   
    ![Toepassingen][5] 
7. <span data-ttu-id="6aff0-137">Selecteer in het deelvenster met resultaten Hallo  **@Task** , en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6aff0-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Toepassingen][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6aff0-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6aff0-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6aff0-140">Hallo doel van deze sectie is tooshow u hoe tooconfigure en Azure AD test eenmalige aanmelding met @Task op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6aff0-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6aff0-141">Voor één aanmelding toowork Azure AD moet tooknow welke gebruiker Hallo equivalent in @Task tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aff0-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="6aff0-142">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in @Task moet toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6aff0-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="6aff0-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in @Task.</span><span class="sxs-lookup"><span data-stu-id="6aff0-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="6aff0-144">tooconfigure en Azure AD test eenmalige aanmelding met @Task, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6aff0-145">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6aff0-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6aff0-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6aff0-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6aff0-147">**[Maken van een @Tasktest gebruiker](#creating-a-halogen-software-test-user)**  -toohave een equivalent van Britta Simon in @Taskthat gekoppelde toohello Azure AD-weergave van haar is.</span><span class="sxs-lookup"><span data-stu-id="6aff0-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="6aff0-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6aff0-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6aff0-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6aff0-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6aff0-150">Azure AD voor eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="6aff0-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="6aff0-151">Hallo-doel van deze sectie is tooenable Azure AD eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure eenmalige aanmelding in uw @Task toepassing.</span><span class="sxs-lookup"><span data-stu-id="6aff0-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="6aff0-152">**tooconfigure eenmalige aanmelding Azure AD met @Task, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="6aff0-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="6aff0-153">In de klassieke Azure-portal op Hallo Hallo  **@Task**  toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6aff0-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 
2. <span data-ttu-id="6aff0-155">Op Hallo **hoe wilt u gebruikers toosign op too@Task**  pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][7] 
3. <span data-ttu-id="6aff0-157">Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![App-instellingen configureren][8] 
   
     <span data-ttu-id="6aff0-159">a.</span><span class="sxs-lookup"><span data-stu-id="6aff0-159">a.</span></span> <span data-ttu-id="6aff0-160">In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw gebruikers toosign op tooyour @Task toepassing (bijvoorbeeld:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="6aff0-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="6aff0-161">b.</span><span class="sxs-lookup"><span data-stu-id="6aff0-161">b.</span></span> <span data-ttu-id="6aff0-162">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-162">Click **Next**.</span></span>
4. <span data-ttu-id="6aff0-163">Op Hallo **configureren eenmalige aanmelding op @Task**  pagina, klikt u op **metagegevens downloaden**, Hallo metagegevensbestand lokaal op uw computer opslaan en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Wat is Azure AD Connect?][9] 
5. <span data-ttu-id="6aff0-165">Eenmalige aanmelding tooyour @Task bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="6aff0-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="6aff0-166">Ga te**aanmelding op configuratie voor één**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="6aff0-167">Op Hallo **Single Sign-On** dialoogvenster Hallo volgende stappen uit te voeren</span><span class="sxs-lookup"><span data-stu-id="6aff0-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Eenmalige aanmelding configureren][23]
   
    <span data-ttu-id="6aff0-169">a.</span><span class="sxs-lookup"><span data-stu-id="6aff0-169">a.</span></span> <span data-ttu-id="6aff0-170">Als **Type**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="6aff0-171">b.</span><span class="sxs-lookup"><span data-stu-id="6aff0-171">b.</span></span> <span data-ttu-id="6aff0-172">Selecteer **Service Provider-ID**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="6aff0-173">c.</span><span class="sxs-lookup"><span data-stu-id="6aff0-173">c.</span></span> <span data-ttu-id="6aff0-174">Kopieer op Hallo klassieke Azure-portal, Hallo **externe aanmeldings-URL**, en plak deze in Hallo **Portal de aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6aff0-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="6aff0-175">d.</span><span class="sxs-lookup"><span data-stu-id="6aff0-175">d.</span></span> <span data-ttu-id="6aff0-176">Kopieer op Hallo klassieke Azure-portal, Hallo **Service-URL met eenmalige Sign-Out**, en plak deze in Hallo **Sign-Out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6aff0-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="6aff0-177">e.</span><span class="sxs-lookup"><span data-stu-id="6aff0-177">e.</span></span> <span data-ttu-id="6aff0-178">Kopieer op Hallo klassieke Azure-portal, Hallo **URL van wijzigen wachtwoord**, en plak deze in Hallo **URL van wijzigen wachtwoord** textbox.</span><span class="sxs-lookup"><span data-stu-id="6aff0-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="6aff0-179">f.</span><span class="sxs-lookup"><span data-stu-id="6aff0-179">f.</span></span> <span data-ttu-id="6aff0-180">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-180">Click **Save**.</span></span>
8. <span data-ttu-id="6aff0-181">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Wat is Azure AD Connect?][10]
9. <span data-ttu-id="6aff0-183">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Wat is Azure AD Connect?][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6aff0-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6aff0-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="6aff0-186">Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6aff0-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Azure AD-gebruiker maken][20]

<span data-ttu-id="6aff0-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6aff0-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6aff0-189">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="6aff0-191">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="6aff0-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6aff0-192">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="6aff0-194">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="6aff0-196">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="6aff0-198">a.</span><span class="sxs-lookup"><span data-stu-id="6aff0-198">a.</span></span> <span data-ttu-id="6aff0-199">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6aff0-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="6aff0-200">b.</span><span class="sxs-lookup"><span data-stu-id="6aff0-200">b.</span></span> <span data-ttu-id="6aff0-201">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="6aff0-202">c.</span><span class="sxs-lookup"><span data-stu-id="6aff0-202">c.</span></span> <span data-ttu-id="6aff0-203">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-203">Click **Next**.</span></span>
6. <span data-ttu-id="6aff0-204">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="6aff0-206">a.</span><span class="sxs-lookup"><span data-stu-id="6aff0-206">a.</span></span> <span data-ttu-id="6aff0-207">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="6aff0-208">b.</span><span class="sxs-lookup"><span data-stu-id="6aff0-208">b.</span></span> <span data-ttu-id="6aff0-209">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="6aff0-210">c.</span><span class="sxs-lookup"><span data-stu-id="6aff0-210">c.</span></span> <span data-ttu-id="6aff0-211">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="6aff0-212">d.</span><span class="sxs-lookup"><span data-stu-id="6aff0-212">d.</span></span> <span data-ttu-id="6aff0-213">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="6aff0-214">e.</span><span class="sxs-lookup"><span data-stu-id="6aff0-214">e.</span></span> <span data-ttu-id="6aff0-215">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-215">Click **Next**.</span></span>

7. <span data-ttu-id="6aff0-216">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="6aff0-218">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="6aff0-220">a.</span><span class="sxs-lookup"><span data-stu-id="6aff0-220">a.</span></span> <span data-ttu-id="6aff0-221">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="6aff0-222">b.</span><span class="sxs-lookup"><span data-stu-id="6aff0-222">b.</span></span> <span data-ttu-id="6aff0-223">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="6aff0-224">Maken van een @Task testgebruiker</span><span class="sxs-lookup"><span data-stu-id="6aff0-224">Creating an @Task test user</span></span>
<span data-ttu-id="6aff0-225">Hallo-doel van deze sectie is toocreate een gebruiker Britta Simon aangeroepen in @Task.</span><span class="sxs-lookup"><span data-stu-id="6aff0-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="6aff0-226">**een gebruiker Britta Simon aangeroepen in toocreate @Task, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="6aff0-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="6aff0-227">Meld u aan bij tooyour @Task bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="6aff0-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="6aff0-228">Klik in het menu bovenaan Hallo Hallo **mensen**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="6aff0-229">Klik op **nieuwe persoon**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="6aff0-230">Voer in het dialoogvenster van de nieuwe persoon Hallo, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6aff0-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Maak een @Task testgebruiker][21] 
   
    <span data-ttu-id="6aff0-232">a.</span><span class="sxs-lookup"><span data-stu-id="6aff0-232">a.</span></span> <span data-ttu-id="6aff0-233">In Hallo **voornaam** textbox, typt u 'Britta'.</span><span class="sxs-lookup"><span data-stu-id="6aff0-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="6aff0-234">b.</span><span class="sxs-lookup"><span data-stu-id="6aff0-234">b.</span></span> <span data-ttu-id="6aff0-235">In Hallo **achternaam** textbox, typt u 'Simon'.</span><span class="sxs-lookup"><span data-stu-id="6aff0-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="6aff0-236">c.</span><span class="sxs-lookup"><span data-stu-id="6aff0-236">c.</span></span> <span data-ttu-id="6aff0-237">In Hallo **e-mailadres** textbox Britta Simon van e-mailadres typt in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6aff0-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="6aff0-238">d.</span><span class="sxs-lookup"><span data-stu-id="6aff0-238">d.</span></span> <span data-ttu-id="6aff0-239">Klik op **persoon toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6aff0-240">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aff0-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="6aff0-241">Hallo doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding door haar toegang te verlenen too@Task.</span><span class="sxs-lookup"><span data-stu-id="6aff0-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6aff0-243">**tooassign Britta Simon too@Task, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="6aff0-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="6aff0-244">Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="6aff0-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Gebruiker toewijzen][201] 
2. <span data-ttu-id="6aff0-246">Selecteer in de lijst met de toepassingen van Hallo  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="6aff0-246">In hello applications list, select **@Task**.</span></span>
   
    ![Gebruiker toewijzen][202] 
3. <span data-ttu-id="6aff0-248">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203] 
4. <span data-ttu-id="6aff0-250">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="6aff0-251">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="6aff0-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="6aff0-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6aff0-253">Testing Single Sign-On</span></span>
<span data-ttu-id="6aff0-254">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6aff0-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="6aff0-255">Wanneer u klikt op Hallo @Task tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour @Task toepassing.</span><span class="sxs-lookup"><span data-stu-id="6aff0-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6aff0-256">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="6aff0-256">Additional Resources</span></span>
* [<span data-ttu-id="6aff0-257">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6aff0-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6aff0-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6aff0-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






