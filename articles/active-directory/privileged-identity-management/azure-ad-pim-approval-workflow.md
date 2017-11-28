---
title: Goedkeuring door Privileged Identity Management-werkstromen aaaAzure | Microsoft Docs
description: Meer informatie over werkstromen voor goedkeuring in Privileged Identity Management (PIM)
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="2648b-103">Goedkeuringen (Preview)</span><span class="sxs-lookup"><span data-stu-id="2648b-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="2648b-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2648b-104">Overview</span></span>

<span data-ttu-id="2648b-105">Met goedkeuringen voor Privileged Identity Management, kunt u rollen toorequire goedkeuring voor activering configureren en een of meer gebruikers of groepen kiezen als gedelegeerde fiatteurs.</span><span class="sxs-lookup"><span data-stu-id="2648b-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="2648b-106">Toolearn houden hoe lezen tooconfigure rollen en fiatteurs selecteren.</span><span class="sxs-lookup"><span data-stu-id="2648b-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="2648b-107">Houd er rekening mee dat deze functie nog in ontwikkeling is en fouten kunnen optreden.</span><span class="sxs-lookup"><span data-stu-id="2648b-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="2648b-108">Hallo-functionaliteit, met inbegrip van tekst naamconventies nog worden gewijzigd en mag niet worden beschouwd als laatste.</span><span class="sxs-lookup"><span data-stu-id="2648b-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="2648b-109">Belangrijkste termen</span><span class="sxs-lookup"><span data-stu-id="2648b-109">Key Terminology</span></span>

<span data-ttu-id="2648b-110">*In aanmerking komende gebruiker van de rol* – een in aanmerking komende rol is een gebruiker binnen uw organisatie die is toegewezen tooan Azure AD-rol als in aanmerking komende (rol activering vereist is).</span><span class="sxs-lookup"><span data-stu-id="2648b-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="2648b-111">*Gedelegeerde goedkeurder* – een gemachtigde goedkeurder is een of meerdere personen of groepen binnen uw Azure AD die verantwoordelijk zijn voor het goedkeuren van aanvragen voor activering van rollen.</span><span class="sxs-lookup"><span data-stu-id="2648b-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="2648b-112">Scenario's</span><span class="sxs-lookup"><span data-stu-id="2648b-112">Scenarios</span></span>

<span data-ttu-id="2648b-113">Hallo private preview ondersteunt Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="2648b-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="2648b-114">**Als een bevoorrechte rol beheerder (PRA) kunt u:**</span><span class="sxs-lookup"><span data-stu-id="2648b-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="2648b-115">goedkeuring voor specifieke rollen inschakelen</span><span class="sxs-lookup"><span data-stu-id="2648b-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="2648b-116">Geef goedkeurder gebruikers en/of groepen tooapprove aanvragen</span><span class="sxs-lookup"><span data-stu-id="2648b-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="2648b-117">Geschiedenis van de aanvraag en goedkeuring voor alle bevoorrechte rollen weergeven</span><span class="sxs-lookup"><span data-stu-id="2648b-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="2648b-118">**Als een specifieke goedkeurder kunt u:**</span><span class="sxs-lookup"><span data-stu-id="2648b-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="2648b-119">in afwachting van goedkeuring (aanvragen) weergeven</span><span class="sxs-lookup"><span data-stu-id="2648b-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="2648b-120">goedkeuren of afwijzen aanvragen voor uitbreiding van de rol (één en/of bulk)</span><span class="sxs-lookup"><span data-stu-id="2648b-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="2648b-121">Geef de reden voor Mijn goedkeuring/afwijzing</span><span class="sxs-lookup"><span data-stu-id="2648b-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="2648b-122">**Als een in aanmerking komende gebruiker voor de rol kunt u:**</span><span class="sxs-lookup"><span data-stu-id="2648b-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="2648b-123">activering van de aanvraag van een rol die goedkeuring vereist</span><span class="sxs-lookup"><span data-stu-id="2648b-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="2648b-124">Hallo-status van uw aanvraag tooactivate weergeven</span><span class="sxs-lookup"><span data-stu-id="2648b-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="2648b-125">uw taak te voltooien in Azure AD als activering is goedgekeurd</span><span class="sxs-lookup"><span data-stu-id="2648b-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="2648b-126">Navigatie</span><span class="sxs-lookup"><span data-stu-id="2648b-126">Navigation</span></span>

<span data-ttu-id="2648b-127">We hebben Hallo navigatie toosupport goedkeuringen bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="2648b-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="2648b-128">Hallo standaard startpagina biedt snel toegang tooinformation over PIM en Hallo nieuwe goedkeuringen documentatie.</span><span class="sxs-lookup"><span data-stu-id="2648b-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="2648b-129">We hebben hebt ook een nieuwe sectie voor alle gebruikers van PIM, 'Mijn controlegeschiedenis' toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2648b-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="2648b-130">Hier vindt u alle relevante tooyour identiteit van de Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="2648b-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="2648b-131">Dit omvat alle uw in behandeling en voltooid aanvragen, alle beslissingen over Hallo aanvragen die u hebt opgelost en de afgelopen rol activeringen op één handige locatie.</span><span class="sxs-lookup"><span data-stu-id="2648b-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="2648b-132">Goedkeuring voor specifieke rollen inschakelen</span><span class="sxs-lookup"><span data-stu-id="2648b-132">Enable approval for specific roles</span></span>

<span data-ttu-id="2648b-133">Directory-functies tooenable goedkeuring voor een specifieke rol eerst uit de linkernavigatiebalk Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="2648b-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="2648b-134">Zoek en selecteer de instellingen in Hallo linkernavigatiegedeelte van Directory-functies</span><span class="sxs-lookup"><span data-stu-id="2648b-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="2648b-135">Selecteer de bevoorrechte rollen:</span><span class="sxs-lookup"><span data-stu-id="2648b-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="2648b-136">Selecteert u 'Inschakelen' in hello goedkeuringssectie vereisen:</span><span class="sxs-lookup"><span data-stu-id="2648b-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="2648b-137">Eenmaal is ingeschakeld, uitbreidt Hallo blade tooshow Hallo volgende details:</span><span class="sxs-lookup"><span data-stu-id="2648b-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="2648b-138">Als u niet alle goedkeurders opgeeft, worden Hallo PRA(s) Hallo standaard fiatteur (s).</span><span class="sxs-lookup"><span data-stu-id="2648b-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="2648b-139">PRA(s) zijn vereiste tooapprove activering van alle voor deze rol aanvragen.</span><span class="sxs-lookup"><span data-stu-id="2648b-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="2648b-140">Geef goedkeurder gebruikers en/of groepen tooapprove aanvragen</span><span class="sxs-lookup"><span data-stu-id="2648b-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="2648b-141">toodelegate goedkeuring, klikt u op de optie Hallo 'Goedkeurders selecteren' te:</span><span class="sxs-lookup"><span data-stu-id="2648b-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="2648b-142">Wanneer Hallo Selecteer goedkeurders blade wordt geladen, u kunt zoeken naar een specifieke gebruiker of groep met behulp van de zoekbalk Hallo op Hallo top- of te selecteren in de vooraf ingestelde lijst Hallo en klik vervolgens op 'Selecteren' als voltooid:</span><span class="sxs-lookup"><span data-stu-id="2648b-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="2648b-143">Opmerking: U kunt meerdere gebruikers of groepen tegelijkertijd selecteren.</span><span class="sxs-lookup"><span data-stu-id="2648b-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="2648b-144">Uw selectie weergegeven in de lijst Hallo van geselecteerde goedkeurders zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="2648b-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="2648b-145">tooremove goedkeurder, klik op Hallo verwijderen volgende tootheir naam van de knop.</span><span class="sxs-lookup"><span data-stu-id="2648b-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="2648b-146">tooadd extra fiatteurs herhaaldelijk Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="2648b-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="2648b-147">Geschiedenis van de aanvraag en goedkeuring voor alle bevoorrechte rollen weergeven</span><span class="sxs-lookup"><span data-stu-id="2648b-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="2648b-148">de aanvraag en goedkeuring geschiedenis tooview voor alle bevoorrechte rollen selecteren controlegeschiedenis Hallo dashboard:</span><span class="sxs-lookup"><span data-stu-id="2648b-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="2648b-149">Hallo-gegevens door de actie sorteren en zoek naar 'Activering goedgekeurd'</span><span class="sxs-lookup"><span data-stu-id="2648b-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="2648b-150">In afwachting van goedkeuring (aanvragen) weergeven</span><span class="sxs-lookup"><span data-stu-id="2648b-150">View pending approvals (requests)</span></span>

<span data-ttu-id="2648b-151">U zult als een gemachtigde goedkeurder e-mailmeldingen ontvangen wanneer een aanvraag wacht op uw goedkeuring wordt.</span><span class="sxs-lookup"><span data-stu-id="2648b-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="2648b-152">tooview van deze aanvragen in Hallo PIM-portal op het dashboardtabblad (in de nieuwe navigatie Hallo) Selecteer Hallo 'in behandeling goedkeuringsaanvragen' hello navigatiebalk links.</span><span class="sxs-lookup"><span data-stu-id="2648b-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="2648b-153">Van daaruit ziet u een lijst met aanvragen in afwachting van goedkeuring:</span><span class="sxs-lookup"><span data-stu-id="2648b-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="2648b-154">Goedkeuren of afwijzen aanvragen voor uitbreiding van de rol (één en/of bulk)</span><span class="sxs-lookup"><span data-stu-id="2648b-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="2648b-155">Selecteer Hallo aanvragen u wenst dat tooapprove of weigeren en klik op de knop Hallo in de actiebalk die met uw beslissing overeenkomt:</span><span class="sxs-lookup"><span data-stu-id="2648b-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="2648b-156">Geef de reden voor Mijn goedkeuring/afwijzing</span><span class="sxs-lookup"><span data-stu-id="2648b-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="2648b-157">Dit wordt een nieuwe blade tooapprove openen of meerdere aanvragen tegelijk weigeren.</span><span class="sxs-lookup"><span data-stu-id="2648b-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="2648b-158">Voer een reden voor uw beslissing en klikt u op (toestaan of weigeren) op Hallo onder of Hallo blade:</span><span class="sxs-lookup"><span data-stu-id="2648b-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="2648b-159">Wanneer het Hallo-aanvraag is voltooid, Hallo statussymbool geeft de beslissingen die u hebt gemaakt (in dit voorbeeld Hallo besluit is goedkeuren):</span><span class="sxs-lookup"><span data-stu-id="2648b-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="2648b-160">Activering van de aanvraag van een rol die goedkeuring vereist</span><span class="sxs-lookup"><span data-stu-id="2648b-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="2648b-161">Activering van een rol waarvoor goedkeuring kan worden gestart vanuit Hallo oude PIM navigatie of nieuwe navigatie Hallo aanvraagt, als Hallo-proces voor de rol activering blijft Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="2648b-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="2648b-162">Selecteer een rol gewoon uit Hallo lijst met rollen te activeren:</span><span class="sxs-lookup"><span data-stu-id="2648b-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="2648b-163">Als een bevoorrechte rol meerledige verificatie vereist, wordt u gevraagd eerst die taak te voltooien:</span><span class="sxs-lookup"><span data-stu-id="2648b-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="2648b-164">Wanneer u klaar bent, klikt u op activeren en een reden opgeven (indien nodig):</span><span class="sxs-lookup"><span data-stu-id="2648b-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="2648b-165">Hallo aanvrager ziet een melding dat de aanvraag Hallo is in afwachting van goedkeuring:</span><span class="sxs-lookup"><span data-stu-id="2648b-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="2648b-166">Hallo-status van uw aanvraag tooactivate weergeven</span><span class="sxs-lookup"><span data-stu-id="2648b-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="2648b-167">Hallo-status van een aanvraag in behandeling tooactivate weergeven moet worden geopend in de nieuwe navigatie.</span><span class="sxs-lookup"><span data-stu-id="2648b-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="2648b-168">Selecteer in de Hallo linkernavigatiebalk Hallo 'Mijn aanvragen' tabblad:</span><span class="sxs-lookup"><span data-stu-id="2648b-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="2648b-169">aanvraag voor weergave van Hallo standaardwaarden te 'In behandeling', maar u kunt alle toosee schakelen of afgewezen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="2648b-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="2648b-170">Uw taak te voltooien in Azure AD als activering is goedgekeurd</span><span class="sxs-lookup"><span data-stu-id="2648b-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="2648b-171">Zodra het Hallo-aanvraag is goedgekeurd, Hallo rol actief is en u kunt doorgaan met werk waarvoor deze rol is vereist.</span><span class="sxs-lookup"><span data-stu-id="2648b-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="2648b-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2648b-172">Next steps</span></span>

<span data-ttu-id="2648b-173">Uw feedback is belangrijk toous.</span><span class="sxs-lookup"><span data-stu-id="2648b-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="2648b-174">Kunt u gratis tooshare opmerkingen of feedback met ons hier!</span><span class="sxs-lookup"><span data-stu-id="2648b-174">Please feel free tooshare comments or feedback with us here!</span></span>
