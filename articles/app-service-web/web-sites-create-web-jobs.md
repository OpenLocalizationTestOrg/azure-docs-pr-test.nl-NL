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
# <a name="run-background-tasks-with-webjobs"></a>Achtergrondtaken uitvoeren met WebJobs
## <a name="overview"></a>Overzicht
U kunt de programma's of scripts uitvoeren in WebJobs in uw [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web-app op drie manieren: op aanvraag continu, of volgens een schema. Er is geen extra kosten WebJobs gebruiken.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Dit artikel laat zien hoe u webtaken implementeren met behulp van de [Azure Portal](https://portal.azure.com). Zie voor meer informatie over het implementeren met behulp van Visual Studio of een doorlopende levering proces [hoe Azure WebJobs voor Web-Apps implementeren](websites-dotnet-deploy-webjobs.md).

De Azure WebJobs SDK vereenvoudigt veel WebJobs programmeertaken. Zie voor meer informatie [wat de WebJobs SDK is](websites-dotnet-webjobs-sdk.md).

 Azure Functions bevat een andere manier om uit te voeren programma's en scripts van een zonder server omgeving of van een App Service-app. Zie voor meer informatie [overzicht van Azure Functions](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Acceptabele bestandstypen voor scripts of programma 's
De volgende bestandstypen worden geaccepteerd:

* .cmd, .bat, .exe (met behulp van windows cmd)
* .ps1 (met powershell)
* .sh (met behulp van bash)
* .php (met behulp van php)
* .PY (met behulp van python)
* .js (met behulp van knooppunt)
* JAR (met java)

## <a name="CreateOnDemand"></a>Maken van een on-demand webtaak in de portal
1. In de **Web-App** blade van de [Azure Portal](https://portal.azure.com), klikt u op **alle instellingen > WebJobs** om weer te geven de **WebJobs** blade.
   
    ![Webtaak-blade](./media/web-sites-create-web-jobs/wjblade.png)
2. Klik op **Add**. De **webtaak toevoegen** dialoogvenster wordt weergegeven.
   
    ![Webtaak blade toevoegen](./media/web-sites-create-web-jobs/addwjblade.png)
3. Onder **naam**, Geef een naam voor de webtaak. De naam moet beginnen met een letter of cijfer en andere dan mag geen speciale tekens bevatten '-' en '_'.
4. In de **How to Run** Kies **op aanvraag uitvoeren**.
5. In de **bestand laden** op het pictogram van de map en blader naar het zipbestand met het script. Het zip-bestand moet het uitvoerbare bestand (.exe .cmd .bat .sh .php .py .js) en de ondersteunende bestanden die nodig zijn voor het uitvoeren van het programma of script bevatten.
6. Controleer **maken** voor het uploaden van het script naar uw web-app. 
   
    De door u opgegeven naam voor de webtaak wordt weergegeven in de lijst op de **WebJobs** blade.
7. De webtaak wordt uitgevoerd, met de rechtermuisknop op de naam ervan in de lijst en klikt u op **uitvoeren**.
   
    ![Webtaak wordt uitgevoerd](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Een continu actief webtaak maken
1. Volg dezelfde stappen voor het maken van een webtaak continu uitvoeren voor het maken van een webtaak die eenmaal wordt uitgevoerd, maar in de **How to Run** Kies **doorlopend**.
2. Als u wilt starten of stoppen van een doorlopende webtaak, met de rechtermuisknop op de webtaak in de lijst en klikt u op **Start** of **stoppen**.

> [!NOTE]
> Als uw web-app wordt uitgevoerd op meer dan één exemplaar, wordt een continu actief webtaak wordt uitgevoerd op al uw exemplaren. Op aanvraag en geplande webtaken uitvoeren op één instantie geselecteerd voor de load balancer door Microsoft Azure.
> 
> Inschakelen voor doorlopende webtaken worden uitgevoerd op betrouwbare wijze en op alle instanties de altijd op * configuratie-instelling voor de web-app anders ze kunnen beëindigd wanneer de site van de host SCM te lang inactief is.
> 
> 

## <a name="CreateScheduledCRON"></a>Een geplande webtaak met een CRON expressie maken
Deze techniek is beschikbaar voor Web-Apps die zijn uitgevoerd in de modus Basic, Standard of Premium en vereist dat de **altijd op** instelling zijn ingeschakeld op de app.

Als u wilt een webtaak van de aanvraag op in een geplande webtaak, eenvoudig omvatten een `settings.job` bestand in de hoofdmap van uw webtaak zip-bestand. Deze JSON-bestand bevatten een `schedule` eigenschap met een [CRON expressie](https://en.wikipedia.org/wiki/Cron), per in het volgende voorbeeld.

De CRON-expressie is samengesteld uit 6 velden: `{second} {minute} {hour} {day} {month} {day of the week}`.

Bijvoorbeeld, voor het activeren van uw webtaak elke 15 minuten, uw `settings.job` zou hebben:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Andere voorbeelden van CRON planning:

* Elk uur (dat wil zeggen wanneer het aantal minuten 0 is):`0 0 * * * *` 
* Elk uur uit 9: 00 uur tot 5 PM:`0 0 9-17 * * *` 
* Om 9:30 AM dagelijks:`0 30 9 * * *`
* Om 9:30 AM elke dag van de week:`0 30 9 * * 1-5`

**Opmerking**: bij het implementeren van een webtaak vanuit Visual Studio, zorg ervoor dat u wilt markeren uw `settings.job` bestandseigenschappen als kopiëren indien nieuwer.

## <a name="CreateScheduled"></a>Maken van een geplande webtaak met behulp van de Azure Scheduler
De volgende alternatieve methode wordt gebruikgemaakt van de Azure Scheduler. In dit geval heeft uw webtaak geen rechtstreekse kennis heeft van de planning. De Azure Scheduler opgehaald in plaats daarvan geconfigureerd voor het activeren van uw webtaak volgens een schema. 

De Azure Portal kunt maken van een geplande webtaak nog geen, maar totdat deze functie is toegevoegd. u kunt dit doen met behulp van de [klassieke portal](http://manage.windowsazure.com).

1. In de [klassieke portal](http://manage.windowsazure.com) Ga naar de webtaak pagina en klik op **toevoegen**.
2. In de **How to Run** Kies **volgens een schema uitgevoerd**.
   
    ![Nieuwe geplande taak][NewScheduledJob]
3. Kies de **Scheduler regio** voor uw project en klik vervolgens op de pijl in de rechterbenedenhoek van het dialoogvenster om door te gaan naar het volgende scherm.
4. In de **taak maken** dialoogvenster, kies het type **terugkeerpatroon** gewenste: **eenmalige taak** of **terugkerende taak**.
   
    ![Terugkeerpatroon plannen][SchdRecurrence]
5. Ook voor kiezen een **starten** tijd: **nu** of **op een bepaald tijdstip**.
   
    ![Geplande begintijd][SchdStart]
6. Als u wilt starten op een bepaald tijdstip, kunt u uw eerste tijdwaarden onder **starten op**.
   
    ![Start op een bepaald tijdstip planning][SchdStartOn]
7. Als u een terugkerende taak hebt gekozen, hebt u de **herhalen elke** optie voor de frequentie van de instantie en de **eindigend op** optie voor het opgeven van een eindtijd.
   
    ![Terugkeerpatroon plannen][SchdRecurEvery]
8. Als u ervoor kiest **weken**, kunt u de **op een bepaalde planning** en geef de dagen van de week waarop u wilt dat de taak wilt uitvoeren.
   
    ![Dagen van de planning van de Week][SchdWeeksOnParticular]
9. Als u ervoor kiest **maanden** en selecteer de **op een bepaalde planning** vak kunt u de taak uit te voeren op bepaalde genummerde instellen **dagen** in de maand. 
   
    ![Plannen van bepaalde datums in de maand][SchdMonthsOnPartDays]
10. Als u ervoor kiest **weekdagen**, kunt u welke dag of dagen van de week selecteren in de maand die u wilt dat de taak uit te voeren op.
    
     ![Bepaalde weekdagen in een maand plannen][SchdMonthsOnPartWeekDays]
11. Ten slotte ook kunt u de **voorvallen** kunt kiezen welke week van de maand (eerste, tweede, derde enz.) u wilt dat de taak uit te voeren op de weekdagen die u hebt opgegeven.
    
    ![Bepaalde weekdagen op bepaalde weken in een maand plannen][SchdMonthsOnPartWeekDaysOccurences]
12. Nadat u een of meer taken hebt gemaakt, wordt hun namen worden weergegeven op het tabblad WebJobs met hun status, schematype en andere informatie. Historische gegevens voor de laatste 30 WebJobs wordt bijgehouden.
    
    ![Takenlijst met][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Geplande taken en Azure Scheduler
Geplande taken kunnen verder worden geconfigureerd in de Azure Scheduler-pagina's van de [klassieke portal](http://manage.windowsazure.com).

1. Klik op de taak op de pagina WebJobs **planning** koppeling om te navigeren naar de portal-pagina voor Azure Scheduler. 
   
   ![Koppeling naar Azure Scheduler][LinkToScheduler]
2. Klik op de taak op de pagina Scheduler.
   
    ![Taak op de portal-Scheduler-pagina][SchedulerPortal]
3. De **taakactie** pagina wordt geopend, waarin u kunt de taak verder configureren. 
   
    ![Taakactie PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>De Taakgeschiedenis weergeven
1. Als u wilt weergeven van de geschiedenis van de uitvoering van een taak, met inbegrip van taken die zijn gemaakt met de WebJobs SDK, klikt u op de desbetreffende koppeling onder de **logboeken** kolom van de blade WebJobs. (U kunt het pictogram van het Klembord de URL van de pagina log-bestand naar het Klembord kopiëren als u wilt.)
   
    ![Logboeken koppelen](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Op de koppeling klikt, wordt de detailpagina voor de webtaak geopend. Deze pagina bevat de naam van de opdracht wordt uitgevoerd, de laatste keer die is uitgevoerd, en het slagen of mislukken. Onder **recente taak wordt uitgevoerd**, klikt u op een tijdstip voor meer informatie.
   
    ![WebJobDetails][WebJobDetails]
3. De **Details uitvoering van webtaak** pagina wordt weergegeven. Klik op **wisselknop uitvoer** om te zien van de tekst van de inhoud van het logboek. Het uitvoerlogboek voor is tekst zonder opmaak. 
   
    ![Web-job details uitvoering][WebJobRunDetails]
4. Klik op een overzicht van de uitvoertekst in een apart browservenster de **downloaden** koppeling. Met de rechtermuisknop op de koppeling voor het downloaden van de tekst zelf, en opties van uw browser met inhoud van het bestand opslaan.
   
    ![Logboekuitvoer downloaden][DownloadLogOutput]
5. De **WebJobs** koppeling aan de bovenkant van de pagina biedt een handige manier om een lijst met WebJobs op het dashboard van de geschiedenis.
   
    ![Een koppeling naar de lijst WebJobs][WebJobsLinkToDashboardList]
   
    ![Lijst met WebJobs in geschiedenis dashboard][WebJobsListInJobsDashboard]
   
    Op een van deze koppelingen te klikken gaat u naar de pagina webtaak Details voor de taak die u hebt geselecteerd.

## <a name="WHPNotes"></a>Opmerkingen bij de
* Web-apps in vrije modus kunnen een time-out na 20 minuten als er geen aanvragen voor de site scm (implementatie) en -portal voor de web-app niet is geopend in Azure. Aanvragen voor de werkelijke site wordt niet opnieuw ingesteld dit.
* Code voor een continue taak moet worden geschreven in een oneindige lus uit te voeren.
* Continue taken uitvoeren continu alleen als de web-app actief is.
* Basic en Standard modi aanbieding de altijd op functies die, als deze is ingeschakeld, web-apps kunnen niet langer inactief.
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

