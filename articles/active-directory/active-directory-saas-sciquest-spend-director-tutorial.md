---
title: 'Zelfstudie: Azure Active Directory-integratie met SciQuest besteden directeur | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SciQuest besteden directeur.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="cdfbb-103">Zelfstudie: Azure Active Directory-integratie met SciQuest besteden directeur</span><span class="sxs-lookup"><span data-stu-id="cdfbb-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="cdfbb-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate SciQuest besteden directeur met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cdfbb-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="cdfbb-105">SciQuest besteden directeur integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="cdfbb-106">U kunt beheren in Azure AD die toegang tooSciQuest uitgaven directeur heeft</span><span class="sxs-lookup"><span data-stu-id="cdfbb-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="cdfbb-107">U kunt uw gebruikers tooautomatically get aangemelde tooSciQuest uitgaven directeur (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="cdfbb-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="cdfbb-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="cdfbb-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="cdfbb-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cdfbb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdfbb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cdfbb-110">Prerequisites</span></span>
<span data-ttu-id="cdfbb-111">Azure AD-integratie met SciQuest besteden directeur tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="cdfbb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="cdfbb-112">An Azure AD subscription</span></span>
* <span data-ttu-id="cdfbb-113">Een SciQuest besteden directeur eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="cdfbb-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cdfbb-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="cdfbb-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="cdfbb-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="cdfbb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdfbb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="cdfbb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cdfbb-118">Scenario Description</span></span>
<span data-ttu-id="cdfbb-119">Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="cdfbb-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cdfbb-121">Het toevoegen van SciQuest besteden directeur van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cdfbb-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="cdfbb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cdfbb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="cdfbb-123">Het toevoegen van SciQuest besteden directeur van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cdfbb-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="cdfbb-124">tooconfigure hello integratie van SciQuest besteden directeur in Azure AD, moet u tooadd SciQuest besteden directeur uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cdfbb-125">**tooadd SciQuest besteden directeur via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cdfbb-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfbb-126">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="cdfbb-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="cdfbb-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Toepassingen][2]

4. <span data-ttu-id="cdfbb-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3]

5. <span data-ttu-id="cdfbb-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Toepassingen][4]

6. <span data-ttu-id="cdfbb-135">Typ in het zoekvak Hallo **sciQuest besteden directeur**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Toepassingen][5]

7. <span data-ttu-id="cdfbb-137">Selecteer in het deelvenster met resultaten Hallo **SciQuest besteden directeur**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Toepassingen][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cdfbb-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cdfbb-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cdfbb-140">Hallo-doel van deze sectie is tooshow u hoe tooconfigure en eenmalige aanmelding Azure AD-test met SciQuest besteden directeur op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cdfbb-141">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SciQuest besteden directeur tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="cdfbb-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SciQuest besteden directeur toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="cdfbb-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="cdfbb-144">tooconfigure en eenmalige aanmelding Azure AD-test met SciQuest besteden directeur, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cdfbb-145">**[Configureren van Azure AD één Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cdfbb-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cdfbb-147">**[Maken van een testgebruiker SciQuest besteden directeur](#creating-a-halogen-software-test-user)**  -toohave een equivalent van Britta Simon in SciQuest besteden directeur die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cdfbb-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cdfbb-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="cdfbb-150">Azure AD één eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="cdfbb-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="cdfbb-151">Hallo-doel van deze sectie is tooenable Azure AD eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure eenmalige aanmelding in uw toepassing SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="cdfbb-152">**tooconfigure eenmalige aanmelding Azure AD met SciQuest besteden directeur uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cdfbb-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfbb-153">In de klassieke Azure-portal op Hallo Hallo **SciQuest besteden directeur** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][8]

2. <span data-ttu-id="cdfbb-155">Op Hallo **wilt u hoe gebruikers toosign op tooSciQuest uitgaven directeur** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][9]

3. <span data-ttu-id="cdfbb-157">Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![App-instellingen configureren][10]
   
     <span data-ttu-id="cdfbb-159">a.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-159">a.</span></span> <span data-ttu-id="cdfbb-160">In Hallo **aanmelding op URL** textbox, typ uw URL wordt gebruikt door uw gebruikers toosign op tooyour SciQuest besteden directeur toepassing hello patroon volgen: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="cdfbb-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="cdfbb-161">b.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-161">b.</span></span> <span data-ttu-id="cdfbb-162">In Hallo **antwoord-URL** textbox, type Hallo dezelfde waarde als u hebt in Hallo hebt getypt **aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="cdfbb-163">c.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-163">c.</span></span> <span data-ttu-id="cdfbb-164">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-164">Click **Next**.</span></span>

4. <span data-ttu-id="cdfbb-165">Op Hallo **eenmalige aanmelding configureren op SciQuest besteden directeur** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens Hallo lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Wat is Azure AD Connect?][11]

5. <span data-ttu-id="cdfbb-167">Neem contact op met SciQuest ondersteuning tooenable deze verificatiemethode met metagegevens voor de bovenstaande Hallo gedownload.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="cdfbb-168">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Wat is Azure AD Connect?][15]

7. <span data-ttu-id="cdfbb-170">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cdfbb-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cdfbb-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="cdfbb-172">Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="cdfbb-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cdfbb-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfbb-174">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Wat is Azure AD Connect?][100] 

2. <span data-ttu-id="cdfbb-176">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="cdfbb-177">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Wat is Azure AD Connect?][101] 

4. <span data-ttu-id="cdfbb-179">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Wat is Azure AD Connect?][102] 

5. <span data-ttu-id="cdfbb-181">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Wat is Azure AD Connect?][103] 
   
    <span data-ttu-id="cdfbb-183">a.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-183">a.</span></span> <span data-ttu-id="cdfbb-184">Als **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="cdfbb-185">b.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-185">b.</span></span> <span data-ttu-id="cdfbb-186">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="cdfbb-187">c.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-187">c.</span></span> <span data-ttu-id="cdfbb-188">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-188">Click **Next**.</span></span>

6. <span data-ttu-id="cdfbb-189">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Wat is Azure AD Connect?][104] 
   
    <span data-ttu-id="cdfbb-191">a.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-191">a.</span></span> <span data-ttu-id="cdfbb-192">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="cdfbb-193">b.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-193">b.</span></span> <span data-ttu-id="cdfbb-194">In Hallo **achternaam** txtbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="cdfbb-195">c.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-195">c.</span></span> <span data-ttu-id="cdfbb-196">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="cdfbb-197">d.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-197">d.</span></span> <span data-ttu-id="cdfbb-198">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="cdfbb-199">e.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-199">e.</span></span> <span data-ttu-id="cdfbb-200">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-200">Click **Next**.</span></span>

7. <span data-ttu-id="cdfbb-201">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Wat is Azure AD Connect?][105]  

8. <span data-ttu-id="cdfbb-203">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cdfbb-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Wat is Azure AD Connect?][106]   
   
    <span data-ttu-id="cdfbb-205">a.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-205">a.</span></span> <span data-ttu-id="cdfbb-206">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="cdfbb-207">b.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-207">b.</span></span> <span data-ttu-id="cdfbb-208">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="cdfbb-209">Een testgebruiker SciQuest besteden directeur maken</span><span class="sxs-lookup"><span data-stu-id="cdfbb-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="cdfbb-210">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in SciQuest besteden directeur van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="cdfbb-211">U moet toocontact ondersteuningsteam SciQuest besteden directeur en hen voorzien Hallo details over uw test account tooget die deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="cdfbb-212">U kunt ook kunt u gebruikmaken van just-in-time-inrichting, een eenmalige aanmelding functie die wordt ondersteund door SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="cdfbb-213">Als just-in-time-inrichting is ingeschakeld, worden gebruikers automatisch gemaakt door SciQuest besteden directeur tijdens een poging voor aanmelding als ze nog niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="cdfbb-214">Deze functie Hallo overbodig toomanually gebruikers eenmalige aanmelding equivalent maken.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="cdfbb-215">tooget just-in-time-inrichting is ingeschakeld, moet u toocontact je het ondersteuningsteam SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cdfbb-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfbb-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="cdfbb-217">Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar toegang tooSciQuest uitgaven directeur verleent.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Wat is Azure AD Connect?][200]

<span data-ttu-id="cdfbb-219">**tooassign Britta Simon tooSciQuest uitgaven directeur, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cdfbb-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfbb-220">Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Wat is Azure AD Connect?][201]

2. <span data-ttu-id="cdfbb-222">Selecteer in de lijst met de toepassingen van Hallo **SciQuest besteden directeur**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Wat is Azure AD Connect?][202]

3. <span data-ttu-id="cdfbb-224">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Wat is Azure AD Connect?][203]

4. <span data-ttu-id="cdfbb-226">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Wat is Azure AD Connect?][204]

5. <span data-ttu-id="cdfbb-228">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Wat is Azure AD Connect?][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="cdfbb-230">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cdfbb-230">Testing Single Sign-On</span></span>
<span data-ttu-id="cdfbb-231">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="cdfbb-232">Als u op Hallo SciQuest besteden directeur tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SciQuest besteden directeur toepassing.</span><span class="sxs-lookup"><span data-stu-id="cdfbb-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cdfbb-233">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="cdfbb-233">Additional Resources</span></span>
* [<span data-ttu-id="cdfbb-234">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cdfbb-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cdfbb-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cdfbb-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

