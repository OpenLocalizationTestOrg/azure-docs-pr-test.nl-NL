---
title: 'Zelfstudie: Cerner centraal configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe Azure Active Directory-tooautomatically tooconfigure gebruikers tooa schema in Cerner centrale inrichten.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="ef907-103">Zelfstudie: Cerner centraal configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="ef907-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="ef907-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Cerner centraal en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooa gebruiker schema in Cerner centrale Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef907-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="ef907-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ef907-105">Prerequisites</span></span>

<span data-ttu-id="ef907-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ef907-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ef907-107">Een Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="ef907-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="ef907-108">Een tenant Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="ef907-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="ef907-109">Azure Active Directory is geïntegreerd met Cerner centraal Hallo met [SCIM](http://www.simplecloud.info/) protocol.</span><span class="sxs-lookup"><span data-stu-id="ef907-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="ef907-110">Toewijzen van gebruikers tooCerner centraal</span><span class="sxs-lookup"><span data-stu-id="ef907-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="ef907-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="ef907-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ef907-112">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="ef907-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="ef907-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u bepalen welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooCerner centraal vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="ef907-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="ef907-114">Als besloten, kunt u deze gebruikers tooCerner centraal kunt toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef907-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="ef907-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="ef907-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="ef907-116">Belangrijke tips voor het toewijzen van gebruikers tooCerner centraal</span><span class="sxs-lookup"><span data-stu-id="ef907-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="ef907-117">Het is raadzaam om één Azure AD-gebruiker tooCerner centrale tootest Hallo inrichting configuratie worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ef907-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="ef907-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ef907-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="ef907-119">Zodra de eerste testen is voltooid voor één gebruiker, raadt Cerner centraal Hallo volledige lijst met gebruikers die zijn bedoeld tooaccess gebruikerslijst alle Cerner oplossing (niet alleen Cerner centraal) toobe ingericht tooCerner toewijzen.</span><span class="sxs-lookup"><span data-stu-id="ef907-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="ef907-120">Andere oplossingen Cerner gebruikmaken van deze lijst van gebruikers in de gebruikerslijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef907-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="ef907-121">Wanneer u een gebruiker tooCerner centraal toewijst, moet u Hallo **gebruiker** rol in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="ef907-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="ef907-122">Gebruikers met Hallo 'Default toegang' rol worden uitgesloten van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="ef907-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="ef907-123">Gebruikers inrichten tooCerner centraal configureren</span><span class="sxs-lookup"><span data-stu-id="ef907-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="ef907-124">In deze sectie helpt u bij het verbinden van uw Azure AD tooCerner centraal gebruiker schema van Cerner SCIM gebruikersaccount gebruikt API-inrichting en Hallo service toocreate inrichting configureren, bijwerken en toegewezen gebruiker op basis van accounts in Cerner centrale uitschakelen op de toewijzing van gebruikers en groepen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef907-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="ef907-125">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Cerner centraal, Hallo-instructies die zijn opgegeven in [Azure-portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef907-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="ef907-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.</span><span class="sxs-lookup"><span data-stu-id="ef907-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="ef907-127">Zie voor meer informatie, Hallo [één centrale Cerner aanmelding zelfstudie](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ef907-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="ef907-128">tooconfigure automatische gebruikersaccount tooCerner centraal ingericht in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ef907-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="ef907-129">In de volgorde tooprovision gebruiker accounts tooCerner centraal, u moet een Cerner centraal system-account van Cerner toorequest, en genereren van een OAuth-bearer-token die Azure AD van tooconnect tooCerner SCIM eindpunt kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef907-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="ef907-130">Het wordt ook aanbevolen Hallo integratie worden uitgevoerd in een Cerner sandbox-omgeving voordat u tooproduction implementeert.</span><span class="sxs-lookup"><span data-stu-id="ef907-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="ef907-131">Hallo eerste stap is tooensure Hallo mensen Hallo Cerner beheren en Azure AD-integratie hebben een CernerCare-account is vereist tooaccess Hallo documentatie nodig toocomplete Hallo instructies.</span><span class="sxs-lookup"><span data-stu-id="ef907-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="ef907-132">Gebruik indien nodig Hallo-URL's onder toocreate CernerCare accounts in elke omgeving van toepassing.</span><span class="sxs-lookup"><span data-stu-id="ef907-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="ef907-133">Sandbox: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="ef907-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="ef907-134">Productie: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="ef907-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="ef907-135">Vervolgens moet een systeem-account worden gemaakt voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef907-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="ef907-136">Hallo instructies hieronder toorequest een systeemaccount gebruiken voor uw sandbox en productie-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="ef907-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="ef907-137">Instructies: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="ef907-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="ef907-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ef907-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="ef907-139">Productie: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ef907-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="ef907-140">Vervolgens een OAuth bearer-token genereren voor elk van uw systeemaccounts.</span><span class="sxs-lookup"><span data-stu-id="ef907-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="ef907-141">toodo deze, Hallo instructies hieronder.</span><span class="sxs-lookup"><span data-stu-id="ef907-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="ef907-142">Instructies: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="ef907-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="ef907-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ef907-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="ef907-144">Productie: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ef907-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="ef907-145">Tot slot moet u tooacquire gebruikers schema Realm-id's voor beide Hallo sandbox en productie-omgevingen in Cerner toocomplete Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="ef907-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="ef907-146">Voor meer informatie over tooacquire deze, Zie: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="ef907-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="ef907-147">Nu kunt u Azure AD tooprovision gebruiker accounts tooCerner configureren.</span><span class="sxs-lookup"><span data-stu-id="ef907-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="ef907-148">Meld u aan toohello [Azure-portal](https://portal.azure.com), en blader toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="ef907-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="ef907-149">Als u Cerner centraal al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Cerner centraal met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ef907-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="ef907-150">Selecteer anders **toevoegen** en zoek naar **Cerner centraal** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="ef907-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="ef907-151">Selecteer Cerner centraal in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ef907-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="ef907-152">Selecteer uw exemplaar van de centrale Cerner en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ef907-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="ef907-153">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="ef907-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Cerner centraal inrichten](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="ef907-155">Hallo volgen onder velden invullen **beheerdersreferenties**:</span><span class="sxs-lookup"><span data-stu-id="ef907-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="ef907-156">In Hallo **Tenant-URL** veld, voer een URL in de indeling Hallo hieronder, "Gebruiker-schema-Realm-ID" vervangen door een Hallo realm ID die u hebt verkregen in stap &#4;.</span><span class="sxs-lookup"><span data-stu-id="ef907-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="ef907-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="ef907-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="ef907-158">Productie: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="ef907-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="ef907-159">In Hallo **geheim Token** veld Hallo OAuth bearer-token die u in stap &#3; gegenereerd en op **testverbinding**.</span><span class="sxs-lookup"><span data-stu-id="ef907-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="ef907-160">U ziet een melding geslaagd Hallo upperright zijde van de portal.</span><span class="sxs-lookup"><span data-stu-id="ef907-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="ef907-161">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="ef907-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="ef907-162">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ef907-162">Click **Save**.</span></span> 

12. <span data-ttu-id="ef907-163">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruiker en groep kenmerken toobe gesynchroniseerd met Azure AD tooCerner centraal.</span><span class="sxs-lookup"><span data-stu-id="ef907-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="ef907-164">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts en groepen in de centrale Cerner voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ef907-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="ef907-165">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ef907-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="ef907-166">tooenable Hallo inrichting Azure AD-service voor het hoofdkantoor Cerner, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="ef907-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="ef907-167">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ef907-167">Click **Save**.</span></span> 

<span data-ttu-id="ef907-168">Hiermee start u de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooCerner centraal in de sectie gebruikers en groepen Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ef907-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="ef907-169">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang Hallo inrichting Azure AD-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ef907-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="ef907-170">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Cerner centraal inrichting beschrijven.</span><span class="sxs-lookup"><span data-stu-id="ef907-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="ef907-171">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="ef907-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef907-172">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ef907-172">Additional resources</span></span>

* [<span data-ttu-id="ef907-173">Cerner centraal: Publiceren van identiteitsgegevens met behulp van Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef907-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="ef907-174">Zelfstudie: Cerner centraal configureren voor eenmalige aanmelding bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef907-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="ef907-175">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="ef907-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="ef907-176">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ef907-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="ef907-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef907-177">Next steps</span></span>
* <span data-ttu-id="ef907-178">[Meer informatie over hoe tooreview registreert en get rapporten over het inrichten van de activiteit](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="ef907-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
