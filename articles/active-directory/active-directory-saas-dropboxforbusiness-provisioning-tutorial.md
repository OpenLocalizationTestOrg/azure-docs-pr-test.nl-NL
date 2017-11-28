---
title: 'Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Dropbox voor bedrijven.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6f7616e47322242f01a13d763f71c93d4ac06a92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="9cfdc-103">Zelfstudie: Dropbox voor bedrijven configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="9cfdc-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="9cfdc-104">Het doel van deze zelfstudie is zodat u de stappen die u wilt uitvoeren in Dropbox voor bedrijven en Azure AD automatisch inrichten en ongedaan inrichten gebruikersaccounts vanuit Azure AD naar Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cfdc-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9cfdc-105">Prerequisites</span></span>

<span data-ttu-id="9cfdc-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="9cfdc-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="9cfdc-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="9cfdc-108">Een Dropbox voor bedrijven-eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="9cfdc-109">Een gebruikersaccount in Dropbox voor bedrijven met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="9cfdc-110">Gebruikers toewijzen aan Dropbox voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="9cfdc-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="9cfdc-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9cfdc-112">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="9cfdc-113">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot uw Dropbox voor bedrijven-app.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="9cfdc-114">Als besloten, kunt u deze gebruikers toewijzen aan uw Dropbox voor bedrijven-app door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="9cfdc-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="9cfdc-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="9cfdc-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="9cfdc-116">Belangrijke tips voor het toewijzen van gebruikers aan Dropbox voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="9cfdc-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="9cfdc-117">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan Dropbox voor bedrijven voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="9cfdc-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9cfdc-119">Wanneer een gebruiker toewijzen aan Dropbox voor bedrijven, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="9cfdc-120">De rol 'Default toegang' werkt niet voor het inrichten van...</span><span class="sxs-lookup"><span data-stu-id="9cfdc-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9cfdc-121">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="9cfdc-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="9cfdc-122">Deze sectie helpt u bij het verbinden van uw Azure AD met Dropbox voor bedrijven van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Dropbox voor bedrijven op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9cfdc-123">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Dropbox voor bedrijven, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cfdc-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9cfdc-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="9cfdc-125">Voor het configureren van automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="9cfdc-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="9cfdc-126">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="9cfdc-127">Als u al Dropbox voor bedrijven voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Dropbox voor bedrijven met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="9cfdc-128">Selecteer anders **toevoegen** en zoek naar **Dropbox voor bedrijven** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="9cfdc-129">Selecteer Dropbox voor bedrijven in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="9cfdc-130">Selecteer uw exemplaar van Dropbox voor bedrijven en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="9cfdc-131">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9cfdc-133">Onder de **beheerdersreferenties** sectie, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="9cfdc-134">Er wordt een Dropbox voor zakelijke aanmeldingsdialoogvenster geopend in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="9cfdc-135">Op de **aanmelden bij Dropbox om te koppelen aan Azure AD** dialoogvenster Aanmelden bij uw Dropbox voor bedrijven-tenant.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="9cfdc-136">![Gebruikers inrichten](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "gebruikers inrichten")</span><span class="sxs-lookup"><span data-stu-id="9cfdc-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="9cfdc-137">Bevestig dat u wilt machtigen voor Azure Active Directory wijzigingen aanbrengen in uw Dropbox voor bedrijven-tenant.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="9cfdc-138">Klik op **toestaan**.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="9cfdc-139">![Gebruikers inrichten](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "gebruikers inrichten")</span><span class="sxs-lookup"><span data-stu-id="9cfdc-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="9cfdc-140">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw Dropbox voor bedrijven-app.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="9cfdc-141">Als de verbinding is mislukt, zorg ervoor dat uw Dropbox voor bedrijven-account Team beheerdersmachtigingen heeft en probeer de **'Autoriseren'** stap opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="9cfdc-142">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="9cfdc-143">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="9cfdc-143">Click **Save.**</span></span>

11. <span data-ttu-id="9cfdc-144">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers Dropbox voor bedrijven.**</span><span class="sxs-lookup"><span data-stu-id="9cfdc-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="9cfdc-145">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker van Azure AD worden gesynchroniseerd met Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="9cfdc-146">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Dropbox voor bedrijven voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="9cfdc-147">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="9cfdc-148">Wijzigen om de Azure AD-service voor Dropbox voor bedrijven inricht, de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="9cfdc-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="9cfdc-149">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="9cfdc-149">Click **Save.**</span></span>

<span data-ttu-id="9cfdc-150">De initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan Dropbox voor bedrijven in de sectie gebruikers en groepen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="9cfdc-151">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="9cfdc-152">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw Dropbox voor bedrijven-app.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="9cfdc-153">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-153">You can now create a test account.</span></span> <span data-ttu-id="9cfdc-154">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd met Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-154">Wait for up to 20 minutes to verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="9cfdc-155">Een is voltooid gebruikersaanvragen cyclus wordt aangegeven door de bijbehorende status.</span><span class="sxs-lookup"><span data-stu-id="9cfdc-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="9cfdc-156">![Gebruikers toewijzen](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="9cfdc-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9cfdc-157">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9cfdc-157">Additional resources</span></span>

* [<span data-ttu-id="9cfdc-158">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="9cfdc-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cfdc-159">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cfdc-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9cfdc-160">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="9cfdc-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)