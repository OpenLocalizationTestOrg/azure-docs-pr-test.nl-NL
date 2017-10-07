---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Meer informatie over hoe toouse Salesforce Sandbox met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer!.
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
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="e12d5-103">Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="e12d5-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="e12d5-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e12d5-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="e12d5-105">Zie voor feedback over Hallo [Azure ondersteuningspagina](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="e12d5-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="e12d5-106">Sandboxes geven u Hallo mogelijkheid toocreate meerdere kopieën van uw organisatie in een afzonderlijke omgeving voor verschillende doeleinden, zoals ontwikkeling, testen en training, zonder in gevaar te brengen Hallo gegevens en toepassingen in uw productieomgeving Salesforce de organisatie.</span><span class="sxs-lookup"><span data-stu-id="e12d5-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="e12d5-107">Zie voor meer informatie [sandbox-overzicht](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="e12d5-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="e12d5-108">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e12d5-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="e12d5-109">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e12d5-109">A valid Azure subscription</span></span>
* <span data-ttu-id="e12d5-110">Een sandbox in Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="e12d5-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="e12d5-111">Als u nog een geldige sandbox in Salesforce.com hebt, moet u toocontact Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e12d5-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="e12d5-112">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e12d5-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="e12d5-113">Hallo toepassingsintegratie voor Salesforce Sandbox inschakelen</span><span class="sxs-lookup"><span data-stu-id="e12d5-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="e12d5-114">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="e12d5-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="e12d5-115">Uw domein inschakelen</span><span class="sxs-lookup"><span data-stu-id="e12d5-115">Enabling your domain</span></span>
4. <span data-ttu-id="e12d5-116">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="e12d5-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="e12d5-117">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e12d5-117">Assigning users</span></span>

<span data-ttu-id="e12d5-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="e12d5-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="e12d5-119">Hallo toepassingsintegratie voor Salesforce Sandbox inschakelen</span><span class="sxs-lookup"><span data-stu-id="e12d5-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="e12d5-120">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Salesforce sandbox.</span><span class="sxs-lookup"><span data-stu-id="e12d5-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="e12d5-121">**tooenable hello toepassingsintegratie voor Salesforce-sandbox Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e12d5-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="e12d5-122">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="e12d5-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e12d5-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e12d5-124">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="e12d5-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="e12d5-125">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="e12d5-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="e12d5-126">![Toepassingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="e12d5-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e12d5-127">Hallo tooopen **Toepassingsgalerie**, klikt u op **een App toevoegen**, en klik vervolgens op **toevoegen van een toepassing voor mijn organisatie toouse**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="e12d5-128">![Wat wilt u wilt dat toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Wat wilt u wilt dat toodo?")</span><span class="sxs-lookup"><span data-stu-id="e12d5-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="e12d5-129">In Hallo **zoekvak**, type **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="e12d5-130">![Toepassingsgalerie](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="e12d5-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="e12d5-131">Selecteer in het deelvenster met resultaten Hallo **Salesforce Sandbox**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e12d5-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="e12d5-132">![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="e12d5-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="e12d5-133">Configur eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="e12d5-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="e12d5-134">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooSalesforce aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="e12d5-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="e12d5-135">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e12d5-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="e12d5-136">In de klassieke Azure-portal op Hallo Hallo **Salesforce Sandbox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e12d5-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="e12d5-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e12d5-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="e12d5-138">Op Hallo **wilt u hoe gebruikers toosign op tooSalesforce Sandbox** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="e12d5-139">![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="e12d5-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="e12d5-140">Op Hallo **App-URL configureren** pagina in Hallo **aanmelding op URL** textbox, typt u uw URL Hallo patroon volgen met `http://company.my.salesforce.com`, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="e12d5-141">![App-URL configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="e12d5-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="e12d5-142">Als u al eenmalige aanmelding voor een ander exemplaar van Salesforce Sandbox hebt geconfigureerd in uw directory, dan moet u ook Hallo configureren **id** toohave dezelfde waarde als Hallo Hallo **aanmelden URL**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="e12d5-143">Hallo **id** veld kan worden gevonden door te controleren Hallo **weergeven geavanceerde instellingen** selectievakje op Hallo **App-URL configureren** van Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="e12d5-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="e12d5-144">Op Hallo **eenmalige aanmelding configureren op de Salesforce Sandbox** pagina, klikt u op **certificaat downloaden**, en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e12d5-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="e12d5-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e12d5-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="e12d5-146">In een ander browservenster, meld u bij uw Salesforce-sandbox als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e12d5-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="e12d5-147">Klik in het menu bovenaan Hallo Hallo **Setup**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="e12d5-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="e12d5-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="e12d5-149">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="e12d5-150">![Eenmalige aanmelding instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="e12d5-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="e12d5-151">Op Hallo sectie instellingen voor eenmalige aanmelding, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e12d5-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e12d5-152">![Eenmalige aanmelding instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="e12d5-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="e12d5-153">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="e12d5-154">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-154">Click **New**.</span></span>
10. <span data-ttu-id="e12d5-155">Op Hallo SAML Single Sign-On zoekinstellingen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e12d5-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="e12d5-156">![SAML eenmalige aanmelding-instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="e12d5-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="e12d5-157">Typ in Hallo naam textbox Hallo-naam van Hallo-configuratie (bijvoorbeeld: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="e12d5-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="e12d5-158">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de Salesforce Sandbox** dialoog pagina, kopie Hallo **URL-verlener** waarde en plak deze in Hallo **verlener**textbox.</span><span class="sxs-lookup"><span data-stu-id="e12d5-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="e12d5-159">In Hallo **entiteit-Id** textbox type **https://test.salesforce.com** als het Hallo eerste Salesforce sandbox-exemplaar dat u tooyour directory toevoegt.</span><span class="sxs-lookup"><span data-stu-id="e12d5-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="e12d5-160">Als u al een exemplaar van Salesforce Sandbox, moet u voor Hallo hebt toegevoegd **entiteit-ID** type in Hallo **aanmelding op URL**, die moet worden in deze indeling:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e12d5-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="e12d5-161">Klik op **Bladeren** tooupload Hallo certificaat gedownload.</span><span class="sxs-lookup"><span data-stu-id="e12d5-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="e12d5-162">Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="e12d5-163">Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentifier element van Hallo onderwerp instructie**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="e12d5-164">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de Salesforce Sandbox** dialoog pagina, kopie Hallo **externe aanmeldings-URL** waarde en plak deze in Hallo **id-Provider Aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e12d5-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="e12d5-165">SFDC biedt geen ondersteuning voor SAML-afmelden.</span><span class="sxs-lookup"><span data-stu-id="e12d5-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="e12d5-166">Als een tijdelijke oplossing 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' te plakken in Hallo **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e12d5-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="e12d5-167">Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="e12d5-168">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-168">Click **Save**.</span></span>
11. <span data-ttu-id="e12d5-169">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e12d5-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="e12d5-170">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e12d5-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="e12d5-171">Uw domein inschakelen</span><span class="sxs-lookup"><span data-stu-id="e12d5-171">Enable your domain</span></span>
<span data-ttu-id="e12d5-172">Deze sectie wordt ervan uitgegaan dat u al hebt gemaakt een domein.</span><span class="sxs-lookup"><span data-stu-id="e12d5-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="e12d5-173">Zie voor meer informatie [definiëren van uw domeinnaam](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="e12d5-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="e12d5-174">**tooenable uw domein Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="e12d5-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="e12d5-175">Klik in het Hallo navigatiedeelvenster links op **domeinbeheer**, en klik vervolgens op **mijn domein.**</span><span class="sxs-lookup"><span data-stu-id="e12d5-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="e12d5-176">![Mijn domein](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="e12d5-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e12d5-177">Zorg dat uw domein correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e12d5-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="e12d5-178">In Hallo **aanmelding paginainstellingen** sectie, klikt u op **bewerken**, naarmate **verificatieservice**, selecteer Hallo-naam van Hallo SAML Single Sign-On-instelling van de vorige Hallo sectie en ten slotte op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="e12d5-179">![Mijn domein](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="e12d5-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="e12d5-180">Als u een domein geconfigureerd hebt, moeten uw gebruikers Hallo domein URL toologin toohello Salesforce sandbox gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e12d5-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="e12d5-181">tooget Hallo waarde van de URL van de hello, klikt u op Hallo SSO profiel die u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e12d5-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="e12d5-182">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="e12d5-182">Configure user provisioning</span></span>
<span data-ttu-id="e12d5-183">Hallo-doel van deze sectie is het toooutline hoe tooenable gebruikers inrichten van Active Directory-gebruiker accounts tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e12d5-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="e12d5-184">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e12d5-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e12d5-185">Selecteer in de bovenste navigatiebalk Hallo van Hallo Salesforce Portal uw naam tooexpand uw gebruikersmenu:</span><span class="sxs-lookup"><span data-stu-id="e12d5-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="e12d5-186">![Mijn instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Mijn instellingen")</span><span class="sxs-lookup"><span data-stu-id="e12d5-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="e12d5-187">Selecteer in het gebruikersmenu **Mijn instellingen** tooopen uw **Mijn instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="e12d5-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="e12d5-188">Klik in het linkerdeelvenster Hallo **persoonlijke** tooexpand Hallo persoonlijke sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**:</span><span class="sxs-lookup"><span data-stu-id="e12d5-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="e12d5-189">![Mijn instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Mijn instellingen")</span><span class="sxs-lookup"><span data-stu-id="e12d5-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="e12d5-190">Op Hallo **opnieuw mijn beveiligingstoken** pagina, klikt u op **Security Token opnieuw** toorequest een e-mailbericht met uw beveiligingstoken Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="e12d5-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="e12d5-191">![Nieuw Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "nieuw Token")</span><span class="sxs-lookup"><span data-stu-id="e12d5-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="e12d5-192">Controleer uw postvak voor een e-mailbericht van Salesforce.com met '**salesforce.com.com beveiligingsgegevens**' als onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e12d5-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="e12d5-193">Bekijk deze e-mail en kopiëren hello security token waarde.</span><span class="sxs-lookup"><span data-stu-id="e12d5-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="e12d5-194">In de klassieke Azure-portal op Hallo Hallo **salesforce Sandbox** pagina van de integratie van toepassing, klikt u op **configureren gebruikersaanvragen** tooopen hello **configureren gebruikersaanvragen**dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e12d5-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="e12d5-195">![Configureer gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "gebruikers inrichten configureren")</span><span class="sxs-lookup"><span data-stu-id="e12d5-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="e12d5-196">Op Hallo **Voer uw Salesforce-Sandbox referenties tooenable automatisch gebruikers inrichten** pagina, bieden Hallo na configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="e12d5-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="e12d5-197">![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="e12d5-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="e12d5-198">In Hallo **Salesforce Sandbox-Beheerdersgebruikersnaam** textbox type een sandbox met Salesforce accountnaam die heeft Hallo **systeembeheerder** profiel in Salesforce.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e12d5-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="e12d5-199">In Hallo **Salesforce Sandbox beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.</span><span class="sxs-lookup"><span data-stu-id="e12d5-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="e12d5-200">In Hallo **gebruiker beveiligingstoken** textbox plakken hello security token waarde.</span><span class="sxs-lookup"><span data-stu-id="e12d5-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="e12d5-201">Klik op **valideren** tooverify uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="e12d5-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="e12d5-202">Klik op Hallo **volgende** knop tooopen hello **bevestiging** pagina.</span><span class="sxs-lookup"><span data-stu-id="e12d5-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="e12d5-203">Op Hallo **bevestiging** pagina, klikt u op **Complete** toosave uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="e12d5-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="e12d5-204">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e12d5-204">Assigning users</span></span>

<span data-ttu-id="e12d5-205">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="e12d5-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="e12d5-206">**tooassign gebruikers tooSalesforce Sandbox, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e12d5-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="e12d5-207">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="e12d5-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e12d5-208">Op Hallo ** Salesforce Sandbox ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="e12d5-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e12d5-209">![Gebruikers toewijzen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="e12d5-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="e12d5-210">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e12d5-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="e12d5-211">![Ja](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="e12d5-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e12d5-212">U moet nu wacht tien minuten en controleren of de Hallo-account is gesynchroniseerd tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e12d5-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="e12d5-213">Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="e12d5-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="e12d5-214">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="e12d5-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

