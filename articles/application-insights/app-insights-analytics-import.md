---
title: aaaImport uw tooAnalytics gegevens in Azure Application Insights | Microsoft Docs
description: Statische gegevens toojoin met app telemetrie importeren, of een afzonderlijke gegevensstroom tooquery met Analytics importeren.
services: application-insights
keywords: Open-schema, gegevens importeren
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Gegevens importeren in Analytics

Importeer tabellaire gegevens in [Analytics](app-insights-analytics.md), ofwel toojoin met [Application Insights](app-insights-overview.md) telemetrie van uw app, of dat u deze als een afzonderlijke stream kunt analyseren. Analytics is een krachtige query language geschikt tooanalyzing hoog volume voorzien van een tijdstempel streams telemetrie.

U kunt gegevens importeren in Analytics met uw eigen schema. Heeft geen toouse Hallo standaard Application Insights-schema's zoals aanvraag of trace.

U kunt importeren JSON of DSV (scheidingsteken gescheiden waarden - komma, puntkomma of tab) bestanden.

Er zijn drie situaties waarin tooAnalytics importeren handig is:

* **Voeg met app telemetrie.** U kunt bijvoorbeeld een tabel die is toegewezen URL's van uw website toomore gelezen pagina's importeren. In Analytics, kunt u een dashboard grafiekrapport Hallo tien meest populaire pagina's in uw website. Nu kan worden weergegeven waarop Hallo pagina's in plaats van Hallo URL's.
* **Telemetrie van uw toepassing correleren** met andere bronnen zoals netwerkverkeer, server-gegevens of CDN logboekbestanden.
* **Toepassing Analytics tooa afzonderlijke gegevensstroom.** Application Insights Analytics is een krachtig hulpprogramma dat goed samen met sparse, voorzien van een tijdstempel streams - veel beter dan SQL in veel gevallen werkt. Als u een dergelijke stroom van een andere bron hebt, kunt u deze kunt analyseren met Analytics.

Verzenden de tooyour-gegevensbron is eenvoudig. 

1. (Eenmaal) Hallo-schema van uw gegevens in een gegevensbron definiëren.
2. (Periodiek) Uploaden van uw gegevens tooAzure opslag en Hallo REST-API toonotify ons die nieuwe gegevens opname wacht te bellen. Binnen een paar minuten is Hallo gegevens beschikbaar voor query's in Analytics.

Hello frequentie van Hallo uploaden is door u gedefinieerde en hoe snel wilt u uw gegevens toobe beschikbaar voor query's. Het is efficiënter tooupload gegevens in grotere segmenten, maar niet groter zijn dan 1GB.

> [!NOTE]
> *Hebt u veel gegevensbronnen tooanalyze?* [*Overweeg het gebruik van* logstash *tooship uw gegevens in Application Insights.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Voordat u begint

U hebt de volgende zaken nodig:

1. Een Application Insights-resource in Microsoft Azure.

 * Als u uw gegevens afzonderlijk van andere telemetrie tooanalyze wilt [Maak een nieuwe Application Insights-resource](app-insights-create-new-resource.md).
 * Als u lid worden van of uw gegevens met de telemetrie van een app die al is ingesteld met Application Insights vergelijken, kunt u Hallo resource voor die app gebruiken.
 * Inzender of eigenaar toegang toothat resource.
 
2. Azure-opslag. Uploaden van tooAzure opslag en Analytics uw gegevens ontvangt van daaruit. 

 * U wordt aangeraden dat u een speciale storage-account maken voor uw blobs. Als uw blobs worden gedeeld met andere processen, duurt het langer voor onze tooread processen uw blobs.


## <a name="define-your-schema"></a>Uw schema definiëren

Voordat u gegevens importeren kunt, moet u een *gegevensbron* waarmee Hallo-schema van uw gegevens.
U kunt hebben van de gegevensbronnen too50 in één Application Insights-resource

1. Start de wizard Gegevensbron Hallo. Gebruik de knop 'Een nieuwe gegevensbron toevoegen'. U kunt ook - klikt u op de knop instellingen in rechts bovenhoek en kies 'Gegevensbronnen' in het vervolgkeuzemenu.

    ![Nieuwe gegevensbron toevoegen](./media/app-insights-analytics-import/add-new-data-source.png)

    Geef een naam voor de nieuwe gegevensbron.

2. Definieer de indeling van Hallo-bestanden die u zult uploaden.

    U kunt Hallo indeling handmatig opgeven of u een voorbeeldbestand uploaden.

    Als Hallo gegevens zich in de CSV-indeling, zijn de eerste rij Hallo van Hallo voorbeeld kolomkoppen. Hallo-veldnamen in de volgende stap hello, kunt u wijzigen.

    Hallo-voorbeeld moet ten minste 10 rijen of records van de gegevens bevatten.

    Kolom- of veldnamen moeten alfanumeriek namen (zonder spaties of leestekens) hebben.

    ![Een voorbeeld-bestand uploaden](./media/app-insights-analytics-import/sample-data-file.png)


3. Bekijk Hallo schema dat wizard Hallo heeft is. Als het Hallo-typen uit een voorbeeld van een afgeleid, moet u mogelijk tooadjust Hallo afgeleid typen Hallo kolommen.

    ![Bekijk Hallo afgeleid schema](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (Optioneel.) Upload een schemadefinitie. Zie de onderstaande Hallo-notatie.

 * Selecteer een tijdstempel. Alle gegevens in Analytics moet beschikken over een tijdstempelveld. Type moet hebben `datetime`, maar heeft geen toobe met de naam 'tijdstempel'. Als uw gegevens een kolom met een datum en tijd in de ISO-indeling heeft, kies deze optie als Hallo timestamp-kolom. Kies anders 'als gegevens ontvangen' en Hallo importproces een timestamp-veld wilt toevoegen.

5. Hallo-gegevensbron maken.

### <a name="schema-definition-file-format"></a>Bestandsindeling van pakketdefinities schema

In plaats van het Hallo-schema in de gebruikersinterface bewerkt, kunt u de schemadefinitie Hallo laden uit een bestand. Hallo schema definitie-indeling is als volgt: 

Gescheiden indeling 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

JSON-indeling 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Elke kolom wordt geïdentificeerd door Hallo locatie, naam en type. 

* Locatie – is voor het bestand met scheidingstekens formatteert u het Hallo-positie van Hallo toegewezen waarde. Voor JSON-indeling is het Hallo jpath van Hallo toegewezen sleutel.
* Naam: Hallo weergegeven naam van Hallo-kolom.
* Type: Hallo-gegevenstype van die kolom.
 
Als een voorbeeldgegevens gebruikt en bestandsindeling worden gescheiden, moet Hallo schemadefinitie alle kolommen toewijzen en nieuwe kolommen toevoegen aan Hallo einde. 

JSON staat gedeeltelijke Hallo gegevens worden toegewezen, daarom hello schemadefinitie van JSON-indeling heeft geen toomap elke sleutel die is gevonden in een voorbeeldgegevens. Deze kunt kolommen die geen deel uitmaken van de voorbeeldgegevens Hallo ook toewijzen. 

## <a name="import-data"></a>Gegevens importeren

tooimport gegevens, tooAzure opslag te uploaden, een toegangssleutel voor het maken en breng vervolgens een REST-API-aanroep.

![Nieuwe gegevensbron toevoegen](./media/app-insights-analytics-import/analytics-upload-process.png)

U kunt Hallo na handmatig uitvoeren of instellen van een toodo automatisch deze met regelmatige tussenpozen. U moet toofollow deze stappen voor elk gegevensblok tooimport gewenste.

1. Hallo-gegevens te uploaden[Azure blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * BLOBs kunnen elke grootte van niet-gecomprimeerd too1GB zijn. Grote blobs honderden MB zijn ideaal vanuit het oogpunt van prestaties van.
 * U kunt het comprimeren met Gzip tooimprove uploadtijd en de latentie voor Hallo gegevens toobe beschikbaar voor query. Gebruik Hallo `.gz` bestandsnaamextensie.
 * Is het beste toouse een afzonderlijke opslagaccount voor dit doel, tooavoid aanroepen vanuit verschillende services prestaties te vertragen.
 * Tijdens het verzenden van gegevens met hoge frequentie, om de paar seconden verdient toouse meer dan één opslagaccount opgeven voor betere prestaties.

 
2. [Maak een Shared Access Signature-sleutel voor Hallo blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). Hallo-sleutel moet een vervalperiode van één dag hebben en geef leestoegang.
3. Controleer een REST-aanroep toonotify Application Insights dat gegevens wordt verwacht.

 * Eindpunt:`https://dc.services.visualstudio.com/v2/track`
 * HTTP-methode: POST
 * De nettolading van:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

Hallo tijdelijke aanduidingen zijn:

* `Blob URI with Shared Access Key`: U krijgt deze van Hallo procedure voor het maken van een sleutel. Het is specifieke toohello blob.
* `Schema ID`: Hallo schema-ID gegenereerd voor uw gedefinieerd schema. Hallo-gegevens in deze blob moet toohello schema voldoen.
* `DateTime`: Hallo UTC-tijd van aanvraag is verzonden op welke hello,. We accepteren van deze indelingen: ISO8601 (zoals ' 01-01-2016 13:45:01 '); RFC822 (' Wed, 14 december 16 14:57:01 + 0000 '); RFC850 ("woensdag, 14-december-16 14:57:00 UTC"); RFC1123 (' Wed 14 december 2016 14:57:00 + 0000 ').
* `Instrumentation key`van uw Application Insights-resource.

Hallo-gegevens zijn beschikbaar in Analytics na een paar minuten.

## <a name="error-responses"></a>Foutberichten

* **400 onjuiste aanvraag**: geeft aan dat verzoek Hallo nettolading is ongeldig. Controleren:
 * Juiste instrumentatiesleutel.
 * Geldige tijd-waarde. Hallo UTC-tijd nu moeten worden.
 * De JSON van de gebeurtenis Hallo voldoet toohello schema.
* **403-verboden**: Hallo blob die u hebt verzonden, is niet toegankelijk. Zorg ervoor dat Hallo gedeelde toegangssleutel is geldig en niet is verlopen.
* **404 niet gevonden**:
 * Hallo blob bestaat niet.
 * Hallo sourceId is onjuist.

Meer gedetailleerde informatie is beschikbaar in het foutbericht Hallo-antwoord.


## <a name="sample-code"></a>Voorbeeldcode

Deze code gebruikt Hallo [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet-pakket.

### <a name="classes"></a>Klassen

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Gegevens opnemen

Deze code gebruiken voor elke blob. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Volgende stappen

* [Rondleiding Hallo querytaal Log Analytics](app-insights-analytics-tour.md)
* [Gebruik *Logstash* toosend gegevens tooApplication Insights](https://github.com/Microsoft/logstash-output-application-insights)
