---
title: 'Zelfstudie: Azure Active Directory-integratie met Wizergos productiviteitssoftware | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Wizergos productiviteitssoftware.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="35215-103">Zelfstudie: Azure Active Directory-integratie met Wizergos productiviteitssoftware</span><span class="sxs-lookup"><span data-stu-id="35215-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="35215-104">Er is het doel van deze zelfstudie leert u Wizergos productiviteitssoftware integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35215-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35215-105">Wizergos productiviteitssoftware integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="35215-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="35215-106">U kunt beheren in Azure AD die toegang tot Software voor Wizergos productiviteit heeft</span><span class="sxs-lookup"><span data-stu-id="35215-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="35215-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Wizergos productiviteitssoftware eenmalige aanmelding (SSO) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="35215-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="35215-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="35215-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="35215-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35215-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35215-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="35215-110">Prerequisites</span></span>
<span data-ttu-id="35215-111">Voor het configureren van Azure AD-integratie met Wizergos productiviteitssoftware, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="35215-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="35215-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="35215-112">An Azure AD subscription</span></span>
* <span data-ttu-id="35215-113">Een abonnement Wizergos productiviteit Software SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="35215-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="35215-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="35215-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="35215-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="35215-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="35215-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="35215-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="35215-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35215-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35215-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="35215-118">Scenario description</span></span>
<span data-ttu-id="35215-119">Het doel van deze zelfstudie is zodat u Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="35215-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="35215-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="35215-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35215-121">Wizergos productiviteitssoftware uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="35215-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="35215-122">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="35215-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="35215-123">Wizergos productiviteitssoftware uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="35215-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="35215-124">Voor het configureren van de integratie van Software voor Wizergos productiviteit in Azure AD, moet u Wizergos productiviteitssoftware uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="35215-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="35215-125">**Als u wilt toevoegen Wizergos productiviteitssoftware uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="35215-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="35215-126">In de **klassieke Azure-Portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35215-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="35215-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="35215-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="35215-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="35215-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Toepassingen][2]
4. <span data-ttu-id="35215-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="35215-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Toepassingen][3]
5. <span data-ttu-id="35215-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="35215-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Toepassingen][4]
6. <span data-ttu-id="35215-135">Typ in het zoekvak **Wizergos productiviteitssoftware**.</span><span class="sxs-lookup"><span data-stu-id="35215-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="35215-137">Selecteer in het deelvenster resultaten **Wizergos productiviteitssoftware**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="35215-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![De app selecteren in de galerie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="35215-139">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="35215-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="35215-140">Het doel van deze sectie is het beschreven hoe u met het configureren en testen van Azure AD-SSO met Wizergos productiviteitssoftware op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="35215-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35215-141">Azure AD moet weten wat de gebruiker equivalent in Wizergos productiviteitssoftware aan een gebruiker in Azure AD is voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="35215-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="35215-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Wizergos productiviteitssoftware worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="35215-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="35215-143">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Wizergos productiviteitssoftware.</span><span class="sxs-lookup"><span data-stu-id="35215-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="35215-144">Om te configureren en testen van Azure AD eenmalige aanmelding met BynWizergos productiviteit Softwareder, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="35215-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="35215-145">**[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="35215-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="35215-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35215-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35215-147">**[Maken van een testgebruiker Wizergos productiviteitssoftware](#creating-a-wizergos-productivity-software-test-user)**  - Wizergos productiviteitssoftware die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="35215-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="35215-148">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="35215-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35215-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="35215-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="35215-150">Configuratie van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="35215-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="35215-151">In deze sectie Azure AD eenmalige aanmelding in de klassieke portal inschakelen en configureren van eenmalige aanmelding in uw toepassing Wizergos productiviteit.</span><span class="sxs-lookup"><span data-stu-id="35215-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="35215-152">**Voor het configureren van Azure AD eenmalige aanmelding met Wizergos productiviteitssoftware, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="35215-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="35215-153">In de klassieke portal op de **Wizergos productiviteitssoftware** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="35215-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 
2. <span data-ttu-id="35215-155">Op de **hoe wilt u dat gebruikers zich aanmelden op voor de Software voor Wizergos productiviteit** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="35215-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="35215-157">Op de **App-instellingen configureren** dialoogvenster pagina, klikt u op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="35215-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="35215-159">Op de **eenmalige aanmelding op Wizergos productiviteitssoftware configureren** pagina, klikt u op **certificaat downloaden**, en sla het bestand op uw computer:</span><span class="sxs-lookup"><span data-stu-id="35215-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="35215-161">In een ander browservenster aanmelding bij uw tenant Wizergos productiviteitssoftware als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="35215-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="35215-162">Selecteer in het menu hamburger **Admin**.</span><span class="sxs-lookup"><span data-stu-id="35215-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="35215-164">Selecteer in de beheerpagina linkerkant menu **verificatie** en klik op **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="35215-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="35215-166">Voer de volgende stappen uit op **verificatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="35215-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="35215-168">Klik op **uploaden** knop om de gedownloade certificaat van Azure AD te uploaden.</span><span class="sxs-lookup"><span data-stu-id="35215-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="35215-169">In de **URL-verlener** textbox plaatsen de waarde van **URL-verlener** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="35215-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="35215-170">In de **-URL met eenmalige aanmelding** textbox plaatsen de waarde van **één Service-URL aanmelding** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="35215-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="35215-171">In de **-URL met eenmalige Sign-Out** textbox plaatsen de waarde van **Service-URL met eenmalige Sign-out** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="35215-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="35215-172">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="35215-172">Click **Save** button.</span></span>
9. <span data-ttu-id="35215-173">In de klassieke portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="35215-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][10]
10. <span data-ttu-id="35215-175">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="35215-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="35215-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="35215-177">Create an Azure AD test user</span></span>
<span data-ttu-id="35215-178">Het doel van deze sectie is het een testgebruiker maken in de klassieke portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="35215-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="35215-180">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="35215-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="35215-181">In de **klassieke Azure-Portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35215-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="35215-183">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="35215-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="35215-184">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="35215-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="35215-186">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="35215-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="35215-188">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="35215-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="35215-190">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="35215-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="35215-191">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35215-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="35215-192">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="35215-192">Click **Next**.</span></span>
6. <span data-ttu-id="35215-193">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="35215-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="35215-195">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="35215-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="35215-196">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="35215-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="35215-197">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="35215-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="35215-198">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="35215-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="35215-199">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="35215-199">Click **Next**.</span></span>
7. <span data-ttu-id="35215-200">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="35215-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="35215-202">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="35215-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="35215-204">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="35215-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="35215-205">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="35215-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="35215-206">Een testgebruiker Wizergos productiviteitssoftware maken</span><span class="sxs-lookup"><span data-stu-id="35215-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="35215-207">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Wizergos productiviteitssoftware maken.</span><span class="sxs-lookup"><span data-stu-id="35215-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="35215-208">Neem contact op met het ondersteuningsteam Wizergos productiviteitssoftware via [ support@wizergos.com ](emailTo:support@wizergos.com) de gebruikers van het platform Wizergos productiviteitssoftware toevoegen.</span><span class="sxs-lookup"><span data-stu-id="35215-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="35215-209">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="35215-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="35215-210">Het doel van deze sectie is het Britta Simon haar toegang verlenen aan Wizergos productiviteitssoftware gebruikt Azure eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="35215-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Gebruiker toewijzen][200]

<span data-ttu-id="35215-212">**Britta Simon om aan te wijzen Wizergos productiviteitssoftware, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="35215-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="35215-213">In de klassieke portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="35215-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Gebruiker toewijzen][201]
2. <span data-ttu-id="35215-215">Selecteer in de lijst met toepassingen **Wizergos productiviteitssoftware**.</span><span class="sxs-lookup"><span data-stu-id="35215-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="35215-217">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="35215-217">In the menu on the top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203]
4. <span data-ttu-id="35215-219">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="35215-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="35215-220">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="35215-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="35215-222">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="35215-222">Test single sign-on</span></span>
<span data-ttu-id="35215-223">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="35215-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="35215-224">Als u op de tegel Wizergos productiviteitssoftware in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Wizergos productiviteitssoftware.</span><span class="sxs-lookup"><span data-stu-id="35215-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35215-225">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="35215-225">Additional resources</span></span>
* [<span data-ttu-id="35215-226">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35215-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35215-227">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35215-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
