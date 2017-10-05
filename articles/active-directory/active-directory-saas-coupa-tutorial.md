---
title: 'Zelfstudie: Azure Active Directory-integratie met Coupa | Microsoft Docs'
description: Meer informatie over het gebruik van Coupa met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="68461-103">Zelfstudie: Azure Active Directory-integratie met Coupa</span><span class="sxs-lookup"><span data-stu-id="68461-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="68461-104">Het doel van deze zelfstudie is om de integratie van Azure en Coupa weer te geven.</span><span class="sxs-lookup"><span data-stu-id="68461-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="68461-105">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="68461-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="68461-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="68461-106">A valid Azure subscription</span></span>
* <span data-ttu-id="68461-107">Een Coupa eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="68461-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="68461-108">Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Coupa kan worden één Meld u aan bij de toepassing met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68461-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="68461-109">Het scenario in deze zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="68461-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="68461-110">De integratie van toepassingen voor Coupa inschakelen</span><span class="sxs-lookup"><span data-stu-id="68461-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="68461-111">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="68461-111">Configuring single sign-on</span></span>
* <span data-ttu-id="68461-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="68461-112">Configuring user provisioning</span></span>
* <span data-ttu-id="68461-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="68461-113">Assigning users</span></span>

<span data-ttu-id="68461-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="68461-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="68461-115">De integratie van toepassingen voor Coupa inschakelen</span><span class="sxs-lookup"><span data-stu-id="68461-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="68461-116">Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor Coupa overzicht.</span><span class="sxs-lookup"><span data-stu-id="68461-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="68461-117">**Als u wilt de integratie van toepassingen voor Coupa inschakelen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="68461-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="68461-118">Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68461-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="68461-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="68461-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="68461-120">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="68461-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="68461-121">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="68461-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="68461-122">![Toepassingen](./media/active-directory-saas-coupa-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="68461-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="68461-123">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="68461-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="68461-124">![Toepassing toevoegen](./media/active-directory-saas-coupa-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="68461-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="68461-125">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="68461-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="68461-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="68461-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="68461-127">In de **zoekvak**, type **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="68461-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="68461-128">![Toepassingsgalerie](./media/active-directory-saas-coupa-tutorial/IC791898.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="68461-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="68461-129">Selecteer in het deelvenster met resultaten **Coupa**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="68461-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="68461-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="68461-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="68461-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="68461-131">Configure single sign-on</span></span>

<span data-ttu-id="68461-132">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren Coupa aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="68461-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="68461-133">Eenmalige aanmelding voor Coupa configureren, moet u een vingerafdrukwaarde wordt opgehaald uit een certificaat.</span><span class="sxs-lookup"><span data-stu-id="68461-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="68461-134">Als u niet bekend met deze procedure bent, Zie [hoe op te halen van een certificaat vingerafdrukwaarde](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="68461-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="68461-135">**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="68461-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="68461-136">Meld u op met uw bedrijf Coupa site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="68461-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="68461-137">Ga naar **Setup \> beveiligingscontrole**.</span><span class="sxs-lookup"><span data-stu-id="68461-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="68461-138">![Beveiligingsmechanismen](./media/active-directory-saas-coupa-tutorial/IC791900.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="68461-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="68461-139">Het bestand te downloaden Coupa metagegevens op uw computer, klikt u op **downloaden en importeren SP metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="68461-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="68461-140">![Coupa SP metagegevens](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metagegevens")</span><span class="sxs-lookup"><span data-stu-id="68461-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="68461-141">In een ander browservenster, moet u zich aanmelden bij de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="68461-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="68461-142">Op de **Coupa** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="68461-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="68461-143">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791902.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="68461-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="68461-144">Op de **hoe wilt u dat gebruikers zich aanmelden op Coupa** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="68461-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="68461-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791903.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="68461-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="68461-146">Op de **App-URL configureren** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="68461-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="68461-147">![App-URL configureren](./media/active-directory-saas-coupa-tutorial/IC791904.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="68461-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="68461-148">In de **aanmelding op URL** textbox, typ de URL die wordt gebruikt door uw gebruikers aanmelden bij uw toepassing Coupa (bijvoorbeeld: '*http://company.Coupa.com*').</span><span class="sxs-lookup"><span data-stu-id="68461-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="68461-149">Open het gedownloade Coupa metagegevens-bestand en kopieer de **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="68461-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="68461-150">In de **Coupa antwoord-URL** textbox, plak de **AssertionConsumerService index/URL** waarde.</span><span class="sxs-lookup"><span data-stu-id="68461-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="68461-151">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="68461-151">Click **Next**.</span></span>
8. <span data-ttu-id="68461-152">Op de **eenmalige aanmelding configureren op Coupa** pagina voor het downloaden van het metagegevensbestand, klikt u op **metagegevens downloaden**, en sla het bestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="68461-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="68461-153">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791905.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="68461-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="68461-154">Op de site van het bedrijf Coupa, gaat u naar **Setup \> beveiligingscontrole**.</span><span class="sxs-lookup"><span data-stu-id="68461-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="68461-155">![Beveiligingsmechanismen](./media/active-directory-saas-coupa-tutorial/IC791900.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="68461-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="68461-156">In de **Meld u aan met referenties Coupa** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="68461-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="68461-157">![Meld u aan met referenties Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Meld u aan met referenties Coupa")</span><span class="sxs-lookup"><span data-stu-id="68461-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="68461-158">Selecteer **aanmelden via SAML**.</span><span class="sxs-lookup"><span data-stu-id="68461-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="68461-159">Klik op **Bladeren** uw gedownloade Azure Active-metagegevens-bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="68461-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="68461-160">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="68461-160">Click **Save**.</span></span>
11. <span data-ttu-id="68461-161">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="68461-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="68461-162">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791907.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="68461-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="68461-163">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="68461-163">Configure user provisioning</span></span>

<span data-ttu-id="68461-164">Om in te schakelen gebruikers van Azure AD aan te melden bij Coupa, moeten ze worden ingericht in Coupa.</span><span class="sxs-lookup"><span data-stu-id="68461-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="68461-165">In het geval van Coupa is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="68461-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="68461-166">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="68461-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="68461-167">Meld u aan bij uw **Coupa** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="68461-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="68461-168">Klik in het menu bovenaan op **Setup**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="68461-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="68461-169">![Gebruikers](./media/active-directory-saas-coupa-tutorial/IC791908.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="68461-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="68461-170">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="68461-170">Click **Create**.</span></span>
   
   <span data-ttu-id="68461-171">![Gebruikers maken](./media/active-directory-saas-coupa-tutorial/IC791909.png "gebruikers maken")</span><span class="sxs-lookup"><span data-stu-id="68461-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="68461-172">In de **gebruiker maken** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="68461-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="68461-173">![Details van gebruiker](./media/active-directory-saas-coupa-tutorial/IC791910.png "Gebruikersdetails")</span><span class="sxs-lookup"><span data-stu-id="68461-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="68461-174">Typ de **aanmelding**, **voornaam**, **achternaam**, **Single Sign-On-ID**, **e** kenmerken van een geldige Azure Active Directory-account die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="68461-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="68461-175">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="68461-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="68461-176">De houder van Azure Active Directory-account ontvangt een e-mailbericht met een koppeling naar het account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="68461-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="68461-177">U kunt andere Coupa gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Coupa aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="68461-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="68461-178">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="68461-178">Assign users</span></span>
<span data-ttu-id="68461-179">Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="68461-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="68461-180">**Gebruikers om aan te wijzen Coupa, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="68461-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="68461-181">In de klassieke Azure portal een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="68461-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="68461-182">Op de ** Coupa ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="68461-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="68461-183">![Gebruikers toewijzen](./media/active-directory-saas-coupa-tutorial/IC791911.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="68461-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="68461-184">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="68461-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="68461-185">![Ja](./media/active-directory-saas-coupa-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="68461-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="68461-186">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="68461-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="68461-187">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68461-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

