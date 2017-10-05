---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix GoToMeeting | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="77e7f-103">Zelfstudie: Citrix GoToMeeting configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="77e7f-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="77e7f-104">Het doel van deze zelfstudie is zodat u de stappen die u wilt uitvoeren in Citrix GoToMeeting en Azure AD automatisch inrichten en de gebruikersaccounts van Azure AD naar Citrix GoToMeeting inrichten.</span><span class="sxs-lookup"><span data-stu-id="77e7f-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77e7f-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="77e7f-105">Prerequisites</span></span>

<span data-ttu-id="77e7f-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="77e7f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="77e7f-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="77e7f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="77e7f-108">Een Citrix GoToMeeting eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="77e7f-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="77e7f-109">Een gebruikersaccount in Citrix GoToMeeting met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="77e7f-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="77e7f-110">Gebruikers toewijzen aan Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="77e7f-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="77e7f-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="77e7f-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="77e7f-112">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="77e7f-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="77e7f-113">Voordat u configureren en inschakelen van de inrichting service, moet u om te bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang tot uw app Citrix GoToMeeting nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="77e7f-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="77e7f-114">Als besloten, kunt u deze gebruikers toewijzen aan uw app Citrix GoToMeeting door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="77e7f-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="77e7f-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="77e7f-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="77e7f-116">Belangrijke tips voor het toewijzen van gebruikers aan Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="77e7f-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="77e7f-117">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan Citrix GoToMeeting voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="77e7f-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="77e7f-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="77e7f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="77e7f-119">Wanneer een gebruiker aan Citrix GoToMeeting toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="77e7f-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="77e7f-120">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="77e7f-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="77e7f-121">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="77e7f-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="77e7f-122">Deze sectie helpt u bij het verbinden van uw Azure AD met Citrix GoToMeeting van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van de toegewezen gebruiker accounts in Citrix GoToMeeting op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77e7f-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="77e7f-123">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Citrix GoToMeeting, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77e7f-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="77e7f-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="77e7f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="77e7f-125">Voor het configureren van automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="77e7f-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="77e7f-126">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="77e7f-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="77e7f-127">Als u Citrix GoToMeeting al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Citrix GoToMeeting met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="77e7f-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="77e7f-128">Selecteer anders **toevoegen** en zoek naar **Citrix GoToMeeting** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="77e7f-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="77e7f-129">Citrix GoToMeeting selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="77e7f-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="77e7f-130">Selecteer uw exemplaar van Citrix GoToMeeting en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="77e7f-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="77e7f-131">Stel de **inrichting** modus **automatische**.</span><span class="sxs-lookup"><span data-stu-id="77e7f-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="77e7f-133">In de sectie beheerdersreferenties, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="77e7f-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="77e7f-134">a.</span><span class="sxs-lookup"><span data-stu-id="77e7f-134">a.</span></span> <span data-ttu-id="77e7f-135">In de **Citrix GoToMeeting Beheerdersgebruikersnaam** textbox, typ de gebruikersnaam van een beheerder.</span><span class="sxs-lookup"><span data-stu-id="77e7f-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="77e7f-136">b.</span><span class="sxs-lookup"><span data-stu-id="77e7f-136">b.</span></span> <span data-ttu-id="77e7f-137">In de **Citrix GoToMeeting beheerderswachtwoord** textbox, het administrator wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="77e7f-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="77e7f-138">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw app Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="77e7f-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="77e7f-139">Als de verbinding is mislukt, zorg je account Citrix GoToMeeting Team beheerdersmachtigingen heeft en probeer de **'Beheerdersreferenties'** stap opnieuw.</span><span class="sxs-lookup"><span data-stu-id="77e7f-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="77e7f-140">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="77e7f-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="77e7f-141">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="77e7f-141">Click **Save.**</span></span>

9. <span data-ttu-id="77e7f-142">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers Citrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="77e7f-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="77e7f-143">In de **kenmerktoewijzingen** sectie, moet u de kenmerken van de gebruiker van Azure AD worden gesynchroniseerd met Citrix GoToMeeting controleren.</span><span class="sxs-lookup"><span data-stu-id="77e7f-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="77e7f-144">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Citrix GoToMeeting voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77e7f-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="77e7f-145">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="77e7f-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="77e7f-146">Om de Azure AD-service voor Citrix GoToMeeting inricht, wijzigen de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="77e7f-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="77e7f-147">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="77e7f-147">Click **Save.**</span></span>

<span data-ttu-id="77e7f-148">De initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan Citrix GoToMeeting in de sectie gebruikers en groepen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="77e7f-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="77e7f-149">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77e7f-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="77e7f-150">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw app Citrix GoToMeeting beschrijven.</span><span class="sxs-lookup"><span data-stu-id="77e7f-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77e7f-151">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="77e7f-151">Additional resources</span></span>

* [<span data-ttu-id="77e7f-152">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="77e7f-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77e7f-153">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77e7f-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="77e7f-154">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="77e7f-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


