---
title: 'Zelfstudie: Samanage configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Informatie over het configureren van Azure Active Directory voor het automatisch inrichten en gebruikersaccounts aan Samanage ongedaan in te richten.
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 278ebf464fbe815568fbe332f80d5ea6b29e1811
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="789df-103">Zelfstudie: Samanage configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="789df-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="789df-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in Samanage en Azure AD wilt om automatisch in te richten en inrichten van gebruikersaccounts vanuit Azure AD naar Samanage ongedaan.</span><span class="sxs-lookup"><span data-stu-id="789df-104">The objective of this tutorial is to show you the steps you need to perform in Samanage and Azure AD to automatically provision and de-provision user accounts from Azure AD to Samanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="789df-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="789df-105">Prerequisites</span></span>

<span data-ttu-id="789df-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="789df-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="789df-107">Een Azure Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="789df-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="789df-108">Een tenant Samanage met de [Professional plan](https://www.samanage.com/pricing/) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="789df-108">A Samanage tenant with the [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="789df-109">Een gebruikersaccount in Samanage met beheerdersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="789df-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="789df-110">De Azure AD integratie inrichting is afhankelijk van de [Samanage REST-API](https://www.samanage.com/api/), die beschikbaar zijn voor Samanage teams op het plan Professional of een betere is.</span><span class="sxs-lookup"><span data-stu-id="789df-110">The Azure AD provisioning integration relies on the [Samanage REST API](https://www.samanage.com/api/), which is available to Samanage teams on the Professional plan or better.</span></span>

## <a name="assigning-users-to-samanage"></a><span data-ttu-id="789df-111">Gebruikers toewijzen aan Samanage</span><span class="sxs-lookup"><span data-stu-id="789df-111">Assigning users to Samanage</span></span>

<span data-ttu-id="789df-112">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="789df-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="789df-113">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="789df-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="789df-114">Voordat u configureren en inschakelen van de inrichting service, moet u om te bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang tot uw app Samanage nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="789df-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Samanage app.</span></span> <span data-ttu-id="789df-115">Als besloten, kunt u deze gebruikers toewijzen aan uw app Samanage door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="789df-115">Once decided, you can assign these users to your Samanage app by following the instructions here:</span></span>

[<span data-ttu-id="789df-116">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="789df-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-samanage"></a><span data-ttu-id="789df-117">Belangrijke tips voor het toewijzen van gebruikers aan Samanage</span><span class="sxs-lookup"><span data-stu-id="789df-117">Important tips for assigning users to Samanage</span></span>

*   <span data-ttu-id="789df-118">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan Samanage voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="789df-118">It is recommended that a single Azure AD user is assigned to Samanage to test the provisioning configuration.</span></span> <span data-ttu-id="789df-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="789df-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="789df-120">Wanneer een gebruiker aan Samanage toewijzen, moet u ofwel de **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster toewijzing.</span><span class="sxs-lookup"><span data-stu-id="789df-120">When assigning a user to Samanage, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="789df-121">De **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="789df-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="789df-122">Als een toegevoegde functie en de inrichting service eventuele aangepaste rollen gedefinieerd in Samanage leest en importeert ze in Azure AD waarin ze kunnen worden geselecteerd in het dialoogvenster rol selecteren.</span><span class="sxs-lookup"><span data-stu-id="789df-122">As an added feature, the provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="789df-123">Deze rollen zijn zichtbaar in de Azure portal nadat de inrichting-service is ingeschakeld en een synchronisatiecyclus is voltooid.</span><span class="sxs-lookup"><span data-stu-id="789df-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-samanage"></a><span data-ttu-id="789df-124">Gebruikersaanvragen voor Samanage configureren</span><span class="sxs-lookup"><span data-stu-id="789df-124">Configuring user provisioning to Samanage</span></span> 

<span data-ttu-id="789df-125">Deze sectie helpt u bij het verbinding maken met uw Azure AD Samanage van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Samanage op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="789df-125">This section guides you through connecting your Azure AD to Samanage's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="789df-126">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor Samanage, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="789df-126">You may also choose to enabled SAML-based Single Sign-On for Samanage, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="789df-127">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="789df-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-samanage-in-azure-ad"></a><span data-ttu-id="789df-128">Configureer Automatische account gebruikersaanvragen naar Samanage in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="789df-128">Configure automatic user account provisioning to Samanage in Azure AD:</span></span>


1. <span data-ttu-id="789df-129">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="789df-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="789df-130">Als u al Samanage voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Samanage met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="789df-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using the search field.</span></span> <span data-ttu-id="789df-131">Selecteer anders **toevoegen** en zoek naar **Samanage** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="789df-131">Otherwise, select **Add** and search for **Samanage** in the application gallery.</span></span> <span data-ttu-id="789df-132">Samanage selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="789df-132">Select Samanage from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="789df-133">Selecteer uw exemplaar van Samanage en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="789df-133">Select your instance of Samanage, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="789df-134">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="789df-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Samanage inrichten](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="789df-136">Onder de **beheerdersreferenties** sectie, voer de **Admin Username & beheerderswachtwoord** van uw Samanage-account.</span><span class="sxs-lookup"><span data-stu-id="789df-136">Under the **Admin Credentials** section, input the **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="789df-137">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw app Samanage.</span><span class="sxs-lookup"><span data-stu-id="789df-137">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Samanage app.</span></span> <span data-ttu-id="789df-138">Als de verbinding is mislukt, zorg ervoor dat uw account Samanage beheerdersmachtigingen heeft en probeer het opnieuw stap 5.</span><span class="sxs-lookup"><span data-stu-id="789df-138">If the connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="789df-139">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje "Een e-mailmelding verzenden wanneer een fout optreedt."</span><span class="sxs-lookup"><span data-stu-id="789df-139">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="789df-140">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="789df-140">Click **Save**.</span></span> 

9. <span data-ttu-id="789df-141">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers Samanage**.</span><span class="sxs-lookup"><span data-stu-id="789df-141">Under the Mappings section, select **Synchronize Azure Active Directory Users to Samanage**.</span></span>

10. <span data-ttu-id="789df-142">In de **kenmerktoewijzingen** sectie, moet u de kenmerken van de gebruiker is gesynchroniseerd vanuit Azure AD Samanage controleren.</span><span class="sxs-lookup"><span data-stu-id="789df-142">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Samanage.</span></span> <span data-ttu-id="789df-143">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Samanage voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="789df-143">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span></span> <span data-ttu-id="789df-144">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="789df-144">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="789df-145">Om de Azure AD-service voor Samanage inricht, wijzigen de **inrichting Status** naar **op** in de **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="789df-145">To enable the Azure AD provisioning service for Samanage, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="789df-146">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="789df-146">Click **Save**.</span></span> 

<span data-ttu-id="789df-147">Deze bewerking begint de initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan Samanage in de sectie gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="789df-147">This operation starts the initial synchronization of any users and/or groups assigned to Samanage in the Users and Groups section.</span></span> <span data-ttu-id="789df-148">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="789df-148">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="789df-149">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service beschrijven.</span><span class="sxs-lookup"><span data-stu-id="789df-149">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="789df-150">Zie voor meer informatie over het lezen van de Azure AD inrichting logboeken [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="789df-150">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="789df-151">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="789df-151">Additional resources</span></span>

* [<span data-ttu-id="789df-152">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="789df-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="789df-153">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="789df-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="789df-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="789df-154">Next steps</span></span>

* [<span data-ttu-id="789df-155">Informatie over het bekijken van Logboeken en rapporten over het inrichten van de activiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="789df-155">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
