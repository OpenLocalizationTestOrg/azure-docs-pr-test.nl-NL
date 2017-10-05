---
title: 'Zelfstudie: Azure Active Directory-integratie met Soonr werkplek | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Soonr werkplek.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="f52b3-103">Zelfstudie: Azure Active Directory-integratie met Soonr werkplek</span><span class="sxs-lookup"><span data-stu-id="f52b3-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="f52b3-104">Het doel van deze zelfstudie is het ziet u hoe werkplek Soonr integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f52b3-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="f52b3-105">Soonr werkplek integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f52b3-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f52b3-106">U kunt beheren in Azure AD die toegang tot Soonr werkplek heeft</span><span class="sxs-lookup"><span data-stu-id="f52b3-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="f52b3-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Soonr werkplek (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f52b3-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f52b3-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="f52b3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f52b3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f52b3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f52b3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f52b3-110">Prerequisites</span></span>

<span data-ttu-id="f52b3-111">Voor het configureren van Azure AD-integratie met Soonr werkplek, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f52b3-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="f52b3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f52b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f52b3-113">Een Soonr werkplek eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f52b3-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="f52b3-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f52b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f52b3-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f52b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f52b3-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f52b3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f52b3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f52b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f52b3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f52b3-118">Scenario description</span></span>
<span data-ttu-id="f52b3-119">Het doel van deze zelfstudie is zodat u kunt eenmalige aanmelding Azure AD te testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f52b3-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="f52b3-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f52b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f52b3-121">Soonr werkplek toevoegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="f52b3-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="f52b3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f52b3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="f52b3-123">Soonr werkplek toevoegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="f52b3-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="f52b3-124">Voor het configureren van de integratie van Soonr werkplek in Azure AD, moet u Soonr werkplek uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f52b3-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f52b3-125">**Als u wilt toevoegen Soonr werkplek uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f52b3-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f52b3-126">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f52b3-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="f52b3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f52b3-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f52b3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Toepassingen][2]

4. <span data-ttu-id="f52b3-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="f52b3-131">Click **Add** at the bottom of the page.</span></span>

    ![Toepassingen][3]

5. <span data-ttu-id="f52b3-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Toepassingen][4]

6. <span data-ttu-id="f52b3-135">Typ in het zoekvak **Soonr werkplek**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="f52b3-137">Selecteer in het deelvenster met resultaten **Soonr werkplek**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f52b3-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f52b3-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f52b3-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f52b3-140">Het doel van deze sectie wordt beschreven hoe u met het configureren en testen Azure AD eenmalige aanmelding bij Soonr werkplek op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f52b3-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f52b3-141">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Soonr werkplek aan een gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="f52b3-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="f52b3-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gebruiker op de werkplek Soonr tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f52b3-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="f52b3-143">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Soonr werkplek.</span><span class="sxs-lookup"><span data-stu-id="f52b3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="f52b3-144">Om te configureren en testen van Azure AD eenmalige aanmelding bij Soonr werkplek, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f52b3-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f52b3-145">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f52b3-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f52b3-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f52b3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f52b3-147">**[Maken van een testgebruiker Soonr werkplek](#creating-a-soonr-workplace-test-user)**  - Soonr werkplek die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f52b3-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f52b3-148">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f52b3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f52b3-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f52b3-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f52b3-150">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f52b3-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f52b3-151">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de klassieke portal en eenmalige aanmelding configureren in uw toepassing Soonr werkplek.</span><span class="sxs-lookup"><span data-stu-id="f52b3-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="f52b3-152">**Voor het configureren van Azure AD eenmalige aanmelding bij Soonr werkplek, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f52b3-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="f52b3-153">In de klassieke Azure-portal op de **Soonr werkplek** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f52b3-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Eenmalige aanmelding configureren][6] 

2. <span data-ttu-id="f52b3-155">Op de **hoe wilt u dat gebruikers zich aanmelden op de werkplek Soonr** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="f52b3-157">Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:.</span><span class="sxs-lookup"><span data-stu-id="f52b3-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="f52b3-159">a.</span><span class="sxs-lookup"><span data-stu-id="f52b3-159">a.</span></span> <span data-ttu-id="f52b3-160">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="f52b3-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="f52b3-161">b.</span><span class="sxs-lookup"><span data-stu-id="f52b3-161">b.</span></span> <span data-ttu-id="f52b3-162">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f52b3-163">Houd er rekening mee dat dit geen de feitelijke waarde is.</span><span class="sxs-lookup"><span data-stu-id="f52b3-163">Please note that this is not the real value.</span></span> <span data-ttu-id="f52b3-164">U moet deze waarde met de werkelijke aanmelding op de URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f52b3-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="f52b3-165">Neem contact op met het ondersteuningsteam Soonr werkplek deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="f52b3-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="f52b3-166">Op de **eenmalige aanmelding configureren op de werkplek Soonr** pagina, klikt u op **metagegevens downloaden** en sla het bestand op uw computer:</span><span class="sxs-lookup"><span data-stu-id="f52b3-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="f52b3-168">Neem contact op met het ondersteuningsteam Soonr werkplek om SSO is geconfigureerd voor uw toepassing, en geef met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="f52b3-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="f52b3-169">• De gedownloade **metagegevens** bestand</span><span class="sxs-lookup"><span data-stu-id="f52b3-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="f52b3-170">• De **URL-verlener**</span><span class="sxs-lookup"><span data-stu-id="f52b3-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="f52b3-171">• De **SAML SSO-URL**</span><span class="sxs-lookup"><span data-stu-id="f52b3-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="f52b3-172">• De **eenmalige afmelden Service-URL**</span><span class="sxs-lookup"><span data-stu-id="f52b3-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="f52b3-173">Deze toepassing wordt vervangen door <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask werkplek</a> en u kunt verwijzen <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">dit</a> zelfstudie voor het configureren van de toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f52b3-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="f52b3-174">In de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD voor eenmalige aanmelding][10]

7. <span data-ttu-id="f52b3-176">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD voor eenmalige aanmelding][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f52b3-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f52b3-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="f52b3-179">Het doel van deze sectie is een testgebruiker maken in de klassieke Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f52b3-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Azure AD-gebruiker maken][20]

<span data-ttu-id="f52b3-181">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f52b3-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f52b3-182">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="f52b3-184">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="f52b3-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f52b3-185">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f52b3-187">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f52b3-189">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f52b3-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="f52b3-191">a.</span><span class="sxs-lookup"><span data-stu-id="f52b3-191">a.</span></span> <span data-ttu-id="f52b3-192">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f52b3-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="f52b3-193">b.</span><span class="sxs-lookup"><span data-stu-id="f52b3-193">b.</span></span> <span data-ttu-id="f52b3-194">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f52b3-195">c.</span><span class="sxs-lookup"><span data-stu-id="f52b3-195">c.</span></span> <span data-ttu-id="f52b3-196">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-196">Click **Next**.</span></span>

6.  <span data-ttu-id="f52b3-197">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f52b3-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="f52b3-199">a.</span><span class="sxs-lookup"><span data-stu-id="f52b3-199">a.</span></span> <span data-ttu-id="f52b3-200">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="f52b3-201">b.</span><span class="sxs-lookup"><span data-stu-id="f52b3-201">b.</span></span> <span data-ttu-id="f52b3-202">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="f52b3-203">c.</span><span class="sxs-lookup"><span data-stu-id="f52b3-203">c.</span></span> <span data-ttu-id="f52b3-204">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="f52b3-205">d.</span><span class="sxs-lookup"><span data-stu-id="f52b3-205">d.</span></span> <span data-ttu-id="f52b3-206">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="f52b3-207">e.</span><span class="sxs-lookup"><span data-stu-id="f52b3-207">e.</span></span> <span data-ttu-id="f52b3-208">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-208">Click **Next**.</span></span>

7. <span data-ttu-id="f52b3-209">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f52b3-211">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f52b3-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="f52b3-213">a.</span><span class="sxs-lookup"><span data-stu-id="f52b3-213">a.</span></span> <span data-ttu-id="f52b3-214">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="f52b3-215">b.</span><span class="sxs-lookup"><span data-stu-id="f52b3-215">b.</span></span> <span data-ttu-id="f52b3-216">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="f52b3-217">Maken van een testgebruiker Soonr werkplek</span><span class="sxs-lookup"><span data-stu-id="f52b3-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="f52b3-218">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Soonr werkplek.</span><span class="sxs-lookup"><span data-stu-id="f52b3-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="f52b3-219">Neem contact op met het ondersteuningsteam Soonr werkplek een gebruiker te maken van het platform.</span><span class="sxs-lookup"><span data-stu-id="f52b3-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="f52b3-220">U kunt de ondersteuningsticket met Soonr van verhogen <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">hier</a>.</span><span class="sxs-lookup"><span data-stu-id="f52b3-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f52b3-221">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f52b3-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f52b3-222">Het doel van deze sectie is het Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang te verlenen aan de werkplek Soonr inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f52b3-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f52b3-224">**Als u wilt toewijzen Britta Simon Soonr werkplek, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f52b3-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="f52b3-225">In de klassieke Azure portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f52b3-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f52b3-227">Selecteer in de lijst met toepassingen **Soonr werkplek**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="f52b3-229">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-229">In the menu on the top, click **Users**.</span></span>

    ![Gebruiker toewijzen][203] 

1. <span data-ttu-id="f52b3-231">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="f52b3-232">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="f52b3-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Gebruiker toewijzen][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="f52b3-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f52b3-234">Testing single sign-on</span></span>

<span data-ttu-id="f52b3-235">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f52b3-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f52b3-236">Als u op de tegel Soonr werkplek in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Soonr werkplek.</span><span class="sxs-lookup"><span data-stu-id="f52b3-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f52b3-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f52b3-237">Additional resources</span></span>

* [<span data-ttu-id="f52b3-238">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f52b3-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f52b3-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f52b3-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
