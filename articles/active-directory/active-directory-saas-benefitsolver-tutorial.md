---
title: 'Zelfstudie: Azure Active Directory-integratie met Benefitsolver | Microsoft Docs'
description: Meer informatie over het gebruik van Benefitsolver met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="5a50f-103">Zelfstudie: Azure Active Directory-integratie met Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="5a50f-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="5a50f-104">Het doel van deze zelfstudie is om de integratie van Azure en Benefitsolver weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5a50f-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="5a50f-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="5a50f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5a50f-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="5a50f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5a50f-107">Een Benefitsolver eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5a50f-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="5a50f-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Benefitsolver kan worden één Meld u aan bij de toepassing met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a50f-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5a50f-109">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="5a50f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="5a50f-110">De integratie van toepassingen voor Benefitsolver inschakelen</span><span class="sxs-lookup"><span data-stu-id="5a50f-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="5a50f-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="5a50f-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="5a50f-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="5a50f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="5a50f-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="5a50f-113">Assigning users</span></span>

<span data-ttu-id="5a50f-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="5a50f-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="5a50f-115">De integratie van toepassingen voor Benefitsolver inschakelen</span><span class="sxs-lookup"><span data-stu-id="5a50f-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="5a50f-116">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor Benefitsolver overzicht.</span><span class="sxs-lookup"><span data-stu-id="5a50f-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="5a50f-117">Als u wilt de integratie van toepassingen voor Benefitsolver inschakelen, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5a50f-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="5a50f-118">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5a50f-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5a50f-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5a50f-120">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="5a50f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5a50f-121">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="5a50f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5a50f-122">![Toepassingen](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="5a50f-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5a50f-123">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="5a50f-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5a50f-124">![Toepassing toevoegen](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="5a50f-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5a50f-125">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5a50f-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="5a50f-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5a50f-127">In de **zoekvak**, type **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="5a50f-128">![Toepassingsgalerie](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="5a50f-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="5a50f-129">Selecteer in het deelvenster met resultaten **Benefitsolver**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a50f-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="5a50f-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="5a50f-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5a50f-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="5a50f-131">Configure single sign-on</span></span>

<span data-ttu-id="5a50f-132">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren Benefitsolver aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="5a50f-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="5a50f-133">Uw toepassing Benefitsolver verwacht de SAML-asserties in een specifieke indeling waarvoor u het toevoegen van aangepast kenmerktoewijzingen aan uw **saml-token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="5a50f-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="5a50f-134">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="5a50f-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="5a50f-135">![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="5a50f-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="5a50f-136">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5a50f-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="5a50f-137">In de klassieke Azure-portal op de **Benefitsolver** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5a50f-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5a50f-138">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="5a50f-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="5a50f-139">Op de **hoe wilt u dat gebruikers zich aanmelden op Benefitsolver** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5a50f-140">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="5a50f-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="5a50f-141">Op de **App-instellingen configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5a50f-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="5a50f-142">![App-instellingen configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "App-instellingen configureren")</span><span class="sxs-lookup"><span data-stu-id="5a50f-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="5a50f-143">In de **aanmelding op URL** textbox type **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="5a50f-144">In de **antwoord-URL** textbox type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="5a50f-145">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-145">Click **Next**.</span></span>
4. <span data-ttu-id="5a50f-146">Op de **eenmalige aanmelding configureren op Benefitsolver** pagina voor het downloaden van de metagegevens, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5a50f-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="5a50f-147">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="5a50f-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="5a50f-148">Het metagegevensbestand van de gedownloade verzenden naar het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="5a50f-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5a50f-149">Het ondersteuningsteam Benefitsolver heeft te maken van de werkelijke SSO-configuratie.</span><span class="sxs-lookup"><span data-stu-id="5a50f-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="5a50f-150">U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5a50f-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="5a50f-151">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5a50f-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5a50f-152">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="5a50f-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="5a50f-153">Klik in het menu bovenaan op **kenmerken** openen de **SAML-Token kenmerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5a50f-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="5a50f-154">![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="5a50f-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="5a50f-155">Als u wilt de vereiste kenmerktoewijzingen toevoegen, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5a50f-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="5a50f-156">![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="5a50f-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="5a50f-157">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="5a50f-157">Attribute Name</span></span> | <span data-ttu-id="5a50f-158">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="5a50f-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="5a50f-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="5a50f-159">ClientID</span></span> |<span data-ttu-id="5a50f-160">U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="5a50f-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="5a50f-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="5a50f-161">ClientKey</span></span> |<span data-ttu-id="5a50f-162">U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="5a50f-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="5a50f-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="5a50f-163">LogoutURL</span></span> |<span data-ttu-id="5a50f-164">U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="5a50f-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="5a50f-165">Werknemer-id</span><span class="sxs-lookup"><span data-stu-id="5a50f-165">EmployeeID</span></span> |<span data-ttu-id="5a50f-166">U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="5a50f-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="5a50f-167">Voor elke gegevensrij in de bovenstaande tabel, klikt u op **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="5a50f-168">In de **kenmerknaam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="5a50f-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="5a50f-169">In de **kenmerkwaarde** textbox, selecteert u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="5a50f-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="5a50f-170">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-170">Click **Complete**.</span></span>
9. <span data-ttu-id="5a50f-171">Klik op **wijzigingen toepassen**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="5a50f-172">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="5a50f-172">Configure user provisioning</span></span>
<span data-ttu-id="5a50f-173">Om in te schakelen gebruikers van Azure AD aan te melden bij Benefitsolver, moeten ze worden ingericht in Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="5a50f-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="5a50f-174">In het geval van Benefitsolver is werknemersgegevens in uw toepassing ingevuld met behulp van een bestand telling van het systeem HRIS (doorgaans elke nacht).</span><span class="sxs-lookup"><span data-stu-id="5a50f-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="5a50f-175">U kunt andere Benefitsolver gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Benefitsolver aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="5a50f-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="5a50f-176">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="5a50f-176">Assigning users</span></span>
<span data-ttu-id="5a50f-177">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="5a50f-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="5a50f-178">Gebruikers om aan te wijzen Benefitsolver, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5a50f-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="5a50f-179">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="5a50f-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5a50f-180">Op de ** Benefitsolver ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="5a50f-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5a50f-181">![Gebruikers toewijzen](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="5a50f-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="5a50f-182">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="5a50f-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5a50f-183">![Ja](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="5a50f-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5a50f-184">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="5a50f-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5a50f-185">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a50f-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

