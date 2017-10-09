---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="347f5-103">Zelfstudie: Salesforce configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="347f5-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="347f5-104">Hallo-doel van deze zelfstudie is tooshow Hallo stappen vereist tooperform in Salesforce en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="347f5-104">hello objective of this tutorial is tooshow hello steps required tooperform in Salesforce and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSalesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="347f5-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="347f5-105">Prerequisites</span></span>

<span data-ttu-id="347f5-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="347f5-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="347f5-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="347f5-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="347f5-108">U moet een geldige tenant voor Salesforce voor werk- of Salesforce voor onderwijs hebben.</span><span class="sxs-lookup"><span data-stu-id="347f5-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="347f5-109">U kunt een gratis proefaccount voor de service.</span><span class="sxs-lookup"><span data-stu-id="347f5-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="347f5-110">Een gebruikersaccount in Salesforce met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="347f5-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-toosalesforce"></a><span data-ttu-id="347f5-111">Gebruikers tooSalesforce toewijzen</span><span class="sxs-lookup"><span data-stu-id="347f5-111">Assigning users tooSalesforce</span></span>

<span data-ttu-id="347f5-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="347f5-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="347f5-113">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="347f5-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="347f5-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Salesforce-app.</span><span class="sxs-lookup"><span data-stu-id="347f5-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Salesforce app.</span></span> <span data-ttu-id="347f5-115">Als besloten, kunt u deze gebruikers tooyour Salesforce-app kunt toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="347f5-115">Once decided, you can assign these users tooyour Salesforce app by following hello instructions here:</span></span>

[<span data-ttu-id="347f5-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="347f5-116">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a><span data-ttu-id="347f5-117">Belangrijke tips voor het toewijzen van gebruikers tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="347f5-117">Important tips for assigning users tooSalesforce</span></span>

*   <span data-ttu-id="347f5-118">Het is raadzaam om één tooSalesforce tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="347f5-118">It is recommended that a single Azure AD user is assigned tooSalesforce tootest hello provisioning configuration.</span></span> <span data-ttu-id="347f5-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="347f5-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="347f5-120">Wanneer u een gebruiker tooSalesforce toewijst, moet u een geldige gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="347f5-120">When assigning a user tooSalesforce, you must select a valid user role.</span></span> <span data-ttu-id="347f5-121">Hallo 'Default toegang' rol werkt niet voor inrichting</span><span class="sxs-lookup"><span data-stu-id="347f5-121">hello "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="347f5-122">Deze app kunt u aangepaste rollen uit Salesforce als onderdeel van Hallo inrichtingsproces, welke klant Hallo wil tooselect bij het toewijzen van gebruikers importeren</span><span class="sxs-lookup"><span data-stu-id="347f5-122">This app imports custom roles from Salesforce as part of hello provisioning process, which hello customer may want tooselect when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="347f5-123">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="347f5-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="347f5-124">Deze sectie helpt u bij het verbinden van uw Azure AD-tooSalesforce gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Salesforce op basis van gebruikers en groepen toewijzen in Azure AD .</span><span class="sxs-lookup"><span data-stu-id="347f5-124">This section guides you through connecting your Azure AD tooSalesforce's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="347f5-125">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Salesforce, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="347f5-125">You may also choose tooenabled SAML-based Single Sign-On for Salesforce, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="347f5-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="347f5-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="347f5-127">tooconfigure automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="347f5-127">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="347f5-128">Hallo-doel van deze sectie is het toooutline hoe tooSalesforce tooenable gebruikers inrichten van Active Directory-gebruiker accounts.</span><span class="sxs-lookup"><span data-stu-id="347f5-128">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce.</span></span>

1. <span data-ttu-id="347f5-129">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="347f5-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="347f5-130">Als u Salesforce al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Salesforce met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="347f5-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using hello search field.</span></span> <span data-ttu-id="347f5-131">Selecteer anders **toevoegen** en zoek naar **Salesforce** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="347f5-131">Otherwise, select **Add** and search for **Salesforce** in hello application gallery.</span></span> <span data-ttu-id="347f5-132">Selecteer Salesforce in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="347f5-132">Select Salesforce from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="347f5-133">Selecteer uw exemplaar van Salesforce en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="347f5-133">Select your instance of Salesforce, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="347f5-134">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="347f5-134">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
<span data-ttu-id="347f5-135">![inrichting](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="347f5-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="347f5-136">Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="347f5-136">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="347f5-137">a.</span><span class="sxs-lookup"><span data-stu-id="347f5-137">a.</span></span> <span data-ttu-id="347f5-138">In Hallo **Beheerdersgebruikersnaam** textbox type een Salesforce accountnaam die heeft Hallo **systeembeheerder** profiel in Salesforce.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="347f5-138">In hello **Admin User Name** textbox, type a Salesforce account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="347f5-139">b.</span><span class="sxs-lookup"><span data-stu-id="347f5-139">b.</span></span> <span data-ttu-id="347f5-140">In Hallo **beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.</span><span class="sxs-lookup"><span data-stu-id="347f5-140">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="347f5-141">tooget uw Salesforce-beveiligingstoken, een nieuw tabblad openen en meld u aan bij Hallo dezelfde Salesforce-beheeraccount.</span><span class="sxs-lookup"><span data-stu-id="347f5-141">tooget your Salesforce security token, open a new tab and sign into hello same Salesforce admin account.</span></span> <span data-ttu-id="347f5-142">Op Hallo rechtsboven Hallo pagina, klikt u op uw naam en klik vervolgens op **Mijn instellingen**.</span><span class="sxs-lookup"><span data-stu-id="347f5-142">On hello top right corner of hello page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="347f5-143">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="347f5-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="347f5-144">Klik op Hallo navigatiedeelvenster links **persoonlijke** tooexpand Hallo bijbehorende sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**.</span><span class="sxs-lookup"><span data-stu-id="347f5-144">On hello left navigation pane, click **Personal** tooexpand hello related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="347f5-145">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="347f5-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="347f5-146">Op Hallo **opnieuw mijn beveiligingstoken** pagina, klikt u op **Security Token opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="347f5-146">On hello **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="347f5-147">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="347f5-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="347f5-148">Controleer Hallo postvak die zijn gekoppeld aan dit admin-account.</span><span class="sxs-lookup"><span data-stu-id="347f5-148">Check hello email inbox associated with this admin account.</span></span> <span data-ttu-id="347f5-149">Zoek naar een e-mailbericht van Salesforce.com die nieuw beveiligingstoken Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="347f5-149">Look for an email from Salesforce.com that contains hello new security token.</span></span>
10. <span data-ttu-id="347f5-150">Hallo token, gaat u tooyour Azure AD-venster Kopieer en plak deze in Hallo **Socket Token** veld.</span><span class="sxs-lookup"><span data-stu-id="347f5-150">Copy hello token, go tooyour Azure AD window, and paste it into hello **Socket Token** field.</span></span>

11. <span data-ttu-id="347f5-151">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Salesforce-app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="347f5-151">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Salesforce app.</span></span>

12. <span data-ttu-id="347f5-152">In Hallo **e-mailmelding** Voer Hallo e-mailadres van een persoon of groep die moet inrichting fout meldingen ontvangen, en schakel Hallo selectievakje hieronder.</span><span class="sxs-lookup"><span data-stu-id="347f5-152">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox below.</span></span>

13. <span data-ttu-id="347f5-153">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="347f5-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="347f5-154">Selecteer onder Hallo toewijzingen sectie, **tooSalesforce synchroniseren Azure Active Directory-gebruikers.**</span><span class="sxs-lookup"><span data-stu-id="347f5-154">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSalesforce.**</span></span>

15. <span data-ttu-id="347f5-155">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="347f5-155">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSalesforce.</span></span> <span data-ttu-id="347f5-156">Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Salesforce voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="347f5-156">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="347f5-157">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="347f5-157">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="347f5-158">tooenable Hallo inrichting Azure AD-service voor Salesforce, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="347f5-158">tooenable hello Azure AD provisioning service for Salesforce, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

17. <span data-ttu-id="347f5-159">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="347f5-159">Click **Save.**</span></span>

<span data-ttu-id="347f5-160">Hiermee start u de initiële synchronisatie Hallo van gebruikers en/of groepen die zijn toegewezen tooSalesforce in Hallo gebruikers en groepen sectie.</span><span class="sxs-lookup"><span data-stu-id="347f5-160">This starts hello initial synchronization of any users and/or groups assigned tooSalesforce in hello Users and Groups section.</span></span> <span data-ttu-id="347f5-161">Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="347f5-161">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="347f5-162">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw Salesforce-app inrichten.</span><span class="sxs-lookup"><span data-stu-id="347f5-162">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="347f5-163">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="347f5-163">You can now create a test account.</span></span> <span data-ttu-id="347f5-164">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="347f5-164">Wait for up too20 minutes tooverify that hello account has been synchronized tooSalesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="347f5-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="347f5-165">Additional resources</span></span>

* [<span data-ttu-id="347f5-166">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="347f5-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="347f5-167">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="347f5-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="347f5-168">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="347f5-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)