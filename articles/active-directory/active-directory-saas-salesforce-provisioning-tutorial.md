---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Salesforce.
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
ms.openlocfilehash: a573a7ef79e28c50ae0923849a88f88af40f21be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="77ee9-103">Zelfstudie: Salesforce configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="77ee9-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="77ee9-104">Het doel van deze zelfstudie is om de stappen die nodig zijn om uit te voeren in Salesforce en Azure AD om automatisch te stellen en deactivering inrichten gebruikersaccounts vanuit Azure AD bij Salesforce.</span><span class="sxs-lookup"><span data-stu-id="77ee9-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77ee9-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="77ee9-105">Prerequisites</span></span>

<span data-ttu-id="77ee9-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="77ee9-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="77ee9-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="77ee9-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="77ee9-108">U moet een geldige tenant voor Salesforce voor werk- of Salesforce voor onderwijs hebben.</span><span class="sxs-lookup"><span data-stu-id="77ee9-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="77ee9-109">U kunt een gratis proefaccount voor de service.</span><span class="sxs-lookup"><span data-stu-id="77ee9-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="77ee9-110">Een gebruikersaccount in Salesforce met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="77ee9-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce"></a><span data-ttu-id="77ee9-111">Gebruikers toewijzen aan Salesforce</span><span class="sxs-lookup"><span data-stu-id="77ee9-111">Assigning users to Salesforce</span></span>

<span data-ttu-id="77ee9-112">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="77ee9-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="77ee9-113">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="77ee9-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="77ee9-114">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot uw Salesforce-app.</span><span class="sxs-lookup"><span data-stu-id="77ee9-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce app.</span></span> <span data-ttu-id="77ee9-115">Als besloten, kunt u deze gebruikers toewijzen aan uw Salesforce-app door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="77ee9-115">Once decided, you can assign these users to your Salesforce app by following the instructions here:</span></span>

[<span data-ttu-id="77ee9-116">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="77ee9-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce"></a><span data-ttu-id="77ee9-117">Belangrijke tips voor het toewijzen van gebruikers aan Salesforce</span><span class="sxs-lookup"><span data-stu-id="77ee9-117">Important tips for assigning users to Salesforce</span></span>

*   <span data-ttu-id="77ee9-118">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan Salesforce voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="77ee9-118">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span></span> <span data-ttu-id="77ee9-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="77ee9-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="77ee9-120">Wanneer een gebruiker aan Salesforce toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="77ee9-120">When assigning a user to Salesforce, you must select a valid user role.</span></span> <span data-ttu-id="77ee9-121">De rol 'Default toegang' werkt niet voor inrichting</span><span class="sxs-lookup"><span data-stu-id="77ee9-121">The "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="77ee9-122">Deze app kunt u aangepaste rollen uit Salesforce als onderdeel van het inrichtingsproces, de klant selecteren kunt bij het toewijzen van gebruikers importeren</span><span class="sxs-lookup"><span data-stu-id="77ee9-122">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="77ee9-123">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="77ee9-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="77ee9-124">Deze sectie helpt u bij uw Azure AD verbinden met Salesforce van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Salesforce op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77ee9-124">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="77ee9-125">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Salesforce, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77ee9-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="77ee9-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="77ee9-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="77ee9-127">Voor het configureren van automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="77ee9-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="77ee9-128">Het doel van deze sectie is het inschakelen van de gebruiker het inrichten van Active Directory-gebruikersaccounts met Salesforce overzicht.</span><span class="sxs-lookup"><span data-stu-id="77ee9-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span></span>

1. <span data-ttu-id="77ee9-129">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="77ee9-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="77ee9-130">Als u al Salesforce voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Salesforce met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="77ee9-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span></span> <span data-ttu-id="77ee9-131">Selecteer anders **toevoegen** en zoek naar **Salesforce** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="77ee9-131">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span></span> <span data-ttu-id="77ee9-132">Salesforce selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="77ee9-132">Select Salesforce from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="77ee9-133">Selecteer uw exemplaar van Salesforce en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="77ee9-133">Select your instance of Salesforce, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="77ee9-134">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="77ee9-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
<span data-ttu-id="77ee9-135">![inrichting](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="77ee9-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="77ee9-136">Onder de **beheerdersreferenties** sectie, bieden de volgende configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="77ee9-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="77ee9-137">a.</span><span class="sxs-lookup"><span data-stu-id="77ee9-137">a.</span></span> <span data-ttu-id="77ee9-138">In de **Beheerdersgebruikersnaam** textbox type een Salesforce-accountnaam met de **systeembeheerder** profiel in Salesforce.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="77ee9-138">In the **Admin User Name** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="77ee9-139">b.</span><span class="sxs-lookup"><span data-stu-id="77ee9-139">b.</span></span> <span data-ttu-id="77ee9-140">In de **beheerderswachtwoord** textbox, typt u het wachtwoord voor dit account.</span><span class="sxs-lookup"><span data-stu-id="77ee9-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="77ee9-141">Als u de beveiliging van uw Salesforce-token, open een nieuw tabblad en meld u aan dezelfde Salesforce-admin-account.</span><span class="sxs-lookup"><span data-stu-id="77ee9-141">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="77ee9-142">In de rechterbovenhoek van de pagina, klikt u op uw naam en klik vervolgens op **Mijn instellingen**.</span><span class="sxs-lookup"><span data-stu-id="77ee9-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="77ee9-143">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="77ee9-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="77ee9-144">Klik in het navigatiedeelvenster links op **persoonlijke** Vouw de bijbehorende sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**.</span><span class="sxs-lookup"><span data-stu-id="77ee9-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="77ee9-145">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="77ee9-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="77ee9-146">Op de **opnieuw mijn beveiligingstoken** pagina, klikt u op **Security Token opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="77ee9-146">On the **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="77ee9-147">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="77ee9-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="77ee9-148">Controleer de Postvak die zijn gekoppeld aan dit admin-account.</span><span class="sxs-lookup"><span data-stu-id="77ee9-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="77ee9-149">Zoek naar een e-mailbericht van Salesforce.com waarin het nieuwe beveiligingstoken.</span><span class="sxs-lookup"><span data-stu-id="77ee9-149">Look for an email from Salesforce.com that contains the new security token.</span></span>
10. <span data-ttu-id="77ee9-150">Kopiëren van het token, Ga naar uw Azure AD-venster en plak deze in de **Socket Token** veld.</span><span class="sxs-lookup"><span data-stu-id="77ee9-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="77ee9-151">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw Salesforce-app.</span><span class="sxs-lookup"><span data-stu-id="77ee9-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span></span>

12. <span data-ttu-id="77ee9-152">In de **e-mailmelding** en voer het e-mailadres van een persoon of groep die u moet inrichting fout meldingen ontvangen en schakel het selectievakje hieronder in.</span><span class="sxs-lookup"><span data-stu-id="77ee9-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span></span>

13. <span data-ttu-id="77ee9-153">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="77ee9-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="77ee9-154">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers Salesforce.**</span><span class="sxs-lookup"><span data-stu-id="77ee9-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span></span>

15. <span data-ttu-id="77ee9-155">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker van Azure AD worden gesynchroniseerd met Salesforce.</span><span class="sxs-lookup"><span data-stu-id="77ee9-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span></span> <span data-ttu-id="77ee9-156">Let op de kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Salesforce voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77ee9-156">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="77ee9-157">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="77ee9-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="77ee9-158">Om de Azure AD-service voor Salesforce inricht, wijzigen de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="77ee9-158">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="77ee9-159">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="77ee9-159">Click **Save.**</span></span>

<span data-ttu-id="77ee9-160">Hiermee start u de initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan Salesforce in de sectie gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="77ee9-160">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span></span> <span data-ttu-id="77ee9-161">Houd er rekening mee dat de eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77ee9-161">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="77ee9-162">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw Salesforce-app.</span><span class="sxs-lookup"><span data-stu-id="77ee9-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="77ee9-163">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="77ee9-163">You can now create a test account.</span></span> <span data-ttu-id="77ee9-164">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd met Salesforce.</span><span class="sxs-lookup"><span data-stu-id="77ee9-164">Wait for up to 20 minutes to verify that the account has been synchronized to Salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77ee9-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="77ee9-165">Additional resources</span></span>

* [<span data-ttu-id="77ee9-166">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="77ee9-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77ee9-167">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77ee9-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="77ee9-168">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="77ee9-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)