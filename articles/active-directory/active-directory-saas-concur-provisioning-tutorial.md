---
title: 'Zelfstudie: Azure Active Directory-integratie met Concur | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="baa9d-103">Zelfstudie: Configureren voor gebruikers inrichten instemming</span><span class="sxs-lookup"><span data-stu-id="baa9d-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="baa9d-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in Concur en Azure AD wilt om automatisch in te richten en inrichten van gebruikersaccounts vanuit Azure AD naar Concur ongedaan.</span><span class="sxs-lookup"><span data-stu-id="baa9d-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa9d-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="baa9d-105">Prerequisites</span></span>

<span data-ttu-id="baa9d-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="baa9d-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="baa9d-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="baa9d-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="baa9d-108">Een Concur eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="baa9d-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="baa9d-109">Een gebruikersaccount in Concur met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="baa9d-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="baa9d-110">Gebruikers toewijzen aan Concur</span><span class="sxs-lookup"><span data-stu-id="baa9d-110">Assigning users to Concur</span></span>

<span data-ttu-id="baa9d-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="baa9d-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="baa9d-112">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="baa9d-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="baa9d-113">Voordat u configureren en inschakelen van de inrichting service, moet u om te bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang tot uw app Concur nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="baa9d-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="baa9d-114">Als besloten, kunt u deze gebruikers toewijzen aan uw app Concur door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="baa9d-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="baa9d-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="baa9d-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="baa9d-116">Belangrijke tips voor het toewijzen van gebruikers aan Concur</span><span class="sxs-lookup"><span data-stu-id="baa9d-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="baa9d-117">Het is raadzaam om één Azure AD-gebruiker worden toegewezen aan Concur voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="baa9d-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="baa9d-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="baa9d-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="baa9d-119">Wanneer een gebruiker aan Concur toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="baa9d-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="baa9d-120">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="baa9d-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="baa9d-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="baa9d-121">Enable user provisioning</span></span>

<span data-ttu-id="baa9d-122">Deze sectie helpt u bij het verbinding maken met uw Azure AD Concur van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Concur op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="baa9d-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="baa9d-123">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Concur, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="baa9d-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="baa9d-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="baa9d-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="baa9d-125">Configureren voor het inrichten van het account:</span><span class="sxs-lookup"><span data-stu-id="baa9d-125">To configure user account provisioning:</span></span>

<span data-ttu-id="baa9d-126">Het doel van deze sectie is het inschakelen van de inrichting van Active Directory-gebruikersaccounts met Concur overzicht.</span><span class="sxs-lookup"><span data-stu-id="baa9d-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="baa9d-127">Heeft zodat apps in de Service onkosten, er moet een juiste installatie en het gebruik van een profiel voor een Web-servicebeheerder.</span><span class="sxs-lookup"><span data-stu-id="baa9d-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="baa9d-128">Voeg de WS-beheerrol niet aan uw bestaande administrator-profiel dat u voor T & en beheerfuncties gebruikt.</span><span class="sxs-lookup"><span data-stu-id="baa9d-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="baa9d-129">Adviseurs instemming of de beheerder van de client moet een afzonderlijke Service webbeheerder-profiel maken en de beheerder van de Client Gebruik dit profiel voor de functies van de beheerder van de Web-Services (bijvoorbeeld inschakelen apps).</span><span class="sxs-lookup"><span data-stu-id="baa9d-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="baa9d-130">Deze profielen moeten worden gescheiden gehouden van de client dagelijkse d & E admin beheerdersprofiel (het profiel van de beheerder T & en mag geen rol WSAdmin).</span><span class="sxs-lookup"><span data-stu-id="baa9d-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="baa9d-131">Wanneer u het profiel moet worden gebruikt voor het inschakelen van de app maakt, voert u naam van de beheerder van de client naar de gebruiker profiel velden.</span><span class="sxs-lookup"><span data-stu-id="baa9d-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="baa9d-132">Hiermee wijst u het eigendom toe aan het profiel.</span><span class="sxs-lookup"><span data-stu-id="baa9d-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="baa9d-133">Zodra een of meer profielen is gemaakt, de client moet aanmelden met dit profiel te klikken op de '*inschakelen*' knop voor een App-Partner in het menu Web Services.</span><span class="sxs-lookup"><span data-stu-id="baa9d-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="baa9d-134">De volgende oorzaken hebben, moet deze actie niet aan het profiel dat ze voor het normale beheer van d & E gebruiken worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="baa9d-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="baa9d-135">De client moet zijn die klikt op '*Ja*' in het venster dialoog die wordt weergegeven nadat een app is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="baa9d-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="baa9d-136">Klikt u op bevestigt dat de client is bereid voor de Partner-toepassing voor toegang tot hun gegevens, zodat u of de Partner kan niet daarop Ja klikken.</span><span class="sxs-lookup"><span data-stu-id="baa9d-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="baa9d-137">Als de beheerder van een client die een app is ingeschakeld met behulp van de beheerder d & E profiel het bedrijf verlaat (wat resulteert in het profiel wordt uitgeschakeld), alle apps die zijn ingeschakeld met dat profiel niet werkt totdat de app met een andere actieve WS-Admin-profiel is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="baa9d-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="baa9d-138">Dit is de reden waarom u moet afzonderlijke WS-beheerder om profielen te maken.</span><span class="sxs-lookup"><span data-stu-id="baa9d-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="baa9d-139">Als een beheerder het bedrijf verlaat, kan de naam gekoppeld aan het profiel WS-beheer worden gewijzigd in de beheerder van de vervangende indien gewenst zonder enige impact op dat de ingeschakelde app omdat dit profiel niet hoeft deactiveren.</span><span class="sxs-lookup"><span data-stu-id="baa9d-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="baa9d-140">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="baa9d-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="baa9d-141">Meld u aan bij uw **Concur** tenant.</span><span class="sxs-lookup"><span data-stu-id="baa9d-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="baa9d-142">Van de **beheer** selecteert u **webservices**.</span><span class="sxs-lookup"><span data-stu-id="baa9d-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="baa9d-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span><span class="sxs-lookup"><span data-stu-id="baa9d-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="baa9d-144">Aan de linkerkant van de **webservices** deelvenster **partnertoepassing inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="baa9d-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="baa9d-145">![Partnertoepassing inschakelen](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "partnertoepassing inschakelen")</span><span class="sxs-lookup"><span data-stu-id="baa9d-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="baa9d-146">Van de **toepassing inschakelen** selecteert **Azure Active Directory**, en klik vervolgens op **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="baa9d-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="baa9d-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="baa9d-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="baa9d-148">Klik op **Ja** sluiten de **bevestigen actie** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="baa9d-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="baa9d-149">![Bevestig de actie](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Bevestig de actie")</span><span class="sxs-lookup"><span data-stu-id="baa9d-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="baa9d-150">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="baa9d-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="baa9d-151">Als u al Concur voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Concur met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="baa9d-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="baa9d-152">Selecteer anders **toevoegen** en zoek naar **Concur** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="baa9d-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="baa9d-153">Concur selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="baa9d-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="baa9d-154">Selecteer uw exemplaar van Concur en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="baa9d-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="baa9d-155">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="baa9d-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![Inrichting](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="baa9d-157">Onder de **beheerdersreferenties** sectie, voert u de **gebruikersnaam** en de **wachtwoord** van uw beheerder Concur.</span><span class="sxs-lookup"><span data-stu-id="baa9d-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="baa9d-158">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw app Concur.</span><span class="sxs-lookup"><span data-stu-id="baa9d-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="baa9d-159">Als de verbinding is mislukt, Controleer of uw account Concur Team beheerder machtigingen.</span><span class="sxs-lookup"><span data-stu-id="baa9d-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="baa9d-160">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="baa9d-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="baa9d-161">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="baa9d-161">Click **Save.**</span></span>

14. <span data-ttu-id="baa9d-162">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers Concur.**</span><span class="sxs-lookup"><span data-stu-id="baa9d-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="baa9d-163">In de **kenmerktoewijzingen** sectie, moet u de kenmerken van de gebruiker die gesynchroniseerd zijn van Azure AD naar Concur controleren.</span><span class="sxs-lookup"><span data-stu-id="baa9d-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="baa9d-164">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Concur voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="baa9d-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="baa9d-165">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="baa9d-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="baa9d-166">Om de Azure AD-service voor Concur inricht, wijzigen de **inrichting Status** naar **op** in de **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="baa9d-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="baa9d-167">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="baa9d-167">Click **Save.**</span></span>

<span data-ttu-id="baa9d-168">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="baa9d-168">You can now create a test account.</span></span> <span data-ttu-id="baa9d-169">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd met Concur.</span><span class="sxs-lookup"><span data-stu-id="baa9d-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="baa9d-170">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="baa9d-170">Additional resources</span></span>

* [<span data-ttu-id="baa9d-171">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="baa9d-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="baa9d-172">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="baa9d-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="baa9d-173">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="baa9d-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

