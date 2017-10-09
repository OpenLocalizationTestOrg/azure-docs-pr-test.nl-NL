---
title: aaaStream Analytics realtime verwerking voor Azure Functions | Microsoft Docs
description: Meer informatie over hoe een Azure-functie toouse verbonden met een Service Bus-wachtrij toopopulate een Azure Redis-Cache van Hallo-uitvoer van een Stream Analytics-taak.
keywords: gegevensstroom, redis-cache, service bus-wachtrij
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>Hoe toostore gegevens uit Azure Stream Analytics in een Azure Redis-Cache met behulp van Azure Functions
Azure Stream Analytics kunt u snel ontwikkelen en implementeren van oplossingen voor goedkope toogain realtime-inzichten van apparaten, sensoren, infrastructuur en -toepassingen of elke andere stroom van gegevens. Hiermee kunt verschillende gebruiksvoorbeelden zoals realtime management en opdracht en controle, fraude te detecteren, verbonden auto's en nog veel meer. In veel dergelijke scenario's kunt u toostore gegevens in Azure Stream Analytics output in een gedistribueerde gegevensarchief, zoals een Azure Redis-cache.

Stel dat u deel uitmaken van een bedrijf telecommunicatie. U probeert toodetect SIM fraude waarbij meerdere aanroepen afkomstig zijn van dezelfde identiteit hello, Hallo op dezelfde tijd, maar in verschillende geografische locaties. U wordt opgedragen alle Hallo mogelijke frauduleuze telefoongesprekken opslaan in een Azure Redis-cache. In deze blog bieden we hulp bij hoe kunt u eenvoudig uw taak uitvoeren. 

## <a name="prerequisites"></a>Vereisten
Volledige Hallo [realtime-Fraudedetectie] [ fraud-detection] procedure voor ASA

## <a name="architecture-overview"></a>Overzicht van de architectuur
![Schermopname van architectuur](./media/stream-analytics-functions-redis/architecture-overview.png)

Zoals in Hallo voorgaande afbeelding wordt weergegeven, kunt u Stream Analytics streaming invoergegevens toobe opgevraagd en tooan uitvoer verzonden. Op basis van de uitvoer hello, kan Azure Functions vervolgens resulteren in een soort gebeurtenis. 

In deze blog er zich richten op Hallo Azure Functions deel van deze pipeline of meer specifiek Hallo activering van een gebeurtenis die frauduleuze-gegevens in Hallo-cache opslaat.
Na het voltooien van Hallo [realtime-Fraudedetectie] [ fraud-detection] zelfstudie hebt u een invoer (een event hub), een query en uitvoer (blobopslag) al is geconfigureerd en actief. In deze blog wijzigen we Hallo uitvoer toouse een Service Bus-wachtrij in plaats daarvan. Daarna we verbinding maken met een Azure-functie toothis wachtrij. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Maken en koppelen van een Service Bus-wachtrij-uitvoer
een Service Bus-wachtrij toocreate stappen 1 en 2 van Hallo .NET-sectie in [aan de slag met Service Bus-wachtrijen][servicebus-getstarted].
Nu gaan we verbinding Hallo wachtrij toohello Stream Analytics-taak die is gemaakt in Hallo eerdere fraude detectie procedure.

1. Ga in de Azure-portal hello, toohello **uitvoer** blade van uw project en selecteer **toevoegen** bovenaan Hallo Hallo pagina.
   
    ![Uitvoer toevoegen](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Kies **Service Bus-wachtrij** als Hallo **Sink** en volg Hallo-instructies op het welkomstscherm. U hebt gemaakt of toochoose Hallo naamruimte Hallo Service Bus-wachtrij worden in [aan de slag met Service Bus-wachtrijen][servicebus-getstarted]. Klik op Hallo 'juiste' wanneer u klaar bent.
3. Geef Hallo volgende waarden:
   
   * **Gebeurtenis serialisatiefunctie indeling**: JSON
   * **Codering**: UTF8
   * **INDELING**: regels gescheiden
4. Klik op Hallo **maken** tooadd knop deze bron- en tooverify dat Stream Analytics verbinding toohello storage-account maken kan.
5. In Hallo **Query** tabblad, de huidige query Hallo vervangen door de volgende Hallo. Vervang * [uw SERVICE BUS NAME] * met Hallo uitvoer naam die u in stap 3 hebt gemaakt. 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a>Maak een Azure Redis Cache
Maken van een Azure Redis-cache door de volgende sectie van de Hallo .NET in [hoe tooUse Azure Redis-Cache] [ use-rediscache] totdat Hallo sectie aangeroepen ***hello cacheclients configureren***.
Hierna kunt hebt u een nieuwe Redis-Cache. Onder **alle instellingen**, selecteer **toegangssleutels** en noteer Hallo ***primaire verbindingsreeks***.

![Schermopname van architectuur](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Een Azure-functie maken
Ga als volgt [uw eerste Azure-functie maken] [ functions-getstarted] zelfstudie tooget de slag met Azure Functions. Als u al een Azure-functie zou u toouse, zoals vervolgens gaat u verder te[tooRedis Cache schrijven](#Writing-to-Redis-Cache)

1. Hallo-portal, selecteer App Services in de linkernavigatiebalk Hallo vervolgens klikt u op de website van uw Azure-functie app name tooget toohello van functie-app.
    ![Schermafbeelding van de lijst met de functie van de app services](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Klik op **nieuwe functie > ServiceBusQueueTrigger – C#**. Voor Hallo volgende velden als volgt:
   
   * **Wachtrijnaam**: Hallo dezelfde naam als Hallo-naam die u hebt opgegeven tijdens het maken van de wachtrij Hallo in [aan de slag met Service Bus-wachtrijen] [ servicebus-getstarted] (niet Hallo naam van Hallo servicebus). Zorg ervoor dat u Hallo wachtrij die is verbonden toohello uitvoer van de Stream Analytics gebruiken.
   * **Service Bus-verbinding**: Selecteer **een verbindingsreeks toevoegen**. toofind hello verbindingsreeks, Ga toohello klassieke portal, selecteer **Service Bus**, Hallo servicebus die u hebt gemaakt, en **VERBINDINGSGEGEVENS** Hallo onder welkomstscherm aan. Zorg ervoor dat u zich op de belangrijkste welkomstscherm op deze pagina. Kopieer en plak de verbindingsreeks Hallo. De naam van een verbinding met gratis tooenter vertrouwen.
     
       ![Schermopname van service bus-verbinding](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights**: kies **beheren**
3. Klik op **Maken**.

## <a name="writing-tooredis-cache"></a>Schrijven tooRedis Cache
Wij hebben nu een Azure-functie die van een Service Bus-wachtrij wordt gemaakt. Alles wat toodo blijft onze toowrite functie gebruiken deze gegevens toohello Redis-Cache is. 

1. Selecteer de zojuist gemaakte **ServiceBusQueueTrigger**, en klik op **werken app-instellingen** op Hallo rechterbovenhoek. Selecteer **Ga tooApp Service-instellingen > Instellingen > Toepassingsinstellingen**
2. In Hallo sectie Connection-tekenreeksen, maakt u een naam in Hallo **naam** sectie. Primaire verbindingsreeks Hallo u in Hallo gevonden plakken **een Redis-Cache maken** stap naar Hallo **waarde** sectie. Selecteer **aangepaste** aanduiding **SQL-Database**.
3. Klik op **opslaan** Hallo bovenaan.
   
    ![Schermopname van service bus-verbinding](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Nu gaat u terug toohello App Service-instellingen en selecteer **Extra > App Service-Editor (Preview) > op > Ga**.
   
    ![Schermopname van service bus-verbinding](./media/stream-analytics-functions-redis/app-service-editor.png)
5. Maak een JSON-bestand met de naam in een editor naar keuze, **project.json** met Hallo volgen en sla het tooyour lokale schijf.
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. Dit bestand niet uploaden naar de hoofdmap Hallo van de functie (geen WWWROOT). Er is een bestand met de naam **project.lock.json** automatisch wordt weergegeven, waarin wordt bevestigd dat Hallo Nuget pakketten 'StackExchange.Redis' en 'Newtonsoft.Json' zijn geïmporteerd.
7. In Hallo **run.csx** bestand, Hallo vooraf gegenereerde code vervangen door Hallo code te volgen. In de functie lazyConnection Hallo naam vervangen door "CONN ' Hallo-naam die u hebt gemaakt in stap 2 van **gegevens opslaan in de Redis-cache Hallo**.

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a>Hallo Stream Analytics-taak starten
1. Hallo telcodatagen.exe toepassing starten. Hallo-gebruik is als volgt:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. Hallo Stream Analytics-taak blade in Hallo-portal klikt u op **Start** bovenaan Hallo Hallo pagina.
   
    ![Schermafbeelding van de taak is gestart](./media/stream-analytics-functions-redis/starting-job.png)
3. In Hallo **starttaak** blade die wordt weergegeven, selecteer **nu** en klik vervolgens op Hallo **Start** knop Hallo onder welkomstscherm aan. Hallo taakstatus verandert tooStarting en na enige tijd wijzigingen tooRunning.
   
    ![Schermopname van start tijd Functieselectie](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Oplossing en de resultaten controleren
Ga terug tooyour **ServiceBusQueueTrigger** pagina u ziet nu aanmelden instructies. Deze logboeken weergeven die u hebt gekregen iets Hallo Service Bus-wachtrij plaatsen in Hallo-database, en het Hallo-tijd gebruikt als Hallo sleutel opgehaald.

tooverify dat uw gegevens in uw Redis-cache, gaat u tooyour Redis-cache-pagina in de nieuwe portal hello (zoals weergegeven in de voorgaande Hallo [maken van een Azure Redis-Cache](#Create-an-Azure-Redis-Cache) stap) en selecteer de Console.

Nu kunt u schrijven Redis opdrachten tooconfirm gegevens zich in feite in Hallo-cache.

![Schermopname van Redis-Console](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Volgende stappen
We zijn blij Hallo nieuwe dingen Azure Functions en we hopen dat u dat dit nieuwe mogelijkheden voor u ontgrendelt Stream analytics samen kunt doen. Als u feedback wilt naast hebt, kunt u gratis toouse hello [Azure UserVoice-site](https://feedback.azure.com/forums/270577-stream-analytics).

Als u nieuwe Microsoft Azure, we nodigen u tootry deze door zich aanmelden voor een [gratis proefaccount voor Azure](https://azure.microsoft.com/pricing/free-trial/). Als u nieuwe tooStream Analytics zijn, en vervolgens we u uit te nodigen[maken van uw eerste Stream Analytics-taak](stream-analytics-create-a-job.md).

Als u een moet helpen of vragen hebt, post een bericht op [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) of [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums. 

U ziet ook Hallo resources te volgen:

* [Naslaginformatie over Azure Functions voor ontwikkelaars](../azure-functions/functions-reference.md)
* [Azure Functions C# referentie voor ontwikkelaars](../azure-functions/functions-reference-csharp.md)
* [Azure Functions F # referentie voor ontwikkelaars](../azure-functions/functions-reference-fsharp.md)
* [Azure Functions NodeJS-referentie voor ontwikkelaars](../azure-functions/functions-reference.md)
* [Azure Functions-triggers en bindingen](../azure-functions/functions-triggers-bindings.md)
* [Hoe toomonitor Azure Redis-Cache](../redis-cache/cache-how-to-monitor.md)

toostay op de hoogte van alle Hallo laatste nieuws en -functies, volg [ @AzureStreaming ](https://twitter.com/AzureStreaming) op Twitter.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
