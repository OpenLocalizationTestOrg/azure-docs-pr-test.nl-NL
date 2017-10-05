---
title: 'Zelfstudie: Azure Active Directory-integratie met SilkRoad levensduur Suite | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SilkRoad levensduur Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="9815b-103">Zelfstudie: Azure Active Directory-integratie met SilkRoad levensduur Suite</span><span class="sxs-lookup"><span data-stu-id="9815b-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="9815b-104">Er is het doel van deze zelfstudie leert u SilkRoad levensduur Suite integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9815b-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="9815b-105">SilkRoad levensduur Suite integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9815b-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="9815b-106">U kunt beheren in Azure AD die toegang tot SilkRoad levensduur Suite heeft</span><span class="sxs-lookup"><span data-stu-id="9815b-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="9815b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SilkRoad levensduur Suite eenmalige aanmelding (SSO) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9815b-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="9815b-108">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9815b-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9815b-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9815b-109">Prerequisites</span></span>
<span data-ttu-id="9815b-110">Voor het configureren van Azure AD-integratie met SilkRoad levensduur Suite, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9815b-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="9815b-111">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9815b-111">An Azure AD subscription</span></span>
* <span data-ttu-id="9815b-112">Een abonnement SilkRoad levensduur Suite SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9815b-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="9815b-113">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9815b-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="9815b-114">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9815b-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="9815b-115">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9815b-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="9815b-116">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9815b-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="9815b-117">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9815b-117">Scenario Description</span></span>
<span data-ttu-id="9815b-118">Het doel van deze zelfstudie is zodat u Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9815b-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="9815b-119">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9815b-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9815b-120">SilkRoad levensduur Suite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9815b-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="9815b-121">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="9815b-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="9815b-122">SilkRoad levensduur Suite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9815b-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="9815b-123">Voor het configureren van de integratie van SilkRoad levensduur Suite in Azure AD, moet u SilkRoad levensduur Suite uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9815b-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9815b-124">**Als u wilt toevoegen SilkRoad levensduur Suite uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9815b-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9815b-125">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9815b-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="9815b-127">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="9815b-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="9815b-128">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="9815b-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Toepassingen][2]

4. <span data-ttu-id="9815b-130">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="9815b-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Toepassingen][3]

5. <span data-ttu-id="9815b-132">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="9815b-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Toepassingen][4]

6. <span data-ttu-id="9815b-134">Typ in het zoekvak **SilkRoad levensduur Suite**.</span><span class="sxs-lookup"><span data-stu-id="9815b-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Toepassingen][5]

7. <span data-ttu-id="9815b-136">Selecteer in het deelvenster met resultaten **SilkRoad levensduur Suite**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9815b-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Toepassingen][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9815b-138">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="9815b-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9815b-139">Het doel van deze sectie is het beschreven hoe u met het configureren en testen van Azure AD-SSO met SilkRoad levensduur Suite op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9815b-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9815b-140">Azure AD moet weten wat de gebruiker equivalent in SilkRoad leven Suite aan een gebruiker in Azure AD is voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="9815b-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="9815b-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SilkRoad leven Suite tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9815b-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="9815b-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in SilkRoad leven Suite.</span><span class="sxs-lookup"><span data-stu-id="9815b-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="9815b-143">Om te configureren en testen van Azure AD eenmalige aanmelding met SilkRoad levensduur Suite, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9815b-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9815b-144">**[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9815b-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9815b-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9815b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9815b-146">**[Maken van een testgebruiker SilkRoad levensduur Suite](#creating-a-silkroad-life-suite-test-user)**  - SilkRoad levensduur Suite die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9815b-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9815b-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9815b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9815b-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9815b-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9815b-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9815b-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="9815b-150">Het doel van deze sectie is Azure AD-eenmalige aanmelding inschakelen in de klassieke Azure portal en eenmalige aanmelding configureren in uw toepassing SilkRoad levensduur Suite.</span><span class="sxs-lookup"><span data-stu-id="9815b-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="9815b-151">**Voor het configureren van Azure AD eenmalige aanmelding met SilkRoad levensduur Suite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9815b-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="9815b-152">Aanmelding bij uw bedrijf SilkRoad site als administrator.</span><span class="sxs-lookup"><span data-stu-id="9815b-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="9815b-153">Toegang tot de toepassing SilkRoad levensduur Suite verificatie voor federatie configureren met Microsoft Azure AD, neem contact op met ondersteuning voor SilkRoad of uw vertegenwoordiger SilkRoad Services.</span><span class="sxs-lookup"><span data-stu-id="9815b-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="9815b-154">Ga naar **serviceprovider**, en klik vervolgens op **Federation Details**.</span><span class="sxs-lookup"><span data-stu-id="9815b-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][10] 

3. <span data-ttu-id="9815b-156">Klik op **Federatiemetagegevens downloaden**, en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9815b-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][11] 

4. <span data-ttu-id="9815b-158">In de klassieke Azure-portal op de **SilkRoad levensduur Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9815b-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 

5. <span data-ttu-id="9815b-160">Op de **hoe wilt u dat gebruikers zich aanmelden op SilkRoad levensduur Suite** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9815b-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][7] 

6. <span data-ttu-id="9815b-162">Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9815b-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD voor eenmalige aanmelding][8]   
 1. <span data-ttu-id="9815b-164">In de **aanmelding op URL** textbox, typ de URL moet worden gebruikt door uw gebruikers aan te melden bij uw site SilkRoad levensduur Suite (bijvoorbeeld: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="9815b-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="9815b-165">Open de gedownloade **Silkroad** bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="9815b-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="9815b-166">Zoek de **AssertionConsumerService** labelen en kopieer de **locatie** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="9815b-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Azure AD voor eenmalige aanmelding][21] 
 4. <span data-ttu-id="9815b-168">Plak de waarde in de **antwoord-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="9815b-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="9815b-169">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9815b-169">Click **Next**.</span></span>

6. <span data-ttu-id="9815b-170">Op de **op SilkRoad levensduur Suite eenmalige aanmelding configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9815b-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Azure AD voor eenmalige aanmelding][9]  
 1. <span data-ttu-id="9815b-172">Klik op downloaden certificaat en sla het bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9815b-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="9815b-173">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9815b-173">Click **Next**.</span></span>

7. <span data-ttu-id="9815b-174">In uw **SilkRoad** toepassing, klikt u op **verificatie bronnen**.</span><span class="sxs-lookup"><span data-stu-id="9815b-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][12] 

8. <span data-ttu-id="9815b-176">Klik op **verificatiebron toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9815b-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][13] 

9. <span data-ttu-id="9815b-178">In de **verificatie-bron toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9815b-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][14]  
 1. <span data-ttu-id="9815b-180">Onder **optie 2 - bestand met metagegevens**, klikt u op **Bladeren** het gedownloade metagegevensbestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="9815b-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="9815b-181">Klik op **maken id-Provider met behulp van bestandsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="9815b-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="9815b-182">In de **verificatie bronnen** sectie, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="9815b-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD voor eenmalige aanmelding][15] 

11. <span data-ttu-id="9815b-184">Op de **verificatiebron bewerken** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9815b-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Azure AD voor eenmalige aanmelding][16] 
 1. <span data-ttu-id="9815b-186">Als **ingeschakeld**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="9815b-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="9815b-187">In de **IdP beschrijving** textbox, typ een beschrijving voor uw configuratie (bijvoorbeeld: *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="9815b-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="9815b-188">In de **IdP naam** textbox, typ een naam die specifiek is voor uw configuratie (bijvoorbeeld: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="9815b-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="9815b-189">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9815b-189">Click **Save**.</span></span>

12. <span data-ttu-id="9815b-190">Uitschakelen voor alle andere verificatie-bronnen.</span><span class="sxs-lookup"><span data-stu-id="9815b-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD voor eenmalige aanmelding][17]

13. <span data-ttu-id="9815b-192">In de klassieke Azure-portal op de **eenmalige aanmelding bevestiging** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9815b-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD voor eenmalige aanmelding][18]

14. <span data-ttu-id="9815b-194">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9815b-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD voor eenmalige aanmelding][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9815b-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9815b-196">Create an Azure AD test user</span></span>
<span data-ttu-id="9815b-197">Het doel van deze sectie is een testgebruiker maken in de klassieke Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9815b-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="9815b-199">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9815b-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9815b-200">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9815b-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="9815b-202">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="9815b-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="9815b-203">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9815b-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9815b-205">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9815b-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="9815b-207">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9815b-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="9815b-209">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9815b-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="9815b-210">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9815b-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="9815b-211">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9815b-211">Click **Next**.</span></span>

6. <span data-ttu-id="9815b-212">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9815b-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="9815b-214">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9815b-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="9815b-215">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9815b-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="9815b-216">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9815b-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="9815b-217">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="9815b-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="9815b-218">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9815b-218">Click **Next**.</span></span>

7. <span data-ttu-id="9815b-219">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="9815b-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="9815b-221">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9815b-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="9815b-223">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9815b-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="9815b-224">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="9815b-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="9815b-225">Maak een testgebruiker SilkRoad levensduur Suite</span><span class="sxs-lookup"><span data-stu-id="9815b-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="9815b-226">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in SilkRoad leven Suite.</span><span class="sxs-lookup"><span data-stu-id="9815b-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="9815b-227">De Britta moet een SSO-ID hebben (ook wel een *AuthParam*) die overeenkomt met de Britta **emailaddress** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9815b-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="9815b-228">**Als u wilt een gebruiker Britta Simon aangeroepen in SilkRoad leven Suite maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9815b-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="9815b-229">Vraag uw team SilkRoad levensduur Suite ondersteuning voor het maken van een gebruiker die als **SSO-ID** kenmerk dezelfde waarde als de **emailaddress** van Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9815b-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9815b-230">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="9815b-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="9815b-231">Het doel van deze sectie is het Britta Simon haar toegang verlenen aan SilkRoad levensduur Suite gebruikt Azure eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9815b-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9815b-233">**Als u wilt toewijzen Britta Simon SilkRoad levensduur Suite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9815b-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="9815b-234">In de klassieke Azure portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="9815b-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9815b-236">Selecteer in de lijst met toepassingen **SilkRoad levensduur Suite**.</span><span class="sxs-lookup"><span data-stu-id="9815b-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Gebruiker toewijzen][202] 

3. <span data-ttu-id="9815b-238">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9815b-238">In the menu on the top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203] 

4. <span data-ttu-id="9815b-240">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9815b-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="9815b-241">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="9815b-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="9815b-243">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9815b-243">Test single sign-on</span></span>
<span data-ttu-id="9815b-244">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="9815b-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="9815b-245">Als u op de tegel SilkRoad levensduur Suite in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing SilkRoad levensduur Suite.</span><span class="sxs-lookup"><span data-stu-id="9815b-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9815b-246">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="9815b-246">Additional Resources</span></span>
* [<span data-ttu-id="9815b-247">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9815b-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9815b-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9815b-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





