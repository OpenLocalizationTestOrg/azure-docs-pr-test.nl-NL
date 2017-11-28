---
title: 'Azure AD Connect: Volgende stappen en hoe Azure AD Connect toomanage | Microsoft Docs'
description: Meer informatie over hoe tooextend standaardconfiguratie en operationele taken Hallo voor Azure AD Connect.
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
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="128f0-103">Volgende stappen en hoe toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="128f0-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="128f0-104">Gebruik Hallo operationele procedures in dit artikel toocustomize verbinding maken met Azure Active Directory (Azure AD) toomeet behoeften en de vereisten van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="128f0-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="128f0-105">Voeg aanvullende sync beheerders toe</span><span class="sxs-lookup"><span data-stu-id="128f0-105">Add additional sync admins</span></span>
<span data-ttu-id="128f0-106">Standaard worden alleen Hallo-gebruiker die Hallo installatie en lokale Administrators kunnen toomanage hello geïnstalleerd synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="128f0-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="128f0-107">Voor andere personen toobe kunnen tooaccess en beheren van Hallo synchronisatie-engine, Hallo groep ADSyncAdmins op de lokale server Hallo vinden en ze toothis groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="128f0-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="128f0-108">Toewijzen van licenties tooAzure AD Premium en Enterprise Mobility Suite-gebruikers</span><span class="sxs-lookup"><span data-stu-id="128f0-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="128f0-109">Nu dat uw gebruikers zijn gesynchroniseerd toohello cloud, moet u tooassign ze een licentie zodat ze kunnen aan de slag met cloud-apps, zoals Office 365.</span><span class="sxs-lookup"><span data-stu-id="128f0-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="128f0-110">tooassign een Azure AD Premium of Enterprise Mobility Suite-licentie</span><span class="sxs-lookup"><span data-stu-id="128f0-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="128f0-111">Meld u aan toohello Azure-portal als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="128f0-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="128f0-112">Selecteer aan de linkerkant Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="128f0-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="128f0-113">Op Hallo **Active Directory** pagina, dubbelklikt u op Hallo map waaraan u tooset-up wilt Hallo-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="128f0-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="128f0-114">Selecteer Hallo bovenaan de pagina directory Hallo in **licenties**.</span><span class="sxs-lookup"><span data-stu-id="128f0-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="128f0-115">Op Hallo **licenties** pagina **Active Directory Premium** of **Enterprise Mobility Suite**, en klik vervolgens op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="128f0-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="128f0-116">Selecteer in het dialoogvenster Hallo Hallo-gebruikers u wilt tooassign licenties aan en klik vervolgens op Hallo vinkje pictogram toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="128f0-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="128f0-117">Controleer of de geplande synchronisatietaak Hallo</span><span class="sxs-lookup"><span data-stu-id="128f0-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="128f0-118">Gebruik hello Azure portal toocheck Hallo status van een synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="128f0-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="128f0-119">tooverify hello geplande synchronisatietaak</span><span class="sxs-lookup"><span data-stu-id="128f0-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="128f0-120">Meld u aan toohello Azure-portal als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="128f0-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="128f0-121">Selecteer aan de linkerkant Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="128f0-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="128f0-122">Op Hallo **Active Directory** pagina, dubbelklikt u op Hallo map waaraan u tooset-up wilt Hallo-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="128f0-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="128f0-123">Selecteer Hallo bovenaan de pagina directory Hallo in **Adreslijstintegratie**.</span><span class="sxs-lookup"><span data-stu-id="128f0-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="128f0-124">Onder **integratie met lokale active directory**, opmerking Hallo tijd van laatste synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="128f0-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="128f0-125"><center>![Tijd van de Directory-synchronisatie](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="128f0-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="128f0-126">Start een geplande synchronisatietaak</span><span class="sxs-lookup"><span data-stu-id="128f0-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="128f0-127">Als u een synchronisatietaak toorun moet, kunt u dit doen door nogmaals via hello Azure AD Connect-wizard uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="128f0-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="128f0-128">U moet uw Azure AD-referenties tooprovide.</span><span class="sxs-lookup"><span data-stu-id="128f0-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="128f0-129">Selecteer in de wizard Hallo Hallo **Synchronisatieopties aanpassen** en op **volgende** toomove via Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="128f0-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="128f0-130">Zorg ervoor dat Hallo aan het einde van Hallo **Hallo synchronisatieproces gestart zodra Hallo eerste configuratie is voltooid** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="128f0-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="128f0-131"><center>![Synchronisatie starten](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="128f0-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="128f0-132">Zie voor meer informatie over hello Azure AD Connect-synchronisatie Scheduler [met Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="128f0-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="128f0-133">Aanvullende taken die beschikbaar zijn in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="128f0-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="128f0-134">Na de initiële installatie van Azure AD Connect, kunt u altijd Hallo wizard opnieuw starten vanuit hello Azure AD Connect start pagina of het bureaublad snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="128f0-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="128f0-135">U ziet dat een aantal nieuwe opties in Hallo vorm van aanvullende taken opnieuw de verbinding met de wizard Hallo biedt.</span><span class="sxs-lookup"><span data-stu-id="128f0-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="128f0-136">Hallo volgende tabel geeft een samenvatting van deze taken en een korte beschrijving van elke taak.</span><span class="sxs-lookup"><span data-stu-id="128f0-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![Lijst met extra taken](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="128f0-138">Extra taak</span><span class="sxs-lookup"><span data-stu-id="128f0-138">Additional task</span></span> | <span data-ttu-id="128f0-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="128f0-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="128f0-140">**Weergave Hallo geselecteerde scenario**</span><span class="sxs-lookup"><span data-stu-id="128f0-140">**View hello selected scenario**</span></span> |<span data-ttu-id="128f0-141">Uw huidige Azure AD Connect-oplossing weergeven.</span><span class="sxs-lookup"><span data-stu-id="128f0-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="128f0-142">Dit omvat algemene instellingen, gesynchroniseerd mappen en de synchronisatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="128f0-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="128f0-143">**Opties voor synchronisatie aanpassen**</span><span class="sxs-lookup"><span data-stu-id="128f0-143">**Customize synchronization options**</span></span> |<span data-ttu-id="128f0-144">De huidige configuratie Hallo zoals het toevoegen van aanvullende configuratie van Active Directory-forests toohello of synchronisatie-opties, zoals gebruikers, groepen, apparaat of wachtwoord terugschrijven inschakelen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="128f0-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="128f0-145">**Faseringsmodus inschakelen**</span><span class="sxs-lookup"><span data-stu-id="128f0-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="128f0-146">Fase-informatie die niet direct is gesynchroniseerd en niet geëxporteerd tooAzure AD of op de lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="128f0-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="128f0-147">Met deze functie kunt u synchronisaties Hallo bekijken voordat ze optreden.</span><span class="sxs-lookup"><span data-stu-id="128f0-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="128f0-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="128f0-148">Next steps</span></span>
<span data-ttu-id="128f0-149">Meer informatie over [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="128f0-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
