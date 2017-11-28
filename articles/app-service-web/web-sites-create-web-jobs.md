---
title: achtergrondtaken aaaRun met WebJobs
description: Meer informatie over hoe toorun achtergrondtaken in Azure web-apps.
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="7d06c-103">Achtergrondtaken uitvoeren met WebJobs</span><span class="sxs-lookup"><span data-stu-id="7d06c-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="7d06c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7d06c-104">Overview</span></span>
<span data-ttu-id="7d06c-105">U kunt de programma's of scripts uitvoeren in WebJobs in uw [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web-app op drie manieren: op aanvraag continu, of volgens een schema.</span><span class="sxs-lookup"><span data-stu-id="7d06c-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="7d06c-106">Er is geen extra kosten toouse WebJobs.</span><span class="sxs-lookup"><span data-stu-id="7d06c-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="7d06c-107">Dit artikel laat zien hoe toodeploy WebJobs met behulp van Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d06c-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="7d06c-108">Voor informatie over het toodeploy met behulp van Visual Studio of een doorlopende levering proces, Zie [hoe tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="7d06c-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="7d06c-109">Hello Azure WebJobs SDK vereenvoudigt veel WebJobs programmeertaken.</span><span class="sxs-lookup"><span data-stu-id="7d06c-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="7d06c-110">Zie voor meer informatie [wat Hallo WebJobs SDK is](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7d06c-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="7d06c-111">Azure Functions bevat een andere manier toorun programma's en scripts van een zonder server omgeving of van een App Service-app.</span><span class="sxs-lookup"><span data-stu-id="7d06c-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="7d06c-112">Zie voor meer informatie [overzicht van Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d06c-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="7d06c-113"><a name="acceptablefiles"></a>Acceptabele bestandstypen voor scripts of programma 's</span><span class="sxs-lookup"><span data-stu-id="7d06c-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="7d06c-114">Hallo volgende bestandstypen worden geaccepteerd:</span><span class="sxs-lookup"><span data-stu-id="7d06c-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="7d06c-115">.cmd, .bat, .exe (met behulp van windows cmd)</span><span class="sxs-lookup"><span data-stu-id="7d06c-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="7d06c-116">.ps1 (met powershell)</span><span class="sxs-lookup"><span data-stu-id="7d06c-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="7d06c-117">.sh (met behulp van bash)</span><span class="sxs-lookup"><span data-stu-id="7d06c-117">.sh (using bash)</span></span>
* <span data-ttu-id="7d06c-118">.php (met behulp van php)</span><span class="sxs-lookup"><span data-stu-id="7d06c-118">.php (using php)</span></span>
* <span data-ttu-id="7d06c-119">.PY (met behulp van python)</span><span class="sxs-lookup"><span data-stu-id="7d06c-119">.py (using python)</span></span>
* <span data-ttu-id="7d06c-120">.js (met behulp van knooppunt)</span><span class="sxs-lookup"><span data-stu-id="7d06c-120">.js (using node)</span></span>
* <span data-ttu-id="7d06c-121">JAR (met java)</span><span class="sxs-lookup"><span data-stu-id="7d06c-121">.jar (using java)</span></span>

## <span data-ttu-id="7d06c-122"><a name="CreateOnDemand"></a>Maken van een on-demand webtaak in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="7d06c-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="7d06c-123">In Hallo **Web-App** blade Hallo [Azure Portal](https://portal.azure.com), klikt u op **alle instellingen > WebJobs** tooshow hello **WebJobs** blade.</span><span class="sxs-lookup"><span data-stu-id="7d06c-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Webtaak-blade](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="7d06c-125">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-125">Click **Add**.</span></span> <span data-ttu-id="7d06c-126">Hallo **webtaak toevoegen** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7d06c-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Webtaak blade toevoegen](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="7d06c-128">Onder **naam**, Geef een naam op voor Hallo webtaak.</span><span class="sxs-lookup"><span data-stu-id="7d06c-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="7d06c-129">Hallo-naam moet beginnen met een letter of cijfer en mag geen speciale tekens dan bevatten '-' en '_'.</span><span class="sxs-lookup"><span data-stu-id="7d06c-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="7d06c-130">In Hallo **hoe tooRun** Kies **op aanvraag uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="7d06c-131">In Hallo **bestand laden** vak en klik op het pictogram map Hallo toohello zip-bestand met het script te bladeren.</span><span class="sxs-lookup"><span data-stu-id="7d06c-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="7d06c-132">Hallo zip-bestand moet het uitvoerbare bestand (.exe .cmd .bat .sh .php .py .js) bevatten en de ondersteunende bestanden nodig toorun Hallo programma of script.</span><span class="sxs-lookup"><span data-stu-id="7d06c-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="7d06c-133">Controleer **maken** tooupload Hallo script tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="7d06c-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="7d06c-134">Hallo naam die u hebt opgegeven voor Hallo webtaak wordt weergegeven in de lijst Hallo op Hallo **WebJobs** blade.</span><span class="sxs-lookup"><span data-stu-id="7d06c-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="7d06c-135">toorun hello webtaak, met de rechtermuisknop op de naam ervan in Hallo lijst en klik op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Webtaak wordt uitgevoerd](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="7d06c-137"><a name="CreateContinuous"></a>Een continu actief webtaak maken</span><span class="sxs-lookup"><span data-stu-id="7d06c-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="7d06c-138">een continu uitgevoerd webtaak toocreate Volg dezelfde stappen voor het maken van een webtaak die eenmaal wordt uitgevoerd, maar in Hallo Hallo **hoe tooRun** Kies **doorlopend**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="7d06c-139">toostart of een doorlopende webtaak stoppen met de rechtermuisknop op Hallo webtaak in Hallo lijst en klik op **Start** of **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="7d06c-140">Als uw web-app wordt uitgevoerd op meer dan één exemplaar, wordt een continu actief webtaak wordt uitgevoerd op al uw exemplaren.</span><span class="sxs-lookup"><span data-stu-id="7d06c-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="7d06c-141">Op aanvraag en geplande webtaken uitvoeren op één instantie geselecteerd voor de load balancer door Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7d06c-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="7d06c-142">Voor doorlopende webtaken toorun betrouwbaar en op alle instanties inschakelen Hallo altijd op * configuratie-instelling voor Hallo web-app anders ze kunnen beëindigd wanneer Hallo SCM hostsite niet actief is te lang is.</span><span class="sxs-lookup"><span data-stu-id="7d06c-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="7d06c-143"><a name="CreateScheduledCRON"></a>Een geplande webtaak met een CRON expressie maken</span><span class="sxs-lookup"><span data-stu-id="7d06c-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="7d06c-144">Deze techniek is beschikbaar tooWeb Apps die worden uitgevoerd in de modus Basic, Standard of Premium en Hallo vereist **altijd op** toobe ingeschakeld op Hallo app instellen.</span><span class="sxs-lookup"><span data-stu-id="7d06c-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="7d06c-145">tooturn een webtaak van aanvraag op in een geplande webtaak eenvoudig omvatten een `settings.job` bestand in de hoofdmap Hallo van uw webtaak zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="7d06c-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="7d06c-146">Deze JSON-bestand bevatten een `schedule` eigenschap met een [CRON expressie](https://en.wikipedia.org/wiki/Cron), per in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7d06c-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="7d06c-147">Hallo CRON expressie bestaat uit 6 velden: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="7d06c-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="7d06c-148">Bijvoorbeeld: tootrigger uw webtaak elke 15 minuten, uw `settings.job` zou hebben:</span><span class="sxs-lookup"><span data-stu-id="7d06c-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="7d06c-149">Andere voorbeelden van CRON planning:</span><span class="sxs-lookup"><span data-stu-id="7d06c-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="7d06c-150">Elk uur (dat wil zeggen wanneer het aantal minuten Hallo 0 is):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="7d06c-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="7d06c-151">Elk uur vanaf too5 09: 00 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="7d06c-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="7d06c-152">Om 9:30 AM dagelijks:`0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="7d06c-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="7d06c-153">Om 9:30 AM elke dag van de week:`0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="7d06c-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="7d06c-154">**Opmerking**: bij het implementeren van een webtaak vanuit Visual Studio, zorg ervoor dat toomark uw `settings.job` bestandseigenschappen als kopiëren indien nieuwer.</span><span class="sxs-lookup"><span data-stu-id="7d06c-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="7d06c-155"><a name="CreateScheduled"></a>Maken van een geplande webtaak met hello Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="7d06c-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="7d06c-156">Hallo na alternatieve methode gebruik maakt van hello Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="7d06c-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="7d06c-157">In dit geval heeft uw webtaak geen rechtstreekse kennis van het Hallo-schema.</span><span class="sxs-lookup"><span data-stu-id="7d06c-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="7d06c-158">In plaats daarvan hello Azure Scheduler opgehaald geconfigureerde tootrigger uw webtaak volgens een schema.</span><span class="sxs-lookup"><span data-stu-id="7d06c-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="7d06c-159">Hello Azure Portal nog geen Hallo mogelijkheid toocreate een geplande webtaak, maar totdat deze functie is toegevoegd. u kunt dit doen met behulp van Hallo [klassieke portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7d06c-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="7d06c-160">In Hallo [klassieke portal](http://manage.windowsazure.com) toohello webtaak pagina gaan en op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="7d06c-161">In Hallo **hoe tooRun** Kies **volgens een schema uitgevoerd**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Nieuwe geplande taak][NewScheduledJob]
3. <span data-ttu-id="7d06c-163">Kies Hallo **Scheduler regio** voor uw project en klik vervolgens op Hallo pijl in de rechterbenedenhoek Hallo van dialoogvenster tooproceed toohello volgende welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="7d06c-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="7d06c-164">In Hallo **taak maken** dialoogvenster Kies Hallo type **terugkeerpatroon** gewenste: **eenmalige taak** of **terugkerende taak**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Terugkeerpatroon plannen][SchdRecurrence]
5. <span data-ttu-id="7d06c-166">Ook voor kiezen een **starten** tijd: **nu** of **op een bepaald tijdstip**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Geplande begintijd][SchdStart]
6. <span data-ttu-id="7d06c-168">Als u toostart op een bepaald tijdstip wilt, kunt u uw eerste tijdwaarden onder **starten op**.</span><span class="sxs-lookup"><span data-stu-id="7d06c-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Start op een bepaald tijdstip planning][SchdStartOn]
7. <span data-ttu-id="7d06c-170">Als u een terugkerende taak hebt gekozen, hebt u Hallo **herhalen elke** toospecify Hallo frequentie van het exemplaar en Hallo optie **eindigend op** optie toospecify een eindtijd.</span><span class="sxs-lookup"><span data-stu-id="7d06c-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Terugkeerpatroon plannen][SchdRecurEvery]
8. <span data-ttu-id="7d06c-172">Als u ervoor kiest **weken**, kunt u Hallo **op een bepaalde planning** en op te geven Hallo dagen van week Hallo die u wilt dat de taak toorun Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d06c-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Dagen van de planning van Hallo Week][SchdWeeksOnParticular]
9. <span data-ttu-id="7d06c-174">Als u ervoor kiest **maanden** en selecteer Hallo **op een bepaalde planning** vak kunt u Hallo taak toorun instellen op bepaalde genummerde **dagen** in Hallo maand.</span><span class="sxs-lookup"><span data-stu-id="7d06c-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Bepaalde datums in Hallo maand plannen][SchdMonthsOnPartDays]
10. <span data-ttu-id="7d06c-176">Als u ervoor kiest **weekdagen**, kunt u welke dag of dagen van week Hallo selecteren in de gewenste taak toorun op Hallo van Hallo-maand.</span><span class="sxs-lookup"><span data-stu-id="7d06c-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Bepaalde weekdagen in een maand plannen][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="7d06c-178">Ten slotte kunt u ook hello gebruiken **voorvallen** optie toochoose welke week van maand Hallo (eerste, tweede, derde enz.) u wilt dat Hallo taak toorun op Hallo weekdagen die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7d06c-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Bepaalde weekdagen op bepaalde weken in een maand plannen][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="7d06c-180">Nadat u een of meer taken hebt gemaakt, wordt hun namen op Hallo webtaken tabblad met hun status, schematype en andere informatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7d06c-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="7d06c-181">Historische gegevens wordt voor Hallo laatste 30 WebJobs bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="7d06c-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![Takenlijst met][WebJobsListWithSeveralJobs]

### <span data-ttu-id="7d06c-183"><a name="Scheduler"></a>Geplande taken en Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="7d06c-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="7d06c-184">Geplande taken kunnen verder worden geconfigureerd in hello Azure Scheduler-pagina's van Hallo [klassieke portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7d06c-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="7d06c-185">Op de pagina WebJobs Hallo op Hallo-taak **planning** koppeling toonavigate toohello Azure Scheduler portalpagina.</span><span class="sxs-lookup"><span data-stu-id="7d06c-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Koppeling tooAzure Scheduler][LinkToScheduler]
2. <span data-ttu-id="7d06c-187">Klik op de pagina Hallo Scheduler op Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="7d06c-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Taak op Hallo Scheduler portal-pagina][SchedulerPortal]
3. <span data-ttu-id="7d06c-189">Hallo **taakactie** pagina wordt geopend, waar u meer Hallo taak kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="7d06c-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![Taakactie PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="7d06c-191"><a name="ViewJobHistory"></a>Hallo-Taakgeschiedenis weergeven</span><span class="sxs-lookup"><span data-stu-id="7d06c-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="7d06c-192">tooview hello uitvoering geschiedenis van een taak, met inbegrip van taken die zijn gemaakt met de Hallo WebJobs SDK, klikt u op de desbetreffende koppeling onder Hallo **logboeken** kolom van Hallo WebJobs-blade.</span><span class="sxs-lookup"><span data-stu-id="7d06c-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="7d06c-193">(U kunt Hallo Klembord pictogram toocopy Hallo-URL van Hallo log-bestand pagina toohello Klembord gebruiken als u wenst.)</span><span class="sxs-lookup"><span data-stu-id="7d06c-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Logboeken koppelen](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="7d06c-195">Te klikken op Hallo koppeling opent u de detailpagina Hallo voor Hallo webtaak.</span><span class="sxs-lookup"><span data-stu-id="7d06c-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="7d06c-196">Deze pagina ziet u de naam van het Hallo-opdracht wordt uitgevoerd, Hallo Hallo laatste keer is uitgevoerd, en het slagen of mislukken.</span><span class="sxs-lookup"><span data-stu-id="7d06c-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="7d06c-197">Onder **recente taak wordt uitgevoerd**, klikt u op een tijd toosee verdere details.</span><span class="sxs-lookup"><span data-stu-id="7d06c-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="7d06c-199">Hallo **Details uitvoering van webtaak** pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7d06c-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="7d06c-200">Klik op **wisselknop uitvoer** toosee Hallo tekst hello logboek inhoud.</span><span class="sxs-lookup"><span data-stu-id="7d06c-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="7d06c-201">Hallo logboek is tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="7d06c-201">hello output log is in text format.</span></span> 
   
    ![Web-job details uitvoering][WebJobRunDetails]
4. <span data-ttu-id="7d06c-203">toosee hello uitvoertekst in een apart browservenster, klikt u op Hallo **downloaden** koppeling.</span><span class="sxs-lookup"><span data-stu-id="7d06c-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="7d06c-204">toodownload hello tekst zelf, met de rechtermuisknop op de koppeling Hallo en uw browser opties toosave Hallo bestandsinhoud gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7d06c-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Logboekuitvoer downloaden][DownloadLogOutput]
5. <span data-ttu-id="7d06c-206">Hallo **WebJobs** koppeling bovenaan Hallo Hallo pagina biedt een handige manier tooget tooa lijst van WebJobs op Hallo geschiedenis dashboard.</span><span class="sxs-lookup"><span data-stu-id="7d06c-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Lijst van de tooWebJobs koppelen][WebJobsLinkToDashboardList]
   
    ![Lijst met WebJobs in geschiedenis dashboard][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="7d06c-209">Op een van deze koppelingen te klikken, gaat u toohello webtaak detailpagina voor het Hallo-taak die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7d06c-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="7d06c-210"><a name="WHPNotes"></a>Opmerkingen bij de</span><span class="sxs-lookup"><span data-stu-id="7d06c-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="7d06c-211">Web-apps in vrije modus kunnen een time-out na 20 minuten als er geen site aanvragen toohello scm (implementatie) en de portal Hallo van web-app niet geopend in Azure is.</span><span class="sxs-lookup"><span data-stu-id="7d06c-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="7d06c-212">Aanvragen toohello Werkelijke site wordt niet opnieuw ingesteld dit.</span><span class="sxs-lookup"><span data-stu-id="7d06c-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="7d06c-213">Code voor een continue job moet toobe toorun geschreven in een oneindige lus.</span><span class="sxs-lookup"><span data-stu-id="7d06c-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="7d06c-214">Continue taken uitvoeren continu alleen als Hallo web-app actief is.</span><span class="sxs-lookup"><span data-stu-id="7d06c-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="7d06c-215">Basic en Standard modi aanbieding Hallo altijd op functie die, als deze is ingeschakeld, web-apps kunnen niet langer inactief.</span><span class="sxs-lookup"><span data-stu-id="7d06c-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="7d06c-216">U kunt alleen fouten opsporen doorlopend uitgevoerde WebJobs.</span><span class="sxs-lookup"><span data-stu-id="7d06c-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="7d06c-217">Geplande of op aanvraag WebJobs foutopsporing wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7d06c-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="7d06c-218"><a name="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d06c-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="7d06c-219">Zie voor meer informatie [Azure WebJobs aanbevolen Resources][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="7d06c-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

