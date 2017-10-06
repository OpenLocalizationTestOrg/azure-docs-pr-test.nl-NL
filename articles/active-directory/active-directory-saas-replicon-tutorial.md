---
title: 'Zelfstudie: Azure Active Directory-integratie met Replicon | Microsoft Docs'
description: Lees hoe toouse Replicon met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="526b8-103">Zelfstudie: Azure Active Directory-integratie met Replicon</span><span class="sxs-lookup"><span data-stu-id="526b8-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="526b8-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Replicon.</span><span class="sxs-lookup"><span data-stu-id="526b8-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="526b8-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="526b8-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="526b8-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="526b8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="526b8-107">Een tenant Replicon</span><span class="sxs-lookup"><span data-stu-id="526b8-107">A Replicon tenant</span></span>

<span data-ttu-id="526b8-108">Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooReplicon kunnen toosingle Meld u aan bij Hallo-toepassing op uw Replicon bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [inleiding toohello toegang Deelvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="526b8-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="526b8-109">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="526b8-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="526b8-110">Hallo toepassingsintegratie voor Replicon inschakelen</span><span class="sxs-lookup"><span data-stu-id="526b8-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="526b8-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="526b8-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="526b8-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="526b8-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="526b8-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="526b8-113">Assigning users</span></span>

<span data-ttu-id="526b8-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="526b8-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="526b8-115">Hallo toepassingsintegratie voor Replicon inschakelen</span><span class="sxs-lookup"><span data-stu-id="526b8-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="526b8-116">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Replicon.</span><span class="sxs-lookup"><span data-stu-id="526b8-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="526b8-117">**tooenable hello toepassingsintegratie voor Replicon, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="526b8-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="526b8-118">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="526b8-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="526b8-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="526b8-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="526b8-120">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="526b8-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="526b8-121">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="526b8-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="526b8-122">![Toepassingen](./media/active-directory-saas-replicon-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="526b8-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="526b8-123">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="526b8-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="526b8-124">![Toepassing toevoegen](./media/active-directory-saas-replicon-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="526b8-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="526b8-125">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="526b8-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="526b8-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="526b8-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="526b8-127">In Hallo **zoekvak**, type **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="526b8-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="526b8-128">![Toepassingsgalerie](./media/active-directory-saas-replicon-tutorial/IC777799.png "-toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="526b8-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="526b8-129">Selecteer in het deelvenster met resultaten Hallo **Replicon**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="526b8-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="526b8-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="526b8-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="526b8-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="526b8-131">Configure single sign-on</span></span>

<span data-ttu-id="526b8-132">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooReplicon aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="526b8-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="526b8-133">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="526b8-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="526b8-134">In de klassieke Azure-portal op Hallo Hallo **Replicon** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="526b8-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="526b8-135">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777801.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="526b8-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="526b8-136">Op Hallo **wilt u hoe gebruikers toosign op tooReplicon** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="526b8-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="526b8-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777802.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="526b8-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="526b8-138">Op Hallo **App-URL configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="526b8-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="526b8-139">![App-URL configureren](./media/active-directory-saas-replicon-tutorial/IC777803.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="526b8-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="526b8-140">In Hallo **Replicon aanmelding op URL** textbox, typt u uw Replicon tenant-URL (bijvoorbeeld: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="526b8-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="526b8-141">In Hallo **Replicon antwoord-URL** textbox, typt u uw Replicon **AssertionConsumerService** URL (bijvoorbeeld: *https://global.replicon.com/! / saml2/bedrijf/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="526b8-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="526b8-142">U kunt Hallo-URL ophalen van Hallo Replicon metagegevens op: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="526b8-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="526b8-143">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="526b8-143">Click **Next**.</span></span>

4. <span data-ttu-id="526b8-144">Op Hallo **eenmalige aanmelding configureren op Replicon** pagina, toodownload uw metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="526b8-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="526b8-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777804.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="526b8-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="526b8-146">In een ander browservenster, meld u bij uw bedrijf Replicon site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="526b8-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="526b8-147">tooconfigure SAML 2.0, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="526b8-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="526b8-148">![SAML-verificatie inschakelen](./media/active-directory-saas-replicon-tutorial/IC777805.png "inschakelen SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="526b8-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="526b8-149">Hallo toodisplay **EnableSAML Authentication2** dialoogvenster Hallo tooyour-URL te volgen nadat de sleutel van uw bedrijf toevoegen: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="526b8-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="526b8-150">Hallo hieronder vindt u Hallo-schema van de volledige URL Hallo:</span><span class="sxs-lookup"><span data-stu-id="526b8-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="526b8-151">**https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="526b8-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="526b8-152">Klik op Hallo  **+**  tooexpand hello **v20Configuration** sectie.</span><span class="sxs-lookup"><span data-stu-id="526b8-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="526b8-153">Klik op Hallo  **+**  tooexpand hello **metaDataConfiguration** sectie.</span><span class="sxs-lookup"><span data-stu-id="526b8-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="526b8-154">Klik op **bestand kiezen**, tooselect uw identiteit provider metagegevens-XML-bestand en klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="526b8-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="526b8-155">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="526b8-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="526b8-156">![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC778418.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="526b8-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="526b8-157">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="526b8-157">Configure user provisioning</span></span>

<span data-ttu-id="526b8-158">In de volgorde tooenable Azure AD gebruikers toolog in Replicon, moeten ze worden ingericht in Replicon.</span><span class="sxs-lookup"><span data-stu-id="526b8-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="526b8-159">In geval van Replicon Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="526b8-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="526b8-160">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="526b8-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="526b8-161">In een browservenster geopend, meld u bij uw bedrijf Replicon site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="526b8-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="526b8-162">Ga te**beheer \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="526b8-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="526b8-163">![Gebruikers](./media/active-directory-saas-replicon-tutorial/IC777806.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="526b8-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="526b8-164">Klik op **+ gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="526b8-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="526b8-165">![Gebruiker toevoegen](./media/active-directory-saas-replicon-tutorial/IC777807.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="526b8-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="526b8-166">In Hallo **gebruikersprofiel** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="526b8-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="526b8-167">![Gebruikersprofiel](./media/active-directory-saas-replicon-tutorial/IC777808.png "gebruikersprofiel")</span><span class="sxs-lookup"><span data-stu-id="526b8-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="526b8-168">In Hallo **aanmeldingsnaam** textbox type hello Azure AD e-mailadres van hello Azure AD-gebruiker die u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="526b8-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="526b8-169">Als **verificatietype**, selecteer **SSO**.</span><span class="sxs-lookup"><span data-stu-id="526b8-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="526b8-170">In Hallo **afdeling** textbox, typ de afdeling Hallo van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="526b8-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="526b8-171">Als **werknemertype**, selecteer **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="526b8-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="526b8-172">Klik op **gebruikersprofiel opslaat**.</span><span class="sxs-lookup"><span data-stu-id="526b8-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="526b8-173">U kunt andere Replicon gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Replicon tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="526b8-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="526b8-174">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="526b8-174">Assign users</span></span>
<span data-ttu-id="526b8-175">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="526b8-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="526b8-176">**tooassign gebruikers tooReplicon, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="526b8-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="526b8-177">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="526b8-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="526b8-178">Op Hallo **Replicon** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="526b8-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="526b8-179">![Gebruikers toewijzen](./media/active-directory-saas-replicon-tutorial/IC777809.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="526b8-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="526b8-180">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="526b8-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="526b8-181">![Ja](./media/active-directory-saas-replicon-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="526b8-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="526b8-182">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="526b8-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="526b8-183">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="526b8-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

