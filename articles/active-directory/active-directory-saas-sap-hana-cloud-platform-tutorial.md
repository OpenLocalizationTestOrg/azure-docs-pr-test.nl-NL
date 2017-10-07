---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP HANA-Cloudplatform | Microsoft Docs'
description: Lees hoe toouse SAP HANA-Cloudplatform met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="cea04-103">Zelfstudie: Azure Active Directory-integratie met SAP HANA-cloudplatform</span><span class="sxs-lookup"><span data-stu-id="cea04-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="cea04-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en SAP HANA-Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="cea04-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="cea04-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="cea04-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="cea04-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="cea04-106">A valid Azure subscription</span></span>
* <span data-ttu-id="cea04-107">Een Cloud-Platform voor SAP HANA-account</span><span class="sxs-lookup"><span data-stu-id="cea04-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="cea04-108">Na het voltooien van deze zelfstudie hello Azure AD-gebruikers die u hebt tooSAP HANA Cloud-Platform worden kunnen toosingle aanmelding toegewezen aan Hallo toepassing hello [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cea04-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="cea04-109">U moet toodeploy uw eigen toepassing of tooan toepassing abonneren op uw SAP HANA Cloud Platform account tootest eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cea04-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="cea04-110">In deze zelfstudie is een toepassing wordt geïmplementeerd in Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="cea04-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="cea04-111">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cea04-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="cea04-112">Hallo toepassingsintegratie voor SAP HANA Cloud-Platform inschakelen</span><span class="sxs-lookup"><span data-stu-id="cea04-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="cea04-113">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="cea04-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="cea04-114">Een rol tooa gebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="cea04-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="cea04-115">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="cea04-115">Assigning users</span></span>

<span data-ttu-id="cea04-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="cea04-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="cea04-117">Hallo toepassingsintegratie voor SAP HANA Cloud-Platform inschakelen</span><span class="sxs-lookup"><span data-stu-id="cea04-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="cea04-118">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor SAP HANA Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="cea04-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="cea04-119">**tooenable hello toepassingsintegratie voor SAP HANA Cloud Platform Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cea04-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="cea04-120">Klik in hello Azure-beheerportal op Hallo navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cea04-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="cea04-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="cea04-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="cea04-122">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="cea04-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="cea04-123">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="cea04-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="cea04-124">![Toepassingen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="cea04-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="cea04-125">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="cea04-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="cea04-126">![Toepassing toevoegen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="cea04-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="cea04-127">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="cea04-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="cea04-128">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="cea04-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="cea04-129">In Hallo **zoekvak**, type **SAP HANA-Cloudplatform**.</span><span class="sxs-lookup"><span data-stu-id="cea04-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="cea04-130">![Toepassingsgalerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="cea04-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="cea04-131">Selecteer in het deelvenster met resultaten Hallo **SAP HANA-Cloudplatform**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cea04-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="cea04-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="cea04-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="cea04-133">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="cea04-133">Configure single sign-on</span></span>

<span data-ttu-id="cea04-134">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooSAP HANA Cloudplatform met een account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="cea04-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="cea04-135">Als onderdeel van deze procedure bent u vereiste tooupload een Base64-gecodeerde certificaat tooyour Cloudplatform voor SAP HANA-tenant.</span><span class="sxs-lookup"><span data-stu-id="cea04-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="cea04-136">Als u niet bekend met deze procedure bent, raadpleegt u [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="cea04-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="cea04-137">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cea04-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="cea04-138">In de klassieke Azure-portal op Hallo Hallo **SAP HANA-Cloudplatform** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding**dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cea04-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="cea04-139">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="cea04-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="cea04-140">Op Hallo **wilt u hoe gebruikers toosign op tooSAP HANA Cloudplatform** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cea04-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="cea04-141">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="cea04-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="cea04-142">Een ander browservenster, meld u aan bij toohello SAP HANA Cloud Platform Cockpit op https://account. \<liggend host\>.ondemand.com/cockpit (bijvoorbeeld: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="cea04-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="cea04-143">Klik op Hallo **vertrouwen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cea04-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="cea04-144">![Vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="cea04-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="cea04-145">In de sectie voor het beheren van vertrouwensrelatie uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cea04-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cea04-146">![Ophalen van metagegevens](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "metagegevens ophalen")</span><span class="sxs-lookup"><span data-stu-id="cea04-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="cea04-147">Klik op Hallo **lokale serviceprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cea04-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="cea04-148">toodownload hello metagegevensbestand voor SAP HANA Cloud-Platform, klikt u op **metagegevens ophalen**.</span><span class="sxs-lookup"><span data-stu-id="cea04-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="cea04-149">In hello Azure Active klassieke portal op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cea04-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="cea04-150">![App-URL configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="cea04-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="cea04-151">In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw toosign gebruikers in uw **SAP HANA-Cloudplatform** toepassing.</span><span class="sxs-lookup"><span data-stu-id="cea04-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="cea04-152">Dit is Hallo accountspecifiek URL van een beveiligde bron in uw Cloud-Platform voor SAP HANA-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cea04-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="cea04-153">Hallo URL is op basis van Hallo patroon volgen: *https://\<applicationName\>\<accountName\>.\< Liggend host\>.ondemand.com/\<pad\_naar\_beveiligd\_resource\>*  (bijvoorbeeld: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="cea04-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="cea04-154">Dit is de URL Hallo in uw Cloud-Platform voor SAP HANA-toepassing die Hallo gebruiker tooauthenticate vereist.</span><span class="sxs-lookup"><span data-stu-id="cea04-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="cea04-155">Open metagegevensbestand voor SAP HANA-Cloudplatform Hallo gedownload, en Ga naar Hallo **ns3:AssertionConsumerService** label.</span><span class="sxs-lookup"><span data-stu-id="cea04-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="cea04-156">Kopieer de waarde Hallo Hallo **locatie** kenmerk en plak deze in Hallo **antwoord-URL voor SAP HANA Cloud Platform** textbox.</span><span class="sxs-lookup"><span data-stu-id="cea04-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="cea04-157">Op Hallo **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** pagina, toodownload uw metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cea04-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="cea04-158">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="cea04-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="cea04-159">Op Hallo SAP HANA Cloud Platform Cockpit in Hallo **lokale serviceprovider** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cea04-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cea04-160">![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "beheer vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="cea04-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="cea04-161">Klik op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="cea04-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="cea04-162">Als **configuratietype**, selecteer **aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="cea04-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="cea04-163">Als **lokale providernaam**, accepteer de standaardwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="cea04-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="cea04-164">toogenerate een **handtekeningsleutel** en een **certificaat voor ondertekening van** sleutelpaar, klikt u op **sleutelpaar genereren**.</span><span class="sxs-lookup"><span data-stu-id="cea04-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="cea04-165">Als **Principal doorgeven**, selecteer **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="cea04-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="cea04-166">Als **Force verificatie**, selecteer **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="cea04-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="cea04-167">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cea04-167">Click **Save**.</span></span>

9. <span data-ttu-id="cea04-168">Klik op Hallo **identiteitsprovider vertrouwde** tabblad en klik vervolgens op **vertrouwde identiteitsprovider toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cea04-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="cea04-169">![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "beheer vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="cea04-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="cea04-170">toomanage hello lijst met vertrouwde id-providers, moet u toohave Hallo aangepaste configuratietype in Hallo lokale serviceprovider sectie gekozen.</span><span class="sxs-lookup"><span data-stu-id="cea04-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="cea04-171">U hebt een niet-bewerkbare en impliciete vertrouwensrelatie toohello SAP-id-Service voor het type standaard configuratie.</span><span class="sxs-lookup"><span data-stu-id="cea04-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="cea04-172">Voor geen hebt u geen vertrouwensrelatie instellingen.</span><span class="sxs-lookup"><span data-stu-id="cea04-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="cea04-173">Klik op Hallo **algemene** tabblad en klik vervolgens op **Bladeren** tooupload Hallo gedownload bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="cea04-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="cea04-174">![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "beheer vertrouwen")</span><span class="sxs-lookup"><span data-stu-id="cea04-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="cea04-175">Na het uploaden van het metagegevensbestand Hallo Hallo waarden voor **-URL met eenmalige aanmelding**, **-URL met eenmalige afmelding** en **certificaat voor ondertekening van** worden automatisch ingevuld.</span><span class="sxs-lookup"><span data-stu-id="cea04-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="cea04-176">Klik op Hallo **kenmerken** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cea04-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="cea04-177">Op Hallo **kenmerken** tabblad, voert u Hallo stap:</span><span class="sxs-lookup"><span data-stu-id="cea04-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="cea04-178">![Kenmerken](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="cea04-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="cea04-179">Klik op **Add Assertion-Based kenmerk**, en voeg vervolgens Hallo kenmerken op basis van een verklaring te volgen:</span><span class="sxs-lookup"><span data-stu-id="cea04-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="cea04-180">Verklaring kenmerk</span><span class="sxs-lookup"><span data-stu-id="cea04-180">Assertion Attribute</span></span> | <span data-ttu-id="cea04-181">Principal-kenmerk</span><span class="sxs-lookup"><span data-stu-id="cea04-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="cea04-182">http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/givenName</span><span class="sxs-lookup"><span data-stu-id="cea04-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="cea04-183">Voornaam</span><span class="sxs-lookup"><span data-stu-id="cea04-183">firstname</span></span> |
    | <span data-ttu-id="cea04-184">http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="cea04-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="cea04-185">Achternaam</span><span class="sxs-lookup"><span data-stu-id="cea04-185">lastname</span></span> |
    | <span data-ttu-id="cea04-186">http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/EmailAddress</span><span class="sxs-lookup"><span data-stu-id="cea04-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="cea04-187">E-mail</span><span class="sxs-lookup"><span data-stu-id="cea04-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="cea04-188">Hallo-configuratie van Hallo kenmerken is afhankelijk van de hoe Hallo toepassing(en) op rechtermuisknop worden ontwikkeld, dat wil zeggen welke kenmerken ze verwachten in Hallo SAML-reactie en onder welke naam (Principal kenmerk) toegang tot dit kenmerk in het Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="cea04-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="cea04-189">Hallo **kenmerk Default** in Hallo schermafbeelding is alleen ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="cea04-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="cea04-190">Het is niet toomake Hallo scenario werk vereist.</span><span class="sxs-lookup"><span data-stu-id="cea04-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="cea04-191">Hallo namen en waarden voor **Principal kenmerk** wordt weergegeven in Hallo schermafbeelding is afhankelijk van hoe de toepassing hello is ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="cea04-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="cea04-192">Het is mogelijk dat uw toepassing andere toewijzingen vereist.</span><span class="sxs-lookup"><span data-stu-id="cea04-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="cea04-193">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** dialoog pagina, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="cea04-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="cea04-194">![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="cea04-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="cea04-195">Verklaring gebaseerde groepen</span><span class="sxs-lookup"><span data-stu-id="cea04-195">Assertion-based groups</span></span>
<span data-ttu-id="cea04-196">U kunt groepen op basis van een bevestiging voor uw Azure Active Directory id-Provider configureren als een optionele stap.</span><span class="sxs-lookup"><span data-stu-id="cea04-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="cea04-197">Groepen gebruiken voor SAP HANA Cloud Platform kunt u toodynamically toewijzen een of meer gebruikers tooone of meer functies in uw toepassingen SAP HANA-Cloudplatform bepaald door waarden van kenmerken in Hallo SAML 2.0-verklaring.</span><span class="sxs-lookup"><span data-stu-id="cea04-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="cea04-198">Bijvoorbeeld, als hello assertion bevat Hallo kenmerk '*contract = tijdelijke*', kunt u alle betrokken gebruikers toobe toegevoegde toohello groep'*tijdelijke*'.</span><span class="sxs-lookup"><span data-stu-id="cea04-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="cea04-199">Hallo groep '*tijdelijke*' een of meer rollen van een of meer toepassingen die zijn geïmplementeerd in uw Cloud-Platform voor SAP HANA-account kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="cea04-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="cea04-200">Gebruik assertion gebaseerde groepen als u wilt dat toosimultaneously toewijzen veel gebruikers tooone of meer functies van toepassingen in uw Cloud-Platform voor SAP HANA-account.</span><span class="sxs-lookup"><span data-stu-id="cea04-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="cea04-201">Als u wilt dat tooassign slechts een enkele of een klein aantal gebruikers toospecific rollen, raden wij aan eraan toe te wijzen rechtstreeks in Hallo '**autorisaties**' hello SAP HANA-Cloudplatform cockpit tabblad.</span><span class="sxs-lookup"><span data-stu-id="cea04-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="cea04-202">Een rol tooa gebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="cea04-202">Assign a role tooa user</span></span>
<span data-ttu-id="cea04-203">In de volgorde tooenable Azure AD gebruikers toolog in SAP HANA Cloud-Platform, moet u de rollen in Hallo SAP HANA-Cloudplatform toothem toewijzen.</span><span class="sxs-lookup"><span data-stu-id="cea04-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="cea04-204">**tooassign een rol tooa gebruiker, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cea04-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="cea04-205">Meld u bij tooyour **SAP HANA-Cloudplatform** cockpit.</span><span class="sxs-lookup"><span data-stu-id="cea04-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="cea04-206">Voer de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="cea04-206">Perform hello following:</span></span>
   
   <span data-ttu-id="cea04-207">![Autorisaties](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "autorisaties")</span><span class="sxs-lookup"><span data-stu-id="cea04-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="cea04-208">Klik op **autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="cea04-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="cea04-209">Klik op Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cea04-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="cea04-210">In Hallo **gebruiker** textbox e-mailadres type Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cea04-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="cea04-211">Klik op **toewijzen** tooassign hello tooa gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="cea04-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="cea04-212">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cea04-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="cea04-213">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="cea04-213">Assign users</span></span>
<span data-ttu-id="cea04-214">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="cea04-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="cea04-215">**tooassign gebruikers tooSAP HANA Cloud-Platform, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cea04-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="cea04-216">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="cea04-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="cea04-217">Op Hallo **SAP HANA-Cloudplatform** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="cea04-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="cea04-218">![Gebruikers toewijzen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="cea04-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="cea04-219">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="cea04-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="cea04-220">![Ja](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="cea04-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="cea04-221">Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="cea04-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="cea04-222">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cea04-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

