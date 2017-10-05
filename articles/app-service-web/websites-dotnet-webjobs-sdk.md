---
title: Wat is de Azure WebJobs SDK?
description: Een inleiding tot de Azure WebJobs SDK. Legt uit wat de SDK is en typische scenario's het is nuttig voor en codevoorbeelden.
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
ms.openlocfilehash: 8eb05b7cbfb4505f2e94c5b8e6d367ec63a2f033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-azure-webjobs-sdk"></a>Wat is de Azure WebJobs SDK?
## <a id="overview"></a>Overzicht
In dit artikel wordt uitgelegd wat de WebJobs SDK is, controleert enkele algemene scenario's het is nuttig voor en geeft een overzicht van hoe u deze in uw code gebruiken.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[WebJobs](websites-webjobs-resources.md) is een functie van Azure App Service waarmee u een programma of script uitvoeren in de context als een web-app, API-app of mobiele app. Het doel van de [WebJobs SDK](websites-webjobs-resources.md) te vereenvoudigen, de code voor algemene taken die een webtaak schrijven, zoals beeldverwerking, wachtrijbewerkingen, RSS aggregatie, onderhouden van bestanden uitvoeren kunt en e-mailberichten verzenden. De WebJobs SDK bevat ingebouwde functies voor het werken met Azure Storage en Service Bus, voor het plannen van taken en het afhandelen van fouten en voor veel andere veelvoorkomende scenario's. Bovendien is het ontworpen kan worden uitgebreid. De [WebJobs SDK is open-source](https://github.com/Azure/azure-webjobs-sdk/), en er is een [open-source-opslagplaats voor uitbreidingen](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

De WebJobs SDK omvat de volgende onderdelen:

* **NuGet-pakketten**. NuGet-pakketten die u aan een project voor Visual Studio-consoletoepassing toevoegt bieden een framework dat uw code wordt gebruikt door uw methoden met de WebJobs SDK kenmerken versieren.
* **Dashboard**. Onderdeel van de WebJobs SDK is opgenomen in Azure App Service en biedt uitgebreide controle en diagnostische gegevens voor programma's die gebruikmaken van de NuGet-pakketten. U hoeft te schrijven van code voor het gebruik van deze functies controle en diagnostische gegevens.

## <a id="scenarios"></a>Scenario 's
Hier volgen enkele typische scenario's die met de Azure WebJobs SDK kunt u er nog gemakkelijker verwerken:

* Afbeelding van verwerking of andere CPU-intensief werk. Een algemene functie van websites is de mogelijkheid voor het uploaden van afbeeldingen of video's. Vaak wilt u de inhoud te bewerken nadat geüpload, maar u niet maken van de gebruiker geduld wilt terwijl u dat doen.
* Verwerking van de wachtrij. Er is een veelgebruikte manier voor een web-front om te communiceren met een back-endservice wachtrijen gebruiken. Als de website werk gedaan te krijgen moet, stuurt deze een bericht naar een wachtrij. Een back-endservice ophaalt van berichten vanuit de wachtrij en de werkt. U kunt wachtrijen gebruiken voor de verwerking van afbeeldingen: bijvoorbeeld nadat de gebruiker een aantal bestanden uploadt, plaatst de bestandsnamen in een wachtrijbericht om te worden opgenomen door de back-end voor verwerking. Of u kunt wachtrijen gebruiken voor het verbeteren van de reactietijd van de site. Bijvoorbeeld, in plaats van schrijft rechtstreeks naar een SQL-database, schrijven naar een wachtrij, laat de gebruiker die u bent klaar, en laat de back-end-ingang hoge latentie relationele database werken. Zie voor een voorbeeld van de wachtrij verwerking met de installatiekopie van het [WebJobs SDK aan de slag zelfstudie](websites-dotnet-webjobs-sdk-get-started.md).
* RSS-aggregatie. Als u een site die een lijst met RSS-feeds onderhoudt hebt, kan u ophalen van alle artikelen in de feeds in een achtergrondproces.
* Onderhoud van bestanden, zoals samenvoegen of opschonen van logboekbestanden.  Mogelijk hebt u logboekbestanden wordt gemaakt door verschillende sites of voor afzonderlijke tijdsspannen die u combineren wilt om de taken van de analyse wordt uitgevoerd. Of u kunt een taak uitvoeren om op te schonen oude logbestanden wekelijks.
* Inkomende gegevens in Azure-tabellen. U mogelijk bestanden die zijn opgeslagen en blobs hebt en wilt ze parseren en opslaan van de gegevens in tabellen. De functie inkomend kan de schrijven groot aantal rijen (miljoenen in sommige gevallen) en de WebJobs SDK kunt u deze functionaliteit eenvoudig te implementeren. De SDK biedt ook realtime-controle van voortgangsindicators zoals het aantal rijen in de tabel wordt geschreven.
* Andere langlopende taken die u wilt uitvoeren, zoals in een achtergrondthread [verzenden van e-mailberichten](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Alle taken die u uitvoeren op een planning wilt, zoals het uitvoeren van een bewerking voor back-up van elke nacht.

In veel van deze scenario's het zijn dat u wilt schalen van een web-app uit te voeren op meerdere virtuele machines die tegelijkertijd meerdere WebJobs zou worden uitgevoerd. In sommige scenario's die dit kan leiden tot dezelfde gegevens meerdere keren wordt verwerkt, maar dit is niet een probleem wanneer u de ingebouwde wachtrij, blobs en Service Bus-triggers van de WebJobs SDK gebruiken. De SDK zorgt ervoor dat uw functies slechts één keer worden verwerkt voor elk bericht of blob.

De WebJobs SDK kunt u gemakkelijk voor het afhandelen van veelvoorkomende scenario's voor foutafhandeling. U kunt waarschuwingen instellen om meldingen te verzenden wanneer een functie mislukt en u time-outs zo instellen kunt dat een functie automatisch wordt geannuleerd als het niet worden voltooid binnen een opgegeven tijd.

## <a id="code"></a>Codevoorbeelden
De code voor het verwerken van veelvoorkomende taken die met Azure Storage werken is eenvoudig. In uw consoletoepassing `Main` methode u maakt een `JobHost` -object dat het aanroepen van methoden u schrijft coördineert. Het framework WebJobs SDK weet het aanroepen van de methoden en parameterwaarden wilt gebruiken op basis van de WebJobs SDK-kenmerken die u in deze gebruiken. De SDK biedt *triggers* die bepalen welke voorwaarden ertoe leiden dat de functie moet worden aangeroepen en *modellen* die het ophalen van gegevens naar en van methodeparameters opgeven.

Bijvoorbeeld, de [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) -kenmerk veroorzaakt door een functie moet worden aangeroepen wanneer een bericht wordt ontvangen op een wachtrij en als de berichtindeling JSON is voor een bytematrix of een aangepast type, het bericht automatisch gedeserialiseerde is. De [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) kenmerk een proces wordt geactiveerd wanneer een nieuwe blob in Azure Storage-account wordt gemaakt.

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

De `JobHost` object is een container voor een verzameling functies van de achtergrond. De `JobHost` object bewaakt de functies, kijkt naar voor gebeurtenissen die ze, activeren en de functies worden uitgevoerd bij de trigger gebeurtenissen plaatsvinden. U kunt aanroepen een `JobHost` methode om aan te geven of u wilt dat de container-proces worden uitgevoerd op de huidige thread of een achtergrond-thread. In het voorbeeld wordt de `RunAndBlock` methode het proces voortdurend uitgevoerd in de huidige thread.

Omdat de `ProcessQueueMessage` methode in dit voorbeeld heeft een `QueueTrigger` kenmerk, de trigger voor die functie is de ontvangst van een nieuwe wachtrijbericht. De `JobHost` object controleert op nieuwe Wachtrijberichten op de opgegeven wachtrij ('webjobsqueue' in dit voorbeeld) en wanneer een wordt gevonden, roept `ProcessQueueMessage`. 

De `QueueTrigger` bindingen kenmerk de `inputText` parameter met de waarde van het bericht uit de wachtrij. En de `Blob` kenmerk bindingen een `TextWriter` object naar een blob met de naam 'blobname' in een container met de naam 'containername'.  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

Deze parameters vervolgens wordt de waarde van de wachtrijbericht schrijven naar de blob:

        writer.WriteLine(inputText);

De trigger en binder functies van de WebJobs SDK aanzienlijk te vereenvoudigen, de code die u hebt te schrijven. De code op laag niveau is vereist voor het verwerken van wachtrijen, blobs of bestanden of geplande taken starten wordt voor u door het framework WebJobs SDK uitgevoerd. Bijvoorbeeld, het framework maakt wachtrijen die niet bestaan nog, opent de wachtrij, leest wachtrij berichten, verwijderingen wachtrij berichten bij de verwerking is voltooid, maakt de blob-containers die niet bestaan nog, schrijft naar BLOB's, enzovoort.

Het volgende codevoorbeeld ziet u diverse triggers in één webtaak: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, en `ErrorTrigger`. 

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
            To = "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors to the Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a>Plannen
De `TimerTrigger` kenmerk kunt u de trigger-functies worden uitgevoerd op een planning. U kunt een webtaak plannen in zijn geheel via Azure of schema afzonderlijke functies van een webtaak met de WebJobs SDK `TimerTrigger`. Hier volgt een voorbeeld van code.

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

Zie voor meer voorbeelden van code, [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in de azure webjobs-sdk extensions opslagplaats op GitHub.com.

## <a name="extensibility"></a>Uitbreidbaarheid
U bent niet beperkt tot ingebouwde functionaliteit--de WebJobs SDK Hiermee kunt u aangepaste triggers en modellen schrijven.  U kunt bijvoorbeeld triggers voor cachegebeurtenissen en periodieke planningen schrijven. Een [open-source opslagplaats](https://github.com/Azure/azure-webjobs-sdk-extensions) bevat een [gedetailleerde richtlijnen voor de WebJobs SDK uitbreidbaarheid](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) en voorbeeldcode om u te helpen uw eigen triggers en modellen schrijven is gestart.

## <a id="workerrole"></a>Met behulp van de WebJobs SDK buiten WebJobs
Een programma dat gebruikmaakt van de de WebJobs SDK is een standaard consoletoepassing en overal kunnen worden uitgevoerd, heeft geen uit te voeren als een webtaak. U kunt het programma lokaal testen op uw ontwikkelcomputer en in productie kunt u deze uitvoeren in een werkrol Cloudservice of een Windows-service als u liever een van deze omgevingen. 

Het dashboard is echter alleen beschikbaar als een uitbreiding voor een Azure App Service-web-app. Als u wilt buiten een webtaak wordt uitgevoerd en nog steeds gebruiken het Dashboard, kunt u een web-app voor het gebruik van hetzelfde opslagaccount of de WebJobs SDK-Dashboard verbindingsreeks verwijst naar en dat de web-app WebJobs-Dashboard worden gegevens over de uitvoering van een functie van uw programma waarop ergens anders wordt vervolgens weergegeven. U toegang krijgen tot het Dashboard met behulp van de URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Zie voor meer informatie [ophalen van een dashboard voor lokale ontwikkeling met de WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), maar houd er rekening mee dat het blogbericht ziet u een oude naam van verbindingsreeks. 

## <a id="nostorage"></a>Dashboardfuncties
De WebJobs SDK biedt verschillende voordelen, zelfs als u de WebJobs SDK triggers of modellen niet gebruikt:

* U kunt functies van het Dashboard kunt aanroepen.
* U kunt functies van het Dashboard opnieuw afspelen.
* U kunt logboeken bekijken in het Dashboard, gekoppeld aan de specifieke webtaak (toepassingslogboeken, geschreven met behulp van Console.Out, Console.Error, Trace, enz.) of gekoppeld aan het aanroepen van bepaalde functie die ze gegenereerd (Logboeken geschreven met behulp van een `TextWriter` -object dat de SDK wordt doorgegeven aan de functie als een parameter). 

Zie voor meer informatie [hoe een functie handmatig worden aangeroepen](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) en [het schrijven van Logboeken](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Volgende stappen
Zie voor meer informatie over de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).

Zie voor meer informatie over de nieuwste verbeteringen aan de WebJobs SDK de [releaseopmerkingen](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

