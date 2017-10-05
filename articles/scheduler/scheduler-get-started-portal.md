---
title: Aan de slag met Azure Scheduler in Azure Portal | Microsoft Docs
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
ms.openlocfilehash: 3861ee121ed1c4d086ea81640e84d924d7d17ea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="b31da-103">Aan de slag met Azure Scheduler in Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b31da-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="b31da-104">Het is eenvoudig om geplande taken te maken in Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="b31da-104">It's easy to create scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="b31da-105">In deze zelfstudie leert u een taak te maken:</span><span class="sxs-lookup"><span data-stu-id="b31da-105">In this tutorial, you'll learn how to create a job.</span></span> <span data-ttu-id="b31da-106">U komt ook te weten hoe de controle- en beheerfuncties van Scheduler werken.</span><span class="sxs-lookup"><span data-stu-id="b31da-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="b31da-107">Een taak maken</span><span class="sxs-lookup"><span data-stu-id="b31da-107">Create a job</span></span>
1. <span data-ttu-id="b31da-108">Meld u aan bij de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b31da-108">Sign in to [Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="b31da-109">Klik op **+Nieuw** > typ *Scheduler* in het zoekvak > selecteer **Scheduler** in de resultaten > klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="b31da-109">Click **+New** > type *Scheduler* in the search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="b31da-110">We gaan een taak maken waarbij we eenvoudig http://www.microsoft.com/ bestoken met een GET-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b31da-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="b31da-111">In het scherm **Scheduler-taak** voert u de volgende gegevens in:</span><span class="sxs-lookup"><span data-stu-id="b31da-111">In the **Scheduler Job** screen, enter the following information:</span></span>
   
   1. <span data-ttu-id="b31da-112">**Naam:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="b31da-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="b31da-113">**Abonnement:** uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="b31da-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="b31da-114">**Taakverzameling:** selecteer een bestaande taakverzameling of klik op **Nieuw** > typ een naam.</span><span class="sxs-lookup"><span data-stu-id="b31da-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="b31da-115">Definieer vervolgens in **Actie-instellingen** de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="b31da-115">Next, in **Action Settings**, define the following values:</span></span>
   
   1. <span data-ttu-id="b31da-116">**Actietype:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="b31da-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="b31da-117">**Methode:** `GET`</span><span class="sxs-lookup"><span data-stu-id="b31da-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="b31da-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="b31da-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="b31da-119">Tot slot gaan we een planning definiëren.</span><span class="sxs-lookup"><span data-stu-id="b31da-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="b31da-120">De taak kan worden gedefinieerd als een eenmalige taak, maar we kiezen een schema voor een terugkerende taak:</span><span class="sxs-lookup"><span data-stu-id="b31da-120">The job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="b31da-121">**Terugkeerpatroon**:`Recurring`</span><span class="sxs-lookup"><span data-stu-id="b31da-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="b31da-122">**Start**: de datum van vandaag</span><span class="sxs-lookup"><span data-stu-id="b31da-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="b31da-123">**Herhaald elke**:`12 Hours`</span><span class="sxs-lookup"><span data-stu-id="b31da-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="b31da-124">**Beëindigen op**: twee dagen na de huidige datum</span><span class="sxs-lookup"><span data-stu-id="b31da-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="b31da-125">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="b31da-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="b31da-126">Taken beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="b31da-126">Manage and monitor jobs</span></span>
<span data-ttu-id="b31da-127">Zodra een taak is gemaakt, wordt deze weergegeven in het belangrijkste Azure-dashboard.</span><span class="sxs-lookup"><span data-stu-id="b31da-127">Once a job is created, it appears in the main Azure dashboard.</span></span> <span data-ttu-id="b31da-128">Klik op de taak, waarna een nieuw venster wordt geopend met de volgende tabbladen:</span><span class="sxs-lookup"><span data-stu-id="b31da-128">Click the job and a new window opens with the following tabs:</span></span>

1. <span data-ttu-id="b31da-129">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b31da-129">Properties</span></span>  
2. <span data-ttu-id="b31da-130">Actie-instellingen</span><span class="sxs-lookup"><span data-stu-id="b31da-130">Action Settings</span></span>  
3. <span data-ttu-id="b31da-131">Planning</span><span class="sxs-lookup"><span data-stu-id="b31da-131">Schedule</span></span>  
4. <span data-ttu-id="b31da-132">Geschiedenis</span><span class="sxs-lookup"><span data-stu-id="b31da-132">History</span></span>
5. <span data-ttu-id="b31da-133">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="b31da-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="b31da-134">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b31da-134">Properties</span></span>
<span data-ttu-id="b31da-135">Deze eigenschappen zijn alleen-lezen en beschrijven de beheermetagegevens voor de Scheduler-taak.</span><span class="sxs-lookup"><span data-stu-id="b31da-135">These read-only properties describe the management metadata for the Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="b31da-136">Actie-instellingen</span><span class="sxs-lookup"><span data-stu-id="b31da-136">Action settings</span></span>
<span data-ttu-id="b31da-137">Door op een taak in het scherm **Taken** te klikken, kunt u die taak configureren.</span><span class="sxs-lookup"><span data-stu-id="b31da-137">Clicking on a job in the **Jobs** screen allows you to configure that job.</span></span> <span data-ttu-id="b31da-138">Hiermee kunt u geavanceerde instellingen configureren, als u deze nog niet hebt geconfigureerd in de wizard Snelle invoer.</span><span class="sxs-lookup"><span data-stu-id="b31da-138">This lets you configure advanced settings, if you didn't configure them in the quick-create wizard.</span></span>

<span data-ttu-id="b31da-139">Voor alle actietypen kunt u het beleid voor opnieuw proberen en de foutactie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b31da-139">For all action types, you may change the retry policy and the error action.</span></span>

<span data-ttu-id="b31da-140">Voor de actietypen HTTP- en HTTPS-taak, kunt u de methode wijzigen in een toegestane HTTP-term.</span><span class="sxs-lookup"><span data-stu-id="b31da-140">For HTTP and HTTPS job action types, you may change the method to any allowed HTTP verb.</span></span> <span data-ttu-id="b31da-141">U kunt ook de koptekst en elementaire verificatiegegevens toevoegen, verwijderen of wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b31da-141">You may also add, delete, or change the headers and basic authentication information.</span></span>

<span data-ttu-id="b31da-142">Voor actietypen Opslagwachtrij kunt u het opslagaccount, de wachtrijnaam, de SAS-token en de hoofdtekst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b31da-142">For storage queue action types, you may change the storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="b31da-143">Voor Service Bus-actietypen kunt u de naamruimte, het onderwerp/wachtrijpad, de verificatie-instellingen, het transporttype, de berichtkenmerken en de hoofdtekst van het bericht wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b31da-143">For service bus action types, you may change the namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="b31da-144">Planning</span><span class="sxs-lookup"><span data-stu-id="b31da-144">Schedule</span></span>
<span data-ttu-id="b31da-145">Hiermee kunt u het schema opnieuw configureren als u de planning wilt wijzigen die u hebt gemaakt in de wizard Snelle invoer.</span><span class="sxs-lookup"><span data-stu-id="b31da-145">This lets you reconfigure the schedule, if you'd like to change the schedule you created in the quick-create wizard.</span></span>

<span data-ttu-id="b31da-146">Dit is een kans om [complexe schema's en een geavanceerd terugkeerpatroon in uw taak in te bouwen](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="b31da-146">This is an opportunity to build [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="b31da-147">U kunt de startdatum en -tijd wijzigen evenals de einddatum en -tijd (als het om een terugkerende taak gaat.)</span><span class="sxs-lookup"><span data-stu-id="b31da-147">You may change the start date and time, recurrence schedule, and the end date and time (if the job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="b31da-148">Geschiedenis</span><span class="sxs-lookup"><span data-stu-id="b31da-148">History</span></span>
<span data-ttu-id="b31da-149">Op het tabblad **Geschiedenis** worden geselecteerde metrische gegevens weergegeven voor elke keer dat er in het systeem voor de geselecteerde taak een taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b31da-149">The **History** tab displays selected metrics for every job execution in the system for the selected job.</span></span> <span data-ttu-id="b31da-150">Deze metrische gegevens bestaan uit realtime-waarden die betrekking hebben op de status van uw exemplaar van Scheduler:</span><span class="sxs-lookup"><span data-stu-id="b31da-150">These metrics provide real-time values regarding the health of your Scheduler:</span></span>

1. <span data-ttu-id="b31da-151">Status</span><span class="sxs-lookup"><span data-stu-id="b31da-151">Status</span></span>  
2. <span data-ttu-id="b31da-152">Details</span><span class="sxs-lookup"><span data-stu-id="b31da-152">Details</span></span>  
3. <span data-ttu-id="b31da-153">Nieuwe pogingen</span><span class="sxs-lookup"><span data-stu-id="b31da-153">Retry attempts</span></span>
4. <span data-ttu-id="b31da-154">Terugkeerpatroon: 1e, 2e, 3e enzovoorts.</span><span class="sxs-lookup"><span data-stu-id="b31da-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="b31da-155">Starttijd van de uitvoering</span><span class="sxs-lookup"><span data-stu-id="b31da-155">Start time of execution</span></span>  
6. <span data-ttu-id="b31da-156">Eindtijd van de uitvoering</span><span class="sxs-lookup"><span data-stu-id="b31da-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="b31da-157">U kunt op een uitvoering klikken om de **Geschiedenisdetails** ervan weer te geven, zoals onder andere het volledige antwoord voor elke uitvoering.</span><span class="sxs-lookup"><span data-stu-id="b31da-157">You can click on a run to view its **History Details**, including the whole response for every execution.</span></span> <span data-ttu-id="b31da-158">Vanuit dit dialoogvenster kunt u ook het antwoord naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b31da-158">This dialog box also allows you to copy the response to the clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="b31da-159">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="b31da-159">Users</span></span>
<span data-ttu-id="b31da-160">Met op rollen gebaseerd toegangsbeheer (RBAC) van Azure beschikt u over geavanceerd toegangsbeheer voor Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="b31da-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="b31da-161">Voor meer informatie over het tabblad Gebruikers, zie [Op rollen gebaseerd toegangsbeheer in Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="b31da-161">To learn how to use the Users tab, refer to [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="b31da-162">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b31da-162">See also</span></span>
 [<span data-ttu-id="b31da-163">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="b31da-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="b31da-164">Scheduler-concepten en terminologie entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="b31da-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="b31da-165">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b31da-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="b31da-166">Complexe schema's en geavanceerde terugkeerpatronen bouwen met Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b31da-166">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="b31da-167">Naslaginformatie over de REST-API van Scheduler</span><span class="sxs-lookup"><span data-stu-id="b31da-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="b31da-168">Naslaginformatie over Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="b31da-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="b31da-169">Hoge beschikbaarheid en betrouwbaarheid Scheduler</span><span class="sxs-lookup"><span data-stu-id="b31da-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="b31da-170">Limieten, standaardwaarden en foutcodes van Scheduler</span><span class="sxs-lookup"><span data-stu-id="b31da-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="b31da-171">Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="b31da-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

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
