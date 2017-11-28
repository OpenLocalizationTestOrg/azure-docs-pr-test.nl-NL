---
title: 'Zelfstudie: Azure Active Directory-integratie met centraal bureaublad | Microsoft Docs'
description: Lees hoe toouse centrale bureaublad met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="e0920-103">Zelfstudie: Azure Active Directory-integratie met centraal bureaublad</span><span class="sxs-lookup"><span data-stu-id="e0920-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="e0920-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en centrale bureaublad.</span><span class="sxs-lookup"><span data-stu-id="e0920-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="e0920-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e0920-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="e0920-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e0920-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e0920-107">Een centrale bureaublad eenmalige aanmelding ingeschakeld abonnement / tenant-centrale bureaublad</span><span class="sxs-lookup"><span data-stu-id="e0920-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="e0920-108">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0920-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="e0920-109">Hallo toepassingsintegratie voor centrale bureaublad inschakelen</span><span class="sxs-lookup"><span data-stu-id="e0920-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="e0920-110">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="e0920-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="e0920-111">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="e0920-111">Configuring user provisioning</span></span>
* <span data-ttu-id="e0920-112">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e0920-112">Assigning users</span></span>

<span data-ttu-id="e0920-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="e0920-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="e0920-114">Integratie van Hallo-toepassing voor centrale bureaublad inschakelen</span><span class="sxs-lookup"><span data-stu-id="e0920-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="e0920-115">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor centrale bureaublad.</span><span class="sxs-lookup"><span data-stu-id="e0920-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="e0920-116">**tooenable hello toepassingsintegratie voor centrale bureaublad Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e0920-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="e0920-117">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0920-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="e0920-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e0920-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e0920-119">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="e0920-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="e0920-120">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0920-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="e0920-121">![Toepassingen](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="e0920-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e0920-122">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="e0920-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="e0920-123">![Toepassing toevoegen](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e0920-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e0920-124">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="e0920-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="e0920-125">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e0920-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e0920-126">In Hallo **zoekvak**, type **centrale bureaublad**.</span><span class="sxs-lookup"><span data-stu-id="e0920-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="e0920-127">![Toepassingsgalerie](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "-toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="e0920-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="e0920-128">Selecteer in het deelvenster met resultaten Hallo **centrale bureaublad**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e0920-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="e0920-129">![Centrale bureaublad](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "centrale bureaublad")</span><span class="sxs-lookup"><span data-stu-id="e0920-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e0920-130">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="e0920-130">Configure single sign-on</span></span>

<span data-ttu-id="e0920-131">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooCentral bureaublad aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="e0920-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="e0920-132">Als onderdeel van deze procedure bent u vereiste tooupload een Base64-gecodeerde certificaat tooyour centrale Desktop-tenant.</span><span class="sxs-lookup"><span data-stu-id="e0920-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="e0920-133">Als u niet bekend met deze procedure bent, Zie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="e0920-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="e0920-134">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e0920-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="e0920-135">In de klassieke Azure-portal op Hallo Hallo **centrale bureaublad** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen Hallo ** configureren eenmalige aanmelding ** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e0920-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="e0920-136">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e0920-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="e0920-137">Op Hallo **wilt u hoe gebruikers toosign op tooCentral bureaublad** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e0920-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="e0920-138">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e0920-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="e0920-139">Op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="e0920-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="e0920-140">In Hallo **centrale bureaublad aanmelding In URL** textbox type Hallo-URL van uw tenant centrale bureaublad (bijvoorbeeld: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="e0920-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="e0920-141">In een tekstvak Hallo centrale bureaublad antwoord-URL, typt u uw centrale bureaublad AssertionConsumerService URL (bijvoorbeeld: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="e0920-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e0920-142">U kunt benutten Hallo Hallo centrale bureaublad metagegevens (bijvoorbeeld: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="e0920-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="e0920-143">![App-URL configureren](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="e0920-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="e0920-144">Op Hallo **op centrale bureaublad eenmalige aanmelding configureren** pagina, toodownload uw certificaat, klik op **certificaat downloaden**, en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e0920-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="e0920-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e0920-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="e0920-146">Meld u bij tooyour **centrale bureaublad** tenant.</span><span class="sxs-lookup"><span data-stu-id="e0920-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="e0920-147">Ga te**instellingen**, klikt u op **Geavanceerd**, en klik vervolgens op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e0920-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="e0920-148">![Setup - geavanceerde](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - geavanceerde")</span><span class="sxs-lookup"><span data-stu-id="e0920-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="e0920-149">Op Hallo **eenmalige aanmelding op instellingen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0920-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="e0920-150">![Eenmalige aanmelding instellingen](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "eenmalige van instellingen")</span><span class="sxs-lookup"><span data-stu-id="e0920-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="e0920-151">Selecteer **inschakelen SAML v2 voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e0920-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="e0920-152">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de centrale bureaublad** pagina, kopie Hallo **URL-verlener** waarde en plak deze in Hallo **URL SSO** textbox.</span><span class="sxs-lookup"><span data-stu-id="e0920-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="e0920-153">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de centrale bureaublad** pagina, kopie Hallo **externe aanmeldings-URL** waarde en plak deze in Hallo **aanmeldings-URL voor eenmalige aanmelding**textbox.</span><span class="sxs-lookup"><span data-stu-id="e0920-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="e0920-154">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de centrale bureaublad** pagina, kopie Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **SSO afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e0920-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="e0920-155">In Hallo **bericht handtekening verificatiemethode** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0920-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e0920-156">![Handtekening verificatiemethode bericht](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "bericht handtekening verificatiemethode")</span><span class="sxs-lookup"><span data-stu-id="e0920-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="e0920-157">Selecteer **certificaat**.</span><span class="sxs-lookup"><span data-stu-id="e0920-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="e0920-158">Van Hallo **SSO certificaat** selecteert **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="e0920-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="e0920-159">Maak een tekstbestand van Hallo gedownload certificaat, kopie Hallo inhoud van het tekstbestand hello, en plak deze in Hallo **SSO certificaat** veld.</span><span class="sxs-lookup"><span data-stu-id="e0920-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="e0920-160">Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="e0920-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="e0920-161">Selecteer **een koppeling tooyour SAMLv2-aanmeldingspagina weergegeven**.</span><span class="sxs-lookup"><span data-stu-id="e0920-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="e0920-162">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="e0920-162">Click **Update**.</span></span>
10. <span data-ttu-id="e0920-163">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e0920-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="e0920-164">![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e0920-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="e0920-165">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="e0920-165">Configure user provisioning</span></span>

<span data-ttu-id="e0920-166">Voor AAD gebruikers toobe kunnen toosign in, moeten ze ingerichte toohello centrale bureaubladtoepassingen zijn.</span><span class="sxs-lookup"><span data-stu-id="e0920-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="e0920-167">Deze sectie beschrijft hoe toocreate AAD gebruikersaccounts in centrale bureaublad.</span><span class="sxs-lookup"><span data-stu-id="e0920-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="e0920-168">**tooprovision gebruiker accounts tooCentral bureaublad:**</span><span class="sxs-lookup"><span data-stu-id="e0920-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="e0920-169">Meld u bij tooyour centrale bureaublad tenant.</span><span class="sxs-lookup"><span data-stu-id="e0920-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="e0920-170">Ga te**mensen \> interne leden**.</span><span class="sxs-lookup"><span data-stu-id="e0920-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="e0920-171">Klik op **interne leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e0920-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="e0920-172">![Mensen](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "personen")</span><span class="sxs-lookup"><span data-stu-id="e0920-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="e0920-173">In Hallo **e-mailadres van nieuwe leden** textbox, typt u een AAD-account u wilt tooprovision en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e0920-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="e0920-174">![E-mailadressen van nieuwe leden](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "e-mailadressen van nieuwe leden")</span><span class="sxs-lookup"><span data-stu-id="e0920-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="e0920-175">Klik op **interne toevoegen leden**.</span><span class="sxs-lookup"><span data-stu-id="e0920-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="e0920-176">![Interne lid toevoegen](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "interne lid toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e0920-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e0920-177">Hallo-gebruikers die u hebt toegevoegd, ontvangt een e-mailbericht met een bevestigingskoppeling ze tooclick tooactivate Hallo-account nodig.</span><span class="sxs-lookup"><span data-stu-id="e0920-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="e0920-178">U kunt andere centrale bureaublad gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door centrale bureaublad tooprovision AAD-gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="e0920-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="e0920-179">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e0920-179">Assign users</span></span>
<span data-ttu-id="e0920-180">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="e0920-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="e0920-181">**tooassign gebruikers tooCentral bureaublad Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e0920-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="e0920-182">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="e0920-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e0920-183">Op Hallo **centrale bureaublad** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="e0920-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e0920-184">![Gebruikers toewijzen](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="e0920-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="e0920-185">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e0920-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="e0920-186">![Ja](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="e0920-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e0920-187">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="e0920-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e0920-188">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e0920-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

