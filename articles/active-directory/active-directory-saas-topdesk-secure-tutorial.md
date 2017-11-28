---
title: 'Zelfstudie: Azure Active Directory-integratie met TOPdesk - beveiligde | Microsoft Docs'
description: Informatie over het gebruik van TOPdesk - beveiligen met Azure Active Directory om het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!.
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
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="6ef8f-103">Zelfstudie: Azure Active Directory-integratie met TOPdesk - beveiligen</span><span class="sxs-lookup"><span data-stu-id="6ef8f-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="6ef8f-104">Het doel van deze zelfstudie is het weergeven van de integratie van Azure en TOPdesk - veilig.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="6ef8f-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6ef8f-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="6ef8f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6ef8f-107">Een TOPdesk - beveiligde eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6ef8f-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="6ef8f-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan TOPdesk - veilig kan worden één Meld u aan bij de toepassing op uw TOPdesk - beveiligd bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6ef8f-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6ef8f-109">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="6ef8f-110">De integratie van toepassingen voor TOPdesk - beveiligde inschakelen</span><span class="sxs-lookup"><span data-stu-id="6ef8f-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="6ef8f-111">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="6ef8f-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="6ef8f-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="6ef8f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="6ef8f-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="6ef8f-113">Assigning users</span></span>

<span data-ttu-id="6ef8f-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="6ef8f-115">De integratie van toepassingen voor TOPdesk - beveiligde inschakelen</span><span class="sxs-lookup"><span data-stu-id="6ef8f-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="6ef8f-116">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor TOPdesk - beveiligde overzicht.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="6ef8f-117">Om in te schakelen van de integratie van toepassingen voor TOPdesk - beveiligen, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="6ef8f-118">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="6ef8f-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="6ef8f-120">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="6ef8f-121">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="6ef8f-122">![Toepassingen](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="6ef8f-123">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="6ef8f-124">![Toepassing toevoegen](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="6ef8f-125">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="6ef8f-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="6ef8f-127">In de **zoekvak**, type **TOPdesk - beveiligde**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="6ef8f-128">![Toepassingsgalerie](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="6ef8f-129">Selecteer in het deelvenster met resultaten **TOPdesk - beveiligde**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="6ef8f-130">![TOPdesk - beveiligde](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - beveiligen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="6ef8f-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="6ef8f-131">Configuring single sign-on</span></span>
<span data-ttu-id="6ef8f-132">Het doel van deze sectie is om een overzicht van gebruikers te verifiëren bij TOPdesk - in staat te beveiligen met een account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="6ef8f-133">Configureren eenmalige aanmelding voor TOPdesk - beveiligen, moet u een pictogram logobestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="6ef8f-134">Als u het pictogrambestand, contact op met het ondersteuningsteam TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="6ef8f-135">Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="6ef8f-136">Meld u aan bij uw **TOPdesk - beveiligde** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="6ef8f-137">In de **TOPdesk** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="6ef8f-138">![Instellingen](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="6ef8f-139">Klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="6ef8f-140">![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "aanmeldingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="6ef8f-141">Vouw de **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="6ef8f-142">![Algemene](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "algemeen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="6ef8f-143">In de **Secure** sectie van de **SAML aanmelding** configuratie sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="6ef8f-144">![Instellingen voor technische](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "technische instellingen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="6ef8f-145">a.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-145">a.</span></span> <span data-ttu-id="6ef8f-146">Klik op **downloaden** downloaden van het metagegevensbestand van de openbare en lokaal opslaan op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="6ef8f-147">b.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-147">b.</span></span> <span data-ttu-id="6ef8f-148">Open het metagegevensbestand en Ga naar de **AssertionConsumerService** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="6ef8f-149">![Verklaring Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer-Service")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="6ef8f-150">c.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-150">c.</span></span> <span data-ttu-id="6ef8f-151">Kopieer de **AssertionConsumerService** waarde.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="6ef8f-152">U moet de waarde in de **App-URL configureren** verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="6ef8f-153">In een ander browservenster, meld u aan bij uw **klassieke Azure-portal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="6ef8f-154">Op de **TOPdesk - beveiligde** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de ** configureren eenmalige aanmelding ** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="6ef8f-155">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="6ef8f-156">Op de **hoe wilt u dat gebruikers zich aanmelden op TOPdesk - beveiligde** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="6ef8f-157">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="6ef8f-158">Op de **App-URL configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="6ef8f-159">![App-URL configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="6ef8f-160">a.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-160">a.</span></span> <span data-ttu-id="6ef8f-161">In de **TOPdesk - beveiligde aanmelding op URL** textbox, typ de URL gebruikt door uw gebruikers zich aanmeldt bij uw TOPdesk - beveiligde toepassing (bijvoorbeeld: '*https://qssolutions.topdesk.net*').</span><span class="sxs-lookup"><span data-stu-id="6ef8f-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="6ef8f-162">b.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-162">b.</span></span> <span data-ttu-id="6ef8f-163">In de **TOPdesk – openbare antwoord-URL** textbox, plak de **TOPdesk - beveiligde AssertionConsumerService URL** (bijvoorbeeld: '*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="6ef8f-164">c.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-164">c.</span></span> <span data-ttu-id="6ef8f-165">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-165">Click **Next**.</span></span>

10. <span data-ttu-id="6ef8f-166">Op de **eenmalige aanmelding configureren op TOPdesk - beveiligde** pagina voor het downloaden van het metagegevensbestand, klikt u op **metagegevens downloaden**, en sla het bestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="6ef8f-167">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="6ef8f-168">Voer de volgende stappen uit voor het maken van een certificaatbestand:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="6ef8f-169">![Certificaat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "certificaat")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="6ef8f-170">a.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-170">a.</span></span> <span data-ttu-id="6ef8f-171">Open het metagegevensbestand gedownloade.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="6ef8f-172">b.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-172">b.</span></span> <span data-ttu-id="6ef8f-173">Vouw de **RoleDescriptor** knooppunt met een **xsi: type** van **ingevoerd: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="6ef8f-174">c.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-174">c.</span></span> <span data-ttu-id="6ef8f-175">Kopieer de waarde van de **X509Certificate** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="6ef8f-176">d.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-176">d.</span></span> <span data-ttu-id="6ef8f-177">Opslaan van de gekopieerde **X509Certificate** waarde lokaal op uw computer in een bestand.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="6ef8f-178">Beveiligd op uw TOPdesk - site, bedrijf, in de **TOPdesk** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="6ef8f-179">![Instellingen](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="6ef8f-180">Klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="6ef8f-181">![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "aanmeldingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="6ef8f-182">Vouw de **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="6ef8f-183">![Algemene](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "algemeen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="6ef8f-184">In de **openbare** sectie, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="6ef8f-185">![Voeg](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="6ef8f-186">Op de **SAML-configuratie-assistent** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="6ef8f-187">![SAML-configuratie-assistent](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "assistent voor SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="6ef8f-188">a.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-188">a.</span></span> <span data-ttu-id="6ef8f-189">Voor het uploaden van uw gedownloade metagegevensbestand onder **Federatiemetagegevens**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="6ef8f-190">b.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-190">b.</span></span> <span data-ttu-id="6ef8f-191">Voor het uploaden van het certificaatbestand onder **certificaat (RSA)**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="6ef8f-192">c.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-192">c.</span></span> <span data-ttu-id="6ef8f-193">Het logobestand dat u het ondersteuningsteam TOPdesk onder gekregen te uploaden **Logo pictogram**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="6ef8f-194">d.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-194">d.</span></span> <span data-ttu-id="6ef8f-195">In de **naam gebruikerskenmerk** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="6ef8f-196">e.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-196">e.</span></span> <span data-ttu-id="6ef8f-197">In de **weergavenaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="6ef8f-198">f.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-198">f.</span></span> <span data-ttu-id="6ef8f-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-199">Click **Save**.</span></span>

17. <span data-ttu-id="6ef8f-200">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="6ef8f-201">![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="6ef8f-202">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="6ef8f-202">Configuring user provisioning</span></span>
<span data-ttu-id="6ef8f-203">Om in te schakelen van Azure AD-gebruikers aan te melden bij TOPdesk - wilt beveiligen, ze moeten worden ingericht in TOPdesk - veilig.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="6ef8f-204">In het geval van TOPdesk - veilige, inrichting is een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="6ef8f-205">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="6ef8f-206">Meld u aan bij uw **TOPdesk - beveiligde** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="6ef8f-207">Klik in het menu bovenaan op **TOPdesk \> nieuw \> ondersteuningsbestanden \> Operator**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="6ef8f-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="6ef8f-209">Op de **Operator New** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="6ef8f-210">![Nieuwe Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "nieuwe Operator")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="6ef8f-211">a.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-211">a.</span></span> <span data-ttu-id="6ef8f-212">Klik op het tabblad Algemeen.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-212">Click the General tab.</span></span>
   
    <span data-ttu-id="6ef8f-213">b.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-213">b.</span></span> <span data-ttu-id="6ef8f-214">In de **achternaam** textbox van de **algemene** sectie, typt u de achternaam van een geldig Azure Active Directory-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="6ef8f-215">c.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-215">c.</span></span> <span data-ttu-id="6ef8f-216">Selecteer een **Site** voor het account in de **locatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="6ef8f-217">d.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-217">d.</span></span> <span data-ttu-id="6ef8f-218">In de **aanmeldingsnaam** textbox van de **TOPdesk aanmelding** sectie, typt u een aanmeldingsnaam voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="6ef8f-219">e.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-219">e.</span></span> <span data-ttu-id="6ef8f-220">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6ef8f-221">U kunt andere TOPdesk - hulpmiddelen voor het maken van account beveiligde gebruiker of geleverd door TOPdesk - veilig voor het inrichten van accounts voor gebruikers met AAD-API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="6ef8f-222">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="6ef8f-222">Assigning users</span></span>
<span data-ttu-id="6ef8f-223">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="6ef8f-224">Als u gebruikers toewijzen aan TOPdesk - wilt beveiligen, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6ef8f-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="6ef8f-225">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6ef8f-226">Op de ** TOPdesk - beveiligde ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="6ef8f-227">![Gebruikers toewijzen](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="6ef8f-228">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="6ef8f-229">![Ja](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="6ef8f-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6ef8f-230">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6ef8f-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="6ef8f-231">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6ef8f-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

