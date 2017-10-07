---
title: 'Zelfstudie: Azure Active Directory-integratie met Bynder | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Bynder.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="92fe3-103">Zelfstudie: Azure Active Directory-integratie met Bynder</span><span class="sxs-lookup"><span data-stu-id="92fe3-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="92fe3-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Bynder met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92fe3-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92fe3-105">Bynder integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="92fe3-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="92fe3-106">U kunt beheren in Azure AD die tooBynder toegang heeft</span><span class="sxs-lookup"><span data-stu-id="92fe3-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="92fe3-107">U kunt uw gebruikers tooautomatically get aangemelde tooBynder eenmalige aanmelding (SSO) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="92fe3-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="92fe3-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="92fe3-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="92fe3-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92fe3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92fe3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92fe3-110">Prerequisites</span></span>
<span data-ttu-id="92fe3-111">Azure AD-integratie met Bynder tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="92fe3-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="92fe3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="92fe3-112">An Azure AD subscription</span></span>
* <span data-ttu-id="92fe3-113">Een Bynder eenmalige aanmelding (SSO) abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="92fe3-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="92fe3-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="92fe3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="92fe3-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="92fe3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="92fe3-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="92fe3-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="92fe3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92fe3-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92fe3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="92fe3-118">Scenario description</span></span>
<span data-ttu-id="92fe3-119">Hallo-doel van deze zelfstudie is tooenable u tootest Microsoft Azure AD SSO in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="92fe3-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="92fe3-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="92fe3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92fe3-121">Het toevoegen van Bynder van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="92fe3-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="92fe3-122">Configureren en testen van Microsoft Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="92fe3-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="92fe3-123">Bynder van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="92fe3-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="92fe3-124">tooconfigure hello integratie van Bynder in Azure AD, moet u tooadd Bynder uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="92fe3-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92fe3-125">**tooadd Bynder via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92fe3-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fe3-126">In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="92fe3-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="92fe3-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="92fe3-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="92fe3-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Toepassingen][2]
4. <span data-ttu-id="92fe3-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="92fe3-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3]
5. <span data-ttu-id="92fe3-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Toepassingen][4]
6. <span data-ttu-id="92fe3-135">Typ in het zoekvak Hallo **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-135">In hello search box, type **Bynder**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="92fe3-137">Selecteer in het deelvenster resultaten hello, **Bynder**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="92fe3-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Hallo-app in de galerie Hallo selecteren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="92fe3-139">Configureren en testen van Microsoft Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="92fe3-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="92fe3-140">Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test Microsoft Azure AD-SSO met Bynder op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="92fe3-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92fe3-141">Voor eenmalige aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Bynder tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92fe3-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="92fe3-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Bynder toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="92fe3-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="92fe3-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Bynder.</span><span class="sxs-lookup"><span data-stu-id="92fe3-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="92fe3-144">tooconfigure en test Microsoft Azure AD-SSO met Bynder, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92fe3-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92fe3-145">**[Configureren van eenmalige aanmelding Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="92fe3-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92fe3-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92fe3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="92fe3-147">**[Maken van een testgebruiker Bynder](#creating-a-bynder-test-user)**  -toohave een equivalent van Britta Simon in Bynder die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="92fe3-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="92fe3-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse eenmalige aanmelding Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92fe3-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="92fe3-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="92fe3-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="92fe3-150">Configuratie van Microsoft Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="92fe3-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="92fe3-151">In deze sectie die u kunt Microsoft Azure AD eenmalige aanmelding inschakelen in de klassieke portal Hallo en eenmalige aanmelding in uw toepassing Bynder configureert.</span><span class="sxs-lookup"><span data-stu-id="92fe3-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="92fe3-152">**Microsoft Azure AD-SSO met Bynder, tooconfigure uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92fe3-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fe3-153">In de klassieke portal Hallo op Hallo **Bynder** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92fe3-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 
2. <span data-ttu-id="92fe3-155">Op Hallo **wilt u hoe gebruikers toosign op tooBynder** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="92fe3-157">Op Hallo **App-instellingen configureren** dialoogvenster pagina, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, het uitvoeren van Hallo volgende stappen uit en klik op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="92fe3-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="92fe3-159">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="92fe3-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="92fe3-160">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-160">Click **Next**.</span></span>
4. <span data-ttu-id="92fe3-161">U kunt eventueel tooconfigure Hallo toepassing in **SP geïnitieerd modus** op Hallo **App-instellingen configureren** dialoogvenster pagina, klikt u op Hallo **'Geavanceerde instellingen (optioneel) weergeven'**en voer vervolgens Hallo **aanmelding op URL** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="92fe3-163">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="92fe3-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="92fe3-164">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="92fe3-165">Hallo-waarde voor Hallo aanmelding op de URL in deze zelfstudie is slechts een placeholfer.</span><span class="sxs-lookup"><span data-stu-id="92fe3-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="92fe3-166">tooget hello werkelijke vlaue voor uw omgeving contact op met Bynder.</span><span class="sxs-lookup"><span data-stu-id="92fe3-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="92fe3-167">Op Hallo **eenmalige aanmelding configureren op Bynder** pagina, het uitvoeren van Hallo volgende stappen uit en klik op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="92fe3-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="92fe3-169">Klik op **metagegevens downloaden**, en sla Hallo-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="92fe3-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="92fe3-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-170">Click **Next**.</span></span>
6. <span data-ttu-id="92fe3-171">tooget SSO is geconfigureerd voor uw toepassing contact op met het ondersteuningsteam Bynder.</span><span class="sxs-lookup"><span data-stu-id="92fe3-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="92fe3-172">Hallo metagegevens van het gedownloade bestand toevoegen en delen met Bynder team tooset van eenmalige aanmelding op hun kant.</span><span class="sxs-lookup"><span data-stu-id="92fe3-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="92fe3-173">In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][10]
8. <span data-ttu-id="92fe3-175">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="92fe3-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="92fe3-177">Create an Azure AD test user</span></span>
<span data-ttu-id="92fe3-178">Hallo-doel van deze sectie is toocreate een testgebruiker in de klassieke portal Hallo Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="92fe3-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="92fe3-180">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92fe3-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fe3-181">In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="92fe3-183">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="92fe3-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="92fe3-184">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="92fe3-186">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="92fe3-188">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92fe3-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="92fe3-190">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92fe3-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="92fe3-191">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="92fe3-192">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-192">Click **Next**.</span></span>
6. <span data-ttu-id="92fe3-193">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92fe3-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="92fe3-195">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="92fe3-196">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="92fe3-197">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="92fe3-198">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="92fe3-199">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-199">Click **Next**.</span></span>
7. <span data-ttu-id="92fe3-200">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="92fe3-202">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92fe3-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="92fe3-204">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="92fe3-205">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="92fe3-206">Een testgebruiker Bynder maken</span><span class="sxs-lookup"><span data-stu-id="92fe3-206">Create a Bynder test user</span></span>
<span data-ttu-id="92fe3-207">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Bynder van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92fe3-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="92fe3-208">Bynder ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="92fe3-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="92fe3-209">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="92fe3-209">There is no action item for you in this section.</span></span> <span data-ttu-id="92fe3-210">Een nieuwe gebruiker wordt tijdens een poging tooaccess Bynder gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="92fe3-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="92fe3-211">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello Bynder ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="92fe3-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="92fe3-212">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="92fe3-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="92fe3-213">Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure SSO haar tooBynder toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="92fe3-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Gebruiker toewijzen][200]

<span data-ttu-id="92fe3-215">**tooassign Britta Simon tooBynder, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92fe3-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fe3-216">Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="92fe3-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Gebruiker toewijzen][201]
2. <span data-ttu-id="92fe3-218">Selecteer in de lijst met de toepassingen van Hallo **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="92fe3-220">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203]
4. <span data-ttu-id="92fe3-222">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="92fe3-223">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="92fe3-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="92fe3-225">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="92fe3-225">Test single sign-on</span></span>
<span data-ttu-id="92fe3-226">Hallo-doel van deze sectie is tootest uw Microsoft Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="92fe3-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="92fe3-227">Als u op Hallo Bynder tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Bynder toepassing.</span><span class="sxs-lookup"><span data-stu-id="92fe3-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92fe3-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="92fe3-228">Additional resources</span></span>
* [<span data-ttu-id="92fe3-229">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92fe3-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92fe3-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92fe3-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
