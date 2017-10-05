---
title: 'Zelfstudie: Azure Active Directory-integratie met centraal bureaublad | Microsoft Docs'
description: Meer informatie over het centrale bureaublad gebruiken met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="1dade-103">Zelfstudie: Azure Active Directory-integratie met centraal bureaublad</span><span class="sxs-lookup"><span data-stu-id="1dade-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="1dade-104">Het doel van deze zelfstudie is om de integratie van Azure en centrale bureaublad weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1dade-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="1dade-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="1dade-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1dade-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="1dade-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1dade-107">Een centrale bureaublad eenmalige aanmelding ingeschakeld abonnement / tenant-centrale bureaublad</span><span class="sxs-lookup"><span data-stu-id="1dade-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="1dade-108">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="1dade-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="1dade-109">De integratie van toepassingen voor centrale bureaublad inschakelen</span><span class="sxs-lookup"><span data-stu-id="1dade-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="1dade-110">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="1dade-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="1dade-111">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="1dade-111">Configuring user provisioning</span></span>
* <span data-ttu-id="1dade-112">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="1dade-112">Assigning users</span></span>

<span data-ttu-id="1dade-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="1dade-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="1dade-114">De toepassingsintegratie van de voor centrale bureaublad inschakelen</span><span class="sxs-lookup"><span data-stu-id="1dade-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="1dade-115">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor centrale bureaublad overzicht.</span><span class="sxs-lookup"><span data-stu-id="1dade-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="1dade-116">**Schakel de integratie van toepassingen voor centrale bureaublad door de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1dade-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="1dade-117">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dade-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="1dade-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1dade-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1dade-119">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="1dade-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1dade-120">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="1dade-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="1dade-121">![Toepassingen](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="1dade-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1dade-122">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="1dade-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="1dade-123">![Toepassing toevoegen](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="1dade-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="1dade-124">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="1dade-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="1dade-125">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="1dade-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="1dade-126">In de **zoekvak**, type **centrale bureaublad**.</span><span class="sxs-lookup"><span data-stu-id="1dade-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="1dade-127">![Toepassingsgalerie](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "-toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="1dade-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="1dade-128">Selecteer in het deelvenster met resultaten **centrale bureaublad**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1dade-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="1dade-129">![Centrale bureaublad](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "centrale bureaublad")</span><span class="sxs-lookup"><span data-stu-id="1dade-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="1dade-130">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="1dade-130">Configure single sign-on</span></span>

<span data-ttu-id="1dade-131">Het doel van deze sectie is om een overzicht van gebruikers te verifiëren naar centrale bureaublad met hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="1dade-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="1dade-132">Als onderdeel van deze procedure zich u moet een Base64-gecodeerde certificaat uploaden naar uw tenant centrale bureaublad.</span><span class="sxs-lookup"><span data-stu-id="1dade-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="1dade-133">Als u niet bekend met deze procedure bent, Zie [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="1dade-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="1dade-134">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1dade-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="1dade-135">In de klassieke Azure-portal op de **centrale bureaublad** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de ** configureren eenmalige aanmelding ** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1dade-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="1dade-136">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1dade-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="1dade-137">Op de **hoe wilt u dat gebruikers zich aanmelden op voor de centrale bureaublad** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1dade-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="1dade-138">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1dade-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="1dade-139">Op de **App-URL configureren** pagina, voer de volgende stappen uit en klik vervolgens op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="1dade-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="1dade-140">In de **centrale bureaublad aanmelding In URL** textbox, typ de URL van uw tenant centrale bureaublad (bijvoorbeeld: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="1dade-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="1dade-141">Typ in het tekstvak voor de centrale bureaublad antwoord-URL, uw centrale bureaublad AssertionConsumerService-URL (bijvoorbeeld: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="1dade-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1dade-142">U kunt de waarde niet ophalen uit de centrale bureaublad metagegevens (bijvoorbeeld: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="1dade-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="1dade-143">![App-URL configureren](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="1dade-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="1dade-144">Op de **eenmalige aanmelding configureren op de centrale bureaublad** pagina om uw certificaat te downloaden, klikt u op **certificaat downloaden**, en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1dade-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="1dade-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1dade-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="1dade-146">Meld u aan bij uw **centrale bureaublad** tenant.</span><span class="sxs-lookup"><span data-stu-id="1dade-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="1dade-147">Ga naar **instellingen**, klikt u op **Geavanceerd**, en klik vervolgens op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1dade-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="1dade-148">![Setup - geavanceerde](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - geavanceerde")</span><span class="sxs-lookup"><span data-stu-id="1dade-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="1dade-149">Op de **eenmalige aanmelding op instellingen** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1dade-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="1dade-150">![Eenmalige aanmelding instellingen](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "eenmalige van instellingen")</span><span class="sxs-lookup"><span data-stu-id="1dade-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="1dade-151">Selecteer **inschakelen SAML v2 voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1dade-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="1dade-152">In de klassieke Azure-portal op de **op centrale bureaublad eenmalige aanmelding configureren** pagina, Kopieer de **URL-verlener** waarde en plak deze in de **URL SSO** textbox.</span><span class="sxs-lookup"><span data-stu-id="1dade-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="1dade-153">In de klassieke Azure-portal op de **eenmalige aanmelding configureren op de centrale bureaublad** pagina, Kopieer de **externe aanmeldings-URL** waarde en plak deze in de **aanmeldings-URL voor eenmalige aanmelding** textbox .</span><span class="sxs-lookup"><span data-stu-id="1dade-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="1dade-154">In de klassieke Azure-portal op de **eenmalige aanmelding configureren op de centrale bureaublad** pagina, Kopieer de **Service-URL met eenmalige Sign-Out** waarde en plak deze in de **SSO afmelding URL**textbox.</span><span class="sxs-lookup"><span data-stu-id="1dade-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="1dade-155">In de **bericht handtekening verificatiemethode** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1dade-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="1dade-156">![Handtekening verificatiemethode bericht](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "bericht handtekening verificatiemethode")</span><span class="sxs-lookup"><span data-stu-id="1dade-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="1dade-157">Selecteer **certificaat**.</span><span class="sxs-lookup"><span data-stu-id="1dade-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="1dade-158">Van de **SSO certificaat** selecteert **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="1dade-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="1dade-159">Maak een tekstbestand uit het gedownloade certificaat, Kopieer de inhoud van het tekstbestand en plakt u deze in de **SSO certificaat** veld.</span><span class="sxs-lookup"><span data-stu-id="1dade-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="1dade-160">Zie voor meer informatie [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="1dade-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="1dade-161">Selecteer **een koppeling weergegeven naar de aanmeldingspagina van uw SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="1dade-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="1dade-162">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="1dade-162">Click **Update**.</span></span>
10. <span data-ttu-id="1dade-163">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1dade-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="1dade-164">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1dade-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="1dade-165">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="1dade-165">Configure user provisioning</span></span>

<span data-ttu-id="1dade-166">AAD-gebruikers moeten kunnen aanmelden, als ze worden ingericht voor de toepassing centrale bureaublad.</span><span class="sxs-lookup"><span data-stu-id="1dade-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="1dade-167">Deze sectie beschrijft het maken van gebruikersaccounts van AAD in centrale bureaublad.</span><span class="sxs-lookup"><span data-stu-id="1dade-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="1dade-168">**Voor het inrichten van gebruikersaccounts naar centrale bureaublad:**</span><span class="sxs-lookup"><span data-stu-id="1dade-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="1dade-169">Aanmelden bij uw tenant centrale bureaublad.</span><span class="sxs-lookup"><span data-stu-id="1dade-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="1dade-170">Ga naar **mensen \> interne leden**.</span><span class="sxs-lookup"><span data-stu-id="1dade-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="1dade-171">Klik op **interne leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1dade-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="1dade-172">![Mensen](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "personen")</span><span class="sxs-lookup"><span data-stu-id="1dade-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="1dade-173">In de **e-mailadres van nieuwe leden** textbox, typt u een AAD-account u wilt inrichten, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1dade-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="1dade-174">![E-mailadressen van nieuwe leden](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "e-mailadressen van nieuwe leden")</span><span class="sxs-lookup"><span data-stu-id="1dade-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="1dade-175">Klik op **interne toevoegen leden**.</span><span class="sxs-lookup"><span data-stu-id="1dade-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="1dade-176">![Interne lid toevoegen](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "interne lid toevoegen")</span><span class="sxs-lookup"><span data-stu-id="1dade-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1dade-177">De gebruikers die u hebt toegevoegd, ontvangt een e-mailbericht met een bevestigingskoppeling moet worden geklikt om de account te activeren.</span><span class="sxs-lookup"><span data-stu-id="1dade-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="1dade-178">U kunt andere centrale bureaublad gebruiker account hulpmiddelen voor het maken of API's die is geleverd door centrale bureaublad aan inrichten AAD-gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="1dade-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="1dade-179">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="1dade-179">Assign users</span></span>
<span data-ttu-id="1dade-180">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="1dade-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="1dade-181">**Gebruikers om aan te wijzen centrale bureaublad, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1dade-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="1dade-182">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="1dade-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1dade-183">Op de **centrale bureaublad** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="1dade-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1dade-184">![Gebruikers toewijzen](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="1dade-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="1dade-185">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="1dade-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="1dade-186">![Ja](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="1dade-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1dade-187">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1dade-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1dade-188">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1dade-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

