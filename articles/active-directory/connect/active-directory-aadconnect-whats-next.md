---
title: 'Azure AD Connect: De volgende stappen en het beheren van Azure AD Connect | Microsoft Docs'
description: Informatie over het uitbreiden van de standaardconfiguratie en operationele taken voor Azure AD Connect.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="93937-103">Volgende stappen en het beheren van Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="93937-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="93937-104">Gebruik de operationele procedures in dit artikel voor het aanpassen van Azure Active Directory (Azure AD) verbinden om te voldoen aan de behoeften van uw organisatie en de vereisten.</span><span class="sxs-lookup"><span data-stu-id="93937-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="93937-105">Voeg aanvullende sync beheerders toe</span><span class="sxs-lookup"><span data-stu-id="93937-105">Add additional sync admins</span></span>
<span data-ttu-id="93937-106">Standaard alleen de gebruiker die heeft de installatie en lokale beheerders zich voor het beheren van de geïnstalleerde synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="93937-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="93937-107">Voor andere personen om toegang tot en beheer van de synchronisatie-engine te kunnen vinden van de groep ADSyncAdmins op de lokale server en toe te voegen aan deze groep.</span><span class="sxs-lookup"><span data-stu-id="93937-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="93937-108">Licenties toewijzen aan gebruikers van Azure AD Premium en Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="93937-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="93937-109">Nu uw gebruikers zijn gesynchroniseerd met de cloud, moet u ze een licentie toewijzen zodat ze kunnen aan de slag met cloud-apps, zoals Office 365.</span><span class="sxs-lookup"><span data-stu-id="93937-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="93937-110">Een Azure AD Premium of Enterprise Mobility Suite-licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="93937-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="93937-111">Meld u aan bij de Azure portal als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="93937-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="93937-112">Selecteer aan de linkerkant **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93937-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="93937-113">Op de **Active Directory** pagina, dubbelklikt u op de map met de gebruikers die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="93937-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="93937-114">Selecteer boven aan de pagina met de adreslijst **Licenties**.</span><span class="sxs-lookup"><span data-stu-id="93937-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="93937-115">Op de **licenties** pagina **Active Directory Premium** of **Enterprise Mobility Suite**, en klik vervolgens op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="93937-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="93937-116">Selecteer in het dialoogvenster de gebruikers aan wie u een licentie wilt toewijzen en klik op het vinkje om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="93937-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="93937-117">Controleer of de taak geplande synchronisatie</span><span class="sxs-lookup"><span data-stu-id="93937-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="93937-118">De Azure portal gebruiken om de status van een synchronisatie te controleren.</span><span class="sxs-lookup"><span data-stu-id="93937-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="93937-119">De geplande synchronisatietaak controleren</span><span class="sxs-lookup"><span data-stu-id="93937-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="93937-120">Meld u aan bij de Azure portal als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="93937-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="93937-121">Selecteer aan de linkerkant **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93937-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="93937-122">Op de **Active Directory** pagina, dubbelklikt u op de map met de gebruikers die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="93937-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="93937-123">Selecteer boven aan de directorypagina **Adreslijstintegratie**.</span><span class="sxs-lookup"><span data-stu-id="93937-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="93937-124">Onder **integratie met lokale active directory**, houd er rekening mee de tijd van laatste synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="93937-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="93937-125"><center>![Tijd van de Directory-synchronisatie](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="93937-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="93937-126">Start een geplande synchronisatietaak</span><span class="sxs-lookup"><span data-stu-id="93937-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="93937-127">Als u een synchronisatietaak uitvoeren wilt, kunt u dit doen door het opnieuw met de Azure AD Connect-wizard uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="93937-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="93937-128">U moet uw Azure AD-referenties op te geven.</span><span class="sxs-lookup"><span data-stu-id="93937-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="93937-129">Selecteer in de wizard de **Synchronisatieopties aanpassen** en op **volgende** om de wizard te doorlopen.</span><span class="sxs-lookup"><span data-stu-id="93937-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="93937-130">Zorg ervoor dat aan het einde de **Start het synchronisatieproces zodra de eerste configuratie is voltooid** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="93937-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="93937-131"><center>![Synchronisatie starten](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="93937-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="93937-132">Zie voor meer informatie over de Azure AD Connect sync Scheduler [met Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="93937-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="93937-133">Aanvullende taken die beschikbaar zijn in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="93937-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="93937-134">Na de initiële installatie van Azure AD Connect, kunt u altijd de wizard opnieuw starten vanuit de snelkoppeling Azure AD Connect start pagina of het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="93937-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="93937-135">U ziet dat opnieuw de verbinding met de wizard een aantal nieuwe opties in de vorm van aanvullende taken biedt.</span><span class="sxs-lookup"><span data-stu-id="93937-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="93937-136">De volgende tabel biedt een overzicht van deze taken en een korte beschrijving van elke taak.</span><span class="sxs-lookup"><span data-stu-id="93937-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![Lijst met extra taken](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="93937-138">Extra taak</span><span class="sxs-lookup"><span data-stu-id="93937-138">Additional task</span></span> | <span data-ttu-id="93937-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="93937-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93937-140">**Het geselecteerde scenario weergeven**</span><span class="sxs-lookup"><span data-stu-id="93937-140">**View the selected scenario**</span></span> |<span data-ttu-id="93937-141">Uw huidige Azure AD Connect-oplossing weergeven.</span><span class="sxs-lookup"><span data-stu-id="93937-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="93937-142">Dit omvat algemene instellingen, gesynchroniseerd mappen en de synchronisatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="93937-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="93937-143">**Opties voor synchronisatie aanpassen**</span><span class="sxs-lookup"><span data-stu-id="93937-143">**Customize synchronization options**</span></span> |<span data-ttu-id="93937-144">De huidige configuratie zoals aanvullende Active Directory-forests toevoegen aan de configuratie of het inschakelen van synchronisatie-opties, zoals gebruikers, groepen, apparaat of terugschrijven van wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="93937-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="93937-145">**Faseringsmodus inschakelen**</span><span class="sxs-lookup"><span data-stu-id="93937-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="93937-146">Fase-informatie die niet direct is gesynchroniseerd en is niet geëxporteerd naar Azure AD of on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="93937-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="93937-147">Met deze functie kunt u de synchronisaties bekijken voordat ze optreden.</span><span class="sxs-lookup"><span data-stu-id="93937-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="93937-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93937-148">Next steps</span></span>
<span data-ttu-id="93937-149">Meer informatie over [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="93937-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
