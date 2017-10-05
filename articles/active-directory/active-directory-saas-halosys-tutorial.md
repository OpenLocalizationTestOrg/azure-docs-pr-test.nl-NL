---
title: 'Zelfstudie: Azure Active Directory-integratie met Halosys | Microsoft Docs'
description: Meer informatie over het gebruik van Halosys met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
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
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="52892-103">Zelfstudie: Azure Active Directory-integratie met Halosys</span><span class="sxs-lookup"><span data-stu-id="52892-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="52892-104">In deze zelfstudie leert u hoe Halosys integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52892-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52892-105">Halosys integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="52892-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52892-106">U kunt beheren in Azure AD die toegang tot Halosys heeft</span><span class="sxs-lookup"><span data-stu-id="52892-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="52892-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Halosys (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="52892-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52892-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="52892-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="52892-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52892-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52892-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="52892-110">Prerequisites</span></span>

<span data-ttu-id="52892-111">Voor het configureren van Azure AD-integratie met Halosys, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="52892-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="52892-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="52892-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52892-113">Een Halosys eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="52892-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="52892-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="52892-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="52892-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="52892-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52892-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="52892-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="52892-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52892-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="52892-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="52892-118">Scenario description</span></span>
<span data-ttu-id="52892-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="52892-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="52892-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="52892-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52892-121">Halosys uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="52892-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="52892-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="52892-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="52892-123">Halosys uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="52892-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="52892-124">Voor het configureren van de integratie van Halosys in Azure AD, moet u Halosys uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="52892-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52892-125">**Als u wilt toevoegen Halosys uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="52892-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52892-126">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52892-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="52892-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="52892-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="52892-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="52892-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Toepassingen][2]

4. <span data-ttu-id="52892-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="52892-131">Click **Add** at the bottom of the page.</span></span>

    ![Toepassingen][3]

5. <span data-ttu-id="52892-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="52892-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Toepassingen][4]

6. <span data-ttu-id="52892-135">Typ in het zoekvak **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="52892-135">In the search box, type **Halosys**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="52892-137">Selecteer in het deelvenster met resultaten **Halosys**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="52892-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52892-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="52892-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52892-140">In deze sectie configureert en test eenmalige aanmelding Azure AD met Halosys op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="52892-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52892-141">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Halosys is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52892-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="52892-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Halosys tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="52892-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="52892-143">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Halosys.</span><span class="sxs-lookup"><span data-stu-id="52892-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="52892-144">Om te configureren en testen van Azure AD eenmalige aanmelding met Halosys, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="52892-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52892-145">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="52892-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52892-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52892-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52892-147">**[Maken van een testgebruiker Halosys](#creating-a-halosys-test-user)**  - Halosys die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="52892-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="52892-148">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="52892-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52892-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="52892-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52892-150">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="52892-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52892-151">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de klassieke portal en eenmalige aanmelding configureren in uw toepassing Halosys.</span><span class="sxs-lookup"><span data-stu-id="52892-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="52892-152">**Voor het configureren van Azure AD eenmalige aanmelding met Halosys, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="52892-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="52892-153">In de klassieke portal op de **Halosys** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="52892-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Eenmalige aanmelding configureren][6] 

2. <span data-ttu-id="52892-155">Op de **hoe wilt u dat gebruikers zich aanmelden op Halosys** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="52892-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="52892-157">Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="52892-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="52892-159">a.</span><span class="sxs-lookup"><span data-stu-id="52892-159">a.</span></span> <span data-ttu-id="52892-160">In de **aanmelding op URL** textbox, typ de URL moet worden gebruikt door uw gebruikers eenmalige aanmelding voor uw toepassing Halosys is met het volgende patroon volgen: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="52892-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="52892-161">b.In de **identificatie-URL** textbox, typ de URL in het volgende patroon volgen: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="52892-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="52892-162">Op de **eenmalige aanmelding configureren op Halosys** pagina, klikt u op **metagegevens downloaden**, en sla het bestand op uw computer:</span><span class="sxs-lookup"><span data-stu-id="52892-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="52892-164">Neem contact op met het ondersteuningsteam Halosys om SSO is geconfigureerd voor uw toepassing, en geef met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="52892-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="52892-165">• De gedownloade **metagegevensbestand**</span><span class="sxs-lookup"><span data-stu-id="52892-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="52892-166">• De **SAML SSO-URL**</span><span class="sxs-lookup"><span data-stu-id="52892-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="52892-167">In de klassieke portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="52892-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD voor eenmalige aanmelding][10]

7. <span data-ttu-id="52892-169">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="52892-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD voor eenmalige aanmelding][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52892-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="52892-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="52892-172">In deze sectie maakt u een testgebruiker in de klassieke portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="52892-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Azure AD-gebruiker maken][20]

<span data-ttu-id="52892-174">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="52892-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52892-175">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52892-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="52892-177">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="52892-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="52892-178">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="52892-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52892-180">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="52892-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="52892-182">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="52892-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="52892-183">a.</span><span class="sxs-lookup"><span data-stu-id="52892-183">a.</span></span> <span data-ttu-id="52892-184">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="52892-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="52892-185">b.</span><span class="sxs-lookup"><span data-stu-id="52892-185">b.</span></span> <span data-ttu-id="52892-186">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52892-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52892-187">c.</span><span class="sxs-lookup"><span data-stu-id="52892-187">c.</span></span> <span data-ttu-id="52892-188">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="52892-188">Click **Next**.</span></span>

6.  <span data-ttu-id="52892-189">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="52892-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="52892-190">a.</span><span class="sxs-lookup"><span data-stu-id="52892-190">a.</span></span> <span data-ttu-id="52892-191">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="52892-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="52892-192">b.</span><span class="sxs-lookup"><span data-stu-id="52892-192">b.</span></span> <span data-ttu-id="52892-193">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="52892-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="52892-194">c.</span><span class="sxs-lookup"><span data-stu-id="52892-194">c.</span></span> <span data-ttu-id="52892-195">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="52892-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="52892-196">d.</span><span class="sxs-lookup"><span data-stu-id="52892-196">d.</span></span> <span data-ttu-id="52892-197">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="52892-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="52892-198">e.</span><span class="sxs-lookup"><span data-stu-id="52892-198">e.</span></span> <span data-ttu-id="52892-199">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="52892-199">Click **Next**.</span></span>

7. <span data-ttu-id="52892-200">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="52892-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="52892-202">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="52892-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="52892-204">a.</span><span class="sxs-lookup"><span data-stu-id="52892-204">a.</span></span> <span data-ttu-id="52892-205">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="52892-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="52892-206">b.</span><span class="sxs-lookup"><span data-stu-id="52892-206">b.</span></span> <span data-ttu-id="52892-207">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="52892-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="52892-208">Een testgebruiker Halosys maken</span><span class="sxs-lookup"><span data-stu-id="52892-208">Creating a Halosys test user</span></span>

<span data-ttu-id="52892-209">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Halosys maken.</span><span class="sxs-lookup"><span data-stu-id="52892-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="52892-210">Neem contact op met het ondersteuningsteam Halosys de gebruikers van het platform Halosys toevoegen.</span><span class="sxs-lookup"><span data-stu-id="52892-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52892-211">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="52892-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52892-212">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Halosys.</span><span class="sxs-lookup"><span data-stu-id="52892-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="52892-214">**Britta Simon om aan te wijzen Halosys, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="52892-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="52892-215">In de klassieke portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="52892-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="52892-217">Selecteer in de lijst met toepassingen **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="52892-217">In the applications list, select **Halosys**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="52892-219">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="52892-219">In the menu on the top, click **Users**.</span></span>

    ![Gebruiker toewijzen][203]

4. <span data-ttu-id="52892-221">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="52892-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="52892-222">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="52892-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Gebruiker toewijzen][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="52892-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="52892-224">Testing single sign-on</span></span>

<span data-ttu-id="52892-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="52892-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52892-226">Als u op de tegel Halosys in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Halosys.</span><span class="sxs-lookup"><span data-stu-id="52892-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="52892-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="52892-227">Additional resources</span></span>

* [<span data-ttu-id="52892-228">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52892-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52892-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52892-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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
