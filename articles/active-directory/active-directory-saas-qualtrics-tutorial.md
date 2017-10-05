---
title: 'Zelfstudie: Azure Active Directory-integratie met Qualtrics | Microsoft Docs'
description: Meer informatie over het gebruik van Qualtrics met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="c9439-103">Zelfstudie: Azure Active Directory-integratie met Qualtrics</span><span class="sxs-lookup"><span data-stu-id="c9439-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="c9439-104">Het doel van deze zelfstudie is om de integratie van Azure en Qualtrics weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c9439-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="c9439-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="c9439-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c9439-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="c9439-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c9439-107">Een Qualtrics eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c9439-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c9439-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Qualtrics worden kunnen eenmalige aanmelding in de toepassing op uw Qualtrics bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9439-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c9439-109">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="c9439-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="c9439-110">De integratie van toepassingen voor Qualtrics inschakelen</span><span class="sxs-lookup"><span data-stu-id="c9439-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="c9439-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="c9439-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="c9439-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="c9439-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="c9439-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="c9439-113">Assigning users</span></span>

<span data-ttu-id="c9439-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="c9439-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="c9439-115">De integratie van toepassingen voor Qualtrics inschakelen</span><span class="sxs-lookup"><span data-stu-id="c9439-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="c9439-116">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor Qualtrics overzicht.</span><span class="sxs-lookup"><span data-stu-id="c9439-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="c9439-117">**Als u wilt de integratie van toepassingen voor Qualtrics inschakelen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c9439-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="c9439-118">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9439-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c9439-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c9439-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c9439-120">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="c9439-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c9439-121">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c9439-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="c9439-122">![Toepassingen](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="c9439-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c9439-123">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="c9439-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="c9439-124">![Toepassing toevoegen](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="c9439-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c9439-125">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="c9439-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="c9439-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="c9439-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c9439-127">In de **zoekvak**, type **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="c9439-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="c9439-128">![Toepassingsgalerie](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="c9439-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="c9439-129">Selecteer in het deelvenster met resultaten **Qualtrics**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c9439-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="c9439-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="c9439-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c9439-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="c9439-131">Configure single sign-on</span></span>

<span data-ttu-id="c9439-132">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren Qualtrics aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="c9439-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="c9439-133">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c9439-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c9439-134">In de klassieke Azure-portal op de **Qualtrics** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c9439-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c9439-135">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="c9439-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="c9439-136">Op de **hoe wilt u dat gebruikers zich aanmelden op Qualtrics** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c9439-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c9439-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="c9439-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="c9439-138">Op de **App-URL configureren** pagina de **Qualtrics aanmelding op URL** textbox, typ de URL (bijvoorbeeld: '*https://ssotest2ut1.qualtrics.com*'), en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c9439-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="c9439-139">![App-URL configureren](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="c9439-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="c9439-140">Op de **eenmalige aanmelding configureren op Qualtrics** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c9439-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="c9439-141">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="c9439-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="c9439-142">Het metagegevensbestand verzenden naar het ondersteuningsteam Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="c9439-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c9439-143">De SSO-configuratie is door het ondersteuningsteam Qualtrics worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9439-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="c9439-144">U ontvangt een melding zodra de configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c9439-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="c9439-145">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c9439-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c9439-146">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="c9439-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="c9439-147">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="c9439-147">Configure user provisioning</span></span>

<span data-ttu-id="c9439-148">Er is geen actie-item voor gebruikers inrichten voor Qualtrics configuratie.</span><span class="sxs-lookup"><span data-stu-id="c9439-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="c9439-149">Wanneer een toegewezen gebruiker probeert aan te melden bij met het toegangsvenster Qualtrics, Qualtrics u controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="c9439-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="c9439-150">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="c9439-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="c9439-151">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="c9439-151">Assign users</span></span>
<span data-ttu-id="c9439-152">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="c9439-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c9439-153">**Gebruikers om aan te wijzen Qualtrics, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c9439-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="c9439-154">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="c9439-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c9439-155">Op de **Qualtrics** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="c9439-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c9439-156">![Gebruikers toewijzen](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="c9439-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="c9439-157">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="c9439-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="c9439-158">![Ja](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="c9439-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c9439-159">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c9439-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="c9439-160">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9439-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

