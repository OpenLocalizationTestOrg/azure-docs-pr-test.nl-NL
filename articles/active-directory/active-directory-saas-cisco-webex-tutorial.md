---
title: 'Zelfstudie: Azure Active Directory-integratie met Cisco Webex | Microsoft Docs'
description: Meer informatie over het gebruik van Cisco Webex met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="98fbc-103">Zelfstudie: Azure Active Directory-integratie met Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="98fbc-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="98fbc-104">Het doel van deze zelfstudie is om de integratie van Azure en Cisco Webex weer te geven.</span><span class="sxs-lookup"><span data-stu-id="98fbc-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="98fbc-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="98fbc-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="98fbc-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="98fbc-106">A valid Azure subscription</span></span>
* <span data-ttu-id="98fbc-107">Een tenant Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="98fbc-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="98fbc-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Cisco Webex worden kunnen eenmalige aanmelding in de toepassing op uw Cisco Webex bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98fbc-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="98fbc-109">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="98fbc-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="98fbc-110">De integratie van toepassingen voor Cisco Webex inschakelen</span><span class="sxs-lookup"><span data-stu-id="98fbc-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="98fbc-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="98fbc-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="98fbc-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="98fbc-112">Configuring user provisioning</span></span>
* <span data-ttu-id="98fbc-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="98fbc-113">Assigning users</span></span>

<span data-ttu-id="98fbc-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="98fbc-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="98fbc-115">De integratie van toepassingen voor Cisco Webex inschakelen</span><span class="sxs-lookup"><span data-stu-id="98fbc-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="98fbc-116">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor Cisco Webex overzicht.</span><span class="sxs-lookup"><span data-stu-id="98fbc-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="98fbc-117">**Als u wilt de integratie van toepassingen voor Cisco Webex inschakelen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="98fbc-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="98fbc-118">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="98fbc-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="98fbc-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="98fbc-120">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="98fbc-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="98fbc-121">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="98fbc-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="98fbc-122">![Toepassingen](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="98fbc-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="98fbc-123">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="98fbc-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="98fbc-124">![Toepassing toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="98fbc-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="98fbc-125">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="98fbc-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="98fbc-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="98fbc-127">In de **zoekvak**, type **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="98fbc-128">![Toepassingsgalerie](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="98fbc-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="98fbc-129">Selecteer in het deelvenster met resultaten **Cisco Webex**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="98fbc-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="98fbc-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="98fbc-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="98fbc-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="98fbc-131">Configure single sign-on</span></span>

<span data-ttu-id="98fbc-132">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren Cisco Webex aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="98fbc-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="98fbc-133">Als onderdeel van deze procedure moet zijn u vereist voor het maken van een Base64-gecodeerde certificaat.</span><span class="sxs-lookup"><span data-stu-id="98fbc-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="98fbc-134">Als u niet bekend met deze procedure bent, raadpleegt u [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="98fbc-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="98fbc-135">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="98fbc-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="98fbc-136">In de klassieke Azure-portal op de **Cisco Webex** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="98fbc-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="98fbc-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="98fbc-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="98fbc-138">Op de **hoe wilt u dat gebruikers zich aanmelden op voor Cisco Webex** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="98fbc-139">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="98fbc-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="98fbc-140">Op de **App-URL configureren** pagina, voer de volgende stappen uit en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="98fbc-141">![App-URL configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "app-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="98fbc-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="98fbc-142">In de **Sing op URL** textbox, typt u uw Cisco Webex tenant-URL (bijvoorbeeld: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="98fbc-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="98fbc-143">In de **Cisco Webex antwoord-URL** textbox type uw **Cisco Webex AssertionConsumerService URL** (bijvoorbeeld: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="98fbc-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="98fbc-144">Op de **eenmalige aanmelding configureren op Cisco Webex** pagina om uw certificaat te downloaden, klikt u op **certificaat downloaden**, en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="98fbc-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="98fbc-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="98fbc-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="98fbc-146">In een ander browservenster, meld u bij uw bedrijf Cisco Webex site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="98fbc-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="98fbc-147">Klik in het menu bovenaan op **Sitebeheer**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="98fbc-148">![Sitebeheer](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Sitebeheer")</span><span class="sxs-lookup"><span data-stu-id="98fbc-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="98fbc-149">In de **-Site beheren** sectie, klikt u op **SSO configuratie**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="98fbc-150">![Configuratie van de SSO-](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="98fbc-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="98fbc-151">Voer de volgende stappen uit in de sectie federatief Web SSO-configuratie:</span><span class="sxs-lookup"><span data-stu-id="98fbc-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="98fbc-152">![Federatieve SSO configuratie](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "federatieve SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="98fbc-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="98fbc-153">Van de **Protocol Federation** selecteert **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="98fbc-154">Maak een **Base 64-codering** bestand van uw gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="98fbc-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="98fbc-155">Zie voor meer informatie [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="98fbc-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="98fbc-156">Open uw base-64 gecodeerde certificaat in Kladblok en kopieer de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="98fbc-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="98fbc-157">Klik op **SAML-metagegevens importeren**, en plak de base-64 gecodeerde certificaat.</span><span class="sxs-lookup"><span data-stu-id="98fbc-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="98fbc-158">In de klassieke Azure-portal op de **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina-, Kopieer de **URL-verlener** waarde en plak deze in de **verlener voor SAML (IdP-ID)** textbox.</span><span class="sxs-lookup"><span data-stu-id="98fbc-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="98fbc-159">In de klassieke Azure-portal op de **op Cisco Webex eenmalige aanmelding configureren** dialoogvenster pagina-, Kopieer de **externe aanmeldings-URL** waarde en plak deze in de **aanmeldings-URL van de klant SSO Service** textbox.</span><span class="sxs-lookup"><span data-stu-id="98fbc-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="98fbc-160">Van de **NameID indeling** selecteert **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="98fbc-161">In de **AuthnContextClassRef** textbox type **urn: oasis: namen: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="98fbc-162">In de klassieke Azure-portal op de **op Cisco Webex eenmalige aanmelding configureren** dialoogvenster pagina-, Kopieer de **externe URL voor afmelden** waarde en plak deze in de **klant SSO-Service-URL voor afmelden** textbox.</span><span class="sxs-lookup"><span data-stu-id="98fbc-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="98fbc-163">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-163">Click **Update**.</span></span>
9. <span data-ttu-id="98fbc-164">In de klassieke Azure-portal op de **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="98fbc-165">![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="98fbc-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="98fbc-166">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="98fbc-166">Configure user provisioning</span></span>

<span data-ttu-id="98fbc-167">Om in te schakelen gebruikers van Azure AD aan te melden bij Cisco Webex, moeten ze worden ingericht in Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="98fbc-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="98fbc-168">In het geval van een Cisco-Webex is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="98fbc-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="98fbc-169">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="98fbc-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="98fbc-170">Meld u aan bij uw **Cisco Webex** tenant.</span><span class="sxs-lookup"><span data-stu-id="98fbc-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="98fbc-171">Ga naar **gebruikers beheren \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="98fbc-172">![Gebruikers toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="98fbc-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="98fbc-173">Voer de volgende stappen uit in de sectie gebruiker toevoegen:</span><span class="sxs-lookup"><span data-stu-id="98fbc-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="98fbc-174">![Gebruiker toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="98fbc-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="98fbc-175">Als **accounttype**, selecteer **Host**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="98fbc-176">Typ de gegevens van een bestaande Azure AD-gebruiker in de volgende tekstvakken: **voornaam, achternaam**, **gebruikersnaam**, **e**, **wachtwoord**, **wachtwoord bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="98fbc-177">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="98fbc-178">U kunt andere Cisco Webex gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Cisco Webex aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="98fbc-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="98fbc-179">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="98fbc-179">Assign users</span></span>
<span data-ttu-id="98fbc-180">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="98fbc-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="98fbc-181">**Gebruikers om aan te wijzen Cisco Webex, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="98fbc-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="98fbc-182">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="98fbc-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="98fbc-183">Op de **Cisco Webex** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="98fbc-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="98fbc-184">![Gebruikers toewijzen](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="98fbc-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="98fbc-185">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="98fbc-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="98fbc-186">![Ja](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="98fbc-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="98fbc-187">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="98fbc-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="98fbc-188">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98fbc-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

