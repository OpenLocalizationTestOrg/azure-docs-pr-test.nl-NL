---
title: 'Zelfstudie: Azure Active Directory-integratie met Coupa | Microsoft Docs'
description: Lees hoe toouse Coupa met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="e3525-103">Zelfstudie: Azure Active Directory-integratie met Coupa</span><span class="sxs-lookup"><span data-stu-id="e3525-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="e3525-104">Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Coupa.</span><span class="sxs-lookup"><span data-stu-id="e3525-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="e3525-105">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e3525-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="e3525-106">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e3525-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e3525-107">Een Coupa eenmalige aanmelding (SSO) ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e3525-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="e3525-108">Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooCoupa kunnen toosingle Meld u aan bij Hallo toepassing hello [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3525-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="e3525-109">Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3525-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="e3525-110">Hallo toepassingsintegratie voor Coupa inschakelen</span><span class="sxs-lookup"><span data-stu-id="e3525-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="e3525-111">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="e3525-111">Configuring single sign-on</span></span>
* <span data-ttu-id="e3525-112">Configuratie van gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="e3525-112">Configuring user provisioning</span></span>
* <span data-ttu-id="e3525-113">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e3525-113">Assigning users</span></span>

<span data-ttu-id="e3525-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="e3525-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="e3525-115">Hallo toepassingsintegratie voor Coupa inschakelen</span><span class="sxs-lookup"><span data-stu-id="e3525-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="e3525-116">Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Coupa.</span><span class="sxs-lookup"><span data-stu-id="e3525-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="e3525-117">**tooenable hello toepassingsintegratie voor Coupa, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e3525-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3525-118">Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3525-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="e3525-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e3525-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e3525-120">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="e3525-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="e3525-121">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3525-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="e3525-122">![Toepassingen](./media/active-directory-saas-coupa-tutorial/IC700994.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="e3525-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e3525-123">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="e3525-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="e3525-124">![Toepassing toevoegen](./media/active-directory-saas-coupa-tutorial/IC749321.png "toepassing toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e3525-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e3525-125">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="e3525-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="e3525-126">![Een toepassing toevoegen van gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "een toepassing van gallerry toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e3525-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e3525-127">In Hallo **zoekvak**, type **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="e3525-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="e3525-128">![Toepassingsgalerie](./media/active-directory-saas-coupa-tutorial/IC791898.png "-Toepassingsgalerie")</span><span class="sxs-lookup"><span data-stu-id="e3525-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="e3525-129">Selecteer in het deelvenster met resultaten Hallo **Coupa**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e3525-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="e3525-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="e3525-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e3525-131">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="e3525-131">Configure single sign-on</span></span>

<span data-ttu-id="e3525-132">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooCoupa aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="e3525-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="e3525-133">Eenmalige aanmelding voor Coupa configureren, moet u een vingerafdrukwaarde van een certificaat tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="e3525-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="e3525-134">Als u niet bekend met deze procedure bent, Zie [hoe tooretrieve vingerafdrukwaarde van een certificaat](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="e3525-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="e3525-135">**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e3525-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3525-136">Meld u op tooyour Coupa bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="e3525-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="e3525-137">Ga te**Setup \> beveiligingscontrole**.</span><span class="sxs-lookup"><span data-stu-id="e3525-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="e3525-138">![Beveiligingsmechanismen](./media/active-directory-saas-coupa-tutorial/IC791900.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="e3525-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="e3525-139">toodownload hello Coupa metagegevens bestand tooyour computer, klikt u op **downloaden en importeren van metagegevens van de Serviceprovider**.</span><span class="sxs-lookup"><span data-stu-id="e3525-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="e3525-140">![Coupa SP metagegevens](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metagegevens")</span><span class="sxs-lookup"><span data-stu-id="e3525-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="e3525-141">Aanmelding in een ander browservenster toohello klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e3525-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="e3525-142">Op Hallo **Coupa** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e3525-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="e3525-143">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791902.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e3525-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="e3525-144">Op Hallo **wilt u hoe gebruikers toosign op tooCoupa** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e3525-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="e3525-145">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791903.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e3525-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="e3525-146">Op Hallo **App-URL configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3525-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="e3525-147">![App-URL configureren](./media/active-directory-saas-coupa-tutorial/IC791904.png "App-URL configureren")</span><span class="sxs-lookup"><span data-stu-id="e3525-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="e3525-148">In Hallo **aanmelding op URL** textbox, typ de URL die wordt gebruikt door uw gebruikers toosign op tooyour Coupa toepassing (bijvoorbeeld: '*http://company.Coupa.com*').</span><span class="sxs-lookup"><span data-stu-id="e3525-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="e3525-149">Open het gedownloade Coupa metagegevens-bestand en kopieer Hallo **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="e3525-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="e3525-150">In Hallo **Coupa antwoord-URL** textbox plakken Hallo **AssertionConsumerService index/URL** waarde.</span><span class="sxs-lookup"><span data-stu-id="e3525-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="e3525-151">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e3525-151">Click **Next**.</span></span>
8. <span data-ttu-id="e3525-152">Op Hallo **eenmalige aanmelding configureren op Coupa** pagina, toodownload uw bestand met metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo bestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e3525-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="e3525-153">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791905.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e3525-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="e3525-154">Ga te op Hallo Coupa bedrijf site**Setup \> beveiligingscontrole**.</span><span class="sxs-lookup"><span data-stu-id="e3525-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="e3525-155">![Beveiligingsmechanismen](./media/active-directory-saas-coupa-tutorial/IC791900.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="e3525-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="e3525-156">In Hallo **Meld u aan met referenties Coupa** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3525-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="e3525-157">![Meld u aan met referenties Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Meld u aan met referenties Coupa")</span><span class="sxs-lookup"><span data-stu-id="e3525-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="e3525-158">Selecteer **aanmelden via SAML**.</span><span class="sxs-lookup"><span data-stu-id="e3525-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="e3525-159">Klik op **Bladeren** tooupload het gedownloade bestand voor Azure Active metagegevens.</span><span class="sxs-lookup"><span data-stu-id="e3525-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="e3525-160">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e3525-160">Click **Save**.</span></span>
11. <span data-ttu-id="e3525-161">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e3525-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="e3525-162">![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791907.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e3525-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="e3525-163">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="e3525-163">Configure user provisioning</span></span>

<span data-ttu-id="e3525-164">In de volgorde tooenable Azure AD gebruikers toolog in Coupa, moeten ze worden ingericht in Coupa.</span><span class="sxs-lookup"><span data-stu-id="e3525-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="e3525-165">In geval van Coupa Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e3525-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="e3525-166">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e3525-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3525-167">Meld u bij tooyour **Coupa** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="e3525-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="e3525-168">Klik in het menu bovenaan Hallo Hallo **Setup**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e3525-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="e3525-169">![Gebruikers](./media/active-directory-saas-coupa-tutorial/IC791908.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="e3525-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="e3525-170">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3525-170">Click **Create**.</span></span>
   
   <span data-ttu-id="e3525-171">![Gebruikers maken](./media/active-directory-saas-coupa-tutorial/IC791909.png "gebruikers maken")</span><span class="sxs-lookup"><span data-stu-id="e3525-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="e3525-172">In Hallo **gebruiker maken** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3525-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e3525-173">![Details van gebruiker](./media/active-directory-saas-coupa-tutorial/IC791910.png "Gebruikersdetails")</span><span class="sxs-lookup"><span data-stu-id="e3525-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="e3525-174">Type Hallo **aanmelding**, **voornaam**, **achternaam**, **Single Sign-On-ID**, **e** kenmerken van een geldige gewenste tooprovision in hello Azure Active Directory-account gerelateerd tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="e3525-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="e3525-175">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3525-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="e3525-176">Hello Azure Active Directory-accounthouder krijgt een e-mail met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="e3525-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="e3525-177">U kunt andere Coupa gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Coupa tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e3525-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="e3525-178">Gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="e3525-178">Assign users</span></span>
<span data-ttu-id="e3525-179">tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="e3525-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="e3525-180">**tooassign gebruikers tooCoupa, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="e3525-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3525-181">In de klassieke Azure-portal hello, een testaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="e3525-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e3525-182">Op Hallo ** Coupa ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="e3525-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e3525-183">![Gebruikers toewijzen](./media/active-directory-saas-coupa-tutorial/IC791911.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="e3525-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="e3525-184">Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3525-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="e3525-185">![Ja](./media/active-directory-saas-coupa-tutorial/IC767830.png "Ja")</span><span class="sxs-lookup"><span data-stu-id="e3525-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e3525-186">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="e3525-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e3525-187">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3525-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

