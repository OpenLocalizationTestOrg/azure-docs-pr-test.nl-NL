---
title: Azure Privileged Identity Management goedkeuring werkstromen | Microsoft Docs
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
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="30241-103">Goedkeuringen (Preview)</span><span class="sxs-lookup"><span data-stu-id="30241-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="30241-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="30241-104">Overview</span></span>

<span data-ttu-id="30241-105">Met goedkeuringen voor Privileged Identity Management, kunt u rollen configureren om te goedkeuring vereisen voor activering en kies een of meerdere gebruikers of groepen als gedelegeerde fiatteurs.</span><span class="sxs-lookup"><span data-stu-id="30241-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="30241-106">Houd lezen voor meer informatie over het configureren van rollen en fiatteurs selecteren.</span><span class="sxs-lookup"><span data-stu-id="30241-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="30241-107">Houd er rekening mee dat deze functie nog in ontwikkeling is en fouten kunnen optreden.</span><span class="sxs-lookup"><span data-stu-id="30241-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="30241-108">De functionaliteit, met inbegrip van tekst naamconventies nog worden gewijzigd en mogen niet worden beschouwd als laatste.</span><span class="sxs-lookup"><span data-stu-id="30241-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="30241-109">Belangrijkste termen</span><span class="sxs-lookup"><span data-stu-id="30241-109">Key Terminology</span></span>

<span data-ttu-id="30241-110">*In aanmerking komende gebruiker van de rol* – een in aanmerking komende rol is een gebruiker binnen uw organisatie die is toegewezen aan een Azure AD-rol als in aanmerking komende (rol activering vereist is).</span><span class="sxs-lookup"><span data-stu-id="30241-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="30241-111">*Gedelegeerde goedkeurder* – een gemachtigde goedkeurder is een of meerdere personen of groepen binnen uw Azure AD die verantwoordelijk zijn voor het goedkeuren van aanvragen voor activering van rollen.</span><span class="sxs-lookup"><span data-stu-id="30241-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="30241-112">Scenario's</span><span class="sxs-lookup"><span data-stu-id="30241-112">Scenarios</span></span>

<span data-ttu-id="30241-113">De private preview ondersteunt de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="30241-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="30241-114">**Als een bevoorrechte rol beheerder (PRA) kunt u:**</span><span class="sxs-lookup"><span data-stu-id="30241-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="30241-115">goedkeuring voor specifieke rollen inschakelen</span><span class="sxs-lookup"><span data-stu-id="30241-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="30241-116">Geef goedkeurder gebruikers en/of groepen voor het goedkeuren van aanvragen</span><span class="sxs-lookup"><span data-stu-id="30241-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="30241-117">Geschiedenis van de aanvraag en goedkeuring voor alle bevoorrechte rollen weergeven</span><span class="sxs-lookup"><span data-stu-id="30241-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="30241-118">**Als een specifieke goedkeurder kunt u:**</span><span class="sxs-lookup"><span data-stu-id="30241-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="30241-119">in afwachting van goedkeuring (aanvragen) weergeven</span><span class="sxs-lookup"><span data-stu-id="30241-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="30241-120">goedkeuren of afwijzen aanvragen voor uitbreiding van de rol (één en/of bulk)</span><span class="sxs-lookup"><span data-stu-id="30241-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="30241-121">Geef de reden voor Mijn goedkeuring/afwijzing</span><span class="sxs-lookup"><span data-stu-id="30241-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="30241-122">**Als een in aanmerking komende gebruiker voor de rol kunt u:**</span><span class="sxs-lookup"><span data-stu-id="30241-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="30241-123">activering van de aanvraag van een rol die goedkeuring vereist</span><span class="sxs-lookup"><span data-stu-id="30241-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="30241-124">de status van uw aanvraag voor het activeren van weergeven</span><span class="sxs-lookup"><span data-stu-id="30241-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="30241-125">uw taak te voltooien in Azure AD als activering is goedgekeurd</span><span class="sxs-lookup"><span data-stu-id="30241-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="30241-126">Navigatie</span><span class="sxs-lookup"><span data-stu-id="30241-126">Navigation</span></span>

<span data-ttu-id="30241-127">We hebben de navigatie ter ondersteuning van goedkeuringen bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="30241-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="30241-128">De standaardwaarde landingspagina biedt snel toegang tot informatie over PIM en de nieuwe goedkeuringen-documentatie.</span><span class="sxs-lookup"><span data-stu-id="30241-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="30241-129">We hebben hebt ook een nieuwe sectie voor alle gebruikers van PIM, 'Mijn controlegeschiedenis' toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="30241-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="30241-130">Hier vindt u alle informatie die relevant zijn voor uw identiteit.</span><span class="sxs-lookup"><span data-stu-id="30241-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="30241-131">Dit omvat alle uw in behandeling en voltooid aanvragen, alle beslissingen over de aanvragen die u hebt opgelost en de afgelopen rol activeringen op één handige locatie.</span><span class="sxs-lookup"><span data-stu-id="30241-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="30241-132">Goedkeuring voor specifieke rollen inschakelen</span><span class="sxs-lookup"><span data-stu-id="30241-132">Enable approval for specific roles</span></span>

<span data-ttu-id="30241-133">Om goedkeuring voor een specifieke rol, moet u eerst Directory rollen selecteren in de linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="30241-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="30241-134">Zoek en selecteer de instellingen in het linkernavigatievenster van Directory-functies</span><span class="sxs-lookup"><span data-stu-id="30241-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="30241-135">Selecteer de bevoorrechte rollen:</span><span class="sxs-lookup"><span data-stu-id="30241-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="30241-136">Selecteert u 'Inschakelen' in de goedkeuringssectie vereisen:</span><span class="sxs-lookup"><span data-stu-id="30241-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="30241-137">Eenmaal is ingeschakeld, wordt de blade uitvouwen om weer te geven van de volgende details:</span><span class="sxs-lookup"><span data-stu-id="30241-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="30241-138">Als u niet alle goedkeurders opgeeft, worden de PRA(s) de standaard fiatteur (s).</span><span class="sxs-lookup"><span data-stu-id="30241-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="30241-139">PRA(s) nodig zijn voor het goedkeuren van alle activeringsaanvragen voor deze rol.</span><span class="sxs-lookup"><span data-stu-id="30241-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="30241-140">Geef goedkeurder gebruikers en/of groepen voor het goedkeuren van aanvragen</span><span class="sxs-lookup"><span data-stu-id="30241-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="30241-141">Als u wilt delegeren goedkeuring, klik op de optie 'Select goedkeurders':</span><span class="sxs-lookup"><span data-stu-id="30241-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="30241-142">Wanneer de blade Selecteer goedkeurders wordt geladen, u kunt zoeken naar een specifieke gebruiker of groep met behulp van de zoekbalk boven of selecteren in de lijst met vooraf ingestelde en klik vervolgens op 'Selecteren' als voltooid:</span><span class="sxs-lookup"><span data-stu-id="30241-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="30241-143">Opmerking: U kunt meerdere gebruikers of groepen tegelijkertijd selecteren.</span><span class="sxs-lookup"><span data-stu-id="30241-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="30241-144">Uw selectie wordt weergegeven in de lijst met geselecteerde goedkeurders zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="30241-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="30241-145">Als u wilt een goedkeurder verwijderen, klikt u op de knop verwijderen naast hun naam.</span><span class="sxs-lookup"><span data-stu-id="30241-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="30241-146">Aanvullende als fiatteurs wilt toevoegen, moet u het proces herhalen.</span><span class="sxs-lookup"><span data-stu-id="30241-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="30241-147">Geschiedenis van de aanvraag en goedkeuring voor alle bevoorrechte rollen weergeven</span><span class="sxs-lookup"><span data-stu-id="30241-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="30241-148">Aanvraag en goedkeuring als geschiedenis wilt weergeven voor alle bevoorrechte rollen, selecteer controlegeschiedenis vanuit het dashboard:</span><span class="sxs-lookup"><span data-stu-id="30241-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="30241-149">Sorteer de gegevens door de actie en zoek naar 'Activering goedgekeurd'</span><span class="sxs-lookup"><span data-stu-id="30241-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="30241-150">In afwachting van goedkeuring (aanvragen) weergeven</span><span class="sxs-lookup"><span data-stu-id="30241-150">View pending approvals (requests)</span></span>

<span data-ttu-id="30241-151">U zult als een gemachtigde goedkeurder e-mailmeldingen ontvangen wanneer een aanvraag wacht op uw goedkeuring wordt.</span><span class="sxs-lookup"><span data-stu-id="30241-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="30241-152">Selecteer het tabblad 'goedkeuringsaanvragen in behandeling' in de linkernavigatiebalk om weer te geven deze aanvragen in de PIM-portal, vanuit het dashboard (in het navigatievenster aan de nieuwe).</span><span class="sxs-lookup"><span data-stu-id="30241-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="30241-153">Van daaruit ziet u een lijst met aanvragen in afwachting van goedkeuring:</span><span class="sxs-lookup"><span data-stu-id="30241-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="30241-154">Goedkeuren of afwijzen aanvragen voor uitbreiding van de rol (één en/of bulk)</span><span class="sxs-lookup"><span data-stu-id="30241-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="30241-155">Selecteer de aanvragen die u wilt goedkeuren of weigeren en klik op de knop in de actiebalk die met uw beslissing overeenkomt:</span><span class="sxs-lookup"><span data-stu-id="30241-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="30241-156">Geef de reden voor Mijn goedkeuring/afwijzing</span><span class="sxs-lookup"><span data-stu-id="30241-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="30241-157">Hiermee opent u een nieuwe blade als u wilt goedkeuren of weigeren van meerdere aanvragen tegelijk.</span><span class="sxs-lookup"><span data-stu-id="30241-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="30241-158">Voer een reden voor uw beslissing en klikt u op (toestaan of weigeren) aan de onderkant of de blade:</span><span class="sxs-lookup"><span data-stu-id="30241-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="30241-159">Wanneer het proces voor aanvragen voltooid is, geeft het statussymbool hand van de beslissing (in dit voorbeeld wordt de beslissing is goedkeuren):</span><span class="sxs-lookup"><span data-stu-id="30241-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="30241-160">Activering van de aanvraag van een rol die goedkeuring vereist</span><span class="sxs-lookup"><span data-stu-id="30241-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="30241-161">Activering van een rol die goedkeuring vereist aanvraagt kan van de oude PIM-navigatie of de nieuwe navigatie worden gestart omdat het proces voor rolactivering hetzelfde is gebleven.</span><span class="sxs-lookup"><span data-stu-id="30241-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="30241-162">Selecteer een rol gewoon uit de lijst met rollen te activeren:</span><span class="sxs-lookup"><span data-stu-id="30241-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="30241-163">Als een bevoorrechte rol meerledige verificatie vereist, wordt u gevraagd eerst die taak te voltooien:</span><span class="sxs-lookup"><span data-stu-id="30241-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="30241-164">Wanneer u klaar bent, klikt u op activeren en een reden opgeven (indien nodig):</span><span class="sxs-lookup"><span data-stu-id="30241-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="30241-165">De aanvrager ziet een melding dat de aanvraag in afwachting van goedkeuring is:</span><span class="sxs-lookup"><span data-stu-id="30241-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="30241-166">De status van uw aanvraag voor het activeren van weergeven</span><span class="sxs-lookup"><span data-stu-id="30241-166">View the status of your request to activate</span></span>

<span data-ttu-id="30241-167">De statuscontrole van een aanvraag in behandeling activeren moet worden geopend in de nieuwe navigatie.</span><span class="sxs-lookup"><span data-stu-id="30241-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="30241-168">Selecteer het tabblad 'Mijn aanvragen' in de linkernavigatiebalk:</span><span class="sxs-lookup"><span data-stu-id="30241-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="30241-169">De aanvraagstatus wordt standaard ingesteld op 'In behandeling', maar u kunt schakelen om alle te zien of afgewezen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="30241-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="30241-170">Uw taak te voltooien in Azure AD als activering is goedgekeurd</span><span class="sxs-lookup"><span data-stu-id="30241-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="30241-171">Zodra de aanvraag is goedgekeurd, wordt de rol actief is en u kunt doorgaan met werk waarvoor deze rol is vereist.</span><span class="sxs-lookup"><span data-stu-id="30241-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="30241-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30241-172">Next steps</span></span>

<span data-ttu-id="30241-173">Uw feedback is belangrijk voor ons.</span><span class="sxs-lookup"><span data-stu-id="30241-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="30241-174">Aarzel niet om te delen opmerkingen of feedback met ons hier!</span><span class="sxs-lookup"><span data-stu-id="30241-174">Please feel free to share comments or feedback with us here!</span></span>
