---
title: Achtergrondtaken uitvoeren met WebJobs
description: Informatie over het uitvoeren van achtergrondtaken in Azure-web-apps.
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
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="266b7-103">Achtergrondtaken uitvoeren met WebJobs</span><span class="sxs-lookup"><span data-stu-id="266b7-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="266b7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="266b7-104">Overview</span></span>
<span data-ttu-id="266b7-105">U kunt de programma's of scripts uitvoeren in WebJobs in uw [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web-app op drie manieren: op aanvraag continu, of volgens een schema.</span><span class="sxs-lookup"><span data-stu-id="266b7-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="266b7-106">Er is geen extra kosten WebJobs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="266b7-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="266b7-107">Dit artikel laat zien hoe u webtaken implementeren met behulp van de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="266b7-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="266b7-108">Zie voor meer informatie over het implementeren met behulp van Visual Studio of een doorlopende levering proces [hoe Azure WebJobs voor Web-Apps implementeren](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="266b7-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="266b7-109">De Azure WebJobs SDK vereenvoudigt veel WebJobs programmeertaken.</span><span class="sxs-lookup"><span data-stu-id="266b7-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="266b7-110">Zie voor meer informatie [wat de WebJobs SDK is](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="266b7-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="266b7-111">Azure Functions bevat een andere manier om uit te voeren programma's en scripts van een zonder server omgeving of van een App Service-app.</span><span class="sxs-lookup"><span data-stu-id="266b7-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="266b7-112">Zie voor meer informatie [overzicht van Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="266b7-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="266b7-113"><a name="acceptablefiles"></a>Acceptabele bestandstypen voor scripts of programma 's</span><span class="sxs-lookup"><span data-stu-id="266b7-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="266b7-114">De volgende bestandstypen worden geaccepteerd:</span><span class="sxs-lookup"><span data-stu-id="266b7-114">The following file types are accepted:</span></span>

* <span data-ttu-id="266b7-115">.cmd, .bat, .exe (met behulp van windows cmd)</span><span class="sxs-lookup"><span data-stu-id="266b7-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="266b7-116">.ps1 (met powershell)</span><span class="sxs-lookup"><span data-stu-id="266b7-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="266b7-117">.sh (met behulp van bash)</span><span class="sxs-lookup"><span data-stu-id="266b7-117">.sh (using bash)</span></span>
* <span data-ttu-id="266b7-118">.php (met behulp van php)</span><span class="sxs-lookup"><span data-stu-id="266b7-118">.php (using php)</span></span>
* <span data-ttu-id="266b7-119">.PY (met behulp van python)</span><span class="sxs-lookup"><span data-stu-id="266b7-119">.py (using python)</span></span>
* <span data-ttu-id="266b7-120">.js (met behulp van knooppunt)</span><span class="sxs-lookup"><span data-stu-id="266b7-120">.js (using node)</span></span>
* <span data-ttu-id="266b7-121">JAR (met java)</span><span class="sxs-lookup"><span data-stu-id="266b7-121">.jar (using java)</span></span>

## <span data-ttu-id="266b7-122"><a name="CreateOnDemand"></a>Maken van een on-demand webtaak in de portal</span><span class="sxs-lookup"><span data-stu-id="266b7-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="266b7-123">In de **Web-App** blade van de [Azure Portal](https://portal.azure.com), klikt u op **alle instellingen > WebJobs** om weer te geven de **WebJobs** blade.</span><span class="sxs-lookup"><span data-stu-id="266b7-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![Webtaak-blade](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="266b7-125">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="266b7-125">Click **Add**.</span></span> <span data-ttu-id="266b7-126">De **webtaak toevoegen** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="266b7-126">The **Add WebJob** dialog appears.</span></span>
   
    ![Webtaak blade toevoegen](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="266b7-128">Onder **naam**, Geef een naam voor de webtaak.</span><span class="sxs-lookup"><span data-stu-id="266b7-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="266b7-129">De naam moet beginnen met een letter of cijfer en andere dan mag geen speciale tekens bevatten '-' en '_'.</span><span class="sxs-lookup"><span data-stu-id="266b7-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="266b7-130">In de **How to Run** Kies **op aanvraag uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="266b7-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="266b7-131">In de **bestand laden** op het pictogram van de map en blader naar het zipbestand met het script.</span><span class="sxs-lookup"><span data-stu-id="266b7-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="266b7-132">Het zip-bestand moet het uitvoerbare bestand (.exe .cmd .bat .sh .php .py .js) en de ondersteunende bestanden die nodig zijn voor het uitvoeren van het programma of script bevatten.</span><span class="sxs-lookup"><span data-stu-id="266b7-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="266b7-133">Controleer **maken** voor het uploaden van het script naar uw web-app.</span><span class="sxs-lookup"><span data-stu-id="266b7-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="266b7-134">De door u opgegeven naam voor de webtaak wordt weergegeven in de lijst op de **WebJobs** blade.</span><span class="sxs-lookup"><span data-stu-id="266b7-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="266b7-135">De webtaak wordt uitgevoerd, met de rechtermuisknop op de naam ervan in de lijst en klikt u op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="266b7-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Webtaak wordt uitgevoerd](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="266b7-137"><a name="CreateContinuous"></a>Een continu actief webtaak maken</span><span class="sxs-lookup"><span data-stu-id="266b7-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="266b7-138">Volg dezelfde stappen voor het maken van een webtaak continu uitvoeren voor het maken van een webtaak die eenmaal wordt uitgevoerd, maar in de **How to Run** Kies **doorlopend**.</span><span class="sxs-lookup"><span data-stu-id="266b7-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="266b7-139">Als u wilt starten of stoppen van een doorlopende webtaak, met de rechtermuisknop op de webtaak in de lijst en klikt u op **Start** of **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="266b7-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="266b7-140">Als uw web-app wordt uitgevoerd op meer dan één exemplaar, wordt een continu actief webtaak wordt uitgevoerd op al uw exemplaren.</span><span class="sxs-lookup"><span data-stu-id="266b7-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="266b7-141">Op aanvraag en geplande webtaken uitvoeren op één instantie geselecteerd voor de load balancer door Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="266b7-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="266b7-142">Inschakelen voor doorlopende webtaken worden uitgevoerd op betrouwbare wijze en op alle instanties de altijd op * configuratie-instelling voor de web-app anders ze kunnen beëindigd wanneer de site van de host SCM te lang inactief is.</span><span class="sxs-lookup"><span data-stu-id="266b7-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="266b7-143"><a name="CreateScheduledCRON"></a>Een geplande webtaak met een CRON expressie maken</span><span class="sxs-lookup"><span data-stu-id="266b7-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="266b7-144">Deze techniek is beschikbaar voor Web-Apps die zijn uitgevoerd in de modus Basic, Standard of Premium en vereist dat de **altijd op** instelling zijn ingeschakeld op de app.</span><span class="sxs-lookup"><span data-stu-id="266b7-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="266b7-145">Als u wilt een webtaak van de aanvraag op in een geplande webtaak, eenvoudig omvatten een `settings.job` bestand in de hoofdmap van uw webtaak zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="266b7-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="266b7-146">Deze JSON-bestand bevatten een `schedule` eigenschap met een [CRON expressie](https://en.wikipedia.org/wiki/Cron), per in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="266b7-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="266b7-147">De CRON-expressie is samengesteld uit 6 velden: `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="266b7-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="266b7-148">Bijvoorbeeld, voor het activeren van uw webtaak elke 15 minuten, uw `settings.job` zou hebben:</span><span class="sxs-lookup"><span data-stu-id="266b7-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="266b7-149">Andere voorbeelden van CRON planning:</span><span class="sxs-lookup"><span data-stu-id="266b7-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="266b7-150">Elk uur (dat wil zeggen wanneer het aantal minuten 0 is):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="266b7-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="266b7-151">Elk uur uit 9: 00 uur tot 5 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="266b7-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="266b7-152">Om 9:30 AM dagelijks:`0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="266b7-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="266b7-153">Om 9:30 AM elke dag van de week:`0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="266b7-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="266b7-154">**Opmerking**: bij het implementeren van een webtaak vanuit Visual Studio, zorg ervoor dat u wilt markeren uw `settings.job` bestandseigenschappen als kopiëren indien nieuwer.</span><span class="sxs-lookup"><span data-stu-id="266b7-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="266b7-155"><a name="CreateScheduled"></a>Maken van een geplande webtaak met behulp van de Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="266b7-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="266b7-156">De volgende alternatieve methode wordt gebruikgemaakt van de Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="266b7-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="266b7-157">In dit geval heeft uw webtaak geen rechtstreekse kennis heeft van de planning.</span><span class="sxs-lookup"><span data-stu-id="266b7-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="266b7-158">De Azure Scheduler opgehaald in plaats daarvan geconfigureerd voor het activeren van uw webtaak volgens een schema.</span><span class="sxs-lookup"><span data-stu-id="266b7-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="266b7-159">De Azure Portal kunt maken van een geplande webtaak nog geen, maar totdat deze functie is toegevoegd. u kunt dit doen met behulp van de [klassieke portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="266b7-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="266b7-160">In de [klassieke portal](http://manage.windowsazure.com) Ga naar de webtaak pagina en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="266b7-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="266b7-161">In de **How to Run** Kies **volgens een schema uitgevoerd**.</span><span class="sxs-lookup"><span data-stu-id="266b7-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![Nieuwe geplande taak][NewScheduledJob]
3. <span data-ttu-id="266b7-163">Kies de **Scheduler regio** voor uw project en klik vervolgens op de pijl in de rechterbenedenhoek van het dialoogvenster om door te gaan naar het volgende scherm.</span><span class="sxs-lookup"><span data-stu-id="266b7-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="266b7-164">In de **taak maken** dialoogvenster, kies het type **terugkeerpatroon** gewenste: **eenmalige taak** of **terugkerende taak**.</span><span class="sxs-lookup"><span data-stu-id="266b7-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Terugkeerpatroon plannen][SchdRecurrence]
5. <span data-ttu-id="266b7-166">Ook voor kiezen een **starten** tijd: **nu** of **op een bepaald tijdstip**.</span><span class="sxs-lookup"><span data-stu-id="266b7-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Geplande begintijd][SchdStart]
6. <span data-ttu-id="266b7-168">Als u wilt starten op een bepaald tijdstip, kunt u uw eerste tijdwaarden onder **starten op**.</span><span class="sxs-lookup"><span data-stu-id="266b7-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Start op een bepaald tijdstip planning][SchdStartOn]
7. <span data-ttu-id="266b7-170">Als u een terugkerende taak hebt gekozen, hebt u de **herhalen elke** optie voor de frequentie van de instantie en de **eindigend op** optie voor het opgeven van een eindtijd.</span><span class="sxs-lookup"><span data-stu-id="266b7-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![Terugkeerpatroon plannen][SchdRecurEvery]
8. <span data-ttu-id="266b7-172">Als u ervoor kiest **weken**, kunt u de **op een bepaalde planning** en geef de dagen van de week waarop u wilt dat de taak wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="266b7-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![Dagen van de planning van de Week][SchdWeeksOnParticular]
9. <span data-ttu-id="266b7-174">Als u ervoor kiest **maanden** en selecteer de **op een bepaalde planning** vak kunt u de taak uit te voeren op bepaalde genummerde instellen **dagen** in de maand.</span><span class="sxs-lookup"><span data-stu-id="266b7-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![Plannen van bepaalde datums in de maand][SchdMonthsOnPartDays]
10. <span data-ttu-id="266b7-176">Als u ervoor kiest **weekdagen**, kunt u welke dag of dagen van de week selecteren in de maand die u wilt dat de taak uit te voeren op.</span><span class="sxs-lookup"><span data-stu-id="266b7-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![Bepaalde weekdagen in een maand plannen][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="266b7-178">Ten slotte ook kunt u de **voorvallen** kunt kiezen welke week van de maand (eerste, tweede, derde enz.) u wilt dat de taak uit te voeren op de weekdagen die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="266b7-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![Bepaalde weekdagen op bepaalde weken in een maand plannen][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="266b7-180">Nadat u een of meer taken hebt gemaakt, wordt hun namen worden weergegeven op het tabblad WebJobs met hun status, schematype en andere informatie.</span><span class="sxs-lookup"><span data-stu-id="266b7-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="266b7-181">Historische gegevens voor de laatste 30 WebJobs wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="266b7-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![Takenlijst met][WebJobsListWithSeveralJobs]

### <span data-ttu-id="266b7-183"><a name="Scheduler"></a>Geplande taken en Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="266b7-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="266b7-184">Geplande taken kunnen verder worden geconfigureerd in de Azure Scheduler-pagina's van de [klassieke portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="266b7-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="266b7-185">Klik op de taak op de pagina WebJobs **planning** koppeling om te navigeren naar de portal-pagina voor Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="266b7-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Koppeling naar Azure Scheduler][LinkToScheduler]
2. <span data-ttu-id="266b7-187">Klik op de taak op de pagina Scheduler.</span><span class="sxs-lookup"><span data-stu-id="266b7-187">On the Scheduler page, click the job.</span></span>
   
    ![Taak op de portal-Scheduler-pagina][SchedulerPortal]
3. <span data-ttu-id="266b7-189">De **taakactie** pagina wordt geopend, waarin u kunt de taak verder configureren.</span><span class="sxs-lookup"><span data-stu-id="266b7-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![Taakactie PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="266b7-191"><a name="ViewJobHistory"></a>De Taakgeschiedenis weergeven</span><span class="sxs-lookup"><span data-stu-id="266b7-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="266b7-192">Als u wilt weergeven van de geschiedenis van de uitvoering van een taak, met inbegrip van taken die zijn gemaakt met de WebJobs SDK, klikt u op de desbetreffende koppeling onder de **logboeken** kolom van de blade WebJobs.</span><span class="sxs-lookup"><span data-stu-id="266b7-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="266b7-193">(U kunt het pictogram van het Klembord de URL van de pagina log-bestand naar het Klembord kopiëren als u wilt.)</span><span class="sxs-lookup"><span data-stu-id="266b7-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![Logboeken koppelen](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="266b7-195">Op de koppeling klikt, wordt de detailpagina voor de webtaak geopend.</span><span class="sxs-lookup"><span data-stu-id="266b7-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="266b7-196">Deze pagina bevat de naam van de opdracht wordt uitgevoerd, de laatste keer die is uitgevoerd, en het slagen of mislukken.</span><span class="sxs-lookup"><span data-stu-id="266b7-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="266b7-197">Onder **recente taak wordt uitgevoerd**, klikt u op een tijdstip voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="266b7-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="266b7-199">De **Details uitvoering van webtaak** pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="266b7-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="266b7-200">Klik op **wisselknop uitvoer** om te zien van de tekst van de inhoud van het logboek.</span><span class="sxs-lookup"><span data-stu-id="266b7-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="266b7-201">Het uitvoerlogboek voor is tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="266b7-201">The output log is in text format.</span></span> 
   
    ![Web-job details uitvoering][WebJobRunDetails]
4. <span data-ttu-id="266b7-203">Klik op een overzicht van de uitvoertekst in een apart browservenster de **downloaden** koppeling.</span><span class="sxs-lookup"><span data-stu-id="266b7-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="266b7-204">Met de rechtermuisknop op de koppeling voor het downloaden van de tekst zelf, en opties van uw browser met inhoud van het bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="266b7-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![Logboekuitvoer downloaden][DownloadLogOutput]
5. <span data-ttu-id="266b7-206">De **WebJobs** koppeling aan de bovenkant van de pagina biedt een handige manier om een lijst met WebJobs op het dashboard van de geschiedenis.</span><span class="sxs-lookup"><span data-stu-id="266b7-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![Een koppeling naar de lijst WebJobs][WebJobsLinkToDashboardList]
   
    ![Lijst met WebJobs in geschiedenis dashboard][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="266b7-209">Op een van deze koppelingen te klikken gaat u naar de pagina webtaak Details voor de taak die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="266b7-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="266b7-210"><a name="WHPNotes"></a>Opmerkingen bij de</span><span class="sxs-lookup"><span data-stu-id="266b7-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="266b7-211">Web-apps in vrije modus kunnen een time-out na 20 minuten als er geen aanvragen voor de site scm (implementatie) en -portal voor de web-app niet is geopend in Azure.</span><span class="sxs-lookup"><span data-stu-id="266b7-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="266b7-212">Aanvragen voor de werkelijke site wordt niet opnieuw ingesteld dit.</span><span class="sxs-lookup"><span data-stu-id="266b7-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="266b7-213">Code voor een continue taak moet worden geschreven in een oneindige lus uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="266b7-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="266b7-214">Continue taken uitvoeren continu alleen als de web-app actief is.</span><span class="sxs-lookup"><span data-stu-id="266b7-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="266b7-215">Basic en Standard modi aanbieding de altijd op functies die, als deze is ingeschakeld, web-apps kunnen niet langer inactief.</span><span class="sxs-lookup"><span data-stu-id="266b7-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="266b7-216">U kunt alleen fouten opsporen doorlopend uitgevoerde WebJobs.</span><span class="sxs-lookup"><span data-stu-id="266b7-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="266b7-217">Geplande of op aanvraag WebJobs foutopsporing wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="266b7-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="266b7-218"><a name="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="266b7-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="266b7-219">Zie voor meer informatie [Azure WebJobs aanbevolen Resources][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="266b7-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

