---
title: 'Zelfstudie: Azure Active Directory-integratie met @Task| Microsoft Docs'
description: Meer informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en @Task.
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
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="b5018-103">Zelfstudie: Azure Active Directory-integratie met@Task</span><span class="sxs-lookup"><span data-stu-id="b5018-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="b5018-104">Het doel van deze zelfstudie is beschreven hoe u met het integreren van @Task met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5018-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="b5018-105">Integratie van @Task met Azure AD biedt u de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b5018-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="b5018-106">U kunt beheren in Azure AD die toegang heeft tot@Task</span><span class="sxs-lookup"><span data-stu-id="b5018-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="b5018-107">U kunt uw gebruikers automatisch aangemeld bij inschakelen @Task (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b5018-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="b5018-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure Portal beheren</span><span class="sxs-lookup"><span data-stu-id="b5018-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="b5018-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5018-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5018-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b5018-110">Prerequisites</span></span>
<span data-ttu-id="b5018-111">Voor het configureren van Azure AD-integratie met @Task, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b5018-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="b5018-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b5018-112">An Azure AD subscription</span></span>
* <span data-ttu-id="b5018-113">Een @Task eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b5018-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5018-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b5018-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="b5018-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b5018-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b5018-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b5018-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b5018-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5018-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="b5018-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b5018-118">Scenario Description</span></span>
<span data-ttu-id="b5018-119">Het doel van deze zelfstudie is zodat u kunt eenmalige aanmelding Azure AD te testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b5018-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="b5018-120">Het scenario in deze zelfstudie bestaat uit drie belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b5018-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="b5018-121">Toe te voegen @Task uit de galerie</span><span class="sxs-lookup"><span data-stu-id="b5018-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="b5018-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5018-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="b5018-123">Toe te voegen @Task uit de galerie</span><span class="sxs-lookup"><span data-stu-id="b5018-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="b5018-124">Voor het configureren van de integratie van @Task in Azure AD, moet u toevoegen @Task uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b5018-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b5018-125">**Om toe te voegen @Task uit de galerie, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b5018-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b5018-126">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5018-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="b5018-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="b5018-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b5018-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b5018-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Toepassingen][2] 
4. <span data-ttu-id="b5018-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="b5018-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Toepassingen][3] 
5. <span data-ttu-id="b5018-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="b5018-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Toepassingen][4] 
6. <span data-ttu-id="b5018-135">Typ in het zoekvak  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="b5018-135">In the search box, type **@Task**.</span></span>
   
    ![Toepassingen][5] 
7. <span data-ttu-id="b5018-137">Selecteer in het deelvenster met resultaten  **@Task** , en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b5018-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![Toepassingen][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5018-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5018-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5018-140">Het doel van deze sectie is beschreven hoe u met het configureren en testen Azure AD eenmalige aanmelding met @Task op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b5018-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5018-141">Voor eenmalige aanmelding werkt, Azure AD moet weten welke gebruiker de bijbehorende equivalent in @Task is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5018-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="b5018-142">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in @Task moet worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="b5018-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="b5018-143">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in @Task.</span><span class="sxs-lookup"><span data-stu-id="b5018-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="b5018-144">Configureren en testen Azure AD eenmalige aanmelding met @Task, u moet voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="b5018-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b5018-145">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b5018-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b5018-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5018-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5018-147">**[Maken van een @Tasktest gebruiker](#creating-a-halogen-software-test-user)**  - hebben een equivalent van Britta Simon in @Taskthat is gekoppeld aan de Azure AD-representatie van haar.</span><span class="sxs-lookup"><span data-stu-id="b5018-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b5018-148">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b5018-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5018-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b5018-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5018-150">Azure AD voor eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="b5018-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="b5018-151">Het doel van deze sectie is Azure AD eenmalige aanmelding in de klassieke Azure portal inschakelen en configureren van eenmalige aanmelding in uw @Task toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5018-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="b5018-152">**Voor het configureren van Azure AD eenmalige aanmelding met @Task, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="b5018-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="b5018-153">In de klassieke Azure-portal op de  **@Task**  toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5018-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 
2. <span data-ttu-id="b5018-155">Op de **hoe wilt u dat gebruikers zich aanmelden bij @Task**  pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5018-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][7] 
3. <span data-ttu-id="b5018-157">Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5018-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![App-instellingen configureren][8] 
   
     <span data-ttu-id="b5018-159">a.</span><span class="sxs-lookup"><span data-stu-id="b5018-159">a.</span></span> <span data-ttu-id="b5018-160">In de **aanmelding op URL** textbox, typ de URL moet worden gebruikt door uw gebruikers aanmelding bij uw @Task toepassing (bijvoorbeeld:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="b5018-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="b5018-161">b.</span><span class="sxs-lookup"><span data-stu-id="b5018-161">b.</span></span> <span data-ttu-id="b5018-162">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5018-162">Click **Next**.</span></span>
4. <span data-ttu-id="b5018-163">Op de **configureren eenmalige aanmelding op @Task**  pagina, klikt u op **metagegevens downloaden**, sla het metagegevensbestand lokaal op uw computer en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5018-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Wat is Azure AD Connect?][9] 
5. <span data-ttu-id="b5018-165">Aanmelding bij uw @Task bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="b5018-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="b5018-166">Ga naar **eenmalige van configuratie**.</span><span class="sxs-lookup"><span data-stu-id="b5018-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="b5018-167">Op de **Single Sign-On** dialoogvenster de volgende stappen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b5018-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Eenmalige aanmelding configureren][23]
   
    <span data-ttu-id="b5018-169">a.</span><span class="sxs-lookup"><span data-stu-id="b5018-169">a.</span></span> <span data-ttu-id="b5018-170">Als **Type**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="b5018-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="b5018-171">b.</span><span class="sxs-lookup"><span data-stu-id="b5018-171">b.</span></span> <span data-ttu-id="b5018-172">Selecteer **Service Provider-ID**.</span><span class="sxs-lookup"><span data-stu-id="b5018-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="b5018-173">c.</span><span class="sxs-lookup"><span data-stu-id="b5018-173">c.</span></span> <span data-ttu-id="b5018-174">Kopieer op de klassieke Azure portal, de **externe aanmeldings-URL**, en plak deze in de **Portal de aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="b5018-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="b5018-175">d.</span><span class="sxs-lookup"><span data-stu-id="b5018-175">d.</span></span> <span data-ttu-id="b5018-176">Kopieer op de klassieke Azure portal, de **Service-URL met eenmalige Sign-Out**, en plak deze in de **Sign-Out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="b5018-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="b5018-177">e.</span><span class="sxs-lookup"><span data-stu-id="b5018-177">e.</span></span> <span data-ttu-id="b5018-178">Kopieer op de klassieke Azure portal, de **URL van wijzigen wachtwoord**, en plak deze in de **URL van wijzigen wachtwoord** textbox.</span><span class="sxs-lookup"><span data-stu-id="b5018-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="b5018-179">f.</span><span class="sxs-lookup"><span data-stu-id="b5018-179">f.</span></span> <span data-ttu-id="b5018-180">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b5018-180">Click **Save**.</span></span>
8. <span data-ttu-id="b5018-181">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5018-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Wat is Azure AD Connect?][10]
9. <span data-ttu-id="b5018-183">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b5018-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Wat is Azure AD Connect?][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5018-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b5018-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5018-186">Het doel van deze sectie is een testgebruiker maken in de klassieke Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b5018-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Azure AD-gebruiker maken][20]

<span data-ttu-id="b5018-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b5018-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b5018-189">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5018-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="b5018-191">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="b5018-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b5018-192">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b5018-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="b5018-194">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b5018-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="b5018-196">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5018-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="b5018-198">a.</span><span class="sxs-lookup"><span data-stu-id="b5018-198">a.</span></span> <span data-ttu-id="b5018-199">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b5018-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="b5018-200">b.</span><span class="sxs-lookup"><span data-stu-id="b5018-200">b.</span></span> <span data-ttu-id="b5018-201">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5018-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="b5018-202">c.</span><span class="sxs-lookup"><span data-stu-id="b5018-202">c.</span></span> <span data-ttu-id="b5018-203">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5018-203">Click **Next**.</span></span>
6. <span data-ttu-id="b5018-204">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5018-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="b5018-206">a.</span><span class="sxs-lookup"><span data-stu-id="b5018-206">a.</span></span> <span data-ttu-id="b5018-207">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b5018-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="b5018-208">b.</span><span class="sxs-lookup"><span data-stu-id="b5018-208">b.</span></span> <span data-ttu-id="b5018-209">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b5018-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="b5018-210">c.</span><span class="sxs-lookup"><span data-stu-id="b5018-210">c.</span></span> <span data-ttu-id="b5018-211">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b5018-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="b5018-212">d.</span><span class="sxs-lookup"><span data-stu-id="b5018-212">d.</span></span> <span data-ttu-id="b5018-213">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="b5018-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="b5018-214">e.</span><span class="sxs-lookup"><span data-stu-id="b5018-214">e.</span></span> <span data-ttu-id="b5018-215">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5018-215">Click **Next**.</span></span>

7. <span data-ttu-id="b5018-216">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="b5018-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="b5018-218">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5018-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="b5018-220">a.</span><span class="sxs-lookup"><span data-stu-id="b5018-220">a.</span></span> <span data-ttu-id="b5018-221">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b5018-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="b5018-222">b.</span><span class="sxs-lookup"><span data-stu-id="b5018-222">b.</span></span> <span data-ttu-id="b5018-223">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b5018-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="b5018-224">Maken van een @Task testgebruiker</span><span class="sxs-lookup"><span data-stu-id="b5018-224">Creating an @Task test user</span></span>
<span data-ttu-id="b5018-225">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in @Task.</span><span class="sxs-lookup"><span data-stu-id="b5018-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="b5018-226">**Maken van een gebruiker Britta Simon aangeroepen in @Task, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="b5018-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="b5018-227">Meld u aan bij uw @Task bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="b5018-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="b5018-228">Klik in het menu bovenaan op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="b5018-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="b5018-229">Klik op **nieuwe persoon**.</span><span class="sxs-lookup"><span data-stu-id="b5018-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="b5018-230">In het dialoogvenster nieuwe persoon, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b5018-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![Maak een @Task testgebruiker][21] 
   
    <span data-ttu-id="b5018-232">a.</span><span class="sxs-lookup"><span data-stu-id="b5018-232">a.</span></span> <span data-ttu-id="b5018-233">In de **voornaam** textbox, typt u 'Britta'.</span><span class="sxs-lookup"><span data-stu-id="b5018-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="b5018-234">b.</span><span class="sxs-lookup"><span data-stu-id="b5018-234">b.</span></span> <span data-ttu-id="b5018-235">In de **achternaam** textbox, typt u 'Simon'.</span><span class="sxs-lookup"><span data-stu-id="b5018-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="b5018-236">c.</span><span class="sxs-lookup"><span data-stu-id="b5018-236">c.</span></span> <span data-ttu-id="b5018-237">In de **e-mailadres** textbox Britta Simon van e-mailadres typt in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5018-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="b5018-238">d.</span><span class="sxs-lookup"><span data-stu-id="b5018-238">d.</span></span> <span data-ttu-id="b5018-239">Klik op **persoon toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b5018-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b5018-240">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5018-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="b5018-241">Het doel van deze sectie is het inschakelen van Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen tot @Task.</span><span class="sxs-lookup"><span data-stu-id="b5018-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b5018-243">**Toewijzen van Britta Simon naar @Task, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="b5018-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="b5018-244">In de klassieke Azure portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b5018-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Gebruiker toewijzen][201] 
2. <span data-ttu-id="b5018-246">Selecteer in de lijst met toepassingen  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="b5018-246">In the applications list, select **@Task**.</span></span>
   
    ![Gebruiker toewijzen][202] 
3. <span data-ttu-id="b5018-248">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b5018-248">In the menu on the top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203] 
4. <span data-ttu-id="b5018-250">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b5018-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="b5018-251">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="b5018-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="b5018-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5018-253">Testing Single Sign-On</span></span>
<span data-ttu-id="b5018-254">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b5018-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="b5018-255">Wanneer u klikt op de @Task tegel in het deelvenster toegang krijgt u automatisch aangemeld bij uw @Task toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5018-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5018-256">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="b5018-256">Additional Resources</span></span>
* [<span data-ttu-id="b5018-257">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5018-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5018-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b5018-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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






