---
title: 'Zelfstudie: Azure Active Directory-integratie met Benefitsolver | Microsoft Docs'
description: Lees hoe toouse Benefitsolver met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="64b3e-103">Zelfstudie: Azure Active Directory-integratie met Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="64b3e-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="64b3e-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="64b3e-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="64b3e-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="64b3e-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="64b3e-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="64b3e-106">A valid Azure subscription</span></span>
* <span data-ttu-id="64b3e-107">Een Benefitsolver eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="64b3e-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="64b3e-108">Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooBenefitsolver kunnen toosingle Meld u aan bij Hallo toepassing hello [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="64b3e-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="64b3e-109">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64b3e-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="64b3e-110">Hallo toepassingsintegratie voor Benefitsolver inschakelen</span><span class="sxs-lookup"><span data-stu-id="64b3e-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="64b3e-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="64b3e-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="64b3e-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="64b3e-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="64b3e-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="64b3e-113">Assigning users</span></span>

<span data-ttu-id="64b3e-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="64b3e-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="64b3e-115">Hallo toepassingsintegratie voor Benefitsolver inschakelen</span><span class="sxs-lookup"><span data-stu-id="64b3e-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="64b3e-116">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="64b3e-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="64b3e-117">tooenable hello toepassingsintegratie voor Benefitsolver, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64b3e-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="64b3e-118">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="64b3e-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="64b3e-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="64b3e-120">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="64b3e-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="64b3e-121">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="64b3e-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="64b3e-122">![Toepassingen](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="64b3e-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="64b3e-123">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="64b3e-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="64b3e-124">![Toepassing toevoegen](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="64b3e-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="64b3e-125">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="64b3e-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="64b3e-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="64b3e-127">In Hallo **zoekvak**, type **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="64b3e-128">![Toepassingsgalerie](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="64b3e-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="64b3e-129">Selecteer in het deelvenster met resultaten Hallo **Benefitsolver**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="64b3e-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="64b3e-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="64b3e-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="64b3e-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="64b3e-131">Configure single sign-on</span></span>

<span data-ttu-id="64b3e-132">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooBenefitsolver aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="64b3e-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="64b3e-133">Uw toepassing Benefitsolver Hallo SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **saml-token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="64b3e-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="64b3e-134">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="64b3e-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="64b3e-135">![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="64b3e-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="64b3e-136">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="64b3e-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="64b3e-137">In de klassieke Azure-portal op Hallo Hallo **Benefitsolver** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64b3e-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="64b3e-138">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="64b3e-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="64b3e-139">Op Hallo **wilt u hoe gebruikers toosign op tooBenefitsolver** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="64b3e-140">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="64b3e-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="64b3e-141">Op Hallo **App-instellingen configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64b3e-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="64b3e-142">![App-instellingen configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "App-instellingen configureren")</span><span class="sxs-lookup"><span data-stu-id="64b3e-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="64b3e-143">In Hallo **aanmelding op URL** textbox type **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="64b3e-144">In Hallo **antwoord-URL** textbox type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="64b3e-145">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-145">Click **Next**.</span></span>
4. <span data-ttu-id="64b3e-146">Op Hallo **eenmalige aanmelding configureren op Benefitsolver** pagina, toodownload uw metagegevens, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens Hallo lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="64b3e-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="64b3e-147">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="64b3e-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="64b3e-148">Hallo gedownload metagegevens bestand tooyour Benefitsolver ondersteuningsteam verzenden.</span><span class="sxs-lookup"><span data-stu-id="64b3e-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="64b3e-149">Het ondersteuningsteam Benefitsolver is toodo Hallo werkelijke SSO-configuratie.</span><span class="sxs-lookup"><span data-stu-id="64b3e-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="64b3e-150">U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="64b3e-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="64b3e-151">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64b3e-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="64b3e-152">![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="64b3e-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="64b3e-153">Klik in het menu bovenaan Hallo Hallo **kenmerken** tooopen hello **SAML-Token kenmerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64b3e-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="64b3e-154">![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="64b3e-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="64b3e-155">Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64b3e-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="64b3e-156">![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="64b3e-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="64b3e-157">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="64b3e-157">Attribute Name</span></span> | <span data-ttu-id="64b3e-158">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="64b3e-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="64b3e-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="64b3e-159">ClientID</span></span> |<span data-ttu-id="64b3e-160">U moet deze waarde tooget van het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="64b3e-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="64b3e-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="64b3e-161">ClientKey</span></span> |<span data-ttu-id="64b3e-162">U moet deze waarde tooget van het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="64b3e-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="64b3e-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="64b3e-163">LogoutURL</span></span> |<span data-ttu-id="64b3e-164">U moet deze waarde tooget van het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="64b3e-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="64b3e-165">Werknemer-id</span><span class="sxs-lookup"><span data-stu-id="64b3e-165">EmployeeID</span></span> |<span data-ttu-id="64b3e-166">U moet deze waarde tooget van het ondersteuningsteam Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="64b3e-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="64b3e-167">Klik voor elke gegevensrij in bovenstaande tabel voor Hallo **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="64b3e-168">In Hallo **kenmerknaam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="64b3e-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="64b3e-169">In Hallo **kenmerkwaarde** textbox, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="64b3e-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="64b3e-170">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-170">Click **Complete**.</span></span>
9. <span data-ttu-id="64b3e-171">Klik op **wijzigingen toepassen**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="64b3e-172">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="64b3e-172">Configure user provisioning</span></span>
<span data-ttu-id="64b3e-173">In de volgorde tooenable Azure AD gebruikers toolog in Benefitsolver, moeten ze worden ingericht in Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="64b3e-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="64b3e-174">In geval van Benefitsolver Hallo is werknemersgegevens in uw toepassing ingevuld met behulp van een bestand telling van het systeem HRIS (doorgaans elke nacht).</span><span class="sxs-lookup"><span data-stu-id="64b3e-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="64b3e-175">U kunt andere Benefitsolver gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Benefitsolver tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="64b3e-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="64b3e-176">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="64b3e-176">Assigning users</span></span>
<span data-ttu-id="64b3e-177">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="64b3e-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="64b3e-178">tooassign gebruikers tooBenefitsolver, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="64b3e-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="64b3e-179">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="64b3e-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="64b3e-180">Op Hallo ** Benefitsolver ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="64b3e-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="64b3e-181">![Gebruikers toewijzen](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="64b3e-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="64b3e-182">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="64b3e-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="64b3e-183">![Ja](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="64b3e-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="64b3e-184">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="64b3e-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="64b3e-185">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="64b3e-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

