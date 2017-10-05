---
title: 'Zelfstudie: Azure Active Directory-integratie met SciQuest besteden directeur | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SciQuest besteden directeur.
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
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="2bb9c-103">Zelfstudie: Azure Active Directory-integratie met SciQuest besteden directeur</span><span class="sxs-lookup"><span data-stu-id="2bb9c-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="2bb9c-104">Er is het doel van deze zelfstudie leert u SciQuest besteden directeur integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bb9c-104">The objective of this tutorial is to show you how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="2bb9c-105">SciQuest besteden directeur integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="2bb9c-106">U kunt beheren in Azure AD die toegang tot SciQuest besteden directeur heeft</span><span class="sxs-lookup"><span data-stu-id="2bb9c-106">You can control in Azure AD who has access to SciQuest Spend Director</span></span> 
* <span data-ttu-id="2bb9c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SciQuest besteden directeur (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="2bb9c-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="2bb9c-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="2bb9c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="2bb9c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bb9c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bb9c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2bb9c-110">Prerequisites</span></span>
<span data-ttu-id="2bb9c-111">Voor het configureren van Azure AD-integratie met SciQuest besteden directeur, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

* <span data-ttu-id="2bb9c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2bb9c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="2bb9c-113">Een SciQuest besteden directeur eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2bb9c-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2bb9c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="2bb9c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="2bb9c-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="2bb9c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bb9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="2bb9c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2bb9c-118">Scenario Description</span></span>
<span data-ttu-id="2bb9c-119">Het doel van deze zelfstudie is zodat u kunt eenmalige aanmelding Azure AD te testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="2bb9c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bb9c-121">SciQuest besteden directeur uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2bb9c-121">Adding SciQuest Spend Director from the gallery</span></span> 
2. <span data-ttu-id="2bb9c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bb9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="2bb9c-123">SciQuest besteden directeur uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2bb9c-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="2bb9c-124">Voor het configureren van de integratie van SciQuest besteden directeur in Azure AD, moet u SciQuest besteden directeur uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2bb9c-125">**Als u wilt toevoegen SciQuest besteden directeur uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bb9c-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2bb9c-126">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="2bb9c-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="2bb9c-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Toepassingen][2]

4. <span data-ttu-id="2bb9c-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Toepassingen][3]

5. <span data-ttu-id="2bb9c-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Toepassingen][4]

6. <span data-ttu-id="2bb9c-135">Typ in het zoekvak **sciQuest besteden directeur**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-135">In the search box, type **sciQuest spend director**.</span></span>
   
    ![Toepassingen][5]

7. <span data-ttu-id="2bb9c-137">Selecteer in het deelvenster met resultaten **SciQuest besteden directeur**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-137">In the results pane, select **SciQuest Spend Director**, and then click **Complete** to add the application.</span></span>
   
    ![Toepassingen][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2bb9c-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bb9c-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2bb9c-140">Het doel van deze sectie is het beschreven hoe u met het configureren en testen eenmalige aanmelding Azure AD met SciQuest besteden directeur op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2bb9c-141">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in SciQuest besteden directeur aan een gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director to an user in Azure AD is.</span></span> <span data-ttu-id="2bb9c-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SciQuest besteden directeur tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-142">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>  
<span data-ttu-id="2bb9c-143">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="2bb9c-144">Om te configureren en testen van Azure AD eenmalige aanmelding met SciQuest besteden directeur, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-144">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2bb9c-145">**[Configureren van Azure AD één Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2bb9c-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bb9c-147">**[Maken van een testgebruiker SciQuest besteden directeur](#creating-a-halogen-software-test-user)**  - SciQuest besteden directeur die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2bb9c-148">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bb9c-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="2bb9c-150">Azure AD één eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="2bb9c-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="2bb9c-151">Het doel van deze sectie is Azure AD eenmalige aanmelding inschakelen in de klassieke Azure portal en eenmalige aanmelding in uw toepassing SciQuest besteden directeur configureren.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="2bb9c-152">**Voor het configureren van Azure AD eenmalige aanmelding met SciQuest besteden directeur, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bb9c-152">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="2bb9c-153">In de klassieke Azure-portal op de **SciQuest besteden directeur** pagina van de integratie van toepassing, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-153">In the Azure classic portal, on the **SciQuest Spend Director** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][8]

2. <span data-ttu-id="2bb9c-155">Op de **hoe wilt u dat gebruikers zich aanmelden op SciQuest besteden directeur** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-155">On the **How would you like users to sign on to SciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][9]

3. <span data-ttu-id="2bb9c-157">Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![App-instellingen configureren][10]
   
     <span data-ttu-id="2bb9c-159">a.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-159">a.</span></span> <span data-ttu-id="2bb9c-160">In de **aanmelding op URL** textbox, typ de URL van uw gebruikt door uw gebruikers aanmelden bij uw SciQuest te besteden aan de directeur-toepassing met het volgende patroon volgen: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="2bb9c-160">In the **Sign On URL** textbox, type your URL used by your users to sign on to your SciQuest Spend Director application using the following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="2bb9c-161">b.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-161">b.</span></span> <span data-ttu-id="2bb9c-162">In de **antwoord-URL** textbox dezelfde waarde die u hebt opgegeven in de **aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-162">In the **Reply URL** textbox, type the same value you have typed into the **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="2bb9c-163">c.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-163">c.</span></span> <span data-ttu-id="2bb9c-164">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-164">Click **Next**.</span></span>

4. <span data-ttu-id="2bb9c-165">Op de **eenmalige aanmelding configureren op SciQuest besteden directeur** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-165">On the **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![Wat is Azure AD Connect?][11]

5. <span data-ttu-id="2bb9c-167">Neem contact op met SciQuest ondersteuning voor deze methode voor verificatie met behulp van de metagegevens van de bovenstaande gedownloade inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-167">Contact SciQuest support to enable this authentication method using the above downloaded metadata.</span></span>

6. <span data-ttu-id="2bb9c-168">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![Wat is Azure AD Connect?][15]

7. <span data-ttu-id="2bb9c-170">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2bb9c-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2bb9c-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="2bb9c-172">Het doel van deze sectie is een testgebruiker maken in de klassieke Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="2bb9c-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bb9c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2bb9c-174">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Wat is Azure AD Connect?][100] 

2. <span data-ttu-id="2bb9c-176">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="2bb9c-177">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Wat is Azure AD Connect?][101] 

4. <span data-ttu-id="2bb9c-179">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Wat is Azure AD Connect?][102] 

5. <span data-ttu-id="2bb9c-181">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Wat is Azure AD Connect?][103] 
   
    <span data-ttu-id="2bb9c-183">a.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-183">a.</span></span> <span data-ttu-id="2bb9c-184">Als **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="2bb9c-185">b.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-185">b.</span></span> <span data-ttu-id="2bb9c-186">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="2bb9c-187">c.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-187">c.</span></span> <span data-ttu-id="2bb9c-188">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-188">Click **Next**.</span></span>

6. <span data-ttu-id="2bb9c-189">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-189">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Wat is Azure AD Connect?][104] 
   
    <span data-ttu-id="2bb9c-191">a.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-191">a.</span></span> <span data-ttu-id="2bb9c-192">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-192">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="2bb9c-193">b.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-193">b.</span></span> <span data-ttu-id="2bb9c-194">In de **achternaam** txtbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-194">In the **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="2bb9c-195">c.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-195">c.</span></span> <span data-ttu-id="2bb9c-196">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="2bb9c-197">d.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-197">d.</span></span> <span data-ttu-id="2bb9c-198">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-198">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="2bb9c-199">e.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-199">e.</span></span> <span data-ttu-id="2bb9c-200">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-200">Click **Next**.</span></span>

7. <span data-ttu-id="2bb9c-201">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Wat is Azure AD Connect?][105]  

8. <span data-ttu-id="2bb9c-203">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2bb9c-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Wat is Azure AD Connect?][106]   
   
    <span data-ttu-id="2bb9c-205">a.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-205">a.</span></span> <span data-ttu-id="2bb9c-206">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-206">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="2bb9c-207">b.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-207">b.</span></span> <span data-ttu-id="2bb9c-208">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="2bb9c-209">Een testgebruiker SciQuest besteden directeur maken</span><span class="sxs-lookup"><span data-stu-id="2bb9c-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="2bb9c-210">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-210">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="2bb9c-211">Moet u contact op met het ondersteuningsteam SciQuest besteden directeur en geeft u de details over uw testaccount downloaden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-211">You need to contact your SciQuest Spend Director support team and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="2bb9c-212">U kunt ook kunt u gebruikmaken van just-in-time-inrichting, een eenmalige aanmelding functie die wordt ondersteund door SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="2bb9c-213">Als just-in-time-inrichting is ingeschakeld, worden gebruikers automatisch gemaakt door SciQuest besteden directeur tijdens een poging voor aanmelding als ze nog niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="2bb9c-214">Deze functie hoeven gebruikers eenmalige aanmelding equivalent handmatig maken.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-214">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="2bb9c-215">Als u just-in-time-inrichting is ingeschakeld, moet u contact opnemen met je het ondersteuningsteam SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-215">To get just-in-time provisioning enabled, you need to contact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2bb9c-216">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bb9c-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="2bb9c-217">Het doel van deze sectie is het Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang te verlenen aan SciQuest besteden directeur inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SciQuest Spend Director.</span></span>

![Wat is Azure AD Connect?][200]

<span data-ttu-id="2bb9c-219">**Als u wilt toewijzen Britta Simon SciQuest besteden directeur, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bb9c-219">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="2bb9c-220">In de klassieke Azure portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Wat is Azure AD Connect?][201]

2. <span data-ttu-id="2bb9c-222">Selecteer in de lijst met toepassingen **SciQuest besteden directeur**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-222">In the applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Wat is Azure AD Connect?][202]

3. <span data-ttu-id="2bb9c-224">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-224">In the menu on the top, click **Users**.</span></span>
   
    ![Wat is Azure AD Connect?][203]

4. <span data-ttu-id="2bb9c-226">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-226">In the Users list, select **Britta Simon**.</span></span>
   
    ![Wat is Azure AD Connect?][204]

5. <span data-ttu-id="2bb9c-228">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-228">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Wat is Azure AD Connect?][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="2bb9c-230">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bb9c-230">Testing Single Sign-On</span></span>
<span data-ttu-id="2bb9c-231">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="2bb9c-232">Als u op de tegel SciQuest besteden directeur in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing SciQuest besteden directeur.</span><span class="sxs-lookup"><span data-stu-id="2bb9c-232">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bb9c-233">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="2bb9c-233">Additional Resources</span></span>
* [<span data-ttu-id="2bb9c-234">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bb9c-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bb9c-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bb9c-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

