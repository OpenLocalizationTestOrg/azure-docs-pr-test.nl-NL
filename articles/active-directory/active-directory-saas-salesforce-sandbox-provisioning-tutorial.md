---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Salesforce Sandbox.
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
ms.openlocfilehash: 7d3c655a754f83284c386d2007c604a731367814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a><span data-ttu-id="18f4e-103">Zelfstudie: Sandbox-Salesforce configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="18f4e-103">Tutorial: Configuring Salesforce Sandbox for Automatic User Provisioning</span></span>

<span data-ttu-id="18f4e-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in Salesforce Sandbox en Azure AD wilt om automatisch inrichten en de gebruikersaccounts van Azure AD bij Salesforce Sandbox ongedaan in te richten.</span><span class="sxs-lookup"><span data-stu-id="18f4e-104">The objective of this tutorial is to show you the steps you need to perform in Salesforce Sandbox and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce Sandbox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18f4e-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="18f4e-105">Prerequisites</span></span>

<span data-ttu-id="18f4e-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="18f4e-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="18f4e-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="18f4e-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="18f4e-108">U moet een geldige tenant voor Salesforce Sandbox voor werk of Salesforce Sandbox voor onderwijs hebben.</span><span class="sxs-lookup"><span data-stu-id="18f4e-108">You must have a valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education.</span></span> <span data-ttu-id="18f4e-109">U kunt een gratis proefaccount voor de service.</span><span class="sxs-lookup"><span data-stu-id="18f4e-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="18f4e-110">Een gebruikersaccount in Salesforce Sandbox met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="18f4e-110">A user account in Salesforce Sandbox with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="18f4e-111">Gebruikers toewijzen aan Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="18f4e-111">Assigning users to Salesforce Sandbox</span></span>

<span data-ttu-id="18f4e-112">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="18f4e-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="18f4e-113">In de context van automatische gebruikers account inrichten, worden alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="18f4e-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="18f4e-114">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot uw Salesforce-Sandbox-app.</span><span class="sxs-lookup"><span data-stu-id="18f4e-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce Sandbox app.</span></span> <span data-ttu-id="18f4e-115">Als besloten, kunt u deze gebruikers toewijzen aan uw Salesforce-Sandbox-app door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="18f4e-115">Once decided, you can assign these users to your Salesforce Sandbox app by following the instructions here:</span></span>

[<span data-ttu-id="18f4e-116">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="18f4e-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="18f4e-117">Belangrijke tips voor het toewijzen van gebruikers aan de Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="18f4e-117">Important tips for assigning users to Salesforce Sandbox</span></span>

* <span data-ttu-id="18f4e-118">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan de Salesforce Sandbox voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="18f4e-118">It is recommended that a single Azure AD user is assigned to Salesforce Sandbox to test the provisioning configuration.</span></span> <span data-ttu-id="18f4e-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="18f4e-119">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="18f4e-120">Wanneer een gebruiker aan de Salesforce Sandbox toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="18f4e-120">When assigning a user to Salesforce Sandbox, you must select a valid user role.</span></span> <span data-ttu-id="18f4e-121">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="18f4e-121">The "Default Access" role does not work for provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="18f4e-122">Deze app importeert aangepaste rollen van Salesforce Sandbox als onderdeel van het inrichtingsproces, de klant selecteren kunt bij het toewijzen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="18f4e-122">This app imports custom roles from Salesforce Sandbox as part of the provisioning process, which the customer may want to select when assigning users.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="18f4e-123">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="18f4e-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="18f4e-124">Deze sectie helpt u bij het verbinding maken met uw Azure AD van Salesforce Sandbox gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van de toegewezen gebruiker accounts in het Salesforce-Sandbox op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18f4e-124">This section guides you through connecting your Azure AD to Salesforce Sandbox's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="18f4e-125">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Salesforce Sandbox, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="18f4e-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce Sandbox, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="18f4e-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="18f4e-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="18f4e-127">Voor het configureren van automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="18f4e-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="18f4e-128">Het doel van deze sectie is het inschakelen van de gebruiker het inrichten van Active Directory-gebruikersaccounts met Salesforce Sandbox overzicht.</span><span class="sxs-lookup"><span data-stu-id="18f4e-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

1. <span data-ttu-id="18f4e-129">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="18f4e-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="18f4e-130">Als u al Salesforce Sandbox voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Salesforce Sandbox met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="18f4e-130">If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using the search field.</span></span> <span data-ttu-id="18f4e-131">Selecteer anders **toevoegen** en zoek naar **Salesforce Sandbox** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="18f4e-131">Otherwise, select **Add** and search for **Salesforce Sandbox** in the application gallery.</span></span> <span data-ttu-id="18f4e-132">Salesforce Sandbox selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="18f4e-132">Select Salesforce Sandbox from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="18f4e-133">Selecteer uw exemplaar van Salesforce Sandbox en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="18f4e-133">Select your instance of Salesforce Sandbox, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="18f4e-134">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="18f4e-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
    <span data-ttu-id="18f4e-135">![inrichting](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="18f4e-135">![provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="18f4e-136">Onder de **beheerdersreferenties** sectie, bieden de volgende configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="18f4e-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="18f4e-137">a.</span><span class="sxs-lookup"><span data-stu-id="18f4e-137">a.</span></span> <span data-ttu-id="18f4e-138">In de **Beheerdersgebruikersnaam** textbox type een Sandbox met Salesforce-accountnaam met de **systeembeheerder** profiel in Salesforce.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="18f4e-138">In the **Admin User Name** textbox, type a Salesforce Sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="18f4e-139">b.</span><span class="sxs-lookup"><span data-stu-id="18f4e-139">b.</span></span> <span data-ttu-id="18f4e-140">In de **beheerderswachtwoord** textbox, typt u het wachtwoord voor dit account.</span><span class="sxs-lookup"><span data-stu-id="18f4e-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="18f4e-141">Als u de beveiliging van uw Salesforce-sandbox-token, open een nieuw tabblad en meld u aan dezelfde Salesforce Sandbox admin-account.</span><span class="sxs-lookup"><span data-stu-id="18f4e-141">To get your Salesforce Sandbox security token, open a new tab and sign into the same Salesforce Sandbox admin account.</span></span> <span data-ttu-id="18f4e-142">In de rechterbovenhoek van de pagina, klikt u op uw naam en klik vervolgens op **Mijn instellingen**.</span><span class="sxs-lookup"><span data-stu-id="18f4e-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="18f4e-143">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="18f4e-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="18f4e-144">Klik in het navigatiedeelvenster links op **persoonlijke** Vouw de bijbehorende sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**.</span><span class="sxs-lookup"><span data-stu-id="18f4e-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="18f4e-145">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="18f4e-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="18f4e-146">Op de **opnieuw mijn beveiligingstoken** pagina, klikt u op de **Security Token opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="18f4e-146">On the **Reset My Security Token** page, click the **Reset Security Token** button.</span></span>

    <span data-ttu-id="18f4e-147">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="18f4e-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="18f4e-148">Controleer de Postvak die zijn gekoppeld aan dit admin-account.</span><span class="sxs-lookup"><span data-stu-id="18f4e-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="18f4e-149">Zoek naar een e-mailbericht van Salesforce Sandbox.com waarin het nieuwe beveiligingstoken.</span><span class="sxs-lookup"><span data-stu-id="18f4e-149">Look for an email from Salesforce Sandbox.com that contains the new security token.</span></span>
10. <span data-ttu-id="18f4e-150">Kopiëren van het token, Ga naar uw Azure AD-venster en plak deze in de **Socket Token** veld.</span><span class="sxs-lookup"><span data-stu-id="18f4e-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="18f4e-151">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw Salesforce-Sandbox-app.</span><span class="sxs-lookup"><span data-stu-id="18f4e-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce Sandbox app.</span></span>

12. <span data-ttu-id="18f4e-152">In de **e-mailmelding** en voer het e-mailadres van een persoon of groep die u moet inrichting fout meldingen ontvangen en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="18f4e-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

13. <span data-ttu-id="18f4e-153">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="18f4e-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="18f4e-154">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory: gebruikers aan de Salesforce Sandbox.**</span><span class="sxs-lookup"><span data-stu-id="18f4e-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce Sandbox.**</span></span>

15. <span data-ttu-id="18f4e-155">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker die zijn gesynchroniseerd vanuit Azure AD bij Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="18f4e-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce Sandbox.</span></span> <span data-ttu-id="18f4e-156">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Salesforce Sandbox voor de update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="18f4e-156">The attributes selected as **Matching** properties are used to match the user accounts in Salesforce Sandbox for update operations.</span></span> <span data-ttu-id="18f4e-157">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="18f4e-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="18f4e-158">Om de Azure AD-service voor Salesforce Sandbox inricht, wijzigen de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="18f4e-158">To enable the Azure AD provisioning service for Salesforce Sandbox, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="18f4e-159">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="18f4e-159">Click **Save.**</span></span>


<span data-ttu-id="18f4e-160">De initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan de Salesforce Sandbox in de sectie gebruikers en groepen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="18f4e-160">It starts the initial synchronization of any users and/or groups assigned to Salesforce Sandbox in the Users and Groups section.</span></span> <span data-ttu-id="18f4e-161">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="18f4e-161">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="18f4e-162">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op de Salesforce Sandbox-app.</span><span class="sxs-lookup"><span data-stu-id="18f4e-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on Salesforce Sandbox app.</span></span>

<span data-ttu-id="18f4e-163">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="18f4e-163">You can now create a test account.</span></span> <span data-ttu-id="18f4e-164">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd met salesforce.</span><span class="sxs-lookup"><span data-stu-id="18f4e-164">Wait for up to 20 minutes to verify that the account has been synchronized to salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18f4e-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="18f4e-165">Additional resources</span></span>

* [<span data-ttu-id="18f4e-166">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="18f4e-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18f4e-167">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18f4e-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="18f4e-168">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="18f4e-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforcesandbox-tutorial.md)