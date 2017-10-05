---
title: 'Zelfstudie: Azure Active Directory-integratie met ServiceNow | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ServiceNow en ServiceNow Express.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="8ddc3-103">Zelfstudie: Azure Active Directory-integratie met ServiceNow</span><span class="sxs-lookup"><span data-stu-id="8ddc3-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="8ddc3-104">In deze zelfstudie leert u hoe ServiceNow en ServiceNow Express integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ddc3-105">ServiceNow en ServiceNow Express integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8ddc3-106">U kunt beheren in Azure AD die toegang tot ServiceNow en ServiceNow Express heeft</span><span class="sxs-lookup"><span data-stu-id="8ddc3-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="8ddc3-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ServiceNow en ServiceNow Express (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="8ddc3-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8ddc3-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="8ddc3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8ddc3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ddc3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8ddc3-110">Prerequisites</span></span>
<span data-ttu-id="8ddc3-111">Voor het configureren van Azure AD-integratie met ServiceNow en ServiceNow Express, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="8ddc3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8ddc3-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8ddc3-113">Voor ServiceNow, een exemplaar of de tenant van ServiceNow, Calgary versie of hoger</span><span class="sxs-lookup"><span data-stu-id="8ddc3-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="8ddc3-114">Voor ServiceNow snelle, een exemplaar van ServiceNow Express, Helsinki versie of hoger</span><span class="sxs-lookup"><span data-stu-id="8ddc3-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="8ddc3-115">De ServiceNow-tenant moet hebben de [meerdere Provider eenmalige aanmelding op invoegtoepassing](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="8ddc3-116">Dit kan worden gedaan door [indienen van een serviceaanvraag](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="8ddc3-117">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8ddc3-118">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8ddc3-119">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8ddc3-120">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ddc3-121">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8ddc3-121">Scenario description</span></span>
<span data-ttu-id="8ddc3-122">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ddc3-123">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ddc3-124">ServiceNow uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8ddc3-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="8ddc3-125">Configureren en testen van Azure AD eenmalige aanmelding voor ServiceNow of ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="8ddc3-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="8ddc3-126">ServiceNow uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8ddc3-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="8ddc3-127">Voor het configureren van de integratie van ServiceNow of ServiceNow Express in Azure AD, moet u ServiceNow uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="8ddc3-128">**Als u wilt toevoegen ServiceNow uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8ddc3-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ddc3-129">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="8ddc3-131">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8ddc3-132">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Toepassingen][2]
4. <span data-ttu-id="8ddc3-134">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Toepassingen][3]
5. <span data-ttu-id="8ddc3-136">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Toepassingen][4]
6. <span data-ttu-id="8ddc3-138">Typ in het zoekvak **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="8ddc3-140">Selecteer in het deelvenster met resultaten **ServiceNow**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ddc3-142">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8ddc3-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ddc3-143">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met ServiceNow of ServiceNow snelle op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ddc3-144">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ServiceNow is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="8ddc3-145">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante ServiceNow-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="8ddc3-146">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="8ddc3-147">Om te configureren en testen van Azure AD eenmalige aanmelding met ServiceNow, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ddc3-148">**[Azure AD eenmalige aanmelding configureren voor ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ddc3-149">**[Configureren van Azure AD eenmalige aanmelding voor snelle ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="8ddc3-150">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="8ddc3-151">**[Maken van een testgebruiker ServiceNow](#creating-a-servicenow-test-user)**  - ServiceNow die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="8ddc3-152">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="8ddc3-153">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="8ddc3-154">Als u wilt configureren ServiceNow weglaten stap 2.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="8ddc3-155">Op dezelfde manier als u wilt configureren ServiceNow Express weglaten stap 1.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="8ddc3-156">Azure AD voor eenmalige aanmelding configureren voor ServiceNow</span><span class="sxs-lookup"><span data-stu-id="8ddc3-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="8ddc3-157">In de klassieke Azure AD-portal op de **ServiceNow** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="8ddc3-158">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="8ddc3-159">Op de **hoe wilt u dat gebruikers zich aanmelden op ServiceNow** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="8ddc3-160">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749324.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="8ddc3-161">Op de **App-instellingen configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="8ddc3-162">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC769497.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="8ddc3-163">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-163">a.</span></span> <span data-ttu-id="8ddc3-164">in de **ServiceNow aanmelding op URL** textbox, typ de URL van uw gebruikt door uw gebruikers aan te melden bij uw ServiceNow-toepassing die het patroon volgen: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="8ddc3-165">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-165">b.</span></span> <span data-ttu-id="8ddc3-166">In de **id** textbox, typ de URL van uw gebruikt door uw gebruikers aan te melden bij uw ServiceNow-toepassing die het patroon volgen: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="8ddc3-167">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-167">c.</span></span> <span data-ttu-id="8ddc3-168">Klik op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="8ddc3-168">Click **Next**</span></span>

4. <span data-ttu-id="8ddc3-169">Azure AD ServiceNow automatisch te configureren voor verificatie op basis van SAML Voer uw ServiceNow-instantienaam, beheerdersgebruikersnaam en beheerwachtwoord in de **automatisch eenmalige aanmelding configureren** vormen en klikt u op  *Configureer*.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="8ddc3-170">Let op: de opgegeven beheerdersgebruikersnaam moet de **security_admin** rol die is toegewezen in ServiceNow voor deze werkt.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="8ddc3-171">Klik anders op om handmatig te configureren tussen ServiceNow voor het gebruik van Azure AD als SAML-identiteitsprovider, **handmatig configureren van de toepassing voor eenmalige aanmelding**, klikt u vervolgens op **volgende** en voltooi de volgende stappen .</span><span class="sxs-lookup"><span data-stu-id="8ddc3-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="8ddc3-172">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="8ddc3-173">Op de **eenmalige aanmelding configureren op ServiceNow** pagina, klikt u op **certificaat downloaden**, sla het certificaatbestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="8ddc3-174">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749325.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="8ddc3-175">Aanmelding bij uw ServiceNow-toepassing als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="8ddc3-176">Activeer de *integratie - meerdere Provider Single Sign-On-installatieprogramma* invoegtoepassing door de volgende stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="8ddc3-177">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-177">a.</span></span> <span data-ttu-id="8ddc3-178">Ga in het navigatievenster aan de linkerkant naar **System Definition** sectie en klik vervolgens op **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="8ddc3-179">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "invoegtoepassing activeren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="8ddc3-180">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-180">b.</span></span> <span data-ttu-id="8ddc3-181">Zoeken naar *integratie - meerdere Provider Single Sign-On-installatieprogramma*.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="8ddc3-182">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "invoegtoepassing activeren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="8ddc3-183">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-183">c.</span></span> <span data-ttu-id="8ddc3-184">Selecteer de invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-184">Select the plugin.</span></span> <span data-ttu-id="8ddc3-185">Rigth op en selecteer **activeren/Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="8ddc3-186">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-186">d.</span></span> <span data-ttu-id="8ddc3-187">Klik op de **activeren** knop.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="8ddc3-188">Klik in het navigatievenster aan de linkerkant op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="8ddc3-189">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="8ddc3-190">Op de **meerdere eigenschappen van de Provider SSO** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="8ddc3-191">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="8ddc3-192">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-192">a.</span></span> <span data-ttu-id="8ddc3-193">Als **provider voor meervoudige eenmalige aanmelding inschakelen**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="8ddc3-194">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-194">b.</span></span> <span data-ttu-id="8ddc3-195">Als **logboekregistratie voor foutopsporing hebt u de provider voor meervoudige SSO-integratie inschakelen**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="8ddc3-196">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-196">c.</span></span> <span data-ttu-id="8ddc3-197">In **het veld op de gebruiker die tabel...**  textbox type **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="8ddc3-198">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-198">d.</span></span> <span data-ttu-id="8ddc3-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-199">Click **Save**.</span></span>

10. <span data-ttu-id="8ddc3-200">Klik in het navigatievenster aan de linkerkant op **x509 certificaten**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="8ddc3-201">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="8ddc3-202">Op de **X.509-certificaten** dialoogvenster, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="8ddc3-203">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="8ddc3-204">Op de **X.509-certificaten** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="8ddc3-205">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="8ddc3-206">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-206">a.</span></span> <span data-ttu-id="8ddc3-207">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-207">Click **New**.</span></span>
    
     <span data-ttu-id="8ddc3-208">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-208">b.</span></span> <span data-ttu-id="8ddc3-209">In de **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="8ddc3-210">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-210">c.</span></span> <span data-ttu-id="8ddc3-211">Selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-211">Select **Active**.</span></span>
    
     <span data-ttu-id="8ddc3-212">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-212">d.</span></span> <span data-ttu-id="8ddc3-213">Als **indeling**, selecteer **PEM**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="8ddc3-214">e.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-214">e.</span></span> <span data-ttu-id="8ddc3-215">Als **Type**, selecteer **vertrouwen Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="8ddc3-216">f.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-216">f.</span></span> <span data-ttu-id="8ddc3-217">De met Base64 versleuteld certificaat openen in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **PEM certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="8ddc3-218">g.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-218">g.</span></span> <span data-ttu-id="8ddc3-219">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-219">Click **Update**.</span></span>

13. <span data-ttu-id="8ddc3-220">Klik in het navigatievenster aan de linkerkant op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="8ddc3-221">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="8ddc3-222">Op de **identiteitsproviders** dialoogvenster, klikt u op **nieuw**:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="8ddc3-223">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="8ddc3-224">Op de **identiteitsproviders** dialoogvenster, klikt u op **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="8ddc3-225">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="8ddc3-226">Voer de volgende stappen uit in het dialoogvenster SAML2 Update1 eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="8ddc3-227">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="8ddc3-228">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-228">a.</span></span> <span data-ttu-id="8ddc3-229">in de **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="8ddc3-230">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-230">b.</span></span> <span data-ttu-id="8ddc3-231">In de **Gebruikersveld** textbox type **e** of **gebruikersnaam**, afhankelijk van welk veld wordt gebruikt als unieke identificatie van gebruikers in uw ServiceNow-implementatie.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="8ddc3-232">U kunt configue Azure AD voor het verzenden van de Azure AD-gebruikers-ID (UPN) of het e-mailadres als de unieke id in het SAML-token door te gaan naar de **ServiceNow > kenmerken > eenmalige aanmelding** sectie van de klassieke Azure Portal Portal en de toewijzing van het gewenste veld de **nameidentifier** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="8ddc3-233">De waarde voor het geselecteerde kenmerk opgeslagen in Azure AD (bijvoorbeeld gebruiker principal name) moet overeenkomen met de waarde die is opgeslagen in ServiceNow voor het opgegeven veld (bijvoorbeeld gebruikersnaam)</span><span class="sxs-lookup"><span data-stu-id="8ddc3-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="8ddc3-234">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-234">c.</span></span> <span data-ttu-id="8ddc3-235">In de klassieke Azure AD-portal kopieert de **identiteit Provider-ID** waarde en plak deze in de **identiteit Provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="8ddc3-236">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-236">d.</span></span> <span data-ttu-id="8ddc3-237">In de klassieke Azure AD-portal kopieert de **aanvraag-URL voor webverificatie** waarde en plak deze in de **van de identiteitsprovider AuthnRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="8ddc3-238">e.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-238">e.</span></span> <span data-ttu-id="8ddc3-239">In de klassieke Azure AD-portal kopieert de **Service-URL met eenmalige Sign-Out** waarde en plak deze in de **van de identiteitsprovider SingleLogoutRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="8ddc3-240">f.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-240">f.</span></span> <span data-ttu-id="8ddc3-241">In de **ServiceNow Homepage** textbox, typ de URL van de startpagina van uw ServiceNow-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ddc3-242">De startpagina ServiceNow-exemplaar is een samenvoeging van uw **ServieNow tenant-URL** en **/navpage.do** (bijvoorbeeld:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="8ddc3-243">g.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-243">g.</span></span> <span data-ttu-id="8ddc3-244">In de **entiteit-ID / verlener** textbox, typ de URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="8ddc3-245">h.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-245">h.</span></span> <span data-ttu-id="8ddc3-246">In de **doelgroep URL** textbox, typ de URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="8ddc3-247">ik.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-247">i.</span></span> <span data-ttu-id="8ddc3-248">In de **Protocol Binding voor de IDP SingleLogoutRequest** textbox type **urn: oasis: namen: tc: SAML:2.0:bindings:HTTP-omleiden**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="8ddc3-249">j.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-249">j.</span></span> <span data-ttu-id="8ddc3-250">Typ in het tekstvak NameID beleid **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: niet-gespecificeerde**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="8ddc3-251">k.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-251">k.</span></span> <span data-ttu-id="8ddc3-252">Hef de selectie **maken van een AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="8ddc3-253">l.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-253">l.</span></span> <span data-ttu-id="8ddc3-254">In de **AuthnContextClassRef methode**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="8ddc3-255">Dit is alleen nodig als u alleen cloud-organisatie.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="8ddc3-256">Als u werkt met on-premises AD FS of MFA voor verificatie en vervolgens moet u deze waarde niet configureren.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="8ddc3-257">m.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-257">m.</span></span> <span data-ttu-id="8ddc3-258">In **klok leiden tot onjuiste** textbox type **60**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="8ddc3-259">n.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-259">n.</span></span> <span data-ttu-id="8ddc3-260">Als **eenmalige aanmelding op Script**, selecteer **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="8ddc3-261">o.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-261">o.</span></span> <span data-ttu-id="8ddc3-262">Als **x509 certificaat**, selecteert u het certificaat dat u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="8ddc3-263">p.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-263">p.</span></span> <span data-ttu-id="8ddc3-264">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="8ddc3-265">Bij de klassieke Azure AD-portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="8ddc3-266">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="8ddc3-267">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="8ddc3-268">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="8ddc3-269">Configureren van Azure AD voor eenmalige aanmelding voor snelle ServiceNow</span><span class="sxs-lookup"><span data-stu-id="8ddc3-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="8ddc3-270">In de klassieke Azure AD-portal op de **ServiceNow** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="8ddc3-271">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="8ddc3-272">Op de **hoe wilt u dat gebruikers zich aanmelden op ServiceNow** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="8ddc3-273">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749324.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="8ddc3-274">Op de **App-instellingen configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="8ddc3-275">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC769497.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="8ddc3-276">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-276">a.</span></span> <span data-ttu-id="8ddc3-277">in de **ServiceNow aanmelding op URL** textbox, typ de URL van uw gebruikt door uw gebruikers aan te melden bij uw ServiceNow-toepassing die het patroon volgen: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="8ddc3-278">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-278">b.</span></span> <span data-ttu-id="8ddc3-279">In de **URL-verlener** textbox, typ de URL van uw gebruikt door uw gebruikers aan te melden bij uw ServiceNow-toepassing die het patroon volgen `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="8ddc3-280">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-280">c.</span></span> <span data-ttu-id="8ddc3-281">Klik op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="8ddc3-281">Click **Next**</span></span>

4. <span data-ttu-id="8ddc3-282">Klik op **handmatig configureren van de toepassing voor eenmalige aanmelding**, klikt u vervolgens op **volgende** en de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="8ddc3-283">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="8ddc3-284">Op de **eenmalige aanmelding configureren op ServiceNow** pagina, klikt u op **certificaat downloaden**, sla het certificaatbestand lokaal op uw computer en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="8ddc3-285">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749325.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="8ddc3-286">Aanmelding bij uw ServiceNow-Express-toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="8ddc3-287">Klik in het navigatievenster aan de linkerkant op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="8ddc3-288">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="8ddc3-289">Op de **Single Sign-On** dialoogvenster, klikt u op het configuratiepictogram op de rechterbovenhoek en stelt u de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="8ddc3-290">![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="8ddc3-291">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-291">a.</span></span> <span data-ttu-id="8ddc3-292">Wisselknop **provider voor meervoudige eenmalige aanmelding inschakelen** naar rechts.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="8ddc3-293">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-293">b.</span></span> <span data-ttu-id="8ddc3-294">Wisselknop **logboekregistratie voor de provider voor meervoudige SSO-integratie voor het inschakelen van foutopsporing** naar rechts.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="8ddc3-295">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-295">c.</span></span> <span data-ttu-id="8ddc3-296">In **het veld op de gebruiker die tabel...**  textbox type **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="8ddc3-297">Op de **Single Sign-On** dialoogvenster, klikt u op **nieuw certificaat toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="8ddc3-298">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="8ddc3-299">Op de **X.509-certificaten** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="8ddc3-300">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="8ddc3-301">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-301">a.</span></span> <span data-ttu-id="8ddc3-302">In de **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="8ddc3-303">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-303">b.</span></span> <span data-ttu-id="8ddc3-304">Selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-304">Select **Active**.</span></span>
    
    <span data-ttu-id="8ddc3-305">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-305">c.</span></span> <span data-ttu-id="8ddc3-306">Als **indeling**, selecteer **PEM**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="8ddc3-307">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-307">d.</span></span> <span data-ttu-id="8ddc3-308">Als **Type**, selecteer **vertrouwen Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="8ddc3-309">e.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-309">e.</span></span> <span data-ttu-id="8ddc3-310">Maak een Base64-gecodeerde bestand uit het gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="8ddc3-311">Zie voor meer informatie [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="8ddc3-312">f.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-312">f.</span></span> <span data-ttu-id="8ddc3-313">De met Base64 versleuteld certificaat openen in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **PEM certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="8ddc3-314">g.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-314">g.</span></span> <span data-ttu-id="8ddc3-315">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-315">Click **Update**.</span></span>
11. <span data-ttu-id="8ddc3-316">Op de **Single Sign-On** dialoogvenster, klikt u op **toevoegen van nieuwe IdP**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="8ddc3-317">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="8ddc3-318">Op de **identiteitsprovider toevoegen** dialoogvenster onder **id-Provider configureren**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="8ddc3-319">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="8ddc3-320">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-320">a.</span></span> <span data-ttu-id="8ddc3-321">in de **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="8ddc3-322">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-322">b.</span></span> <span data-ttu-id="8ddc3-323">In de klassieke Azure AD-portal kopieert de **identiteit Provider-ID** waarde en plak deze in de **identiteit Provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="8ddc3-324">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-324">c.</span></span> <span data-ttu-id="8ddc3-325">In de klassieke Azure AD-portal kopieert de **aanvraag-URL voor webverificatie** waarde en plak deze in de **van de identiteitsprovider AuthnRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="8ddc3-326">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-326">d.</span></span> <span data-ttu-id="8ddc3-327">In de klassieke Azure AD-portal kopieert de **Service-URL met eenmalige Sign-Out** waarde en plak deze in de **van de identiteitsprovider SingleLogoutRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="8ddc3-328">e.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-328">e.</span></span> <span data-ttu-id="8ddc3-329">Als **Provider identiteitscertificaat**, selecteert u het certificaat dat u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="8ddc3-330">Klik op **geavanceerde instellingen**, en klikt u onder **extra identiteitseigenschappen Provider**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="8ddc3-331">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8ddc3-332">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-332">a.</span></span> <span data-ttu-id="8ddc3-333">In de **Protocol Binding voor de IDP SingleLogoutRequest** textbox type **urn: oasis: namen: tc: SAML:2.0:bindings:HTTP-omleiden**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="8ddc3-334">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-334">b.</span></span> <span data-ttu-id="8ddc3-335">In de **NameID beleid** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: niet-gespecificeerde**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="8ddc3-336">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-336">c.</span></span> <span data-ttu-id="8ddc3-337">In de **AuthnContextClassRef methode**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="8ddc3-338">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-338">d.</span></span> <span data-ttu-id="8ddc3-339">Hef de selectie **maken van een AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="8ddc3-340">Onder **extra eigenschappen van de Service Provider**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="8ddc3-341">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8ddc3-342">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-342">a.</span></span> <span data-ttu-id="8ddc3-343">In de **ServiceNow Homepage** textbox, typ de URL van de startpagina van uw ServiceNow-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="8ddc3-344">De startpagina ServiceNow-exemplaar is een samenvoeging van uw **ServieNow tenant-URL** en **/navpage.do** (bijvoorbeeld: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="8ddc3-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="8ddc3-345">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-345">b.</span></span> <span data-ttu-id="8ddc3-346">In de **entiteit-ID / verlener** textbox, typ de URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="8ddc3-347">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-347">c.</span></span> <span data-ttu-id="8ddc3-348">In de **doelgroep-URI** textbox, typ de URL van uw ServiceNow-tenant.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="8ddc3-349">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-349">d.</span></span> <span data-ttu-id="8ddc3-350">In **klok leiden tot onjuiste** textbox type **60**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="8ddc3-351">e.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-351">e.</span></span> <span data-ttu-id="8ddc3-352">In de **Gebruikersveld** textbox type **e** of **gebruikersnaam**, afhankelijk van welk veld wordt gebruikt als unieke identificatie van gebruikers in uw ServiceNow-implementatie.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="8ddc3-353">U kunt configue Azure AD voor het verzenden van de Azure AD-gebruikers-ID (UPN) of het e-mailadres als de unieke id in het SAML-token door te gaan naar de **ServiceNow > kenmerken > eenmalige aanmelding** sectie van de klassieke Azure Portal Portal en de toewijzing van het gewenste veld de **nameidentifier** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="8ddc3-354">De waarde voor het geselecteerde kenmerk opgeslagen in Azure AD (bijvoorbeeld gebruiker principal name) moet overeenkomen met de waarde die is opgeslagen in ServiceNow voor het opgegeven veld (bijvoorbeeld gebruikersnaam)</span><span class="sxs-lookup"><span data-stu-id="8ddc3-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="8ddc3-355">f.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-355">f.</span></span> <span data-ttu-id="8ddc3-356">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-356">Click **Save**.</span></span> 

3. <span data-ttu-id="8ddc3-357">Bij de klassieke Azure AD-portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="8ddc3-358">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="8ddc3-359">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="8ddc3-360">![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="8ddc3-361">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="8ddc3-361">Configuring user provisioning</span></span>
<span data-ttu-id="8ddc3-362">Het doel van deze sectie is het inschakelen van de gebruiker het inrichten van Active Directory-gebruikersaccounts met ServiceNow overzicht.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="8ddc3-363">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="8ddc3-364">In de klassieke Azure Management-portal op de **ServiceNow** pagina van de integratie van toepassing, klikt u op **configureren gebruikersaanvragen**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="8ddc3-365">![Gebruikers inrichten](./media/active-directory-saas-servicenow-tutorial/IC769498.png "gebruikers inrichten")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="8ddc3-366">Op de **Voer uw ServiceNow-referenties om in te schakelen automatisch gebruikers inrichten** pagina, bieden de volgende configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="8ddc3-367">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-367">a.</span></span> <span data-ttu-id="8ddc3-368">In de **ServiceNow-exemplaarnaam** textbox, typ de naam van het ServiceNow-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="8ddc3-369">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-369">b.</span></span> <span data-ttu-id="8ddc3-370">In de **ServiceNow-Beheerdersgebruikersnaam** textbox, typ de naam van de ServiceNow-account.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="8ddc3-371">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-371">c.</span></span> <span data-ttu-id="8ddc3-372">In de **ServiceNow-beheerderswachtwoord** textbox, typt u het wachtwoord voor dit account.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="8ddc3-373">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-373">d.</span></span> <span data-ttu-id="8ddc3-374">Klik op **valideren** om te controleren of uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="8ddc3-375">e.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-375">e.</span></span> <span data-ttu-id="8ddc3-376">Klik op de **volgende** te openen de **Vervolgstappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="8ddc3-377">f.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-377">f.</span></span> <span data-ttu-id="8ddc3-378">Als u inrichten van alle gebruikers deze toepassing wilt, selecteert u '**automatisch inrichten van alle gebruikersaccounts in de directory voor deze toepassing**'.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="8ddc3-379">![Volgende stappen](./media/active-directory-saas-servicenow-tutorial/IC698804.png "volgende stappen")</span><span class="sxs-lookup"><span data-stu-id="8ddc3-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="8ddc3-380">g.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-380">g.</span></span> <span data-ttu-id="8ddc3-381">Op de **Vervolgstappen** pagina, klikt u op **Complete** aan uw configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ddc3-382">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8ddc3-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ddc3-383">In deze sectie maakt u een testgebruiker in de klassieke portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="8ddc3-385">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8ddc3-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ddc3-386">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="8ddc3-388">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8ddc3-389">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ddc3-391">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="8ddc3-393">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="8ddc3-395">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-395">a.</span></span> <span data-ttu-id="8ddc3-396">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="8ddc3-397">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-397">b.</span></span> <span data-ttu-id="8ddc3-398">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8ddc3-399">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-399">c.</span></span> <span data-ttu-id="8ddc3-400">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-400">Click **Next**.</span></span>

6. <span data-ttu-id="8ddc3-401">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="8ddc3-403">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-403">a.</span></span> <span data-ttu-id="8ddc3-404">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="8ddc3-405">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-405">b.</span></span> <span data-ttu-id="8ddc3-406">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="8ddc3-407">c.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-407">c.</span></span> <span data-ttu-id="8ddc3-408">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="8ddc3-409">d.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-409">d.</span></span> <span data-ttu-id="8ddc3-410">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="8ddc3-411">e.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-411">e.</span></span> <span data-ttu-id="8ddc3-412">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-412">Click **Next**.</span></span>

7. <span data-ttu-id="8ddc3-413">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="8ddc3-415">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ddc3-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="8ddc3-417">a.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-417">a.</span></span> <span data-ttu-id="8ddc3-418">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="8ddc3-419">b.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-419">b.</span></span> <span data-ttu-id="8ddc3-420">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="8ddc3-421">Maken van een testgebruiker ServiceNow</span><span class="sxs-lookup"><span data-stu-id="8ddc3-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="8ddc3-422">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="8ddc3-423">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="8ddc3-424">Als u niet hoe u een gebruiker in uw ServiceNow of ServiceNow Express-account toevoegt weet, moet u contact op met ServiceNow-ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ddc3-425">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ddc3-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="8ddc3-426">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8ddc3-428">**Britta Simon om aan te wijzen ServiceNow, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8ddc3-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="8ddc3-429">In de klassieke portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8ddc3-431">Selecteer in de lijst met toepassingen **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="8ddc3-433">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-433">In the menu on the top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203] 

4. <span data-ttu-id="8ddc3-435">Selecteer in de lijst met alle gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="8ddc3-436">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8ddc3-438">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8ddc3-438">Testing single sign-on</span></span>
<span data-ttu-id="8ddc3-439">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8ddc3-440">Als u op de tegel ServiceNow in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw ServiceNow-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ddc3-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ddc3-441">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8ddc3-441">Additional resources</span></span>
* [<span data-ttu-id="8ddc3-442">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ddc3-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ddc3-443">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ddc3-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
