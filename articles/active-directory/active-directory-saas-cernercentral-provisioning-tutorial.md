---
title: 'Zelfstudie: Cerner centraal configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Informatie over het configureren van Azure Active Directory automatisch inrichten-beheerders kunnen een schema in Cerner centraal.
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
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="e1268-103">Zelfstudie: Cerner centraal configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="e1268-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="e1268-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in Cerner centraal en Azure AD wilt om automatisch in te richten en inrichten van gebruikersaccounts vanuit Azure AD naar een schema van de gebruiker in Cerner centrale ongedaan.</span><span class="sxs-lookup"><span data-stu-id="e1268-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="e1268-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e1268-105">Prerequisites</span></span>

<span data-ttu-id="e1268-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="e1268-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="e1268-107">Een Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="e1268-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="e1268-108">Een tenant Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="e1268-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="e1268-109">Azure Active Directory is geïntegreerd met Cerner centraal met behulp van de [SCIM](http://www.simplecloud.info/) protocol.</span><span class="sxs-lookup"><span data-stu-id="e1268-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="e1268-110">Gebruikers toewijzen aan Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="e1268-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="e1268-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="e1268-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="e1268-112">In de context van automatische gebruikers account inrichten, worden alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="e1268-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="e1268-113">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD de gebruikers die toegang nodig tot Cerner centraal vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="e1268-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="e1268-114">Als besloten, kunt u deze gebruikers toewijzen aan Cerner centraal door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1268-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="e1268-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="e1268-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="e1268-116">Belangrijke tips voor het toewijzen van gebruikers aan Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="e1268-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="e1268-117">Het is raadzaam om één Azure AD-gebruiker worden toegewezen aan Cerner centraal voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="e1268-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="e1268-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e1268-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="e1268-119">Zodra het eerste testen is voltooid voor één gebruiker Cerner centraal raadt aan om de volledige lijst met gebruikers die bestemd zijn voor toegang tot een Cerner-oplossing (niet alleen Cerner centraal) om te worden ingericht op de gebruikerslijst van Cerner toewijzen.</span><span class="sxs-lookup"><span data-stu-id="e1268-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="e1268-120">Andere oplossingen Cerner gebruikmaken van deze lijst van gebruikers in de gebruikerslijst.</span><span class="sxs-lookup"><span data-stu-id="e1268-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="e1268-121">Wanneer een gebruiker aan Cerner centraal toewijzen, moet u de **gebruiker** rol in het dialoogvenster toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e1268-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="e1268-122">Gebruikers met de rol 'Default toegang' zijn uitgesloten van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="e1268-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="e1268-123">Gebruikersaanvragen voor Cerner centraal configureren</span><span class="sxs-lookup"><span data-stu-id="e1268-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="e1268-124">Deze sectie helpt u bij het verbinding maken met uw Azure AD Cerner centraal van gebruiker schema van Cerner SCIM gebruikersaccount gebruikt API-inrichting, en configureren van de inrichting service te maken, bijwerken en uitschakelen van de toegewezen gebruiker accounts in Cerner centrale op basis van toewijzing van gebruikers en groepen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1268-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="e1268-125">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Cerner centraal, volgt de instructies in [Azure-portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1268-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="e1268-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.</span><span class="sxs-lookup"><span data-stu-id="e1268-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="e1268-127">Zie voor meer informatie de [één centrale Cerner aanmelding zelfstudie](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e1268-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="e1268-128">Voor het configureren van automatische account gebruikersaanvragen naar Cerner centraal in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e1268-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="e1268-129">Gebruikersaccounts aan Cerner centraal inricht, hebt u nodig voor een systeemaccount Cerner centraal aanvragen bij Cerner en het genereren van een OAuth bearer-token die Azure AD gebruiken kunt voor het verbinding maken met de Cerner SCIM eindpunt.</span><span class="sxs-lookup"><span data-stu-id="e1268-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="e1268-130">Het is ook raadzaam de integratie worden uitgevoerd in een Cerner sandbox-omgeving voordat u implementeert naar productie.</span><span class="sxs-lookup"><span data-stu-id="e1268-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="e1268-131">De eerste stap is om te controleren of de mensen die het beheer van de Cerner en Azure AD-integratie hebben een CernerCare-account is vereist voor toegang tot de documentatie die nodig zijn voor de instructies.</span><span class="sxs-lookup"><span data-stu-id="e1268-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="e1268-132">Gebruik de onderstaande URL's CernerCare accounts maken in elke omgeving van toepassing, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="e1268-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="e1268-133">Sandbox: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="e1268-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="e1268-134">Productie: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="e1268-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="e1268-135">Vervolgens moet een systeem-account worden gemaakt voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1268-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="e1268-136">Volg de onderstaande instructies om aan te vragen van een systeem-Account voor uw sandbox en productie-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="e1268-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="e1268-137">Instructies: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="e1268-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="e1268-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="e1268-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="e1268-139">Productie: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="e1268-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="e1268-140">Vervolgens een OAuth bearer-token genereren voor elk van uw systeemaccounts.</span><span class="sxs-lookup"><span data-stu-id="e1268-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="e1268-141">U doet dit door de onderstaande instructies uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e1268-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="e1268-142">Instructies: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="e1268-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="e1268-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="e1268-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="e1268-144">Productie: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="e1268-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="e1268-145">Tot slot moet u aan te schaffen gebruikersnamen schema Realm voor de sandbox en de productie-omgevingen in Cerner om de configuratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e1268-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="e1268-146">Zie voor meer informatie over het verkrijgen van dit: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="e1268-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="e1268-147">Nu kunt u Azure AD om gebruikersaccounts in inrichten op Cerner te configureren.</span><span class="sxs-lookup"><span data-stu-id="e1268-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="e1268-148">Aanmelden bij de [Azure-portal](https://portal.azure.com), en blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="e1268-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="e1268-149">Als u al Cerner centraal hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Cerner centraal met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="e1268-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="e1268-150">Selecteer anders **toevoegen** en zoek naar **Cerner centraal** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e1268-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="e1268-151">Cerner centraal selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e1268-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="e1268-152">Selecteer uw exemplaar van de centrale Cerner en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e1268-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="e1268-153">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="e1268-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Cerner centraal inrichten](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="e1268-155">Vul de volgende velden onder **beheerdersreferenties**:</span><span class="sxs-lookup"><span data-stu-id="e1268-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="e1268-156">In de **Tenant-URL** en voer een URL in de notatie, "Gebruiker-schema-Realm-ID" vervangen door de realm-ID die u hebt verkregen in stap &#4;.</span><span class="sxs-lookup"><span data-stu-id="e1268-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="e1268-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="e1268-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="e1268-158">Productie: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="e1268-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="e1268-159">In de **geheim Token** veld, voert u het OAuth bearer-token die u in stap &#3; gegenereerd en klikt u op **testverbinding**.</span><span class="sxs-lookup"><span data-stu-id="e1268-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="e1268-160">U ziet een melding met succes de upperright-zijde van de portal.</span><span class="sxs-lookup"><span data-stu-id="e1268-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="e1268-161">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje hieronder in.</span><span class="sxs-lookup"><span data-stu-id="e1268-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="e1268-162">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e1268-162">Click **Save**.</span></span> 

12. <span data-ttu-id="e1268-163">In de **kenmerktoewijzingen** sectie, moet u de gebruikers- en groepskenmerken moeten worden gesynchroniseerd vanuit Azure AD naar Cerner centraal controleren.</span><span class="sxs-lookup"><span data-stu-id="e1268-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="e1268-164">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts en groepen in de centrale Cerner voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e1268-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="e1268-165">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="e1268-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="e1268-166">Om de Azure AD-service voor het hoofdkantoor Cerner inricht, wijzigen de **inrichting Status** naar **op** in de **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="e1268-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="e1268-167">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e1268-167">Click **Save**.</span></span> 

<span data-ttu-id="e1268-168">Hiermee start u de initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan de centrale Cerner in de sectie gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="e1268-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="e1268-169">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de Azure AD-service inricht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e1268-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="e1268-170">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw app Cerner centraal beschrijven.</span><span class="sxs-lookup"><span data-stu-id="e1268-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="e1268-171">Zie voor meer informatie over het lezen van de Azure AD inrichting logboeken [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="e1268-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1268-172">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e1268-172">Additional resources</span></span>

* [<span data-ttu-id="e1268-173">Cerner centraal: Publiceren van identiteitsgegevens met behulp van Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1268-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="e1268-174">Zelfstudie: Cerner centraal configureren voor eenmalige aanmelding bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1268-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="e1268-175">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="e1268-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="e1268-176">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1268-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="e1268-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e1268-177">Next steps</span></span>
* <span data-ttu-id="e1268-178">[Informatie over het bekijken van Logboeken en rapporten over het inrichten van de activiteit](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="e1268-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
