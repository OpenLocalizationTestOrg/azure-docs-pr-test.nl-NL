---
title: 'Zelfstudie: Azure Active Directory-integratie met Netsuite | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="43386-103">Zelfstudie: Netsuite configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="43386-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="43386-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in Netsuite en Azure AD wilt om automatisch in te richten en inrichten van gebruikersaccounts vanuit Azure AD naar Netsuite ongedaan.</span><span class="sxs-lookup"><span data-stu-id="43386-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43386-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="43386-105">Prerequisites</span></span>

<span data-ttu-id="43386-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="43386-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="43386-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="43386-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="43386-108">Een Netsuite eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="43386-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="43386-109">Een gebruikersaccount in Netsuite met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="43386-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="43386-110">Gebruikers toewijzen aan Netsuite</span><span class="sxs-lookup"><span data-stu-id="43386-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="43386-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="43386-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="43386-112">In de context van automatische gebruikers account inrichten, worden alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="43386-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="43386-113">Voordat u configureren en inschakelen van de inrichting service, moet u om te bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang tot uw app Netsuite nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="43386-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="43386-114">Als besloten, kunt u deze gebruikers toewijzen aan uw app Netsuite door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="43386-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="43386-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="43386-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="43386-116">Belangrijke tips voor het toewijzen van gebruikers aan Netsuite</span><span class="sxs-lookup"><span data-stu-id="43386-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="43386-117">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan Netsuite voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="43386-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="43386-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="43386-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="43386-119">Wanneer een gebruiker aan Netsuite toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="43386-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="43386-120">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="43386-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="43386-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="43386-121">Enable User Provisioning</span></span>

<span data-ttu-id="43386-122">Deze sectie helpt u bij het verbinding maken met uw Azure AD Netsuite van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Netsuite op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43386-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="43386-123">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Netsuite, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43386-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="43386-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="43386-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="43386-125">Configureren voor het inrichten van het account:</span><span class="sxs-lookup"><span data-stu-id="43386-125">To configure user account provisioning:</span></span>

<span data-ttu-id="43386-126">Het doel van deze sectie is het inschakelen van de gebruiker het inrichten van Active Directory-gebruikersaccounts met Netsuite overzicht.</span><span class="sxs-lookup"><span data-stu-id="43386-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="43386-127">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="43386-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="43386-128">Als u al Netsuite voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Netsuite met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="43386-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="43386-129">Selecteer anders **toevoegen** en zoek naar **Netsuite** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="43386-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="43386-130">Netsuite selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="43386-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="43386-131">Selecteer uw exemplaar van Netsuite en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="43386-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="43386-132">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="43386-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="43386-134">Onder de **beheerdersreferenties** sectie, bieden de volgende configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="43386-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="43386-135">a.</span><span class="sxs-lookup"><span data-stu-id="43386-135">a.</span></span> <span data-ttu-id="43386-136">In de **Beheerdersgebruikersnaam** textbox type een Netsuite accountnaam met de **systeembeheerder** profiel in Netsuite.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="43386-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="43386-137">b.</span><span class="sxs-lookup"><span data-stu-id="43386-137">b.</span></span> <span data-ttu-id="43386-138">In de **beheerderswachtwoord** textbox, typt u het wachtwoord voor dit account.</span><span class="sxs-lookup"><span data-stu-id="43386-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="43386-139">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw app Netsuite.</span><span class="sxs-lookup"><span data-stu-id="43386-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="43386-140">In de **e-mailmelding** en voer het e-mailadres van een persoon of groep die u moet inrichting fout meldingen ontvangen en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="43386-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="43386-141">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="43386-141">Click **Save.**</span></span>

9. <span data-ttu-id="43386-142">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers Netsuite.**</span><span class="sxs-lookup"><span data-stu-id="43386-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="43386-143">In de **kenmerktoewijzingen** sectie, moet u de kenmerken van de gebruiker is gesynchroniseerd vanuit Azure AD Netsuite controleren.</span><span class="sxs-lookup"><span data-stu-id="43386-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="43386-144">Let op de kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Netsuite voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="43386-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="43386-145">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="43386-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="43386-146">Om de Azure AD-service voor Netsuite inricht, wijzigen de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="43386-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="43386-147">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="43386-147">Click **Save.**</span></span>

<span data-ttu-id="43386-148">De initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan Netsuite in de sectie gebruikers en groepen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="43386-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="43386-149">Houd er rekening mee dat de eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="43386-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="43386-150">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw app Netsuite beschrijven.</span><span class="sxs-lookup"><span data-stu-id="43386-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="43386-151">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="43386-151">You can now create a test account.</span></span> <span data-ttu-id="43386-152">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd voor Netsuite.</span><span class="sxs-lookup"><span data-stu-id="43386-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43386-153">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="43386-153">Additional resources</span></span>

* [<span data-ttu-id="43386-154">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="43386-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43386-155">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43386-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="43386-156">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="43386-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)