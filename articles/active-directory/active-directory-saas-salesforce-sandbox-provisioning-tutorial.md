---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a><span data-ttu-id="e496e-103">Zelfstudie: Sandbox-Salesforce configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="e496e-103">Tutorial: Configuring Salesforce Sandbox for Automatic User Provisioning</span></span>

<span data-ttu-id="e496e-104">Hallo-doel van deze zelfstudie is tooshow Hallo van stappen die u moet tooperform in Salesforce Sandbox en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e496e-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Salesforce Sandbox and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSalesforce Sandbox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e496e-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e496e-105">Prerequisites</span></span>

<span data-ttu-id="e496e-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e496e-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="e496e-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="e496e-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="e496e-108">U moet een geldige tenant voor Salesforce Sandbox voor werk of Salesforce Sandbox voor onderwijs hebben.</span><span class="sxs-lookup"><span data-stu-id="e496e-108">You must have a valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education.</span></span> <span data-ttu-id="e496e-109">U kunt een gratis proefaccount voor de service.</span><span class="sxs-lookup"><span data-stu-id="e496e-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="e496e-110">Een gebruikersaccount in Salesforce Sandbox met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="e496e-110">A user account in Salesforce Sandbox with Team Admin permissions.</span></span>

## <a name="assigning-users-toosalesforce-sandbox"></a><span data-ttu-id="e496e-111">Toewijzen van gebruikers tooSalesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="e496e-111">Assigning users tooSalesforce Sandbox</span></span>

<span data-ttu-id="e496e-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="e496e-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="e496e-113">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="e496e-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="e496e-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Salesforce Sandbox app vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="e496e-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Salesforce Sandbox app.</span></span> <span data-ttu-id="e496e-115">Als besloten, kunt u deze gebruikers tooyour Salesforce Sandbox app toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="e496e-115">Once decided, you can assign these users tooyour Salesforce Sandbox app by following hello instructions here:</span></span>

[<span data-ttu-id="e496e-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="e496e-116">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a><span data-ttu-id="e496e-117">Belangrijke tips voor het toewijzen van gebruikers tooSalesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="e496e-117">Important tips for assigning users tooSalesforce Sandbox</span></span>

* <span data-ttu-id="e496e-118">Het is raadzaam om één tooSalesforce Sandbox tootest Hallo configuratie inrichten door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e496e-118">It is recommended that a single Azure AD user is assigned tooSalesforce Sandbox tootest hello provisioning configuration.</span></span> <span data-ttu-id="e496e-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e496e-119">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="e496e-120">U moet een geldige gebruikersrol selecteren bij het toewijzen van een gebruiker tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e496e-120">When assigning a user tooSalesforce Sandbox, you must select a valid user role.</span></span> <span data-ttu-id="e496e-121">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="e496e-121">hello "Default Access" role does not work for provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="e496e-122">Deze app importeert aangepaste rollen van Salesforce Sandbox als onderdeel van Hallo inrichtingsproces, welke klant Hallo wil tooselect bij het toewijzen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e496e-122">This app imports custom roles from Salesforce Sandbox as part of hello provisioning process, which hello customer may want tooselect when assigning users.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="e496e-123">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="e496e-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="e496e-124">Deze sectie helpt u bij het verbinden van uw Azure AD tooSalesforce Sandbox gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van de toegewezen gebruiker accounts in het Salesforce-Sandbox op basis van gebruikers en groepen toewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e496e-124">This section guides you through connecting your Azure AD tooSalesforce Sandbox's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="e496e-125">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Salesforce Sandbox, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e496e-125">You may also choose tooenabled SAML-based Single Sign-On for Salesforce Sandbox, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e496e-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="e496e-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="e496e-127">tooconfigure automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="e496e-127">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="e496e-128">Hallo-doel van deze sectie is het toooutline hoe tooenable gebruikers inrichten van Active Directory-gebruiker accounts tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e496e-128">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

1. <span data-ttu-id="e496e-129">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="e496e-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="e496e-130">Als u Salesforce Sandbox al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Salesforce Sandbox met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e496e-130">If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using hello search field.</span></span> <span data-ttu-id="e496e-131">Selecteer anders **toevoegen** en zoek naar **Salesforce Sandbox** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="e496e-131">Otherwise, select **Add** and search for **Salesforce Sandbox** in hello application gallery.</span></span> <span data-ttu-id="e496e-132">Selecteer Salesforce Sandbox in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e496e-132">Select Salesforce Sandbox from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="e496e-133">Selecteer uw exemplaar van Salesforce Sandbox en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e496e-133">Select your instance of Salesforce Sandbox, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="e496e-134">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="e496e-134">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
    <span data-ttu-id="e496e-135">![inrichting](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="e496e-135">![provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="e496e-136">Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="e496e-136">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="e496e-137">a.</span><span class="sxs-lookup"><span data-stu-id="e496e-137">a.</span></span> <span data-ttu-id="e496e-138">In Hallo **Beheerdersgebruikersnaam** textbox type een Sandbox met Salesforce accountnaam die heeft Hallo **systeembeheerder** profiel in Salesforce.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e496e-138">In hello **Admin User Name** textbox, type a Salesforce Sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="e496e-139">b.</span><span class="sxs-lookup"><span data-stu-id="e496e-139">b.</span></span> <span data-ttu-id="e496e-140">In Hallo **beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.</span><span class="sxs-lookup"><span data-stu-id="e496e-140">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="e496e-141">tooget het beveiligingstoken Salesforce Sandbox een nieuw tabblad openen en meld u aan bij Hallo dezelfde Salesforce Sandbox-beheeraccount.</span><span class="sxs-lookup"><span data-stu-id="e496e-141">tooget your Salesforce Sandbox security token, open a new tab and sign into hello same Salesforce Sandbox admin account.</span></span> <span data-ttu-id="e496e-142">Op Hallo rechtsboven Hallo pagina, klikt u op uw naam en klik vervolgens op **Mijn instellingen**.</span><span class="sxs-lookup"><span data-stu-id="e496e-142">On hello top right corner of hello page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="e496e-143">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="e496e-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="e496e-144">Klik op Hallo navigatiedeelvenster links **persoonlijke** tooexpand Hallo bijbehorende sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**.</span><span class="sxs-lookup"><span data-stu-id="e496e-144">On hello left navigation pane, click **Personal** tooexpand hello related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="e496e-145">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="e496e-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="e496e-146">Op Hallo **opnieuw mijn beveiligingstoken** pagina, klikt u op Hallo **Security Token opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="e496e-146">On hello **Reset My Security Token** page, click hello **Reset Security Token** button.</span></span>

    <span data-ttu-id="e496e-147">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="e496e-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="e496e-148">Controleer Hallo postvak die zijn gekoppeld aan dit admin-account.</span><span class="sxs-lookup"><span data-stu-id="e496e-148">Check hello email inbox associated with this admin account.</span></span> <span data-ttu-id="e496e-149">Zoek naar een e-mailbericht van Salesforce Sandbox.com die nieuw beveiligingstoken Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="e496e-149">Look for an email from Salesforce Sandbox.com that contains hello new security token.</span></span>
10. <span data-ttu-id="e496e-150">Hallo token, gaat u tooyour Azure AD-venster Kopieer en plak deze in Hallo **Socket Token** veld.</span><span class="sxs-lookup"><span data-stu-id="e496e-150">Copy hello token, go tooyour Azure AD window, and paste it into hello **Socket Token** field.</span></span>

11. <span data-ttu-id="e496e-151">In hello Azure-portal, klikt u op **testverbinding** tooensure Azure AD verbinding tooyour Salesforce sandbox-app kunt maken.</span><span class="sxs-lookup"><span data-stu-id="e496e-151">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Salesforce Sandbox app.</span></span>

12. <span data-ttu-id="e496e-152">In Hallo **e-mailmelding** Voer Hallo e-mailadres van een persoon of groep die moet inrichting fout meldingen ontvangen en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="e496e-152">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

13. <span data-ttu-id="e496e-153">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="e496e-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="e496e-154">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooSalesforce Sandbox.**</span><span class="sxs-lookup"><span data-stu-id="e496e-154">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSalesforce Sandbox.**</span></span>

15. <span data-ttu-id="e496e-155">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e496e-155">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSalesforce Sandbox.</span></span> <span data-ttu-id="e496e-156">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Salesforce Sandbox voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e496e-156">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Salesforce Sandbox for update operations.</span></span> <span data-ttu-id="e496e-157">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e496e-157">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="e496e-158">tooenable Hallo inrichting Azure AD-service voor Salesforce Sandbox, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="e496e-158">tooenable hello Azure AD provisioning service for Salesforce Sandbox, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

17. <span data-ttu-id="e496e-159">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="e496e-159">Click **Save.**</span></span>


<span data-ttu-id="e496e-160">Deze begint de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooSalesforce Sandbox in de sectie gebruikers en groepen Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e496e-160">It starts hello initial synchronization of any users and/or groups assigned tooSalesforce Sandbox in hello Users and Groups section.</span></span> <span data-ttu-id="e496e-161">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e496e-161">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="e496e-162">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle acties die worden uitgevoerd door Salesforce Sandbox app-service inricht Hallo beschrijven.</span><span class="sxs-lookup"><span data-stu-id="e496e-162">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on Salesforce Sandbox app.</span></span>

<span data-ttu-id="e496e-163">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="e496e-163">You can now create a test account.</span></span> <span data-ttu-id="e496e-164">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd toosalesforce.</span><span class="sxs-lookup"><span data-stu-id="e496e-164">Wait for up too20 minutes tooverify that hello account has been synchronized toosalesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e496e-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e496e-165">Additional resources</span></span>

* [<span data-ttu-id="e496e-166">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="e496e-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e496e-167">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e496e-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e496e-168">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="e496e-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforcesandbox-tutorial.md)