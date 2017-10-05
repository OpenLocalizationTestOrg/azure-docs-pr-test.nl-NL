---
title: 'Zelfstudie: Azure Active Directory-integratie met Bynder | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Bynder.
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
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="22e7e-103">Zelfstudie: Azure Active Directory-integratie met Bynder</span><span class="sxs-lookup"><span data-stu-id="22e7e-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="22e7e-104">Er is het doel van deze zelfstudie leert u Bynder integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22e7e-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22e7e-105">Bynder integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="22e7e-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="22e7e-106">U kunt beheren in Azure AD die toegang tot Bynder heeft</span><span class="sxs-lookup"><span data-stu-id="22e7e-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="22e7e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Bynder eenmalige aanmelding (SSO) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="22e7e-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="22e7e-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="22e7e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="22e7e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22e7e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22e7e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="22e7e-110">Prerequisites</span></span>
<span data-ttu-id="22e7e-111">Voor het configureren van Azure AD-integratie met Bynder, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="22e7e-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="22e7e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="22e7e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="22e7e-113">Een Bynder eenmalige aanmelding (SSO) abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="22e7e-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="22e7e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="22e7e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="22e7e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="22e7e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="22e7e-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="22e7e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="22e7e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22e7e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22e7e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="22e7e-118">Scenario description</span></span>
<span data-ttu-id="22e7e-119">Het doel van deze zelfstudie is zodat u kunt Microsoft Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="22e7e-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="22e7e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="22e7e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22e7e-121">Bynder uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="22e7e-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="22e7e-122">Configureren en testen van Microsoft Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="22e7e-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="22e7e-123">Bynder uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="22e7e-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="22e7e-124">Voor het configureren van de integratie van Bynder in Azure AD, moet u Bynder uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="22e7e-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="22e7e-125">**Als u wilt toevoegen Bynder uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22e7e-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="22e7e-126">In de **klassieke Azure-Portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="22e7e-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="22e7e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="22e7e-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="22e7e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Toepassingen][2]
4. <span data-ttu-id="22e7e-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="22e7e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Toepassingen][3]
5. <span data-ttu-id="22e7e-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Toepassingen][4]
6. <span data-ttu-id="22e7e-135">Typ in het zoekvak **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-135">In the search box, type **Bynder**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="22e7e-137">Selecteer in het deelvenster resultaten **Bynder**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="22e7e-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![De app selecteren in de galerie](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="22e7e-139">Configureren en testen van Microsoft Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="22e7e-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="22e7e-140">Het doel van deze sectie is het beschreven hoe u met het configureren en testen van Microsoft Azure AD-SSO met Bynder op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="22e7e-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="22e7e-141">Azure AD moet weten wat de gebruiker van het bijbehorende equivalent in Bynder aan een gebruiker in Azure AD is voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="22e7e-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="22e7e-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Bynder tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="22e7e-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="22e7e-143">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Bynder.</span><span class="sxs-lookup"><span data-stu-id="22e7e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="22e7e-144">Als u wilt configureren en testen van Microsoft Azure AD-SSO met Bynder, moet u de volgende elementen voltooid:</span><span class="sxs-lookup"><span data-stu-id="22e7e-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="22e7e-145">**[Configureren van eenmalige aanmelding Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22e7e-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="22e7e-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Microsoft Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22e7e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="22e7e-147">**[Maken van een testgebruiker Bynder](#creating-a-bynder-test-user)**  - Bynder die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="22e7e-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="22e7e-148">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Microsoft Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="22e7e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="22e7e-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="22e7e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="22e7e-150">Configuratie van Microsoft Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="22e7e-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="22e7e-151">In deze sectie maakt u Microsoft Azure AD eenmalige aanmelding inschakelen in de klassieke portal en eenmalige aanmelding configureren in uw toepassing Bynder.</span><span class="sxs-lookup"><span data-stu-id="22e7e-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="22e7e-152">**Als u wilt Microsoft Azure AD-SSO met Bynder configureert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22e7e-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="22e7e-153">In de klassieke portal op de **Bynder** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="22e7e-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 
2. <span data-ttu-id="22e7e-155">Op de **hoe wilt u dat gebruikers zich aanmelden op Bynder** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="22e7e-157">Op de **App-instellingen configureren** dialoogvenster pagina als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, voer de volgende stappen uit en klik op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="22e7e-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="22e7e-159">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="22e7e-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="22e7e-160">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-160">Click **Next**.</span></span>
4. <span data-ttu-id="22e7e-161">Als u wilt configureren van de toepassing in **SP geïnitieerd modus** op de **App-instellingen configureren** dialoogvenster pagina, klikt u op de **"Weergeven geavanceerde instellingen (optioneel)"** en voer vervolgens de **aanmelding op URL** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="22e7e-163">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="22e7e-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="22e7e-164">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="22e7e-165">De waarde voor de aanmelding op de URL in deze zelfstudie is slechts een placeholfer.</span><span class="sxs-lookup"><span data-stu-id="22e7e-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="22e7e-166">Als u de werkelijke vlaue voor uw omgeving, contact op met Bynder.</span><span class="sxs-lookup"><span data-stu-id="22e7e-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="22e7e-167">Op de **eenmalige aanmelding configureren op Bynder** pagina, voer de volgende stappen uit en klik op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="22e7e-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="22e7e-169">Klik op **metagegevens downloaden**, en sla het bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="22e7e-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="22e7e-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-170">Click **Next**.</span></span>
6. <span data-ttu-id="22e7e-171">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, contact op met het ondersteuningsteam Bynder.</span><span class="sxs-lookup"><span data-stu-id="22e7e-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="22e7e-172">Het metagegevensbestand van de gedownloade koppelen en delen met Bynder team voor het instellen van eenmalige aanmelding op hun kant.</span><span class="sxs-lookup"><span data-stu-id="22e7e-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="22e7e-173">In de klassieke portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][10]
8. <span data-ttu-id="22e7e-175">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="22e7e-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="22e7e-177">Create an Azure AD test user</span></span>
<span data-ttu-id="22e7e-178">Het doel van deze sectie is het een testgebruiker maken in de klassieke portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="22e7e-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="22e7e-180">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22e7e-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="22e7e-181">In de **klassieke Azure-Portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="22e7e-183">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="22e7e-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="22e7e-184">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="22e7e-186">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="22e7e-188">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="22e7e-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="22e7e-190">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="22e7e-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="22e7e-191">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="22e7e-192">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-192">Click **Next**.</span></span>
6. <span data-ttu-id="22e7e-193">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="22e7e-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="22e7e-195">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="22e7e-196">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="22e7e-197">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="22e7e-198">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="22e7e-199">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-199">Click **Next**.</span></span>
7. <span data-ttu-id="22e7e-200">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="22e7e-202">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="22e7e-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="22e7e-204">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="22e7e-205">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="22e7e-206">Een testgebruiker Bynder maken</span><span class="sxs-lookup"><span data-stu-id="22e7e-206">Create a Bynder test user</span></span>
<span data-ttu-id="22e7e-207">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Bynder genoemd.</span><span class="sxs-lookup"><span data-stu-id="22e7e-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="22e7e-208">Bynder ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="22e7e-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="22e7e-209">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="22e7e-209">There is no action item for you in this section.</span></span> <span data-ttu-id="22e7e-210">Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot Bynder als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="22e7e-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="22e7e-211">Als u een gebruiker handmatig maken wilt, moet u contact op met het ondersteuningsteam Bynder.</span><span class="sxs-lookup"><span data-stu-id="22e7e-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="22e7e-212">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="22e7e-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="22e7e-213">Het doel van deze sectie is het Britta Simon Bynder haar toegang verlenen voor het gebruik van Azure eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="22e7e-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Gebruiker toewijzen][200]

<span data-ttu-id="22e7e-215">**Britta Simon om aan te wijzen Bynder, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22e7e-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="22e7e-216">In de klassieke portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="22e7e-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Gebruiker toewijzen][201]
2. <span data-ttu-id="22e7e-218">Selecteer in de lijst met toepassingen **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-218">In the applications list, select **Bynder**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="22e7e-220">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-220">In the menu on the top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203]
4. <span data-ttu-id="22e7e-222">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="22e7e-223">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="22e7e-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="22e7e-225">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="22e7e-225">Test single sign-on</span></span>
<span data-ttu-id="22e7e-226">Het doel van deze sectie is het testen van uw Microsoft Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="22e7e-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="22e7e-227">Als u op de tegel Bynder in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Bynder.</span><span class="sxs-lookup"><span data-stu-id="22e7e-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="22e7e-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="22e7e-228">Additional resources</span></span>
* [<span data-ttu-id="22e7e-229">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22e7e-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22e7e-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="22e7e-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
