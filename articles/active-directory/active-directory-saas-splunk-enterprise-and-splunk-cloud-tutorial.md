---
title: 'Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Splunk Enterprise en Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="df3ca-103">Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="df3ca-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="df3ca-104">In deze zelfstudie leert u hoe Splunk Enterprise en Splunk Cloud integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df3ca-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df3ca-105">Splunk Enterprise en Splunk Cloud integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="df3ca-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df3ca-106">U kunt beheren in Azure AD die toegang tot Splunk Enterprise en Splunk Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="df3ca-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="df3ca-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Splunk Enterprise en Splunk Cloud eenmalige aanmelding (SSO) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="df3ca-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="df3ca-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="df3ca-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="df3ca-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df3ca-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df3ca-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="df3ca-110">Prerequisites</span></span>

<span data-ttu-id="df3ca-111">Voor het configureren van Azure AD-integratie met Splunk Enterprise en Splunk Cloud, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="df3ca-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="df3ca-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="df3ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df3ca-113">Een Splunk Enterprise of Splunk Cloud SSO ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="df3ca-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="df3ca-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="df3ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="df3ca-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="df3ca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df3ca-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="df3ca-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="df3ca-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df3ca-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="df3ca-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="df3ca-118">Scenario description</span></span>
<span data-ttu-id="df3ca-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="df3ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="df3ca-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="df3ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df3ca-121">Splunk Enterprise en Splunk Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="df3ca-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="df3ca-122">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="df3ca-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="df3ca-123">Splunk Enterprise en Splunk Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="df3ca-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="df3ca-124">Voor het configureren van de integratie van Splunk Enterprise en Splunk Cloud met Azure AD, moet u Splunk Enterprise en Splunk Cloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="df3ca-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df3ca-125">**Als u wilt toevoegen Splunk Enterprise en Splunk Cloud uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df3ca-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df3ca-126">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="df3ca-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="df3ca-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="df3ca-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="df3ca-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Toepassingen][2]

4. <span data-ttu-id="df3ca-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="df3ca-131">Click **Add** at the bottom of the page.</span></span>

    ![Toepassingen][3]

5. <span data-ttu-id="df3ca-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Toepassingen][4]

6. <span data-ttu-id="df3ca-135">Typ in het zoekvak **Splunk Enterprise of Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="df3ca-137">Selecteer in het deelvenster met resultaten **Splunk Enterprise en Splunk Cloud**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="df3ca-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="df3ca-139">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="df3ca-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="df3ca-140">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Splunk voor ondernemingen en Splunk Cloud op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="df3ca-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df3ca-141">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Splunk Enterprise en Splunk Cloud is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df3ca-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="df3ca-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Splunk Enterprise en Splunk Cloud worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="df3ca-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="df3ca-143">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="df3ca-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="df3ca-144">Om te configureren en testen van Azure AD eenmalige aanmelding met Splunk Enterprise en Splunk Cloud, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="df3ca-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df3ca-145">**[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df3ca-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df3ca-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df3ca-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df3ca-147">**[Maken van een testgebruiker Splunk Enterprise en Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  : een equivalent van Britta Simon in de onderneming Splunk en Splunk Cloud die is gekoppeld aan de Azure AD-representatie van haar hebben.</span><span class="sxs-lookup"><span data-stu-id="df3ca-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="df3ca-148">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="df3ca-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df3ca-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="df3ca-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="df3ca-150">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="df3ca-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="df3ca-151">In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in de klassieke portal en eenmalige aanmelding configureren in uw toepassing Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="df3ca-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="df3ca-152">**Voor het configureren van Azure AD eenmalige aanmelding met Splunk Enterprise en Splunk Cloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df3ca-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="df3ca-153">In de klassieke portal op de **Splunk Enterprise en Splunk Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On**dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="df3ca-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Eenmalige aanmelding configureren][6] 

2. <span data-ttu-id="df3ca-155">Op de **hoe wilt u dat gebruikers zich aanmelden op Splunk Enterprise-en Splunk** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="df3ca-157">Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df3ca-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="df3ca-159">In de **aanmelding op URL** textbox, typ de URL moet worden gebruikt door uw gebruikers eenmalige aanmelding voor uw Splunk Enterprise en Splunk Cloud-toepassing met het volgende patroon volgen:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="df3ca-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="df3ca-160">In de **id** textbox, typ de URL van uw Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="df3ca-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="df3ca-161">In de **antwoord-URL** textbox, typ de URL met het volgende patroon volgen:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="df3ca-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="df3ca-162">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="df3ca-163">Op de **op Splunk Enterprise- en Splunk Cloud eenmalige aanmelding configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df3ca-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="df3ca-165">Klik op **metagegevens downloaden**, en sla het bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="df3ca-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="df3ca-166">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-166">Click **Next**.</span></span>

5. <span data-ttu-id="df3ca-167">Om eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met Splunk Enterprise en ondersteuningsteam Splunk Cloud en geef met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="df3ca-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="df3ca-168">De gedownloade **federaton metagegevens**</span><span class="sxs-lookup"><span data-stu-id="df3ca-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="df3ca-169">In de klassieke portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD voor eenmalige aanmelding][10]

7. <span data-ttu-id="df3ca-171">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="df3ca-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="df3ca-173">Create an Azure AD test user</span></span>
<span data-ttu-id="df3ca-174">In deze sectie maakt u een testgebruiker in de klassieke portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="df3ca-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="df3ca-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df3ca-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df3ca-177">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="df3ca-179">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="df3ca-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="df3ca-180">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df3ca-182">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="df3ca-184">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df3ca-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="df3ca-186">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="df3ca-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="df3ca-187">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="df3ca-188">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-188">Click **Next**.</span></span>

6.  <span data-ttu-id="df3ca-189">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df3ca-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="df3ca-191">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="df3ca-192">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="df3ca-193">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="df3ca-194">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="df3ca-195">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-195">Click **Next**.</span></span>

7. <span data-ttu-id="df3ca-196">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="df3ca-198">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df3ca-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="df3ca-200">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="df3ca-201">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="df3ca-202">Een Splunk Enterprise en Splunk Cloud testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="df3ca-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="df3ca-203">In deze sectie maakt u een gebruiker met de naam Britta Simon in de onderneming Splunk en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="df3ca-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="df3ca-204">Neem contact op met de Splunk Enterprise en Splunk Cloud ondersteuningsteam toevoegen van de gebruikers in het Splunk Enterprise en Splunk Cloud-platform.</span><span class="sxs-lookup"><span data-stu-id="df3ca-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="df3ca-205">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="df3ca-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="df3ca-206">In deze sectie schakelt u Britta Simon Azure SSOy haar toegang verlenen Splunk Enterprise-en Splunk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df3ca-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="df3ca-208">**Als u Britta Simon naar de onderneming Splunk en Splunk Cloud toewijzen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df3ca-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="df3ca-209">In de klassieke portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="df3ca-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="df3ca-211">Selecteer in de lijst met toepassingen **Splunk Enterprise en Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="df3ca-213">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-213">In the menu on the top, click **Users**.</span></span>

    ![Gebruiker toewijzen][203]

4. <span data-ttu-id="df3ca-215">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="df3ca-216">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="df3ca-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="df3ca-218">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="df3ca-218">Test single sign-on</span></span>

<span data-ttu-id="df3ca-219">In deze sectie kunt u uw Azure AD-SSOonfiguration met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="df3ca-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="df3ca-220">Wanneer u klikt op de onderneming Splunk en Splunk Cloud-tegel in het toegangsvenster, u moet ophalen automatisch aangemeld bij uw toepassing Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="df3ca-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="df3ca-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="df3ca-221">Additional resources</span></span>

* [<span data-ttu-id="df3ca-222">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df3ca-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df3ca-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df3ca-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
