---
title: 'Zelfstudie: Azure Active Directory-integratie met SCC LifeCycle | Microsoft Docs'
description: Meer informatie over het SCC LifeCycle gebruiken met Azure Active Directory om te schakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="15174-103">Zelfstudie: Azure Active Directory-integratie met SCC levenscyclus</span><span class="sxs-lookup"><span data-stu-id="15174-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="15174-104">Het doel van deze zelfstudie is om de integratie van Azure en SCC LifeCycle weer te geven.</span><span class="sxs-lookup"><span data-stu-id="15174-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="15174-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="15174-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="15174-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="15174-106">A valid Azure subscription</span></span>
* <span data-ttu-id="15174-107">Een SCC LifeCycle eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="15174-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="15174-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan de levenscyclus van SCC worden kunnen eenmalige aanmelding in de toepassing op uw site in de levenscyclus van SCC bedrijf (serviceprovider geïnitieerd aanmelding) of met behulp van de [Inleiding tot de toegang Deelvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15174-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="15174-109">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="15174-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="15174-110">Inschakelen van de integratie van toepassingen voor SCC levenscyclus</span><span class="sxs-lookup"><span data-stu-id="15174-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="15174-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="15174-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="15174-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="15174-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="15174-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="15174-113">Assigning users</span></span>

<span data-ttu-id="15174-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="15174-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="15174-115">De integratie van toepassingen voor SCC levenscyclus inschakelen</span><span class="sxs-lookup"><span data-stu-id="15174-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="15174-116">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor SCC levenscyclus overzicht.</span><span class="sxs-lookup"><span data-stu-id="15174-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="15174-117">**Om de integratie van toepassingen voor SCC levenscyclus inschakelt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="15174-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="15174-118">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="15174-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="15174-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="15174-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="15174-120">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="15174-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="15174-121">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="15174-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="15174-122">![Toepassingen](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="15174-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="15174-123">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="15174-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="15174-124">![Toepassing toevoegen](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="15174-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="15174-125">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="15174-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="15174-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="15174-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="15174-127">In de **zoekvak**, type **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="15174-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="15174-128">![Toepassingsgalerie](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="15174-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="15174-129">Selecteer in het deelvenster met resultaten **SCC LifeCycle**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="15174-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="15174-130">![De levenscyclus van SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC levenscyclus")</span><span class="sxs-lookup"><span data-stu-id="15174-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="15174-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="15174-131">Configure single sign-on</span></span>

<span data-ttu-id="15174-132">Het doel van deze sectie is het overzicht van het inschakelen van gebruikers worden geverifieerd bij de levenscyclus van SCC aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="15174-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="15174-133">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="15174-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="15174-134">In de klassieke Azure portal op de **SCC LifeCycle** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de ** configureren eenmalige aanmelding ** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="15174-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="15174-135">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="15174-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="15174-136">Op de **hoe wilt u dat gebruikers zich aanmelden op voor de levenscyclus van SCC** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="15174-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="15174-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="15174-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="15174-138">Op de **App-URL configureren** pagina in de **aanmelding op URL** textbox, typ de URL gebruikt door uw gebruikers aanmelden bij uw SCC LifeCycle-toepassing met het volgende patroon volgen '*https://bs1.scc.com/ lc7/Welcome/Customer/PICTtest.aspx*', en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="15174-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="15174-139">![App-URL configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="15174-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="15174-140">Op de **eenmalige aanmelding configureren op de levenscyclus van SCC** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="15174-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="15174-141">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="15174-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="15174-142">Doorsturen die metagegevensbestand aan SCC LifeCycle Support team.</span><span class="sxs-lookup"><span data-stu-id="15174-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="15174-143">Eenmalige aanmelding moet worden ingeschakeld door het ondersteuningsteam SCC levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="15174-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="15174-144">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="15174-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="15174-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="15174-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="15174-146">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="15174-146">Configure user provisioning</span></span>

<span data-ttu-id="15174-147">Zodat gebruikers van Azure AD aan te melden bij de levenscyclus van SCC moeten ze worden ingericht in de levenscyclus van SCC.</span><span class="sxs-lookup"><span data-stu-id="15174-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="15174-148">Er is geen actie-item voor configuratie gebruikersaanvragen naar SCC levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="15174-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="15174-149">Wanneer een toegewezen gebruiker probeert aan te melden bij SCC levenscyclus, wordt automatisch een SCC LifeCycle-account gemaakt, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="15174-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="15174-150">U kunt andere SCC LifeCycle gebruiker account hulpmiddelen voor het maken of API's geleverd door SCC LifeCycle aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="15174-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="15174-151">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="15174-151">Assign users</span></span>
<span data-ttu-id="15174-152">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="15174-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="15174-153">**Gebruikers om aan te wijzen SCC levenscyclus, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="15174-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="15174-154">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="15174-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="15174-155">Op de ** SCC LifeCycle ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="15174-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="15174-156">![Gebruikers toewijzen](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="15174-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="15174-157">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="15174-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="15174-158">![Ja](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="15174-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="15174-159">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="15174-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="15174-160">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15174-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

