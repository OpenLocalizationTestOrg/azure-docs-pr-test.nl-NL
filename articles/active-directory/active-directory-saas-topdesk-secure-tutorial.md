---
title: 'Zelfstudie: Azure Active Directory-integratie met TOPdesk - beveiligde | Microsoft Docs'
description: Meer informatie over hoe toouse TOPdesk - beveiligen met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="e93a7-103">Zelfstudie: Azure Active Directory-integratie met TOPdesk - beveiligen</span><span class="sxs-lookup"><span data-stu-id="e93a7-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="e93a7-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en TOPdesk - beveiligen.</span><span class="sxs-lookup"><span data-stu-id="e93a7-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="e93a7-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e93a7-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="e93a7-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e93a7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e93a7-107">Een TOPdesk - beveiligde eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e93a7-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="e93a7-108">Na het voltooien van deze zelfstudie, hello Azure AD-gebruikers hebt u tooTOPdesk - beveiligde wordt toegewezen worden kunnen toosingle Meld u aan bij de toepassing hello op uw TOPdesk - beveiligd bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [Inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e93a7-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="e93a7-109">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="e93a7-110">Hallo toepassingsintegratie voor TOPdesk - beveiligde inschakelen</span><span class="sxs-lookup"><span data-stu-id="e93a7-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="e93a7-111">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="e93a7-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="e93a7-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="e93a7-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="e93a7-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e93a7-113">Assigning users</span></span>

<span data-ttu-id="e93a7-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="e93a7-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="e93a7-115">Hallo toepassingsintegratie voor TOPdesk - beveiligde inschakelen</span><span class="sxs-lookup"><span data-stu-id="e93a7-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="e93a7-116">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor TOPdesk - veilig.</span><span class="sxs-lookup"><span data-stu-id="e93a7-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="e93a7-117">tooenable hello toepassingsintegratie voor TOPdesk - wilt beveiligen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="e93a7-118">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="e93a7-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e93a7-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="e93a7-120">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="e93a7-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="e93a7-121">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="e93a7-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="e93a7-122">![Toepassingen](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="e93a7-123">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="e93a7-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="e93a7-124">![Toepassing toevoegen](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="e93a7-125">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="e93a7-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="e93a7-127">In Hallo **zoekvak**, type **TOPdesk - beveiligde**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="e93a7-128">![Toepassingsgalerie](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="e93a7-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="e93a7-129">Selecteer in het deelvenster met resultaten Hallo **TOPdesk - beveiligde**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e93a7-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="e93a7-130">![TOPdesk - beveiligde](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - beveiligen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="e93a7-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="e93a7-131">Configuring single sign-on</span></span>
<span data-ttu-id="e93a7-132">Hallo-doel van deze sectie is het toooutline hoe tooenable gebruikers tooauthenticate tooTOPdesk - beveiligen met een account in Azure AD dat gebruikmaakt van Federatie op basis van Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="e93a7-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="e93a7-133">Vereist de tooupload een pictogrambestand logo configureren eenmalige aanmelding voor TOPdesk - veilig.</span><span class="sxs-lookup"><span data-stu-id="e93a7-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="e93a7-134">tooget pictogrambestand hello, neem contact op met Hallo TOPdesk ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="e93a7-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="e93a7-135">tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="e93a7-136">Meld u aan bij tooyour **TOPdesk - beveiligde** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e93a7-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="e93a7-137">In Hallo **TOPdesk** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="e93a7-138">![Instellingen](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="e93a7-139">Klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="e93a7-140">![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "aanmeldingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="e93a7-141">Vouw Hallo **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="e93a7-142">![Algemene](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "algemeen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="e93a7-143">In Hallo **Secure** sectie Hallo **SAML aanmelding** configuratie sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e93a7-144">![Instellingen voor technische](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "technische instellingen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="e93a7-145">a.</span><span class="sxs-lookup"><span data-stu-id="e93a7-145">a.</span></span> <span data-ttu-id="e93a7-146">Klik op **downloaden** toodownload openbare metagegevensbestand Hallo en lokaal opslaan op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e93a7-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="e93a7-147">b.</span><span class="sxs-lookup"><span data-stu-id="e93a7-147">b.</span></span> <span data-ttu-id="e93a7-148">Open metagegevensbestand hello, en Ga naar Hallo **AssertionConsumerService** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="e93a7-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="e93a7-149">![Verklaring Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer-Service")</span><span class="sxs-lookup"><span data-stu-id="e93a7-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="e93a7-150">c.</span><span class="sxs-lookup"><span data-stu-id="e93a7-150">c.</span></span> <span data-ttu-id="e93a7-151">Kopiëren Hallo **AssertionConsumerService** waarde.</span><span class="sxs-lookup"><span data-stu-id="e93a7-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="e93a7-152">U moet Hallo waarde in Hallo **App-URL configureren** verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e93a7-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="e93a7-153">In een ander browservenster, meld u aan bij uw **klassieke Azure-portal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e93a7-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="e93a7-154">Op Hallo **TOPdesk - beveiligde** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen Hallo ** configureren eenmalige aanmelding ** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e93a7-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="e93a7-155">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e93a7-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="e93a7-156">Op Hallo **hoe wilt u beveiligen zoals gebruikers toosign op tooTOPdesk -** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="e93a7-157">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e93a7-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="e93a7-158">Op Hallo **App-URL configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e93a7-159">![App-URL configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="e93a7-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="e93a7-160">a.</span><span class="sxs-lookup"><span data-stu-id="e93a7-160">a.</span></span> <span data-ttu-id="e93a7-161">In Hallo **TOPdesk - beveiligde aanmelding op URL** textbox type Hallo-URL die door uw gebruikers toosign wordt gebruikt in uw TOPdesk - beveiligde toepassing (bijvoorbeeld: '*https://qssolutions.topdesk.net*').</span><span class="sxs-lookup"><span data-stu-id="e93a7-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="e93a7-162">b.</span><span class="sxs-lookup"><span data-stu-id="e93a7-162">b.</span></span> <span data-ttu-id="e93a7-163">In Hallo **TOPdesk – openbare antwoord-URL** textbox plakken Hallo **TOPdesk - beveiligde AssertionConsumerService URL** (bijvoorbeeld: '*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="e93a7-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="e93a7-164">c.</span><span class="sxs-lookup"><span data-stu-id="e93a7-164">c.</span></span> <span data-ttu-id="e93a7-165">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-165">Click **Next**.</span></span>

10. <span data-ttu-id="e93a7-166">Op Hallo **eenmalige aanmelding configureren op TOPdesk - beveiligde** pagina, toodownload uw bestand met metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo bestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e93a7-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="e93a7-167">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e93a7-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="e93a7-168">een certificaatbestand toocreate uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="e93a7-169">![Certificaat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "certificaat")</span><span class="sxs-lookup"><span data-stu-id="e93a7-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="e93a7-170">a.</span><span class="sxs-lookup"><span data-stu-id="e93a7-170">a.</span></span> <span data-ttu-id="e93a7-171">Open Hallo gedownloade metagegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="e93a7-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="e93a7-172">b.</span><span class="sxs-lookup"><span data-stu-id="e93a7-172">b.</span></span> <span data-ttu-id="e93a7-173">Vouw Hallo **RoleDescriptor** knooppunt met een **xsi: type** van **ingevoerd: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="e93a7-174">c.</span><span class="sxs-lookup"><span data-stu-id="e93a7-174">c.</span></span> <span data-ttu-id="e93a7-175">Kopieer de waarde Hallo Hallo **X509Certificate** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="e93a7-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="e93a7-176">d.</span><span class="sxs-lookup"><span data-stu-id="e93a7-176">d.</span></span> <span data-ttu-id="e93a7-177">Opslaan Hallo gekopieerd **X509Certificate** waarde lokaal op uw computer in een bestand.</span><span class="sxs-lookup"><span data-stu-id="e93a7-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="e93a7-178">Op uw TOPdesk - beveiligd bedrijf site in Hallo **TOPdesk** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="e93a7-179">![Instellingen](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="e93a7-180">Klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="e93a7-181">![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "aanmeldingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="e93a7-182">Vouw Hallo **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="e93a7-183">![Algemene](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "algemeen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="e93a7-184">In Hallo **openbare** sectie, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="e93a7-185">![Voeg](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="e93a7-186">Op Hallo **SAML-configuratie-assistent** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="e93a7-187">![SAML-configuratie-assistent](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "assistent voor SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="e93a7-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="e93a7-188">a.</span><span class="sxs-lookup"><span data-stu-id="e93a7-188">a.</span></span> <span data-ttu-id="e93a7-189">de metagegevens van het gedownloade bestand, onder tooupload **Federatiemetagegevens**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="e93a7-190">b.</span><span class="sxs-lookup"><span data-stu-id="e93a7-190">b.</span></span> <span data-ttu-id="e93a7-191">uw certificaat bestand onder tooupload **certificaat (RSA)**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="e93a7-192">c.</span><span class="sxs-lookup"><span data-stu-id="e93a7-192">c.</span></span> <span data-ttu-id="e93a7-193">tooupload Hallo logo-bestand die u hebt gekregen Hallo TOPdesk ondersteuningsteam, onder **Logo pictogram**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="e93a7-194">d.</span><span class="sxs-lookup"><span data-stu-id="e93a7-194">d.</span></span> <span data-ttu-id="e93a7-195">In Hallo **naam gebruikerskenmerk** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="e93a7-196">e.</span><span class="sxs-lookup"><span data-stu-id="e93a7-196">e.</span></span> <span data-ttu-id="e93a7-197">In Hallo **weergavenaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="e93a7-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="e93a7-198">f.</span><span class="sxs-lookup"><span data-stu-id="e93a7-198">f.</span></span> <span data-ttu-id="e93a7-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-199">Click **Save**.</span></span>

17. <span data-ttu-id="e93a7-200">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e93a7-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="e93a7-201">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e93a7-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="e93a7-202">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="e93a7-202">Configuring user provisioning</span></span>
<span data-ttu-id="e93a7-203">In de volgorde tooenable Azure AD-gebruikers toolog in TOPdesk - veilige, ze moeten worden ingericht in TOPdesk - veilig.</span><span class="sxs-lookup"><span data-stu-id="e93a7-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="e93a7-204">In geval van TOPdesk - Hallo veilige, inrichting is een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e93a7-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="e93a7-205">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="e93a7-206">Meld u aan bij tooyour **TOPdesk - beveiligde** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="e93a7-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="e93a7-207">Klik in het menu bovenaan Hallo Hallo **TOPdesk \> nieuw \> ondersteuningsbestanden \> Operator**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="e93a7-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span><span class="sxs-lookup"><span data-stu-id="e93a7-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="e93a7-209">Op Hallo **Operator New** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="e93a7-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="e93a7-210">![Nieuwe Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "nieuwe Operator")</span><span class="sxs-lookup"><span data-stu-id="e93a7-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="e93a7-211">a.</span><span class="sxs-lookup"><span data-stu-id="e93a7-211">a.</span></span> <span data-ttu-id="e93a7-212">Klik op tabblad Algemeen van Hallo.</span><span class="sxs-lookup"><span data-stu-id="e93a7-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="e93a7-213">b.</span><span class="sxs-lookup"><span data-stu-id="e93a7-213">b.</span></span> <span data-ttu-id="e93a7-214">In Hallo **achternaam** textbox Hallo **algemene** sectie, type Hallo achternaam van een geldige Azure Active Directory-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="e93a7-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="e93a7-215">c.</span><span class="sxs-lookup"><span data-stu-id="e93a7-215">c.</span></span> <span data-ttu-id="e93a7-216">Selecteer een **Site** voor Hallo-account in Hallo **locatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="e93a7-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="e93a7-217">d.</span><span class="sxs-lookup"><span data-stu-id="e93a7-217">d.</span></span> <span data-ttu-id="e93a7-218">In Hallo **aanmeldingsnaam** textbox Hallo **TOPdesk aanmelding** sectie, typt u een aanmeldingsnaam voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e93a7-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="e93a7-219">e.</span><span class="sxs-lookup"><span data-stu-id="e93a7-219">e.</span></span> <span data-ttu-id="e93a7-220">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="e93a7-221">U kunt andere TOPdesk - beveiligde gebruikersaccount hulpmiddelen voor het maken of API's die worden geleverd door TOPdesk - Secure tooprovision AAD-gebruikersaccounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e93a7-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="e93a7-222">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e93a7-222">Assigning users</span></span>
<span data-ttu-id="e93a7-223">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="e93a7-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="e93a7-224">tooassign gebruikers tooTOPdesk - beveiligen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e93a7-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="e93a7-225">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="e93a7-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e93a7-226">Op Hallo ** TOPdesk - beveiligde ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="e93a7-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="e93a7-227">![Gebruikers toewijzen](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="e93a7-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="e93a7-228">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e93a7-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="e93a7-229">![Ja](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="e93a7-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e93a7-230">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="e93a7-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e93a7-231">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e93a7-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

