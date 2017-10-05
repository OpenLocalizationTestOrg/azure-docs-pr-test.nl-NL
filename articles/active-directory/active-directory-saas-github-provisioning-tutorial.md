---
title: 'Zelfstudie: GitHub configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Informatie over het configureren van Azure Active Directory voor het automatisch inrichten en gebruikersaccounts met GitHub ongedaan in te richten.
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
ms.openlocfilehash: 3cc70273e95dbf4913e7bbcd8a37bd9a52987b60
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="fa4c9-103">Zelfstudie: GitHub configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="fa4c9-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="fa4c9-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in GitHub en Azure AD wilt om automatisch inrichten en de gebruikersaccounts van Azure AD met GitHub ongedaan in te richten.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-104">The objective of this tutorial is to show you the steps you need to perform in GitHub and Azure AD to automatically provision and de-provision user accounts from Azure AD to GitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fa4c9-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fa4c9-105">Prerequisites</span></span>

<span data-ttu-id="fa4c9-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="fa4c9-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="fa4c9-107">Een Azure Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="fa4c9-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="fa4c9-108">Een Github-tenant met de [bedrijfsplan](https://help.github.com/articles/organization-billing-plans/#business-plan) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="fa4c9-108">A Github tenant with the [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="fa4c9-109">Een gebruikersaccount in GitHub met beheerdersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="fa4c9-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="fa4c9-110">De Azure AD integratie inrichting is afhankelijk van de [GitHub SCIM API](https://developer.github.com/v3/scim/), die beschikbaar zijn voor Github teams op het bedrijfsplan of hoger is.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-110">The Azure AD provisioning integration relies on the [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available to Github teams on the Business plan or better.</span></span>

## <a name="assigning-users-to-github"></a><span data-ttu-id="fa4c9-111">Gebruikers toewijzen aan GitHub</span><span class="sxs-lookup"><span data-stu-id="fa4c9-111">Assigning users to GitHub</span></span>

<span data-ttu-id="fa4c9-112">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fa4c9-113">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="fa4c9-114">Voordat u configureren en inschakelen van de inrichting service, moet u om te bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot uw app in GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GitHub app.</span></span> <span data-ttu-id="fa4c9-115">Als besloten, kunt u deze gebruikers toewijzen aan uw GitHub-app door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa4c9-115">Once decided, you can assign these users to your GitHub app by following the instructions here:</span></span>

[<span data-ttu-id="fa4c9-116">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="fa4c9-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-github"></a><span data-ttu-id="fa4c9-117">Belangrijke tips voor het toewijzen van gebruikers met GitHub</span><span class="sxs-lookup"><span data-stu-id="fa4c9-117">Important tips for assigning users to GitHub</span></span>

*   <span data-ttu-id="fa4c9-118">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan GitHub voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-118">It is recommended that a single Azure AD user is assigned to GitHub to test the provisioning configuration.</span></span> <span data-ttu-id="fa4c9-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fa4c9-120">Bij het toewijzen van een gebruiker met GitHub, moet u ofwel de **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster toewijzing.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-120">When assigning a user to GitHub, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="fa4c9-121">De **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-github"></a><span data-ttu-id="fa4c9-122">Configuratie van gebruikers inrichten met GitHub</span><span class="sxs-lookup"><span data-stu-id="fa4c9-122">Configuring user provisioning to GitHub</span></span> 

<span data-ttu-id="fa4c9-123">Deze sectie helpt u bij uw Azure AD verbinden met de GitHub-gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in GitHub op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-123">This section guides you through connecting your Azure AD to GitHub's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="fa4c9-124">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor GitHub, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa4c9-124">You may also choose to enabled SAML-based Single Sign-On for GitHub, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fa4c9-125">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-github-in-azure-ad"></a><span data-ttu-id="fa4c9-126">Automatisch gebruikers account inrichten met GitHub in Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fa4c9-126">Configure automatic user account provisioning to GitHub in Azure AD</span></span>


1. <span data-ttu-id="fa4c9-127">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="fa4c9-128">Als u al GitHub voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van het zoekveld met GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using the search field.</span></span> <span data-ttu-id="fa4c9-129">Selecteer anders **toevoegen** en zoek naar **GitHub** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-129">Otherwise, select **Add** and search for **GitHub** in the application gallery.</span></span> <span data-ttu-id="fa4c9-130">GitHub selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-130">Select GitHub from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="fa4c9-131">Selecteer uw exemplaar van GitHub en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-131">Select your instance of GitHub, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="fa4c9-132">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Het inrichten van GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="fa4c9-134">Onder de **beheerdersreferenties** sectie, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="fa4c9-135">Deze bewerking wordt een dialoogvenster met GitHub autorisatie in een nieuw browservenster geopend.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="fa4c9-136">Aanmelden bij uw beheerdersaccount met GitHub in het nieuwe venster.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-136">In the new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="fa4c9-137">Selecteer in de resulterende autorisatie dialoogvenster de GitHub-team dat u inschakelen wilt voor inrichting en selecteer vervolgens **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-137">In the resulting authorization dialog, select the GitHub team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="fa4c9-138">Als voltooid, terug naar de Azure-portal om het inrichtingsproces configuratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

    ![Dialoogvenster autorisatie](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="fa4c9-140">Voer in de Azure portal **Tenant-URL** en klik op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw GitHub-app.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-140">In the Azure portal, input **Tenant URL** and click **Test Connection** to ensure Azure AD can connect to your GitHub app.</span></span> <span data-ttu-id="fa4c9-141">Als de verbinding is mislukt, zorg ervoor dat uw GitHub-account beheerdersmachtigingen heeft en **Tenant-URl** is opgegeven correct en probeer het opnieuw de stap 'Autoriseren' (u kunt vormen **Tenant-URL** door regel: 'https://api.github.com/scim/v2/organizations/ + < Organizations_name >', kunt u uw organisaties vinden onder uw GitHub-account: **instellingen** > **organisaties**).</span><span class="sxs-lookup"><span data-stu-id="fa4c9-141">If the connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try the "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Dialoogvenster autorisatie](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="fa4c9-143">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje "Een e-mailmelding verzenden wanneer een fout optreedt."</span><span class="sxs-lookup"><span data-stu-id="fa4c9-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="fa4c9-144">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-144">Click **Save**.</span></span> 

10. <span data-ttu-id="fa4c9-145">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers met GitHub**.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to GitHub**.</span></span>

11. <span data-ttu-id="fa4c9-146">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker die zijn gesynchroniseerd vanuit Azure AD met GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GitHub.</span></span> <span data-ttu-id="fa4c9-147">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in GitHub voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-147">The attributes selected as **Matching** properties are used to match the user accounts in GitHub for update operations.</span></span> <span data-ttu-id="fa4c9-148">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-148">Select the Save button to commit any changes.</span></span>

12. <span data-ttu-id="fa4c9-149">Om de Azure AD-service voor GitHub inricht, wijzigen de **inrichting Status** naar **op** in de **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="fa4c9-149">To enable the Azure AD provisioning service for GitHub, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13. <span data-ttu-id="fa4c9-150">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-150">Click **Save**.</span></span> 

<span data-ttu-id="fa4c9-151">Deze bewerking begint de initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan GitHub in de sectie gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-151">This operation starts the initial synchronization of any users and/or groups assigned to GitHub in the Users and Groups section.</span></span> <span data-ttu-id="fa4c9-152">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-152">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="fa4c9-153">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service beschrijven.</span><span class="sxs-lookup"><span data-stu-id="fa4c9-153">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="fa4c9-154">Zie voor meer informatie over het lezen van de Azure AD inrichting logboeken [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="fa4c9-154">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fa4c9-155">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fa4c9-155">Additional resources</span></span>

* [<span data-ttu-id="fa4c9-156">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="fa4c9-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="fa4c9-157">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fa4c9-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="fa4c9-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fa4c9-158">Next steps</span></span>

* [<span data-ttu-id="fa4c9-159">Informatie over het bekijken van Logboeken en rapporten over het inrichten van de activiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="fa4c9-159">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
