---
title: aaaGet slag met Azure Scheduler in Azure portal | Microsoft Docs
description: Aan de slag met Azure Scheduler in Azure-portal
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="179f1-103">Aan de slag met Azure Scheduler in Azure-portal</span><span class="sxs-lookup"><span data-stu-id="179f1-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="179f1-104">Het is gemakkelijk toocreate geplande taken in Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="179f1-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="179f1-105">In deze zelfstudie leert u hoe toocreate een taak.</span><span class="sxs-lookup"><span data-stu-id="179f1-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="179f1-106">U komt ook te weten hoe de controle- en beheerfuncties van Scheduler werken.</span><span class="sxs-lookup"><span data-stu-id="179f1-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="179f1-107">Een taak maken</span><span class="sxs-lookup"><span data-stu-id="179f1-107">Create a job</span></span>
1. <span data-ttu-id="179f1-108">Aanmelden te[Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="179f1-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="179f1-109">Klik op **+ nieuw** > type *Scheduler* in het zoekvak Hallo > Selecteer **Scheduler** in resultaten > Klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="179f1-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="179f1-110">We gaan een taak maken waarbij we eenvoudig http://www.microsoft.com/ bestoken met een GET-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="179f1-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="179f1-111">In Hallo **Scheduler-taak** scherm, voert u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="179f1-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="179f1-112">**Naam:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="179f1-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="179f1-113">**Abonnement:** uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="179f1-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="179f1-114">**Taakverzameling:** selecteer een bestaande taakverzameling of klik op **Nieuw** > typ een naam.</span><span class="sxs-lookup"><span data-stu-id="179f1-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="179f1-115">Vervolgens gaat u naar **bewerkingsinstellingen**, definiëren Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="179f1-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="179f1-116">**Actietype:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="179f1-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="179f1-117">**Methode:** `GET`</span><span class="sxs-lookup"><span data-stu-id="179f1-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="179f1-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="179f1-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="179f1-119">Tot slot gaan we een planning definiëren.</span><span class="sxs-lookup"><span data-stu-id="179f1-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="179f1-120">Hallo-taak kan worden gedefinieerd als een eenmalige taak, maar we kiezen een terugkerende planning:</span><span class="sxs-lookup"><span data-stu-id="179f1-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="179f1-121">**Terugkeerpatroon**:`Recurring`</span><span class="sxs-lookup"><span data-stu-id="179f1-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="179f1-122">**Start**: de datum van vandaag</span><span class="sxs-lookup"><span data-stu-id="179f1-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="179f1-123">**Herhaald elke**:`12 Hours`</span><span class="sxs-lookup"><span data-stu-id="179f1-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="179f1-124">**Beëindigen op**: twee dagen na de huidige datum</span><span class="sxs-lookup"><span data-stu-id="179f1-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="179f1-125">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="179f1-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="179f1-126">Taken beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="179f1-126">Manage and monitor jobs</span></span>
<span data-ttu-id="179f1-127">Zodra een taak is gemaakt, wordt deze weergegeven in Hallo belangrijkste Azure-dashboard.</span><span class="sxs-lookup"><span data-stu-id="179f1-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="179f1-128">Klik op Hallo taak en een nieuw venster geopend met Hallo volgende tabbladen:</span><span class="sxs-lookup"><span data-stu-id="179f1-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="179f1-129">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="179f1-129">Properties</span></span>  
2. <span data-ttu-id="179f1-130">Actie-instellingen</span><span class="sxs-lookup"><span data-stu-id="179f1-130">Action Settings</span></span>  
3. <span data-ttu-id="179f1-131">Planning</span><span class="sxs-lookup"><span data-stu-id="179f1-131">Schedule</span></span>  
4. <span data-ttu-id="179f1-132">Geschiedenis</span><span class="sxs-lookup"><span data-stu-id="179f1-132">History</span></span>
5. <span data-ttu-id="179f1-133">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="179f1-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="179f1-134">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="179f1-134">Properties</span></span>
<span data-ttu-id="179f1-135">Deze alleen-lezen eigenschappen beschrijven Hallo management metagegevens voor Hallo Scheduler-taak.</span><span class="sxs-lookup"><span data-stu-id="179f1-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="179f1-136">Actie-instellingen</span><span class="sxs-lookup"><span data-stu-id="179f1-136">Action settings</span></span>
<span data-ttu-id="179f1-137">Te klikken op een taak in Hallo **taken** scherm kunt u tooconfigure die taak.</span><span class="sxs-lookup"><span data-stu-id="179f1-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="179f1-138">Hiermee kunt u geavanceerde instellingen configureren, als deze niet is geconfigureerd in Hallo wizard Snelle invoer.</span><span class="sxs-lookup"><span data-stu-id="179f1-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="179f1-139">Voor alle actietypen kunt wijzigen u beleid voor opnieuw proberen Hallo en Hallo foutactie.</span><span class="sxs-lookup"><span data-stu-id="179f1-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="179f1-140">Voor HTTP en HTTPS taak actietypen kunt wijzigen u Hallo methode tooany HTTP-term wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="179f1-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="179f1-141">U kunt ook toevoegen, verwijderen of wijzigen Hallo koptekst en elementaire verificatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="179f1-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="179f1-142">Voor actietypen opslagwachtrij wijzigen u Hallo opslagaccount, wachtrijnaam, SAS-token en hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="179f1-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="179f1-143">Voor service bus-actietypen kunt wijzigen u Hallo naamruimte, onderwerp/wachtrijpad, verificatie-instellingen, transporttype, berichteigenschappen en hoofdtekst van het bericht.</span><span class="sxs-lookup"><span data-stu-id="179f1-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="179f1-144">Planning</span><span class="sxs-lookup"><span data-stu-id="179f1-144">Schedule</span></span>
<span data-ttu-id="179f1-145">Hiermee kunt u Hallo schema opnieuw configureren, indien gewenst toochange Hallo planning die u hebt gemaakt in Hallo wizard Snelle invoer.</span><span class="sxs-lookup"><span data-stu-id="179f1-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="179f1-146">Dit is een kans toobuild [complexe schema's en geavanceerde terugkeerpatroon in uw taak](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="179f1-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="179f1-147">Hallo begindatum kunnen worden gewijzigd en de tijd, terugkerende planning en Hallo datum en tijd (als Hallo job wordt herhaald.)</span><span class="sxs-lookup"><span data-stu-id="179f1-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="179f1-148">Geschiedenis</span><span class="sxs-lookup"><span data-stu-id="179f1-148">History</span></span>
<span data-ttu-id="179f1-149">Hallo **geschiedenis** tabblad geselecteerde metrische gegevens voor het uitvoeren van elke taak in Hallo-systeem voor de geselecteerde taak Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="179f1-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="179f1-150">Deze metrische gegevens bevatten met betrekking tot het Hallo-status van uw Scheduler realtime-waarden:</span><span class="sxs-lookup"><span data-stu-id="179f1-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="179f1-151">Status</span><span class="sxs-lookup"><span data-stu-id="179f1-151">Status</span></span>  
2. <span data-ttu-id="179f1-152">Details</span><span class="sxs-lookup"><span data-stu-id="179f1-152">Details</span></span>  
3. <span data-ttu-id="179f1-153">Nieuwe pogingen</span><span class="sxs-lookup"><span data-stu-id="179f1-153">Retry attempts</span></span>
4. <span data-ttu-id="179f1-154">Terugkeerpatroon: 1e, 2e, 3e enzovoorts.</span><span class="sxs-lookup"><span data-stu-id="179f1-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="179f1-155">Starttijd van de uitvoering</span><span class="sxs-lookup"><span data-stu-id="179f1-155">Start time of execution</span></span>  
6. <span data-ttu-id="179f1-156">Eindtijd van de uitvoering</span><span class="sxs-lookup"><span data-stu-id="179f1-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="179f1-157">U kunt klikken op een tooview uitvoeren de **Geschiedenisdetails**, inclusief Hallo volledige antwoord voor elke uitvoering.</span><span class="sxs-lookup"><span data-stu-id="179f1-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="179f1-158">Dit dialoogvenster kunt u ook toocopy Hallo antwoord toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="179f1-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="179f1-159">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="179f1-159">Users</span></span>
<span data-ttu-id="179f1-160">Met op rollen gebaseerd toegangsbeheer (RBAC) van Azure beschikt u over geavanceerd toegangsbeheer voor Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="179f1-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="179f1-161">hoe toouse Hallo tabblad gebruikers te verwijzen toolearn[rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="179f1-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="179f1-162">Zie ook</span><span class="sxs-lookup"><span data-stu-id="179f1-162">See also</span></span>
 [<span data-ttu-id="179f1-163">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="179f1-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="179f1-164">Scheduler-concepten en terminologie entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="179f1-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="179f1-165">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="179f1-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="179f1-166">Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="179f1-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="179f1-167">Naslaginformatie over de REST-API van Scheduler</span><span class="sxs-lookup"><span data-stu-id="179f1-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="179f1-168">Naslaginformatie over Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="179f1-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="179f1-169">Hoge beschikbaarheid en betrouwbaarheid Scheduler</span><span class="sxs-lookup"><span data-stu-id="179f1-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="179f1-170">Limieten, standaardwaarden en foutcodes van Scheduler</span><span class="sxs-lookup"><span data-stu-id="179f1-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="179f1-171">Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="179f1-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
