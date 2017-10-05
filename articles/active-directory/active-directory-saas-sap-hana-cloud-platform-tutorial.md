---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP HANA-Cloudplatform | Microsoft Docs'
description: Meer informatie over het SAP HANA Cloud-Platform gebruiken met Azure Active Directory om te schakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="b6931-103">Zelfstudie: Azure Active Directory-integratie met SAP HANA-cloudplatform</span><span class="sxs-lookup"><span data-stu-id="b6931-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="b6931-104">Het doel van deze zelfstudie is het weergeven van de integratie van Azure en SAP HANA-Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="b6931-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="b6931-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="b6931-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="b6931-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="b6931-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b6931-107">Een Cloud-Platform voor SAP HANA-account</span><span class="sxs-lookup"><span data-stu-id="b6931-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="b6931-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Cloud-Platform voor SAP HANA kan worden één Meld u aan bij de toepassing met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6931-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="b6931-109">U moet uw eigen toepassing implementeren of zich abonneert op een toepassing op uw Cloud-Platform voor SAP HANA-account voor het testen van eenmalige aanmelding op.</span><span class="sxs-lookup"><span data-stu-id="b6931-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="b6931-110">In deze zelfstudie is een toepassing wordt geïmplementeerd in het account.</span><span class="sxs-lookup"><span data-stu-id="b6931-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="b6931-111">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="b6931-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="b6931-112">De integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen</span><span class="sxs-lookup"><span data-stu-id="b6931-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="b6931-113">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="b6931-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="b6931-114">Een rol toewijst aan een gebruiker</span><span class="sxs-lookup"><span data-stu-id="b6931-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="b6931-115">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="b6931-115">Assigning users</span></span>

<span data-ttu-id="b6931-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="b6931-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="b6931-117">De integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen</span><span class="sxs-lookup"><span data-stu-id="b6931-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="b6931-118">Het doel van deze sectie is het overzicht van de integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b6931-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="b6931-119">**Als u wilt de integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6931-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="b6931-120">Klik in de Azure-beheerportal, in het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6931-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="b6931-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b6931-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="b6931-122">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="b6931-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b6931-123">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b6931-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="b6931-124">![Toepassingen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="b6931-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="b6931-125">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="b6931-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="b6931-126">![Toepassing toevoegen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="b6931-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="b6931-127">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="b6931-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="b6931-128">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="b6931-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="b6931-129">In de **zoekvak**, type **SAP HANA-Cloudplatform**.</span><span class="sxs-lookup"><span data-stu-id="b6931-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="b6931-130">![Toepassingsgalerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="b6931-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="b6931-131">Selecteer in het deelvenster met resultaten **SAP HANA-Cloudplatform**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b6931-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="b6931-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="b6931-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="b6931-133">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="b6931-133">Configure single sign-on</span></span>

<span data-ttu-id="b6931-134">Het doel van deze sectie is om een overzicht van gebruikers te verifiëren en SAP HANA-Cloudplatform met hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="b6931-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="b6931-135">Als onderdeel van deze procedure bent u een Base64-gecodeerde certificaat uploaden naar uw Cloud-Platform voor SAP HANA-tenant vereist.</span><span class="sxs-lookup"><span data-stu-id="b6931-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="b6931-136">Als u niet bekend met deze procedure bent, raadpleegt u [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="b6931-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="b6931-137">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6931-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="b6931-138">In de klassieke Azure-portal op de **SAP HANA-Cloudplatform** pagina van de integratie van toepassing, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b6931-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="b6931-139">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="b6931-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="b6931-140">Op de **hoe wilt u dat gebruikers zich aanmelden op voor SAP HANA-Cloudplatform** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b6931-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="b6931-141">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="b6931-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="b6931-142">In een ander browservenster geopend, moet u zich aanmelden bij de SAP HANA Cloud Platform Cockpit op https://account. \<liggend host\>.ondemand.com/cockpit (bijvoorbeeld: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="b6931-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="b6931-143">Klik op de **vertrouwen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b6931-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="b6931-144">![Vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="b6931-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="b6931-145">In de sectie trust management, kunt u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b6931-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="b6931-146">![Ophalen van metagegevens](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "metagegevens ophalen")</span><span class="sxs-lookup"><span data-stu-id="b6931-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="b6931-147">Klik op de **lokale serviceprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b6931-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="b6931-148">Voor het downloaden van het metagegevensbestand voor SAP HANA Cloud-Platform, klikt u op **metagegevens ophalen**.</span><span class="sxs-lookup"><span data-stu-id="b6931-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="b6931-149">In de Azure Active klassieke portal op de **App-URL configureren** pagina, voer de volgende stappen uit en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b6931-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="b6931-150">![App-URL configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="b6931-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="b6931-151">In de **aanmelding op URL** textbox, typ de URL gebruikt door uw gebruikers zich aanmeldt bij uw **SAP HANA-Cloudplatform** toepassing.</span><span class="sxs-lookup"><span data-stu-id="b6931-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="b6931-152">Dit is de account-specifieke URL van een beveiligde bron in uw Cloud-Platform voor SAP HANA-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b6931-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="b6931-153">De URL is gebaseerd op het volgende patroon volgen: *https://\<applicationName\>\<accountName\>.\< Liggend host\>.ondemand.com/\<pad\_naar\_beveiligd\_resource\>*  (bijvoorbeeld: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="b6931-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="b6931-154">Dit is de URL in uw Cloud-Platform voor SAP HANA-toepassing waarvoor de gebruiker te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b6931-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="b6931-155">Open het gedownloade bestand van de Cloud-Platform voor SAP HANA-metagegevens, en Ga naar de **ns3:AssertionConsumerService** label.</span><span class="sxs-lookup"><span data-stu-id="b6931-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="b6931-156">Kopieer de waarde van de **locatie** kenmerk en plak deze in de **antwoord-URL voor SAP HANA Cloud Platform** textbox.</span><span class="sxs-lookup"><span data-stu-id="b6931-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="b6931-157">Op de **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** pagina voor het downloaden van de metagegevens, klikt u op **metagegevens downloaden**, en sla het bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b6931-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="b6931-158">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="b6931-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="b6931-159">Op de Cockpit SAP HANA Cloud Platform in de **lokale serviceprovider** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b6931-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b6931-160">![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "beheer vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="b6931-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="b6931-161">Klik op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="b6931-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="b6931-162">Als **configuratietype**, selecteer **aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="b6931-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="b6931-163">Als **lokale providernaam**, accepteer de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="b6931-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="b6931-164">Voor het genereren van een **handtekeningsleutel** en een **certificaat voor ondertekening van** sleutelpaar, klikt u op **sleutelpaar genereren**.</span><span class="sxs-lookup"><span data-stu-id="b6931-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="b6931-165">Als **Principal doorgeven**, selecteer **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="b6931-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="b6931-166">Als **Force verificatie**, selecteer **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="b6931-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="b6931-167">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b6931-167">Click **Save**.</span></span>

9. <span data-ttu-id="b6931-168">Klik op de **identiteitsprovider vertrouwde** tabblad en klik vervolgens op **vertrouwde identiteitsprovider toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b6931-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="b6931-169">![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "beheer vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="b6931-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="b6931-170">Voor het beheren van de lijst met vertrouwde id-providers, moet u het type aangepaste configuratie hebt gekozen in de sectie lokale-Provider.</span><span class="sxs-lookup"><span data-stu-id="b6931-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="b6931-171">U hebt een niet-bewerkbare en impliciete vertrouwensrelatie met de SAP-id-Service voor het type standaard configuratie.</span><span class="sxs-lookup"><span data-stu-id="b6931-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="b6931-172">Voor geen hebt u geen vertrouwensrelatie instellingen.</span><span class="sxs-lookup"><span data-stu-id="b6931-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="b6931-173">Klik op de **algemene** tabblad en klik vervolgens op **Bladeren** het gedownloade metagegevensbestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="b6931-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="b6931-174">![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "beheer vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="b6931-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="b6931-175">Na het uploaden van het metagegevensbestand, de waarden voor **-URL met eenmalige aanmelding**, **-URL met eenmalige afmelding** en **certificaat voor ondertekening van** worden automatisch ingevuld.</span><span class="sxs-lookup"><span data-stu-id="b6931-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="b6931-176">Klik op het tabblad **Kenmerken**.</span><span class="sxs-lookup"><span data-stu-id="b6931-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="b6931-177">Op de **kenmerken** tabblad, voert u de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="b6931-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="b6931-178">![Kenmerken](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b6931-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="b6931-179">Klik op **Add Assertion-Based kenmerk**, en voeg vervolgens de volgende kenmerken op basis van een bevestiging:</span><span class="sxs-lookup"><span data-stu-id="b6931-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="b6931-180">Verklaring kenmerk</span><span class="sxs-lookup"><span data-stu-id="b6931-180">Assertion Attribute</span></span> | <span data-ttu-id="b6931-181">Principal-kenmerk</span><span class="sxs-lookup"><span data-stu-id="b6931-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="b6931-182">http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/givenName</span><span class="sxs-lookup"><span data-stu-id="b6931-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="b6931-183">Voornaam</span><span class="sxs-lookup"><span data-stu-id="b6931-183">firstname</span></span> |
    | <span data-ttu-id="b6931-184">http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="b6931-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="b6931-185">Achternaam</span><span class="sxs-lookup"><span data-stu-id="b6931-185">lastname</span></span> |
    | <span data-ttu-id="b6931-186">http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/EmailAddress</span><span class="sxs-lookup"><span data-stu-id="b6931-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="b6931-187">E-mail</span><span class="sxs-lookup"><span data-stu-id="b6931-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="b6931-188">De configuratie van de kenmerken is afhankelijk van hoe de toepassingen op de rechtermuisknop worden ontwikkeld, dat wil zeggen welke kenmerken ze in de SAML-reactie verwachten en onder welke naam (Principal kenmerk) toegang tot dit kenmerk in de code.</span><span class="sxs-lookup"><span data-stu-id="b6931-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="b6931-189">De **kenmerk Default** in de schermafbeelding is alleen bedoeld ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="b6931-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="b6931-190">Het is niet vereist voor het maken van het scenario werken.</span><span class="sxs-lookup"><span data-stu-id="b6931-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="b6931-191">De namen en waarden voor **Principal kenmerk** weergegeven in de schermafbeelding afhankelijk van hoe de toepassing is ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="b6931-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="b6931-192">Het is mogelijk dat uw toepassing andere toewijzingen vereist.</span><span class="sxs-lookup"><span data-stu-id="b6931-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="b6931-193">In de klassieke Azure-portal op de **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** dialoog pagina, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b6931-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="b6931-194">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="b6931-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="b6931-195">Verklaring gebaseerde groepen</span><span class="sxs-lookup"><span data-stu-id="b6931-195">Assertion-based groups</span></span>
<span data-ttu-id="b6931-196">U kunt groepen op basis van een bevestiging voor uw Azure Active Directory id-Provider configureren als een optionele stap.</span><span class="sxs-lookup"><span data-stu-id="b6931-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="b6931-197">Met behulp van groepen op SAP HANA Cloud-Platform, kunt u een of meer gebruikers dynamisch toewijzen aan een of meer rollen in uw Cloud-Platform voor SAP HANA-toepassingen, bepaald door de waarden van kenmerken in het SAML 2.0-verklaring.</span><span class="sxs-lookup"><span data-stu-id="b6931-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="b6931-198">Bijvoorbeeld, als de bevestiging bevat het kenmerk '*contract = tijdelijke*', kunt u alle betrokken gebruikers worden toegevoegd aan de groep'*tijdelijke*'.</span><span class="sxs-lookup"><span data-stu-id="b6931-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="b6931-199">De groep '*tijdelijke*' een of meer rollen van een of meer toepassingen die zijn geïmplementeerd in uw Cloud-Platform voor SAP HANA-account kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="b6931-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="b6931-200">Groepen op basis van een bewering gebruiken wanneer u veel gebruikers tegelijk toewijzen aan een of meer rollen van toepassingen in uw Cloud-Platform voor SAP HANA-account wilt maken.</span><span class="sxs-lookup"><span data-stu-id="b6931-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="b6931-201">Als u toewijzen slechts een enkele of een klein aantal gebruikers aan specifieke rollen wilt, raden wij aan eraan toe te wijzen rechtstreeks in de '**autorisaties**' tabblad van de cockpit SAP HANA Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="b6931-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="b6931-202">Een rol toewijzen aan een gebruiker</span><span class="sxs-lookup"><span data-stu-id="b6931-202">Assign a role to a user</span></span>
<span data-ttu-id="b6931-203">Om in te schakelen gebruikers van Azure AD aan te melden bij SAP HANA Cloud-Platform, moet u rollen in de Cloud Platform voor SAP HANA aan ze toewijzen.</span><span class="sxs-lookup"><span data-stu-id="b6931-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="b6931-204">**Als u wilt een rol toewijzen aan een gebruiker, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6931-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="b6931-205">Meld u aan bij uw **SAP HANA-Cloudplatform** cockpit.</span><span class="sxs-lookup"><span data-stu-id="b6931-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="b6931-206">Het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b6931-206">Perform the following:</span></span>
   
   <span data-ttu-id="b6931-207">![Autorisaties](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "autorisaties")</span><span class="sxs-lookup"><span data-stu-id="b6931-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="b6931-208">Klik op **autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="b6931-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="b6931-209">Klik op de **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b6931-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="b6931-210">In de **gebruiker** textbox, typ de e-mailadres van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b6931-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="b6931-211">Klik op **toewijzen** toewijzen aan de gebruiker aan een rol.</span><span class="sxs-lookup"><span data-stu-id="b6931-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="b6931-212">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b6931-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="b6931-213">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="b6931-213">Assign users</span></span>
<span data-ttu-id="b6931-214">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="b6931-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="b6931-215">**Gebruikers om aan te wijzen SAP HANA Cloud-Platform, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b6931-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="b6931-216">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="b6931-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="b6931-217">Op de **SAP HANA-Cloudplatform** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="b6931-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="b6931-218">![Gebruikers toewijzen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="b6931-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="b6931-219">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="b6931-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="b6931-220">![Ja](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="b6931-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b6931-221">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b6931-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="b6931-222">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6931-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

