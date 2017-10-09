---
title: metrische gegevens aaaEnabling storage in hello Azure-portal | Microsoft Docs
description: Hoe tooenable metrische gegevens voor storage services Blob, Queue, Table en File Hallo
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>Metrische gegevens Storage inschakelen en weergeven van metrische gegevens
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Overzicht
Metrische gegevens Storage is standaard ingeschakeld wanneer u een nieuw opslagaccount maken. U kunt controleren met de Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), Windows PowerShell of via een programma via een API-opslag.

Wanneer u opslag metrische gegevens inschakelen, moet u een bewaarperiode voor gegevens Hallo kiezen: dit wordt bepaald door de voor de opslag van hoe lang Hallo service houdt Hallo metrische gegevens en kosten die u voor Hallo ruimte van het vereiste toostore ze. Normaal gesproken moet u een kortere bewaartermijn voor minuut metrieken dan elk uur metrische gegevens vanwege Hallo aanzienlijke extra ruimte nodig zijn voor de minuut metrische gegevens. Zodanig zijn dat u voldoende tijd tooanalyze Hallo gegevens hebt en eventuele metrische gegevens die u tookeep voor offline-analyse en rapportage wilt downloaden, moet u een bewaartermijn kiezen. Houd er rekening mee dat u ook de factuur voor het downloaden van metrische gegevens van uw opslagaccount.

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a>Hoe met metrische gegevens tooenable Storage Hallo klassieke Azure-Portal
In Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), u de pagina configureren hello gebruiken voor een storage account toocontrol opslag metrische gegevens. Voor bewaking, kunt u een niveau en een bewaartermijn in dagen voor elk van de blobs, tabellen en wachtrijen instellen. In elk geval is Hallo niveau een van de volgende Hallo:

* Uitgeschakeld: Er is geen metrische gegevens worden verzameld.
* Minimaal: Opslag metrische gegevens verzamelt een elementaire reeks metrische gegevens zoals inkomend en uitgaand, beschikbaarheid, latentie en geslaagd percentages, die voor de services Blob, Table en Queue Hallo worden geaggregeerd.
* Uitgebreide: Opslag metrische gegevens verzamelt een volledige set van metrische gegevens die omvat Hallo dezelfde metrische gegevens voor elke storage-API-bewerking, Daarnaast toohello serviceniveau metrische gegevens. Uitgebreide metrische gegevens inschakelen dichter analyse van problemen die tijdens de bewerkingen van de toepassing optreden.

Houd er rekening mee dat Hallo klassieke Azure-Portal op dit moment kunnen niet u tooconfigure minuut metrische gegevens in uw opslagaccount; u moet inschakelen minuut metrieken met PowerShell of via een programma.

## <a name="how-tooenable-storage-metrics-using-powershell"></a>Hoe tooenable opslag metrische gegevens met behulp van PowerShell
U kunt PowerShell gebruiken op uw lokale machine tooconfigure opslag metrische gegevens in uw opslagaccount met behulp van de huidige instellingen voor hello Azure PowerShell-cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello en Hallo cmdlet Set-AzureStorageServiceMetricsProperty toochange Hallo huidige instellingen.

Hallo-cmdlets waarmee de metrische gegevens Storage gebruiken Hallo volgende parameters:

* MetricsType mogelijke waarden zijn uren en minuten.
* ServiceType mogelijke waarden zijn Blob, wachtrijen en tabellen.
* MetricsLevel mogelijke waarden zijn geen (gelijkwaardige tooOff in de klassieke Azure-Portal Hallo)-Service (gelijkwaardige tooMinimal in de klassieke Azure-Portal Hallo) en ServiceAndApi (gelijkwaardige tooVerbose in Hallo klassieke Azure-Portal).

Bijvoorbeeld: hello volgende opdracht switches op minuut metrische gegevens voor blob-service in uw storage-standaardaccount met bewaarperiode Hallo Hallo toofive dagen instellen:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
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
Wanneer u hebt opslag metrische gegevens toomonitor uw storage-account geconfigureerd, registreert Hallo metrische gegevens in een verzameling van bekende tabellen in uw opslagaccount. Zodra deze beschikbaar op een grafiek, kunt u pagina Hallo-Monitor voor uw opslagaccount in Hallo klassieke Azure-Portal tooview Hallo per uur metrische gegevens. U kunt op deze pagina in de klassieke Azure-Portal Hallo:

* Selecteer welke tooplot metrische gegevens in de grafiek hello (Hallo keuze van de beschikbare metrische gegevens hangen af van of u hebt ervoor gekozen uitgebreide of minimale bewaking voor Hallo-service op de pagina configureren Hallo).
* Selecteer Hallo tijdsbereik voor Hallo metrische gegevens op Hallo grafiek weergegeven.
* Kies toouse een absolute of relatieve schaal tooplot Hallo metrische gegevens.
* Configureren van e-mailbericht waarschuwingen toonotify u wanneer specifieke metrische gegevens een bepaalde waarde heeft bereikt.

Als u wilt dat toodownload Hallo metrische gegevens voor langdurige opslag of tooanalyze ze lokaal wordt toouse een hulpprogramma of u code schrijven tooread Hallo tabellen. U moet downloaden Hallo minuut metrische gegevens voor analyse. Hallo tabellen worden niet weergegeven als u alle Hallo tabellen in uw opslagaccount weergeven, maar u kunt ze rechtstreeks met de naam benaderen. Veel opslag bladeren hulpprogramma's van derden zich bewust bent van deze tabellen en kunt u tooview ze rechtstreeks (Zie Hallo blogbericht [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) voor een lijst met beschikbare hulpprogramma's).

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

U moet overwegen om waarschuwingen in Hallo klassieke Azure-Portal op de pagina van de Monitor Hallo zodat metrische gegevens Storage kan automatisch een melding van belangrijke wijzigingen in gedrag Hallo van uw storage-services. Als u een toodownload storage explorer hulpprogramma deze metrische gegevens in een indeling die gescheiden, kunt u Microsoft Excel tooanalyze Hallo-gegevens. Zie het blogbericht van Hallo [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) voor een lijst met beschikbare opslag explorer-hulpprogramma's.

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

## <a name="next-steps"></a>Volgende stappen:
[Storage Analytics en het benaderen van logboekgegevens inschakelen](https://msdn.microsoft.com/library/dn782840.aspx)
