---
title: 'Zelfstudie: Azure Active Directory-integratie met Replicon | Microsoft Docs'
description: Meer informatie over het gebruik van Replicon met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="44c19-103">Zelfstudie: Azure Active Directory-integratie met Replicon</span><span class="sxs-lookup"><span data-stu-id="44c19-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="44c19-104">Het doel van deze zelfstudie is om de integratie van Azure en Replicon weer te geven.</span><span class="sxs-lookup"><span data-stu-id="44c19-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="44c19-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="44c19-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="44c19-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="44c19-106">A valid Azure subscription</span></span>
* <span data-ttu-id="44c19-107">Een tenant Replicon</span><span class="sxs-lookup"><span data-stu-id="44c19-107">A Replicon tenant</span></span>

<span data-ttu-id="44c19-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Replicon worden kunnen eenmalige aanmelding in de toepassing op uw Replicon bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44c19-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="44c19-109">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="44c19-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="44c19-110">De integratie van toepassingen voor Replicon inschakelen</span><span class="sxs-lookup"><span data-stu-id="44c19-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="44c19-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="44c19-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="44c19-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="44c19-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="44c19-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="44c19-113">Assigning users</span></span>

<span data-ttu-id="44c19-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="44c19-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="44c19-115">De integratie van toepassingen voor Replicon inschakelen</span><span class="sxs-lookup"><span data-stu-id="44c19-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="44c19-116">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor Replicon overzicht.</span><span class="sxs-lookup"><span data-stu-id="44c19-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="44c19-117">**Als u wilt de integratie van toepassingen voor Replicon inschakelen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="44c19-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="44c19-118">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44c19-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="44c19-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="44c19-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="44c19-120">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="44c19-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="44c19-121">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="44c19-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="44c19-122">![Toepassingen](./media/active-directory-saas-replicon-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="44c19-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="44c19-123">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="44c19-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="44c19-124">![Toepassing toevoegen](./media/active-directory-saas-replicon-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="44c19-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="44c19-125">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="44c19-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="44c19-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="44c19-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="44c19-127">In de **zoekvak**, type **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="44c19-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="44c19-128">![Toepassingsgalerie](./media/active-directory-saas-replicon-tutorial/IC777799.png "-toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="44c19-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="44c19-129">Selecteer in het deelvenster met resultaten **Replicon**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="44c19-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="44c19-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="44c19-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="44c19-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="44c19-131">Configure single sign-on</span></span>

<span data-ttu-id="44c19-132">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren Replicon aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="44c19-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="44c19-133">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="44c19-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="44c19-134">In de klassieke Azure-portal op de **Replicon** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="44c19-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="44c19-135">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777801.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="44c19-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="44c19-136">Op de **hoe wilt u dat gebruikers zich aanmelden op Replicon** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="44c19-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="44c19-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777802.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="44c19-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="44c19-138">Op de **App-URL configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="44c19-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="44c19-139">![App-URL configureren](./media/active-directory-saas-replicon-tutorial/IC777803.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="44c19-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="44c19-140">In de **Replicon aanmelding op URL** textbox, typt u uw Replicon tenant-URL (bijvoorbeeld: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="44c19-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="44c19-141">In de **Replicon antwoord-URL** textbox, typt u uw Replicon **AssertionConsumerService** URL (bijvoorbeeld: *https://global.replicon.com/! / saml2/bedrijf/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="44c19-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="44c19-142">U kunt de URL van de metagegevens Replicon op ophalen: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="44c19-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="44c19-143">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="44c19-143">Click **Next**.</span></span>

4. <span data-ttu-id="44c19-144">Op de **eenmalige aanmelding configureren op Replicon** pagina voor het downloaden van de metagegevens, klikt u op **metagegevens downloaden**, en sla de metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="44c19-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="44c19-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777804.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="44c19-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="44c19-146">In een ander browservenster, meld u bij uw bedrijf Replicon site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="44c19-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="44c19-147">Voor het configureren van SAML 2.0, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="44c19-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="44c19-148">![SAML-verificatie inschakelen](./media/active-directory-saas-replicon-tutorial/IC777805.png "inschakelen SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="44c19-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="44c19-149">Om weer te geven de **EnableSAML Authentication2** dialoogvenster het volgende toevoegen aan de URL na de sleutel van uw bedrijf: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="44c19-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="44c19-150">Hieronder ziet u het schema van de volledige URL:</span><span class="sxs-lookup"><span data-stu-id="44c19-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="44c19-151">**https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="44c19-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="44c19-152">Klik op de  **+**  uit te breiden de **v20Configuration** sectie.</span><span class="sxs-lookup"><span data-stu-id="44c19-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="44c19-153">Klik op de  **+**  uit te breiden de **metaDataConfiguration** sectie.</span><span class="sxs-lookup"><span data-stu-id="44c19-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="44c19-154">Klik op **bestand kiezen**, zodat uw identiteit provider metagegevens-XML-bestand selecteren en op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="44c19-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="44c19-155">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="44c19-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="44c19-156">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC778418.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="44c19-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="44c19-157">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="44c19-157">Configure user provisioning</span></span>

<span data-ttu-id="44c19-158">Om in te schakelen gebruikers van Azure AD aan te melden bij Replicon, moeten ze worden ingericht in Replicon.</span><span class="sxs-lookup"><span data-stu-id="44c19-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="44c19-159">In het geval van Replicon is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="44c19-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="44c19-160">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="44c19-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="44c19-161">In een browservenster geopend, meld u bij uw bedrijf Replicon site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="44c19-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="44c19-162">Ga naar **beheer \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="44c19-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="44c19-163">![Gebruikers](./media/active-directory-saas-replicon-tutorial/IC777806.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="44c19-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="44c19-164">Klik op **+ gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="44c19-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="44c19-165">![Gebruiker toevoegen](./media/active-directory-saas-replicon-tutorial/IC777807.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="44c19-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="44c19-166">In de **gebruikersprofiel** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="44c19-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="44c19-167">![Gebruikersprofiel](./media/active-directory-saas-replicon-tutorial/IC777808.png "gebruikersprofiel")</span><span class="sxs-lookup"><span data-stu-id="44c19-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="44c19-168">In de **aanmeldingsnaam** textbox type de Azure AD-e-mailadres van de Azure AD-gebruiker die u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="44c19-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="44c19-169">Als **verificatietype**, selecteer **SSO**.</span><span class="sxs-lookup"><span data-stu-id="44c19-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="44c19-170">In de **afdeling** textbox, typ de afdeling van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="44c19-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="44c19-171">Als **werknemertype**, selecteer **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="44c19-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="44c19-172">Klik op **gebruikersprofiel opslaat**.</span><span class="sxs-lookup"><span data-stu-id="44c19-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="44c19-173">U kunt andere Replicon gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Replicon aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="44c19-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="44c19-174">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="44c19-174">Assign users</span></span>
<span data-ttu-id="44c19-175">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="44c19-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="44c19-176">**Gebruikers om aan te wijzen Replicon, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="44c19-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="44c19-177">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="44c19-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="44c19-178">Op de **Replicon** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="44c19-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="44c19-179">![Gebruikers toewijzen](./media/active-directory-saas-replicon-tutorial/IC777809.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="44c19-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="44c19-180">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="44c19-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="44c19-181">![Ja](./media/active-directory-saas-replicon-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="44c19-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="44c19-182">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="44c19-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="44c19-183">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44c19-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

