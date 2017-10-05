---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Informatie over het gebruik van Salesforce Sandbox met Azure Active Directory om te schakelen eenmalige aanmelding, geautomatiseerde inrichting en meer!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="78dbd-103">Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="78dbd-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="78dbd-104">Het doel van deze zelfstudie is om de integratie van Azure en Salesforce Sandbox weer te geven.</span><span class="sxs-lookup"><span data-stu-id="78dbd-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="78dbd-105">Zie voor feedback over de [Azure ondersteuningspagina](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="78dbd-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="78dbd-106">Sandboxes bieden u de mogelijkheid meerdere kopieën van uw organisatie in een afzonderlijke omgeving voor verschillende doeleinden, zoals ontwikkeling, testen en training, zonder verlies van gegevens en toepassingen in uw productieomgeving Salesforce maken de organisatie.</span><span class="sxs-lookup"><span data-stu-id="78dbd-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="78dbd-107">Zie voor meer informatie [sandbox-overzicht](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="78dbd-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="78dbd-108">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="78dbd-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="78dbd-109">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="78dbd-109">A valid Azure subscription</span></span>
* <span data-ttu-id="78dbd-110">Een sandbox in Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="78dbd-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="78dbd-111">Als u nog een geldige sandbox in Salesforce.com hebt, moet u contact opnemen met Salesforce.</span><span class="sxs-lookup"><span data-stu-id="78dbd-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="78dbd-112">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="78dbd-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="78dbd-113">De integratie van toepassingen voor Salesforce Sandbox inschakelen</span><span class="sxs-lookup"><span data-stu-id="78dbd-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="78dbd-114">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="78dbd-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="78dbd-115">Uw domein inschakelen</span><span class="sxs-lookup"><span data-stu-id="78dbd-115">Enabling your domain</span></span>
4. <span data-ttu-id="78dbd-116">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="78dbd-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="78dbd-117">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="78dbd-117">Assigning users</span></span>

<span data-ttu-id="78dbd-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="78dbd-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="78dbd-119">De integratie van toepassingen voor Salesforce Sandbox inschakelen</span><span class="sxs-lookup"><span data-stu-id="78dbd-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="78dbd-120">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor Salesforce sandbox overzicht.</span><span class="sxs-lookup"><span data-stu-id="78dbd-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="78dbd-121">**Schakel de integratie van toepassingen voor Salesforce sandbox door de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78dbd-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="78dbd-122">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="78dbd-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="78dbd-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="78dbd-124">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="78dbd-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="78dbd-125">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="78dbd-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="78dbd-126">![Toepassingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="78dbd-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="78dbd-127">Openen van de **Toepassingsgalerie**, klikt u op **een App toevoegen**, en klik vervolgens op **toevoegen van een toepassing voor mijn organisatie te gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="78dbd-128">![Wat wilt u doen? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Wat wilt u doen?")</span><span class="sxs-lookup"><span data-stu-id="78dbd-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="78dbd-129">In de **zoekvak**, type **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="78dbd-130">![Toepassingsgalerie](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="78dbd-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="78dbd-131">Selecteer in het deelvenster met resultaten **Salesforce Sandbox**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="78dbd-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="78dbd-132">![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="78dbd-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="78dbd-133">Configur eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="78dbd-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="78dbd-134">Het doel van deze sectie is om een overzicht van gebruikers te verifiëren bij Salesforce met hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="78dbd-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="78dbd-135">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78dbd-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="78dbd-136">In de klassieke Azure portal op de **Salesforce Sandbox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78dbd-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="78dbd-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="78dbd-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="78dbd-138">Op de **hoe wilt u dat gebruikers zich aanmelden op voor de Salesforce Sandbox** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="78dbd-139">![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="78dbd-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="78dbd-140">Op de **App-URL configureren** pagina in de **aanmelding op URL** textbox, typ uw URL met het volgende patroon volgen `http://company.my.salesforce.com`, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="78dbd-141">![App-URL configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="78dbd-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="78dbd-142">Als u al eenmalige aanmelding voor een ander exemplaar van Salesforce Sandbox hebt geconfigureerd in uw directory, dan moet u ook configureren de **id** hebben dezelfde waarde als de **aanmelden URL**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="78dbd-143">De **id** veld kan worden gevonden door het controleren van de **weergeven geavanceerde instellingen** selectievakje op het **App-URL configureren** pagina van het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78dbd-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="78dbd-144">Op de **eenmalige aanmelding configureren op de Salesforce Sandbox** pagina, klikt u op **certificaat downloaden**, en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="78dbd-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="78dbd-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="78dbd-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="78dbd-146">In een ander browservenster, meld u bij uw Salesforce-sandbox als beheerder.</span><span class="sxs-lookup"><span data-stu-id="78dbd-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="78dbd-147">Klik in het menu bovenaan op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="78dbd-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="78dbd-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="78dbd-149">Klik in het navigatievenster aan de linkerkant op **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="78dbd-150">![Eenmalige aanmelding instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="78dbd-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="78dbd-151">Voer de volgende stappen uit in de sectie instellingen voor eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="78dbd-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="78dbd-152">![Eenmalige aanmelding instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="78dbd-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="78dbd-153">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="78dbd-154">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-154">Click **New**.</span></span>
10. <span data-ttu-id="78dbd-155">Voer de volgende stappen uit in de sectie SAML Single Sign-On-instellingen:</span><span class="sxs-lookup"><span data-stu-id="78dbd-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="78dbd-156">![SAML eenmalige aanmelding-instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="78dbd-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="78dbd-157">Typ de naam van de configuratie in het tekstvak naam (bijvoorbeeld: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="78dbd-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="78dbd-158">In de klassieke Azure-portal op de **op Salesforce Sandbox eenmalige aanmelding configureren** dialoog pagina, Kopieer de **URL-verlener** waarde en plak deze in de **verlener** tekstvak.</span><span class="sxs-lookup"><span data-stu-id="78dbd-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="78dbd-159">In de **entiteit-Id** textbox type **https://test.salesforce.com** als dit het eerste exemplaar van Salesforce Sandbox die u aan uw directory toevoegen wilt.</span><span class="sxs-lookup"><span data-stu-id="78dbd-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="78dbd-160">Als u al hebt toegevoegd een exemplaar van Salesforce-Sandbox vervolgens voor de **entiteit-ID** typt u in de **aanmelding op URL**, die moet worden in deze indeling:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="78dbd-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="78dbd-161">Klik op **Bladeren** om de gedownloade certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="78dbd-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="78dbd-162">Als **SAML identiteitstype**, selecteer **Assertion bevat de Federation-ID van het gebruikersobject**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="78dbd-163">Als **SAML identiteit locatie**, selecteer **identiteit is in het element NameIdentifier van het onderwerp overzicht**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="78dbd-164">In de klassieke Azure-portal op de **op Salesforce Sandbox eenmalige aanmelding configureren** dialoog pagina, Kopieer de **externe aanmeldings-URL** waarde en plak deze in de **identiteit Provider aanmeldings-URL**  textbox.</span><span class="sxs-lookup"><span data-stu-id="78dbd-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="78dbd-165">SFDC biedt geen ondersteuning voor SAML-afmelden.</span><span class="sxs-lookup"><span data-stu-id="78dbd-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="78dbd-166">Als een tijdelijke oplossing 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' te plakken in de **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="78dbd-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="78dbd-167">Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="78dbd-168">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-168">Click **Save**.</span></span>
11. <span data-ttu-id="78dbd-169">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78dbd-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="78dbd-170">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="78dbd-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="78dbd-171">Uw domein inschakelen</span><span class="sxs-lookup"><span data-stu-id="78dbd-171">Enable your domain</span></span>
<span data-ttu-id="78dbd-172">Deze sectie wordt ervan uitgegaan dat u al hebt gemaakt een domein.</span><span class="sxs-lookup"><span data-stu-id="78dbd-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="78dbd-173">Zie voor meer informatie [definiëren van uw domeinnaam](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="78dbd-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="78dbd-174">**Als u wilt maken voor uw domein, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78dbd-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="78dbd-175">Klik in het navigatiedeelvenster links op **domeinbeheer**, en klik vervolgens op **mijn domein.**</span><span class="sxs-lookup"><span data-stu-id="78dbd-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="78dbd-176">![Mijn domein](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="78dbd-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="78dbd-177">Zorg dat uw domein correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="78dbd-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="78dbd-178">In de **pagina aanmeldingsinstellingen** sectie, klikt u op **bewerken**, naarmate **verificatieservice**, selecteert u de naam van de SAML Single Sign-On-instelling van de vorige sectie en klik tot slot **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="78dbd-179">![Mijn domein](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="78dbd-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="78dbd-180">Als u een domein geconfigureerd hebt, moeten uw gebruikers de domein-URL voor aanmelding bij de sandbox Salesforce gebruiken.</span><span class="sxs-lookup"><span data-stu-id="78dbd-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="78dbd-181">Als u de waarde van de URL, klikt u op de SSO-profiel dat u hebt gemaakt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="78dbd-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="78dbd-182">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="78dbd-182">Configure user provisioning</span></span>
<span data-ttu-id="78dbd-183">Het doel van deze sectie is het inschakelen van de gebruiker het inrichten van Active Directory-gebruikersaccounts met Salesforce Sandbox overzicht.</span><span class="sxs-lookup"><span data-stu-id="78dbd-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="78dbd-184">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78dbd-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="78dbd-185">Selecteer uw naam om uw gebruikersmenu te openen in de bovenste navigatiebalk de Salesforce-Portal:</span><span class="sxs-lookup"><span data-stu-id="78dbd-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="78dbd-186">![Mijn instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Mijn instellingen")</span><span class="sxs-lookup"><span data-stu-id="78dbd-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="78dbd-187">Selecteer in het gebruikersmenu **Mijn instellingen** openen uw **Mijn instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="78dbd-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="78dbd-188">Klik in het linkerdeelvenster op **persoonlijke** Vouw het persoonlijke gedeelte uit en klik vervolgens op **opnieuw mijn beveiligingstoken**:</span><span class="sxs-lookup"><span data-stu-id="78dbd-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="78dbd-189">![Mijn instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Mijn instellingen")</span><span class="sxs-lookup"><span data-stu-id="78dbd-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="78dbd-190">Op de **opnieuw mijn beveiligingstoken** pagina, klikt u op **Security Token opnieuw** om aan te vragen van een e-mailbericht met uw beveiligingstoken Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="78dbd-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="78dbd-191">![Nieuw Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "nieuw Token")</span><span class="sxs-lookup"><span data-stu-id="78dbd-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="78dbd-192">Controleer uw postvak voor een e-mailbericht van Salesforce.com met '**salesforce.com.com beveiligingsgegevens**' als onderwerp.</span><span class="sxs-lookup"><span data-stu-id="78dbd-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="78dbd-193">Bekijk dit e-mailbericht en kopieer de waarde voor het token.</span><span class="sxs-lookup"><span data-stu-id="78dbd-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="78dbd-194">In de klassieke Azure portal op de **salesforce Sandbox** pagina van de integratie van toepassing, klikt u op **configureren gebruikersaanvragen** openen de **gebruikersaanvragen configureren** het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78dbd-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="78dbd-195">![Configureer gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "gebruikers inrichten configureren")</span><span class="sxs-lookup"><span data-stu-id="78dbd-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="78dbd-196">Op de **Voer uw referenties in Salesforce Sandbox zodat automatisch gebruikers inrichten** pagina, bieden de volgende configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="78dbd-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="78dbd-197">![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="78dbd-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="78dbd-198">In de **Salesforce Sandbox-Beheerdersgebruikersnaam** textbox type een sandbox met Salesforce-accountnaam met de **systeembeheerder** profiel in Salesforce.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="78dbd-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="78dbd-199">In de **Salesforce Sandbox beheerderswachtwoord** textbox, typt u het wachtwoord voor dit account.</span><span class="sxs-lookup"><span data-stu-id="78dbd-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="78dbd-200">In de **gebruiker beveiligingstoken** textbox, plak de security token waarde.</span><span class="sxs-lookup"><span data-stu-id="78dbd-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="78dbd-201">Klik op **valideren** om te controleren of uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="78dbd-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="78dbd-202">Klik op de **volgende** te openen de **bevestiging** pagina.</span><span class="sxs-lookup"><span data-stu-id="78dbd-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="78dbd-203">Op de **bevestiging** pagina, klikt u op **Complete** aan uw configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="78dbd-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="78dbd-204">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="78dbd-204">Assigning users</span></span>

<span data-ttu-id="78dbd-205">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="78dbd-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="78dbd-206">**Als u gebruikers toewijzen aan de Salesforce Sandbox, wilt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78dbd-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="78dbd-207">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="78dbd-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="78dbd-208">Op de ** Salesforce Sandbox ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="78dbd-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="78dbd-209">![Gebruikers toewijzen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="78dbd-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="78dbd-210">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="78dbd-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="78dbd-211">![Ja](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="78dbd-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="78dbd-212">U moet nu wacht tien minuten en controleer of dat het account bij Salesforce Sandbox is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="78dbd-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="78dbd-213">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="78dbd-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="78dbd-214">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="78dbd-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

