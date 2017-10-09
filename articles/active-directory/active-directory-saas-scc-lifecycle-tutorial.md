---
title: 'Zelfstudie: Azure Active Directory-integratie met SCC LifeCycle | Microsoft Docs'
description: Lees hoe toouse SCC LifeCycle met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="a81b2-103">Zelfstudie: Azure Active Directory-integratie met SCC levenscyclus</span><span class="sxs-lookup"><span data-stu-id="a81b2-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="a81b2-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en SCC levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="a81b2-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="a81b2-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a81b2-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="a81b2-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="a81b2-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a81b2-107">Een SCC LifeCycle eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a81b2-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a81b2-108">Na het voltooien van deze zelfstudie hello Azure AD-gebruikers die u hebt toegewezen tooSCC LifeCycle worden kunnen toosingle teken in de toepassing hello op uw site in de levenscyclus van SCC bedrijf (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [Inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a81b2-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a81b2-109">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a81b2-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="a81b2-110">Hallo toepassingsintegratie voor SCC levenscyclus inschakelen</span><span class="sxs-lookup"><span data-stu-id="a81b2-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="a81b2-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="a81b2-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="a81b2-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="a81b2-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="a81b2-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="a81b2-113">Assigning users</span></span>

<span data-ttu-id="a81b2-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a81b2-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="a81b2-115">Hallo toepassingsintegratie voor SCC levenscyclus inschakelen</span><span class="sxs-lookup"><span data-stu-id="a81b2-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="a81b2-116">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor SCC levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="a81b2-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="a81b2-117">**tooenable hello toepassingsintegratie voor SCC levenscyclus, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a81b2-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="a81b2-118">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a81b2-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="a81b2-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a81b2-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a81b2-120">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="a81b2-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a81b2-121">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="a81b2-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="a81b2-122">![Toepassingen](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="a81b2-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a81b2-123">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="a81b2-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="a81b2-124">![Toepassing toevoegen](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="a81b2-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a81b2-125">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="a81b2-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="a81b2-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="a81b2-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a81b2-127">In Hallo **zoekvak**, type **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="a81b2-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="a81b2-128">![Toepassingsgalerie](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="a81b2-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="a81b2-129">Selecteer in het deelvenster met resultaten Hallo **SCC LifeCycle**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a81b2-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="a81b2-130">![De levenscyclus van SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC levenscyclus")</span><span class="sxs-lookup"><span data-stu-id="a81b2-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a81b2-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="a81b2-131">Configure single sign-on</span></span>

<span data-ttu-id="a81b2-132">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooSCC LifeCycle aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="a81b2-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="a81b2-133">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a81b2-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="a81b2-134">In de klassieke Azure-portal op Hallo Hallo **SCC LifeCycle** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen Hallo ** configureren eenmalige aanmelding ** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a81b2-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="a81b2-135">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="a81b2-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="a81b2-136">Op Hallo **wilt u hoe gebruikers toosign op tooSCC LifeCycle** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a81b2-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="a81b2-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="a81b2-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="a81b2-138">Op Hallo **App-URL configureren** pagina in Hallo **aanmelding op URL** textbox type Hallo URL gebruikt door uw gebruikers toosign op tooyour SCC LifeCycle toepassing hello patroon volgen met '*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*', en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a81b2-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="a81b2-139">![App-URL configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="a81b2-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="a81b2-140">Op Hallo **eenmalige aanmelding configureren op de levenscyclus van SCC** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a81b2-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="a81b2-141">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="a81b2-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="a81b2-142">Doorsturen die metagegevens bestand tooSCC LifeCycle Support team.</span><span class="sxs-lookup"><span data-stu-id="a81b2-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="a81b2-143">Eenmalige aanmelding heeft toobe ingeschakeld door Hallo SCC LifeCycle ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="a81b2-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="a81b2-144">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a81b2-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="a81b2-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="a81b2-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="a81b2-146">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="a81b2-146">Configure user provisioning</span></span>

<span data-ttu-id="a81b2-147">In volgorde tooenable Azure AD gebruikers toolog in SCC levenscyclus, moeten ze worden ingericht in SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="a81b2-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="a81b2-148">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooSCC levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="a81b2-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="a81b2-149">Wanneer een toegewezen gebruiker probeert toolog in SCC levenscyclus, wordt automatisch een SCC LifeCycle-account gemaakt, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a81b2-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="a81b2-150">U kunt andere SCC LifeCycle gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door SCC LifeCycle tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="a81b2-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="a81b2-151">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="a81b2-151">Assign users</span></span>
<span data-ttu-id="a81b2-152">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="a81b2-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="a81b2-153">**tooassign gebruikers tooSCC levensduur, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a81b2-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="a81b2-154">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="a81b2-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a81b2-155">Op Hallo ** SCC LifeCycle ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="a81b2-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="a81b2-156">![Gebruikers toewijzen](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="a81b2-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="a81b2-157">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="a81b2-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="a81b2-158">![Ja](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="a81b2-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a81b2-159">Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a81b2-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="a81b2-160">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a81b2-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

