---
title: 'Zelfstudie: Azure Active Directory-integratie met Qualtrics | Microsoft Docs'
description: Lees hoe toouse Qualtrics met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="1c925-103">Zelfstudie: Azure Active Directory-integratie met Qualtrics</span><span class="sxs-lookup"><span data-stu-id="1c925-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="1c925-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="1c925-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="1c925-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1c925-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="1c925-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="1c925-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1c925-107">Een Qualtrics eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1c925-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="1c925-108">Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooQualtrics kunnen toosingle Meld u aan bij Hallo-toepassing op uw Qualtrics bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [inleiding toohello Toegang tot Configuratiescherm](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c925-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="1c925-109">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c925-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="1c925-110">Hallo toepassingsintegratie voor Qualtrics inschakelen</span><span class="sxs-lookup"><span data-stu-id="1c925-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="1c925-111">Configureren van eenmalige aanmelding (SSO)</span><span class="sxs-lookup"><span data-stu-id="1c925-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="1c925-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="1c925-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="1c925-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="1c925-113">Assigning users</span></span>

<span data-ttu-id="1c925-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="1c925-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="1c925-115">Hallo toepassingsintegratie voor Qualtrics inschakelen</span><span class="sxs-lookup"><span data-stu-id="1c925-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="1c925-116">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="1c925-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="1c925-117">**tooenable hello toepassingsintegratie voor Qualtrics, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1c925-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c925-118">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c925-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="1c925-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1c925-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1c925-120">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="1c925-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="1c925-121">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c925-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="1c925-122">![Toepassingen](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="1c925-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1c925-123">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="1c925-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="1c925-124">![Toepassing toevoegen](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="1c925-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="1c925-125">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="1c925-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="1c925-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="1c925-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="1c925-127">In Hallo **zoekvak**, type **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="1c925-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="1c925-128">![Toepassingsgalerie](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="1c925-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="1c925-129">Selecteer in het deelvenster met resultaten Hallo **Qualtrics**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c925-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="1c925-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="1c925-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="1c925-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="1c925-131">Configure single sign-on</span></span>

<span data-ttu-id="1c925-132">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooQualtrics aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="1c925-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="1c925-133">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1c925-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c925-134">In de klassieke Azure-portal op Hallo Hallo **Qualtrics** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c925-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="1c925-135">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1c925-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="1c925-136">Op Hallo **wilt u hoe gebruikers toosign op tooQualtrics** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1c925-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="1c925-137">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1c925-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="1c925-138">Op Hallo **App-URL configureren** pagina in Hallo **Qualtrics aanmelding op URL** textbox, typ de URL (bijvoorbeeld: '*https://ssotest2ut1.qualtrics.com*'), en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="1c925-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="1c925-139">![App-URL configureren](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="1c925-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="1c925-140">Op Hallo **eenmalige aanmelding configureren op Qualtrics** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1c925-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="1c925-141">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1c925-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="1c925-142">Hallo metagegevens bestand toohello Qualtrics ondersteuningsteam verzenden.</span><span class="sxs-lookup"><span data-stu-id="1c925-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1c925-143">Hallo SSO-configuratie heeft toobe uitgevoerd door Hallo Qualtrics ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="1c925-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="1c925-144">U ontvangt een melding zodra het Hallo-configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1c925-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="1c925-145">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c925-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="1c925-146">![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="1c925-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="1c925-147">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="1c925-147">Configure user provisioning</span></span>

<span data-ttu-id="1c925-148">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooQualtrics.</span><span class="sxs-lookup"><span data-stu-id="1c925-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="1c925-149">Wanneer een toegewezen gebruiker toolog in Qualtrics met behulp van het toegangsvenster hello probeert, controleert Qualtrics of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="1c925-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="1c925-150">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="1c925-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="1c925-151">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="1c925-151">Assign users</span></span>
<span data-ttu-id="1c925-152">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="1c925-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="1c925-153">**tooassign gebruikers tooQualtrics, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1c925-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c925-154">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="1c925-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1c925-155">Op Hallo **Qualtrics** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="1c925-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1c925-156">![Gebruikers toewijzen](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="1c925-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="1c925-157">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="1c925-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="1c925-158">![Ja](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="1c925-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1c925-159">Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1c925-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="1c925-160">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c925-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

