---
title: aaaWhat is hello Azure WebJobs SDK
description: Een inleiding toohello Azure WebJobs SDK. Wordt uitgelegd welke Hallo SDK is, typische scenario's die dit is handig voor, en codevoorbeelden.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Wat is Azure WebJobs SDK Hallo
## <a id="overview"></a>Overzicht
Dit artikel wordt uitgelegd wat Hallo WebJobs SDK is, controleert u enkele algemene scenario's het is nuttig voor en geeft een overzicht van hoe u deze in uw code gebruiken.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[WebJobs](websites-webjobs-resources.md) is een functie van Azure App Service waarmee u toorun een programma of script in Hallo dezelfde context als een web-app, API-app of mobiele app. doel van Hallo Hallo [WebJobs SDK](websites-webjobs-resources.md) is toosimplify Hallo code voor algemene taken die een webtaak schrijven, zoals beeldverwerking, wachtrijbewerkingen, RSS aggregatie, onderhouden van bestanden uitvoeren kunt en e-mailberichten verzenden. Hallo WebJobs SDK bevat ingebouwde functies voor het werken met Azure Storage en Service Bus, voor het plannen van taken en het afhandelen van fouten en voor veel andere veelvoorkomende scenario's. Bovendien ontwikkeld toobe extensible. Hallo [WebJobs SDK is open-source](https://github.com/Azure/azure-webjobs-sdk/), en er is een [open-source-opslagplaats voor uitbreidingen](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Hallo WebJobs SDK omvat Hallo volgende onderdelen:

* **NuGet-pakketten**. NuGet-pakketten dat u, tooa Visual Studio-consoletoepassing project toevoegt bieden een framework dat uw code wordt gebruikt door uw methoden met de WebJobs SDK kenmerken versieren.
* **Dashboard**. Onderdeel van Hallo WebJobs SDK is opgenomen in Azure App Service en biedt uitgebreide controle en diagnostische gegevens voor programma's die gebruikmaken van Hallo NuGet-pakketten. U hebt geen toowrite code toouse deze functies controle en diagnostische gegevens.

## <a id="scenarios"></a>Scenario 's
Hier volgen enkele typische scenario's die met hello Azure WebJobs SDK kunt u er nog gemakkelijker verwerken:

* Afbeelding van verwerking of andere CPU-intensief werk. Een algemene functie van websites is Hallo mogelijkheid tooupload afbeeldingen of video's. Vaak wilt u toomanipulate Hallo inhoud nadat geüpload, maar u niet dat toomake Hallo-gebruiker wacht wilt terwijl u dat doen.
* Verwerking van de wachtrij. Een veelgebruikte manier voor een web-front-toocommunicate met een back-endservice is toouse wachtrijen. Wanneer Hallo website tooget werk moet, stuurt deze een bericht naar een wachtrij. Een back-endservice berichten uit de wachtrij Hallo ophaalt en Hallo werk. U kunt wachtrijen gebruiken voor de verwerking van afbeeldingen: bijvoorbeeld nadat Hallo gebruiker een aantal bestanden uploadt, Hallo bestandsnamen plaatsen in een wachtrij bericht toobe opgepikt door Hallo back-end voor verwerking. Of u kunt wachtrijen tooimprove site reactiesnelheid. Bijvoorbeeld, in plaats van schrijft rechtstreeks tooa SQL-database, tooa wachtrij schrijven, Hallo gebruiker melden u klaar bent en u kunt Hallo back-end-service-ingang hoge latentie relationele database werken. Zie voor een voorbeeld van wachtrij voor de verwerking van de installatiekopie, Hallo [WebJobs SDK aan de slag zelfstudie](websites-dotnet-webjobs-sdk-get-started.md).
* RSS-aggregatie. Als u een site die een lijst met RSS-feeds onderhoudt hebt, kan u ophalen van alle artikelen Hallo van Hallo-feeds in een achtergrondproces.
* Onderhoud van bestanden, zoals samenvoegen of opschonen van logboekbestanden.  Moet u wellicht logboekbestanden wordt gemaakt door verschillende sites of voor afzonderlijke tijdsspannen die u wilt toocombine in volgorde toorun analysis taken op deze. Of u kunt een wekelijkse taak toorun-tooclean van oude logboekbestanden tooschedule.
* Inkomende gegevens in Azure-tabellen. U kunt bestanden die zijn opgeslagen en blobs en wilt tooparse ze en opslaan van gegevens van hello in tabellen. Hallo ingress-functie kan de schrijven groot aantal rijen (miljoenen in sommige gevallen) en Hallo WebJobs SDK kunt u mogelijke tooimplement deze functionaliteit eenvoudig. Hallo SDK biedt ook realtime-controle van voortgangsindicators zoals Hallo aantal rijen in de tabel Hallo geschreven.
* Andere langlopende taken die u wilt van toorun in een achtergrondthread zoals [verzenden van e-mailberichten](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Alle taken die u wilt dat toorun volgens een planning, zoals het uitvoeren van een bewerking voor back-up van elke nacht.

In veel van deze scenario's kunt u tooscale een web-app toorun op meerdere virtuele machines die tegelijkertijd meerdere WebJobs zou worden uitgevoerd. In sommige scenario's die dit kan leiden tot Hallo dezelfde verwerkt gegevens is meerdere keren, maar dit geen probleem wanneer u de ingebouwde wachtrij Hallo, blob en Service Bus-triggers Hallo WebJobs SDK. Hallo SDK zorgt ervoor dat uw functies slechts één keer worden verwerkt voor elk bericht of blob.

Hallo WebJobs SDK kunt u eenvoudig toohandle algemene foutafhandeling scenario's. U kunt waarschuwingen instellen toosend meldingen wanneer een functie mislukt en u time-outs zo instellen kunt dat een functie automatisch wordt geannuleerd als het niet worden voltooid binnen een opgegeven tijd.

## <a id="code"></a>Codevoorbeelden
Hallo-code voor het verwerken van veelvoorkomende taken die met Azure Storage werken is eenvoudig. In uw consoletoepassing `Main` methode u maakt een `JobHost` -object dat Hallo coördineert roept toomethods u schrijven. Hallo WebJobs SDK framework kent Wanneer uw methoden en welke parameter toouse waarden op basis van Hallo WebJobs SDK toocall kenmerken in ze gebruiken. Hallo SDK biedt *triggers* die bepalen welke voorwaarden veroorzaken Hallo functie toobe genoemd, en *modellen* die bepalen hoe tooget informatie naar en van methodeparameters.

Bijvoorbeeld, Hallo [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) -kenmerk veroorzaakt door een functie toobe wordt aangeroepen wanneer een bericht wordt ontvangen op een wachtrij en als Hallo berichtindeling JSON is voor een bytematrix of een aangepast type, het Hallo-bericht automatisch gedeserialiseerd is. Hallo [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) kenmerk een proces wordt geactiveerd wanneer een nieuwe blob in Azure Storage-account wordt gemaakt.

Dit is een eenvoudig programma waarmee een wachtrij worden opgevraagd en maakt u een blob voor elke wachtrijbericht ontvangen:

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

Hallo `JobHost` object is een container voor een verzameling functies van de achtergrond. Hallo `JobHost` object monitors Hallo werkt, controleert op gebeurtenissen die deze triggeren en Hallo functies worden uitgevoerd bij de trigger gebeurtenissen plaatsvinden. U kunt aanroepen een `JobHost` methode tooindicate of op het gewenste Hallo container proces toorun Hallo huidige thread of een achtergrond-thread. In voorbeeld Hallo Hallo `RunAndBlock` methode Hallo proces voortdurend uitgevoerd in de huidige thread Hallo.

Omdat Hallo `ProcessQueueMessage` methode in dit voorbeeld heeft een `QueueTrigger` kenmerk, Hallo-trigger voor die functie Hallo ontvangst van een nieuwe wachtrijbericht is. Hallo `JobHost` object controleert op nieuwe Wachtrijberichten op Hallo opgegeven wachtrij ('webjobsqueue' in dit voorbeeld) en wanneer een wordt gevonden, roept `ProcessQueueMessage`. 

Hallo `QueueTrigger` kenmerk wordt gebonden Hallo `inputText` toohello parameterwaarde van wachtrij het Hallo-bericht. En Hallo `Blob` kenmerk bindingen een `TextWriter` object tooa blob met de naam 'blobname' in een container met de naam 'containername'.  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

Hallo-functie wordt deze parameters toowrite Hallo-waarde van Hallo wachtrij bericht toohello blob vervolgens:

        writer.WriteLine(inputText);

Hallo-trigger en binder functies van Hallo WebJobs SDK Hallo-code die u hebt toowrite aanzienlijk te vereenvoudigen. Hallo op laag niveau code vereist tooprocess wachtrijen, blobs, of bestanden of tooinitiate geplande taken, geldt voor u door Hallo WebJobs SDK-framework. Bijvoorbeeld Hallo framework maakt wachtrijen die nog niet bestaat, wordt geopend Hallo wachtrij, leest wachtrij berichten, verwijderingen wachtrij berichten bij de verwerking is voltooid, maakt de blob-containers die niet bestaan nog, schrijft tooblobs, enzovoort.

Hallo volgende codevoorbeeld toont tal van triggers in één webtaak: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, en `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a>Plannen
Hallo `TimerTrigger` biedt u Hallo mogelijkheid tootrigger functies toorun volgens een schema-kenmerk. U kunt een webtaak plannen, zoals een hele via Azure of schema afzonderlijke functies van een webtaak met de WebJobs SDK Hallo `TimerTrigger`. Hier volgt een voorbeeld van code.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Zie voor meer voorbeelden van code, [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in hello azure webjobs-sdk extensions opslagplaats op GitHub.com.

## <a name="extensibility"></a>Uitbreidbaarheid
U bent niet toobuilt in beperkte functionaliteit--Hallo WebJobs SDK kunt u aangepaste toowrite-triggers en modellen.  U kunt bijvoorbeeld triggers voor cachegebeurtenissen en periodieke planningen schrijven. Een [open-source opslagplaats](https://github.com/Azure/azure-webjobs-sdk-extensions) bevat een [gedetailleerde richtlijnen voor de WebJobs SDK uitbreidbaarheid](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) en voorbeeld code toohelp kunt u uw eigen triggers en modellen schrijven.

## <a id="workerrole"></a>Met behulp van Hallo WebJobs SDK buiten WebJobs
Een programma dat gebruikmaakt van Hallo Hallo WebJobs SDK is een standaard-consoletoepassing en overal kunt uitvoeren, heeft geen toorun als een webtaak. U kunt Hallo programma lokaal testen op uw ontwikkelcomputer, en in productie die kunt u deze uitvoeren in een werkrol Cloudservice of een Windows-service als u liever een van deze omgevingen. 

Hallo-dashboard is echter alleen beschikbaar als een uitbreiding voor een Azure App Service-web-app. Als u wilt dat toorun buiten een webtaak en Hallo Dashboard blijven gebruiken, kunt u een web app toouse Hallo hetzelfde opslagaccount dat de WebJobs SDK-Dashboard verbindingsreeks naar verwijst en gegevens over de functie wordt vervolgens wordt die web-app WebJobs-Dashboard weergeven het uitvoeren van uw programma dat wordt uitgevoerd een andere locatie. U kunt Dashboard toohello ophalen met behulp van Hallo URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Zie voor meer informatie [ophalen van een dashboard voor lokale ontwikkeling Hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), maar houd er rekening mee dat Hallo blogbericht ziet u een oude naam van verbindingsreeks. 

## <a id="nostorage"></a>Dashboardfuncties
Hallo WebJobs SDK biedt verschillende voordelen, zelfs als u de WebJobs SDK triggers of modellen niet gebruikt:

* U kunt functies van Hallo Dashboard aanroepen.
* U kunt functies van Hallo Dashboard opnieuw afspelen.
* U kunt logboeken bekijken in het Dashboard, gekoppelde toohello Hallo bepaalde webtaak (toepassingslogboeken, geschreven met behulp van Console.Out, Console.Error, Trace, enz.) of gekoppeld toohello bepaalde functie-aanroep die ze gegenereerd (Logboeken geschreven met behulp van een `TextWriter` een object dat Hallo die SDK toohello functie als parameter doorgegeven). 

Zie voor meer informatie [hoe toomanually aanroepen voor een functie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) en [hoe toowrite registreert](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Volgende stappen
Zie voor meer informatie over WebJobs SDK Hallo [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).

Zie voor informatie over Hallo nieuwste verbeteringen toohello WebJobs SDK Hallo [releaseopmerkingen](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

