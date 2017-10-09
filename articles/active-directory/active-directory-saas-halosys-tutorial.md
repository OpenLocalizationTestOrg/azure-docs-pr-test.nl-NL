---
title: 'Zelfstudie: Azure Active Directory-integratie met Halosys | Microsoft Docs'
description: Lees hoe toouse Halosys met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="fa3b9-103">Zelfstudie: Azure Active Directory-integratie met Halosys</span><span class="sxs-lookup"><span data-stu-id="fa3b9-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="fa3b9-104">In deze zelfstudie leert u hoe toointegrate Halosys met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa3b9-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa3b9-105">Halosys integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fa3b9-106">U kunt beheren in Azure AD die tooHalosys toegang heeft</span><span class="sxs-lookup"><span data-stu-id="fa3b9-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="fa3b9-107">U kunt uw gebruikers tooautomatically get aangemelde tooHalosys (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="fa3b9-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa3b9-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fa3b9-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="fa3b9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa3b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa3b9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fa3b9-110">Prerequisites</span></span>

<span data-ttu-id="fa3b9-111">Azure AD-integratie met Halosys tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="fa3b9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fa3b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa3b9-113">Een Halosys eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fa3b9-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="fa3b9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="fa3b9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa3b9-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="fa3b9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa3b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="fa3b9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fa3b9-118">Scenario description</span></span>
<span data-ttu-id="fa3b9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="fa3b9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa3b9-121">Het toevoegen van Halosys van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fa3b9-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="fa3b9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa3b9-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="fa3b9-123">Het toevoegen van Halosys van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fa3b9-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="fa3b9-124">tooconfigure hello integratie van Halosys in Azure AD, moet u tooadd Halosys uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fa3b9-125">**tooadd Halosys via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa3b9-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3b9-126">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="fa3b9-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="fa3b9-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Toepassingen][2]

4. <span data-ttu-id="fa3b9-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Toepassingen][3]

5. <span data-ttu-id="fa3b9-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Toepassingen][4]

6. <span data-ttu-id="fa3b9-135">Typ in het zoekvak Hallo **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-135">In hello search box, type **Halosys**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="fa3b9-137">Selecteer in het deelvenster met resultaten Hallo **Halosys**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa3b9-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa3b9-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa3b9-140">In deze sectie configureert en test eenmalige aanmelding Azure AD met Halosys op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa3b9-141">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Halosys is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="fa3b9-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Halosys toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="fa3b9-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Halosys.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="fa3b9-144">tooconfigure en eenmalige aanmelding Azure AD-test met Halosys, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fa3b9-145">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fa3b9-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa3b9-147">**[Maken van een testgebruiker Halosys](#creating-a-halosys-test-user)**  -toohave een equivalent van Britta Simon in Halosys die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="fa3b9-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa3b9-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa3b9-150">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fa3b9-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa3b9-151">In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing Halosys.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="fa3b9-152">**Azure AD tooconfigure eenmalige aanmelding met Halosys, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa3b9-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3b9-153">In de klassieke portal Hallo op Hallo **Halosys** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Eenmalige aanmelding configureren][6] 

2. <span data-ttu-id="fa3b9-155">Op Hallo **wilt u hoe gebruikers toosign op tooHalosys** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="fa3b9-157">Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="fa3b9-159">a.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-159">a.</span></span> <span data-ttu-id="fa3b9-160">In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw gebruikers toosign op tooyour Halosys toepassing met behulp van Hallo patroon volgen: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="fa3b9-161">Hallo b.In **identificatie-URL** textbox, typ de URL van de Hallo in Hallo patroon volgen: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="fa3b9-162">Op Hallo **eenmalige aanmelding configureren op Halosys** pagina, klikt u op **metagegevens downloaden**, en sla Hallo-bestand op uw computer:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="fa3b9-164">tooget SSO is geconfigureerd voor uw toepassing, neem contact op met het ondersteuningsteam Halosys en voorzien Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="fa3b9-165">• Hallo gedownload **metagegevensbestand**</span><span class="sxs-lookup"><span data-stu-id="fa3b9-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="fa3b9-166">• Hallo **SAML-URL voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="fa3b9-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="fa3b9-167">In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD voor eenmalige aanmelding][10]

7. <span data-ttu-id="fa3b9-169">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD voor eenmalige aanmelding][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa3b9-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fa3b9-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa3b9-172">In deze sectie kunt u een testgebruiker maken in de klassieke portal Hallo Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Azure AD-gebruiker maken][20]

<span data-ttu-id="fa3b9-174">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa3b9-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3b9-175">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="fa3b9-177">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="fa3b9-178">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa3b9-180">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="fa3b9-182">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="fa3b9-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="fa3b9-183">a.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-183">a.</span></span> <span data-ttu-id="fa3b9-184">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="fa3b9-185">b.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-185">b.</span></span> <span data-ttu-id="fa3b9-186">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa3b9-187">c.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-187">c.</span></span> <span data-ttu-id="fa3b9-188">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-188">Click **Next**.</span></span>

6.  <span data-ttu-id="fa3b9-189">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="fa3b9-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="fa3b9-190">a.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-190">a.</span></span> <span data-ttu-id="fa3b9-191">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="fa3b9-192">b.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-192">b.</span></span> <span data-ttu-id="fa3b9-193">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="fa3b9-194">c.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-194">c.</span></span> <span data-ttu-id="fa3b9-195">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="fa3b9-196">d.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-196">d.</span></span> <span data-ttu-id="fa3b9-197">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="fa3b9-198">e.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-198">e.</span></span> <span data-ttu-id="fa3b9-199">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-199">Click **Next**.</span></span>

7. <span data-ttu-id="fa3b9-200">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="fa3b9-202">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa3b9-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="fa3b9-204">a.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-204">a.</span></span> <span data-ttu-id="fa3b9-205">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="fa3b9-206">b.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-206">b.</span></span> <span data-ttu-id="fa3b9-207">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="fa3b9-208">Een testgebruiker Halosys maken</span><span class="sxs-lookup"><span data-stu-id="fa3b9-208">Creating a Halosys test user</span></span>

<span data-ttu-id="fa3b9-209">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Halosys maken.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="fa3b9-210">Neem contact op met Halosys support team tooadd Hallo gebruikers in Hallo Halosys platform.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fa3b9-211">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa3b9-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fa3b9-212">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooHalosys toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fa3b9-214">**tooassign Britta Simon tooHalosys, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa3b9-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3b9-215">Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fa3b9-217">Selecteer in de lijst met de toepassingen van Hallo **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-217">In hello applications list, select **Halosys**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="fa3b9-219">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-219">In hello menu on hello top, click **Users**.</span></span>

    ![Gebruiker toewijzen][203]

4. <span data-ttu-id="fa3b9-221">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="fa3b9-222">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Gebruiker toewijzen][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="fa3b9-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa3b9-224">Testing single sign-on</span></span>

<span data-ttu-id="fa3b9-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fa3b9-226">Als u op Hallo Halosys-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Halosys toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa3b9-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fa3b9-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fa3b9-227">Additional resources</span></span>

* [<span data-ttu-id="fa3b9-228">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa3b9-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa3b9-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fa3b9-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
