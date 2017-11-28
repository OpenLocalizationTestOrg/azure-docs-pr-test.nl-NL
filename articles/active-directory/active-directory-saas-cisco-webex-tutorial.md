---
title: 'Zelfstudie: Azure Active Directory-integratie met Cisco Webex | Microsoft Docs'
description: Lees hoe toouse Cisco Webex met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="bc322-103">Zelfstudie: Azure Active Directory-integratie met Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="bc322-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="bc322-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="bc322-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="bc322-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="bc322-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="bc322-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="bc322-106">A valid Azure subscription</span></span>
* <span data-ttu-id="bc322-107">Een tenant Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="bc322-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="bc322-108">Na het voltooien van deze zelfstudie hello Azure AD-gebruikers die u hebt toegewezen tooCisco Webex worden kunnen toosingle teken in de toepassing hello op uw Cisco Webex bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [inleiding toohello Toegang tot Configuratiescherm](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bc322-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="bc322-109">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc322-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="bc322-110">Hallo toepassingsintegratie voor Cisco Webex inschakelen</span><span class="sxs-lookup"><span data-stu-id="bc322-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="bc322-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="bc322-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="bc322-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="bc322-112">Configuring user provisioning</span></span>
* <span data-ttu-id="bc322-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="bc322-113">Assigning users</span></span>

<span data-ttu-id="bc322-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="bc322-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="bc322-115">Hallo toepassingsintegratie voor Cisco Webex inschakelen</span><span class="sxs-lookup"><span data-stu-id="bc322-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="bc322-116">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="bc322-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="bc322-117">**tooenable hello toepassingsintegratie voor Cisco Webex, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bc322-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc322-118">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bc322-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="bc322-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="bc322-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="bc322-120">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="bc322-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="bc322-121">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc322-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="bc322-122">![Toepassingen](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="bc322-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="bc322-123">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="bc322-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="bc322-124">![Toepassing toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bc322-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="bc322-125">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="bc322-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="bc322-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bc322-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="bc322-127">In Hallo **zoekvak**, type **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="bc322-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="bc322-128">![Toepassingsgalerie](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="bc322-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="bc322-129">Selecteer in het deelvenster met resultaten Hallo **Cisco Webex**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc322-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="bc322-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="bc322-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="bc322-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="bc322-131">Configure single sign-on</span></span>

<span data-ttu-id="bc322-132">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooCisco Webex aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="bc322-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="bc322-133">Als onderdeel van deze procedure bent u vereiste toocreate een Base64-gecodeerde certificaat.</span><span class="sxs-lookup"><span data-stu-id="bc322-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="bc322-134">Als u niet bekend met deze procedure bent, raadpleegt u [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="bc322-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="bc322-135">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bc322-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc322-136">In de klassieke Azure-portal op Hallo Hallo **Cisco Webex** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bc322-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="bc322-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="bc322-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="bc322-138">Op Hallo **wilt u hoe gebruikers toosign op tooCisco Webex** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bc322-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="bc322-139">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="bc322-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="bc322-140">Op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="bc322-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="bc322-141">![App-URL configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="bc322-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="bc322-142">In Hallo **Sing op URL** textbox, typt u uw Cisco Webex tenant-URL (bijvoorbeeld: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="bc322-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="bc322-143">In Hallo **Cisco Webex antwoord-URL** textbox type uw **Cisco Webex AssertionConsumerService URL** (bijvoorbeeld: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="bc322-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="bc322-144">Op Hallo **op Cisco Webex eenmalige aanmelding configureren** pagina, toodownload uw certificaat, klik op **certificaat downloaden**, en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bc322-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="bc322-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="bc322-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="bc322-146">In een ander browservenster, meld u bij uw bedrijf Cisco Webex site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bc322-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="bc322-147">Klik in het menu bovenaan Hallo Hallo **Sitebeheer**.</span><span class="sxs-lookup"><span data-stu-id="bc322-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="bc322-148">![Sitebeheer](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Sitebeheer")</span><span class="sxs-lookup"><span data-stu-id="bc322-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="bc322-149">In Hallo **-Site beheren** sectie, klikt u op **SSO configuratie**.</span><span class="sxs-lookup"><span data-stu-id="bc322-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="bc322-150">![Configuratie van de SSO-](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="bc322-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="bc322-151">Voer in Hallo federatieve Web-SSO configuratiesectie, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc322-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="bc322-152">![Federatieve SSO configuratie](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "federatieve SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="bc322-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="bc322-153">Van Hallo **Protocol Federation** selecteert **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="bc322-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="bc322-154">Maak een **Base 64-codering** bestand van uw gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="bc322-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="bc322-155">Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="bc322-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="bc322-156">Open uw base-64 gecodeerde certificaat in Kladblok en kopiëren Hallo inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="bc322-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="bc322-157">Klik op **SAML-metagegevens importeren**, en plak de base-64 gecodeerde certificaat.</span><span class="sxs-lookup"><span data-stu-id="bc322-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="bc322-158">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, kopie Hallo **URL-verlener** waarde en plak deze in Hallo **verlener voor SAML (IdP-ID)** textbox.</span><span class="sxs-lookup"><span data-stu-id="bc322-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="bc322-159">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, kopie Hallo **externe aanmeldings-URL** waarde en plak deze in Hallo **klant SSO Service Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="bc322-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="bc322-160">Van Hallo **NameID indeling** selecteert **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="bc322-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="bc322-161">In Hallo **AuthnContextClassRef** textbox type **urn: oasis: namen: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="bc322-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="bc322-162">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, kopie Hallo **externe URL voor afmelden** waarde en plak deze in Hallo **klant SSO Service afmelden URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="bc322-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="bc322-163">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="bc322-163">Click **Update**.</span></span>
9. <span data-ttu-id="bc322-164">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bc322-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="bc322-165">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="bc322-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="bc322-166">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="bc322-166">Configure user provisioning</span></span>

<span data-ttu-id="bc322-167">In volgorde tooenable Azure AD gebruikers toolog in Cisco Webex, moeten ze worden ingericht in Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="bc322-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="bc322-168">In geval van Cisco Webex Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bc322-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="bc322-169">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="bc322-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc322-170">Meld u bij tooyour **Cisco Webex** tenant.</span><span class="sxs-lookup"><span data-stu-id="bc322-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="bc322-171">Ga te**gebruikers beheren \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bc322-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="bc322-172">![Gebruikers toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bc322-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="bc322-173">Op Hallo sectie gebruiker toevoegen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc322-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="bc322-174">![Gebruiker toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bc322-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="bc322-175">Als **accounttype**, selecteer **Host**.</span><span class="sxs-lookup"><span data-stu-id="bc322-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="bc322-176">Hallo-informatie van een bestaande Azure AD-gebruiker in Hallo tekstvakken volgende typen: **voornaam, achternaam**, **gebruikersnaam**, **e**, **wachtwoord**, **Wachtwoord bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="bc322-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="bc322-177">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="bc322-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="bc322-178">U kunt andere Cisco Webex gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Cisco Webex tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bc322-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="bc322-179">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="bc322-179">Assign users</span></span>
<span data-ttu-id="bc322-180">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="bc322-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="bc322-181">**tooassign gebruikers tooCisco Webex, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bc322-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc322-182">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="bc322-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="bc322-183">Op Hallo **Cisco Webex** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="bc322-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="bc322-184">![Gebruikers toewijzen](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="bc322-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="bc322-185">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="bc322-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="bc322-186">![Ja](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="bc322-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="bc322-187">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="bc322-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="bc322-188">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bc322-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

