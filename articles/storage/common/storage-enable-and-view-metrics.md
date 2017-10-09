---
title: metrische gegevens aaaEnabling storage in hello Azure-portal | Microsoft Docs
description: Hoe tooenable metrische gegevens voor storage services Blob, Queue, Table en File Hallo
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a>Inschakelen van Azure Storage metrische gegevens en metrische gegevens weergeven
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Overzicht
Metrische gegevens Storage is standaard ingeschakeld wanneer u een nieuw opslagaccount maken. U kunt configureren via Hallo bewaking [Azure-portal](https://portal.azure.com) of Windows PowerShell of programmatisch via een van de opslagclientbibliotheken Hallo.

U kunt een bewaarperiode voor Hallo metrische gegevens configureren: deze periode bepaalt voor hoe lang Hallo opslag service houdt Hallo metrische gegevens en kosten die u voor Hallo ruimte van het vereiste toostore ze. Normaal gesproken moet u een kortere bewaartermijn voor minuut metrieken dan elk uur metrische gegevens vanwege Hallo aanzienlijke extra ruimte nodig zijn voor de minuut metrische gegevens. Zodanig zijn dat u voldoende tijd tooanalyze Hallo gegevens hebt en eventuele metrische gegevens die u tookeep voor offline-analyse en rapportage wilt downloaden, moet u een bewaartermijn kiezen. Houd er rekening mee dat u ook de factuur voor het downloaden van metrische gegevens van uw opslagaccount.

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a>Hoe tooenable metrische gegevens met behulp van Azure-portal Hallo
Volg deze stappen tooenable metrische gegevens in Hallo [Azure-portal](https://portal.azure.com):

1. Navigeer tooyour storage-account.
1. Selecteer **Diagnostics** op Hallo **Menu** blade
1. Zorg ervoor dat **Status** te is ingesteld,**op**.
1. Selecteer Hallo metrische gegevens voor Hallo services u wilt toomonitor.
1. Geef een bewaarperiode beleid tooindicate hoe lang gegevens van tooretain metrische gegevens en logboekbestanden.
1. Selecteer **Opslaan**.

Houd er rekening mee dat Hallo [Azure-portal](https://portal.azure.com) momenteel kunnen niet u tooconfigure minuut metrische gegevens in uw opslagaccount; u moet inschakelen minuut metrische gegevens met behulp van PowerShell of via een programma.

## <a name="how-tooenable-metrics-using-powershell"></a>Hoe tooenable metrische gegevens met behulp van PowerShell
U kunt PowerShell gebruiken op uw lokale machine tooconfigure opslag metrische gegevens in uw opslagaccount met behulp van de huidige instellingen voor hello Azure PowerShell-cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello en Hallo cmdlet Set-AzureStorageServiceMetricsProperty toochange Hallo huidige instellingen.

Hallo-cmdlets waarmee de metrische gegevens Storage gebruiken Hallo volgende parameters:

* MetricsType: mogelijke waarden zijn uren en minuten.
* ServiceType: mogelijke waarden zijn Blob, wachtrijen en tabellen.
* MetricsLevel: mogelijke waarden zijn geen, Service en ServiceAndApi.

Bijvoorbeeld: hello volgende opdracht switches op minuut metrische gegevens voor Blob-service in uw storage-standaardaccount met bewaarperiode Hallo Hallo toofive dagen instellen:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

Hallo haalt volgende opdracht Hallo huidige per uur metrische gegevens niveau en retentie dagen voor blob-service in uw storage-standaardaccount Hallo:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

Zie voor meer informatie over hoe tooconfigure hello Azure PowerShell-cmdlets toowork met uw Azure-abonnement en hoe tooselect Hallo default storage toouse account: [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Hoe tooenable metrische gegevens Storage programmatisch
Hallo volgende C#-fragment toont hoe tooenable metrische gegevens en logboekregistratie voor het gebruik van Hallo Blob service Hallo storage-clientbibliotheek voor .NET:

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Opslag metrische gegevens weergeven
Nadat u opslag Analytics metrische gegevens toomonitor uw storage-account configureert, registreert Storage Analytics Hallo metrische gegevens in een verzameling van bekende tabellen in uw opslagaccount. U kunt grafieken tooview per uur metrische gegevens configureren in Hallo [Azure-portal](https://portal.azure.com):

1. Navigeer tooyour storage-account in Hallo [Azure-portal](https://portal.azure.com).
1. Selecteer **metrische gegevens** in Hallo **Menu** blade voor Hallo service waarvan metrische gegevens gewenste tooview.
1. Selecteer **bewerken** op Hallo grafiek gewenste tooconfigure.
1. In Hallo **grafiek bewerken** blade, selecteer Hallo **tijdsbereik**, **grafiektype**, en Hallo metrische gegevens die u weergeven in het Hallo-grafiek wilt.
1. Selecteer **OK**

Als u wilt dat toodownload Hallo metrische gegevens voor langdurige opslag of tooanalyze ze lokaal, moet u:

* Gebruik een hulpprogramma waarmee de hoogte is van deze tabellen en wordt kunt u tooview en deze te downloaden.
* Schrijven van een aangepaste toepassing of het script tooread en Hallo tabellen op te slaan.

Veel opslag bladeren hulpprogramma's van derden zich bewust bent van deze tabellen en kunt u tooview ze rechtstreeks.
Zie [hulpprogramma's voor Azure Storage Client](storage-explorers.md) voor een lijst met beschikbare hulpprogramma's.

> [!NOTE]
> Vanaf versie 0.8.0 Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/), u kunt weergeven en downloaden Hallo analytics metrische gegevens tabellen.
> 
> 

Volgorde tooaccess Hallo analytics tabellen programmatisch Noteer op Hallo analytics tabellen worden niet weergegeven als u alle Hallo tabellen in uw opslagaccount weergeven. U kunt toegang tot deze rechtstreeks met de naam of gebruik Hallo [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in Hallo .NET-bibliotheek tooquery Hallo tabelnamen voor clients.

### <a name="hourly-metrics"></a>Elk uur metrische gegevens
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Minuut metrische gegevens
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Capaciteit
* $MetricsCapacityBlob

U vindt alle details van Hallo schema's voor deze tabellen op [Storage Analytics metrische gegevens tabelschema](https://msdn.microsoft.com/library/azure/hh343264.aspx). Hallo onderstaande voorbeeld rijen alleen een subset van de beschikbare Hallo kolommen weergeven, maar illustratie van enkele belangrijke functies van Hallo manier die metrische gegevens Storage Hiermee slaat u deze metrische gegevens:

| PartitionKey | RowKey | tijdstempel | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Beschikbaarheid | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |gebruiker. Alle |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |gebruiker. QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |gebruiker. QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |gebruiker. UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

In dit voorbeeld minuut metrische gegevens gebruikt partitiesleutel Hallo Hallo keer minuut resolutie. Hallo rijsleutel Hallo type informatie die is opgeslagen in de rij Hallo identificeert en dit bestaat uit twee delen van informatie, Hallo toegangstype en Hallo aanvraagtype:

* Hallo-toegangstype is gebruiker of systeem, waarbij gebruiker verwijst tooall gebruiker aanvragen toohello storage-service en system toorequests aangebracht door Storage Analytics verwijst.
* Hallo aanvraagtype is alle in dat geval een samenvatting regel is, of het specifieke API Hallo zoals QueryEntity of UpdateEntity identificeert.

Hallo voorbeeldgegevens hierboven toont die alle Hallo registreert voor één minuut (te beginnen om 11:00 A.M.) in dat geval Hallo aantal QueryEntities aanvragen plus hello aantal QueryEntity aanvragen plus het aantal aanvragen dat UpdateEntity Hallo optellen tooseven die is Hallo totale weergegeven op Hallo gebruiker: All rij. Op deze manier Hallo gemiddelde end-to-end-latentie 104.4286 op Hallo gebruiker: All rij kunnen worden afgeleid door te berekenen ((143.8 * 5) + 3 + 9) / 7.

## <a name="metrics-alerts"></a>Waarschuwingen van de metrische gegevens
U moet overwegen om waarschuwingen in Hallo [Azure-portal](https://portal.azure.com) zodat metrische gegevens Storage kan automatisch een melding van belangrijke wijzigingen in Hallo gedrag van uw storage-services. Als u een toodownload storage explorer hulpprogramma deze metrische gegevens in een indeling die gescheiden, kunt u Microsoft Excel tooanalyze Hallo-gegevens. Zie [hulpprogramma's voor Azure Storage Client](storage-explorers.md) voor een lijst met beschikbare opslag explorer-hulpprogramma's. U kunt waarschuwingen configureren in Hallo **waarschuwing regels** blade toegankelijk is onder **bewaking** in de blade Hallo Opslagaccount menu.

> [!IMPORTANT]
> Er is mogelijk een vertraging tussen een gebeurtenis voor opslag en waarop Hallo overeenkomt per uur of minuut metrische gegevens is geregistreerd. In geval van minuut metrieken Hallo kunnen enkele minuten van gegevens in één keer worden geschreven. Dit kan ertoe leiden tootransactions van eerdere minuten worden geaggregeerd in Hallo transactie voor Hallo huidige minuut. Als dit gebeurt, geconfigureerd Hallo waarschuwing service beschikt niet over alle gegevens van de beschikbare metrische gegevens voor Hallo waarschuwing interval, wat kan leiden tooalerts onverwacht geactiveerd.
>

## <a name="accessing-metrics-data-programmatically"></a>Programmatisch toegang krijgen tot gegevens van de metrische gegevens
Hallo toont volgende overzicht voorbeeld C#-code die toegang heeft tot Hallo minuut metrieken voor een aantal minuten en Hallo resultaten weer in een console-venster. Hallo versie 4 met Hallo CloudAnalyticsClient-klasse die vereenvoudigt de toegang tot Hallo metrische gegevens tabellen in de opslag voor Azure Storage-bibliotheek wordt gebruikt.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Welke kosten worden u wanneer u opslag metrische gegevens inschakelen?
Schrijven aanvragen toocreate tabelentiteiten voor de metrische gegevens worden in rekening gebracht op Hallo standaardtarieven toepasselijke tooall Azure Storage-bewerkingen.

Lees- en delete-aanvragen door een client toometrics gegevens zijn ook factureerbare tegen standaardtarieven. Als u een bewaarbeleid voor gegevens hebt geconfigureerd, er zijn niet in rekening gebracht wanneer Azure Storage oude metrische gegevens worden verwijderd. Echter, als u analytische gegevens verwijdert, uw account wordt belast Hallo delete-bewerkingen.

Hallo-capaciteit die wordt gebruikt door Hallo metrische gegevens tabellen is ook factureerbare: u kunt Hallo tooestimate Hallo hoeveelheid capaciteit die wordt gebruikt voor het opslaan van metrische gegevens te volgen:

* Als u elk uur een service gebruikmaakt van elke API in elke service, wordt ongeveer 148KB aan gegevens elk uur in Hallo metrische gegevens transactietabellen opgeslagen als u zowel de service en de API-niveau samenvatting hebt ingeschakeld.
* Als u elk uur een service gebruikmaakt van elke API in elke service, wordt ongeveer 12KB aan gegevens elk uur in Hallo metrische gegevens transactietabellen opgeslagen als u alleen serviceniveau samenvatting hebt ingeschakeld.
* Hallo capaciteit van de tabel voor blobs heeft twee rijen toegevoegd elke dag (mits de gebruiker heeft gekozen Logboeken): dit betekent dat elke dag Hallo van deze tabel wordt groter door up tooapproximately 300 bytes.

## <a name="next-steps"></a>Volgende stappen
[Opslag en het benaderen van logboekgegevens inschakelen](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
