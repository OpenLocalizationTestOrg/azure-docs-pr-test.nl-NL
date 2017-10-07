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
# <a name="run-background-tasks-with-webjobs"></a>Achtergrondtaken uitvoeren met WebJobs
## <a name="overview"></a>Overzicht
U kunt de programma's of scripts uitvoeren in WebJobs in uw [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web-app op drie manieren: op aanvraag continu, of volgens een schema. Er is geen extra kosten toouse WebJobs.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Dit artikel laat zien hoe toodeploy WebJobs met behulp van Hallo [Azure Portal](https://portal.azure.com). Voor informatie over het toodeploy met behulp van Visual Studio of een doorlopende levering proces, Zie [hoe tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).

Hello Azure WebJobs SDK vereenvoudigt veel WebJobs programmeertaken. Zie voor meer informatie [wat Hallo WebJobs SDK is](websites-dotnet-webjobs-sdk.md).

 Azure Functions bevat een andere manier toorun programma's en scripts van een zonder server omgeving of van een App Service-app. Zie voor meer informatie [overzicht van Azure Functions](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Acceptabele bestandstypen voor scripts of programma 's
Hallo volgende bestandstypen worden geaccepteerd:

* .cmd, .bat, .exe (met behulp van windows cmd)
* .ps1 (met powershell)
* .sh (met behulp van bash)
* .php (met behulp van php)
* .PY (met behulp van python)
* .js (met behulp van knooppunt)
* JAR (met java)

## <a name="CreateOnDemand"></a>Maken van een on-demand webtaak in Hallo-portal
1. In Hallo **Web-App** blade Hallo [Azure Portal](https://portal.azure.com), klikt u op **alle instellingen > WebJobs** tooshow hello **WebJobs** blade.
   
    ![Webtaak-blade](./media/web-sites-create-web-jobs/wjblade.png)
2. Klik op **Add**. Hallo **webtaak toevoegen** dialoogvenster wordt weergegeven.
   
    ![Webtaak blade toevoegen](./media/web-sites-create-web-jobs/addwjblade.png)
3. Onder **naam**, Geef een naam op voor Hallo webtaak. Hallo-naam moet beginnen met een letter of cijfer en mag geen speciale tekens dan bevatten '-' en '_'.
4. In Hallo **hoe tooRun** Kies **op aanvraag uitvoeren**.
5. In Hallo **bestand laden** vak en klik op het pictogram map Hallo toohello zip-bestand met het script te bladeren. Hallo zip-bestand moet het uitvoerbare bestand (.exe .cmd .bat .sh .php .py .js) bevatten en de ondersteunende bestanden nodig toorun Hallo programma of script.
6. Controleer **maken** tooupload Hallo script tooyour web-app. 
   
    Hallo naam die u hebt opgegeven voor Hallo webtaak wordt weergegeven in de lijst Hallo op Hallo **WebJobs** blade.
7. toorun hello webtaak, met de rechtermuisknop op de naam ervan in Hallo lijst en klik op **uitvoeren**.
   
    ![Webtaak wordt uitgevoerd](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Een continu actief webtaak maken
1. een continu uitgevoerd webtaak toocreate Volg dezelfde stappen voor het maken van een webtaak die eenmaal wordt uitgevoerd, maar in Hallo Hallo **hoe tooRun** Kies **doorlopend**.
2. toostart of een doorlopende webtaak stoppen met de rechtermuisknop op Hallo webtaak in Hallo lijst en klik op **Start** of **stoppen**.

> [!NOTE]
> Als uw web-app wordt uitgevoerd op meer dan één exemplaar, wordt een continu actief webtaak wordt uitgevoerd op al uw exemplaren. Op aanvraag en geplande webtaken uitvoeren op één instantie geselecteerd voor de load balancer door Microsoft Azure.
> 
> Voor doorlopende webtaken toorun betrouwbaar en op alle instanties inschakelen Hallo altijd op * configuratie-instelling voor Hallo web-app anders ze kunnen beëindigd wanneer Hallo SCM hostsite niet actief is te lang is.
> 
> 

## <a name="CreateScheduledCRON"></a>Een geplande webtaak met een CRON expressie maken
Deze techniek is beschikbaar tooWeb Apps die worden uitgevoerd in de modus Basic, Standard of Premium en Hallo vereist **altijd op** toobe ingeschakeld op Hallo app instellen.

tooturn een webtaak van aanvraag op in een geplande webtaak eenvoudig omvatten een `settings.job` bestand in de hoofdmap Hallo van uw webtaak zip-bestand. Deze JSON-bestand bevatten een `schedule` eigenschap met een [CRON expressie](https://en.wikipedia.org/wiki/Cron), per in het volgende voorbeeld.

Hallo CRON expressie bestaat uit 6 velden: `{second} {minute} {hour} {day} {month} {day of hello week}`.

Bijvoorbeeld: tootrigger uw webtaak elke 15 minuten, uw `settings.job` zou hebben:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Andere voorbeelden van CRON planning:

* Elk uur (dat wil zeggen wanneer het aantal minuten Hallo 0 is):`0 0 * * * *` 
* Elk uur vanaf too5 09: 00 PM:`0 0 9-17 * * *` 
* Om 9:30 AM dagelijks:`0 30 9 * * *`
* Om 9:30 AM elke dag van de week:`0 30 9 * * 1-5`

**Opmerking**: bij het implementeren van een webtaak vanuit Visual Studio, zorg ervoor dat toomark uw `settings.job` bestandseigenschappen als kopiëren indien nieuwer.

## <a name="CreateScheduled"></a>Maken van een geplande webtaak met hello Azure Scheduler
Hallo na alternatieve methode gebruik maakt van hello Azure Scheduler. In dit geval heeft uw webtaak geen rechtstreekse kennis van het Hallo-schema. In plaats daarvan hello Azure Scheduler opgehaald geconfigureerde tootrigger uw webtaak volgens een schema. 

Hello Azure Portal nog geen Hallo mogelijkheid toocreate een geplande webtaak, maar totdat deze functie is toegevoegd. u kunt dit doen met behulp van Hallo [klassieke portal](http://manage.windowsazure.com).

1. In Hallo [klassieke portal](http://manage.windowsazure.com) toohello webtaak pagina gaan en op **toevoegen**.
2. In Hallo **hoe tooRun** Kies **volgens een schema uitgevoerd**.
   
    ![Nieuwe geplande taak][NewScheduledJob]
3. Kies Hallo **Scheduler regio** voor uw project en klik vervolgens op Hallo pijl in de rechterbenedenhoek Hallo van dialoogvenster tooproceed toohello volgende welkomstscherm.
4. In Hallo **taak maken** dialoogvenster Kies Hallo type **terugkeerpatroon** gewenste: **eenmalige taak** of **terugkerende taak**.
   
    ![Terugkeerpatroon plannen][SchdRecurrence]
5. Ook voor kiezen een **starten** tijd: **nu** of **op een bepaald tijdstip**.
   
    ![Geplande begintijd][SchdStart]
6. Als u toostart op een bepaald tijdstip wilt, kunt u uw eerste tijdwaarden onder **starten op**.
   
    ![Start op een bepaald tijdstip planning][SchdStartOn]
7. Als u een terugkerende taak hebt gekozen, hebt u Hallo **herhalen elke** toospecify Hallo frequentie van het exemplaar en Hallo optie **eindigend op** optie toospecify een eindtijd.
   
    ![Terugkeerpatroon plannen][SchdRecurEvery]
8. Als u ervoor kiest **weken**, kunt u Hallo **op een bepaalde planning** en op te geven Hallo dagen van week Hallo die u wilt dat de taak toorun Hallo.
   
    ![Dagen van de planning van Hallo Week][SchdWeeksOnParticular]
9. Als u ervoor kiest **maanden** en selecteer Hallo **op een bepaalde planning** vak kunt u Hallo taak toorun instellen op bepaalde genummerde **dagen** in Hallo maand. 
   
    ![Bepaalde datums in Hallo maand plannen][SchdMonthsOnPartDays]
10. Als u ervoor kiest **weekdagen**, kunt u welke dag of dagen van week Hallo selecteren in de gewenste taak toorun op Hallo van Hallo-maand.
    
     ![Bepaalde weekdagen in een maand plannen][SchdMonthsOnPartWeekDays]
11. Ten slotte kunt u ook hello gebruiken **voorvallen** optie toochoose welke week van maand Hallo (eerste, tweede, derde enz.) u wilt dat Hallo taak toorun op Hallo weekdagen die u hebt opgegeven.
    
    ![Bepaalde weekdagen op bepaalde weken in een maand plannen][SchdMonthsOnPartWeekDaysOccurences]
12. Nadat u een of meer taken hebt gemaakt, wordt hun namen op Hallo webtaken tabblad met hun status, schematype en andere informatie weergegeven. Historische gegevens wordt voor Hallo laatste 30 WebJobs bijgehouden.
    
    ![Takenlijst met][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Geplande taken en Azure Scheduler
Geplande taken kunnen verder worden geconfigureerd in hello Azure Scheduler-pagina's van Hallo [klassieke portal](http://manage.windowsazure.com).

1. Op de pagina WebJobs Hallo op Hallo-taak **planning** koppeling toonavigate toohello Azure Scheduler portalpagina. 
   
   ![Koppeling tooAzure Scheduler][LinkToScheduler]
2. Klik op de pagina Hallo Scheduler op Hallo-taak.
   
    ![Taak op Hallo Scheduler portal-pagina][SchedulerPortal]
3. Hallo **taakactie** pagina wordt geopend, waar u meer Hallo taak kunt configureren. 
   
    ![Taakactie PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Hallo-Taakgeschiedenis weergeven
1. tooview hello uitvoering geschiedenis van een taak, met inbegrip van taken die zijn gemaakt met de Hallo WebJobs SDK, klikt u op de desbetreffende koppeling onder Hallo **logboeken** kolom van Hallo WebJobs-blade. (U kunt Hallo Klembord pictogram toocopy Hallo-URL van Hallo log-bestand pagina toohello Klembord gebruiken als u wenst.)
   
    ![Logboeken koppelen](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Te klikken op Hallo koppeling opent u de detailpagina Hallo voor Hallo webtaak. Deze pagina ziet u de naam van het Hallo-opdracht wordt uitgevoerd, Hallo Hallo laatste keer is uitgevoerd, en het slagen of mislukken. Onder **recente taak wordt uitgevoerd**, klikt u op een tijd toosee verdere details.
   
    ![WebJobDetails][WebJobDetails]
3. Hallo **Details uitvoering van webtaak** pagina wordt weergegeven. Klik op **wisselknop uitvoer** toosee Hallo tekst hello logboek inhoud. Hallo logboek is tekst zonder opmaak. 
   
    ![Web-job details uitvoering][WebJobRunDetails]
4. toosee hello uitvoertekst in een apart browservenster, klikt u op Hallo **downloaden** koppeling. toodownload hello tekst zelf, met de rechtermuisknop op de koppeling Hallo en uw browser opties toosave Hallo bestandsinhoud gebruiken.
   
    ![Logboekuitvoer downloaden][DownloadLogOutput]
5. Hallo **WebJobs** koppeling bovenaan Hallo Hallo pagina biedt een handige manier tooget tooa lijst van WebJobs op Hallo geschiedenis dashboard.
   
    ![Lijst van de tooWebJobs koppelen][WebJobsLinkToDashboardList]
   
    ![Lijst met WebJobs in geschiedenis dashboard][WebJobsListInJobsDashboard]
   
    Op een van deze koppelingen te klikken, gaat u toohello webtaak detailpagina voor het Hallo-taak die u hebt geselecteerd.

## <a name="WHPNotes"></a>Opmerkingen bij de
* Web-apps in vrije modus kunnen een time-out na 20 minuten als er geen site aanvragen toohello scm (implementatie) en de portal Hallo van web-app niet geopend in Azure is. Aanvragen toohello Werkelijke site wordt niet opnieuw ingesteld dit.
* Code voor een continue job moet toobe toorun geschreven in een oneindige lus.
* Continue taken uitvoeren continu alleen als Hallo web-app actief is.
* Basic en Standard modi aanbieding Hallo altijd op functie die, als deze is ingeschakeld, web-apps kunnen niet langer inactief.
* U kunt alleen fouten opsporen doorlopend uitgevoerde WebJobs. Geplande of op aanvraag WebJobs foutopsporing wordt niet ondersteund.

## <a name="NextSteps"></a>Volgende stappen
Zie voor meer informatie [Azure WebJobs aanbevolen Resources][WebJobsRecommendedResources].

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

