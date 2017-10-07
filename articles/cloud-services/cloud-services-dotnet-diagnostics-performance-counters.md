---
title: aaaUse prestatiemeters in Azure Diagnostics | Microsoft Docs
description: Gebruik prestatiemeters in Azure-cloud-services of virtuele machine toofind knelpunten en prestaties te optimaliseren.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Maken en gebruiken van prestatie-items in een Azure-toepassing
Dit artikel wordt beschreven Hallo voordelen van en hoe tooput van de prestatiemeteritems in uw Azure-toepassing. U kunt ze toocollect gegevens gebruiken, knelpunten vinden en afstemmen van de prestaties van systeem en de toepassing.

Prestatie-items beschikbaar voor Windows Server, IIS en ASP.NET kunnen ook worden verzameld en gebruikt toodetermine Hallo status van uw Azure-web-functies, werkrollen en virtuele Machines. U kunt ook maken en gebruiken van aangepaste prestatiemeteritems.  

U kunt gegevens van prestatiemeteritems controleren

1. Rechtstreeks op de toepassingshost Hallo met Hallo Prestatiemeter hulpprogramma toegankelijk via Extern bureaublad
2. Met het gebruik van System Center Operations Manager hello Azure Management Pack
3. Diagnostische gegevens overgedragen met andere controleprogramma's die toegang hebben tot Hallo tooAzure opslag. Zie [Store en diagnostische gegevens weergeven in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) voor meer informatie.  

Voor meer informatie over het bewaken van de prestaties van uw toepassing in Hallo Hallo [Azure-portal](http://portal.azure.com/), Zie [hoe tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Voor meer gedetailleerde informatie over het maken van een logboekregistratie en tracering strategie en met behulp van diagnostische gegevens en andere technieken tootroubleshoot problemen en optimaliseren van de Azure-toepassingen, Zie [aanbevolen procedures voor het ontwikkelen van Azure oplossen Toepassingen](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Schakel de bewaking van prestatiemeteritems
Prestatiemeteritems zijn standaard niet ingeschakeld. Uw toepassing of het starten van de taak moet Hallo standaard diagnostics agent tooinclude Hallo specifieke prestatiemeteritems configuration gewenste toomonitor voor elk rolexemplaar wijzigen.

### <a name="performance-counters-available-for-microsoft-azure"></a>Prestatie-items voor Microsoft Azure
Azure biedt een subset van de beschikbare Hallo prestatiemeteritems voor Windows Server, IIS en ASP.NET-stack Hallo. Hallo volgende tabel bevat enkele van de prestatiemeteritems Hallo met name van belang voor Azure-toepassingen.

| Prestatiemeteritem-categorie: Object (exemplaar) | Naam van het meteritem | Naslaginformatie |
| --- | --- | --- |
| .NET CLR-uitzonderingen (*globale*) |# Uitzonderingen veroorzaakt per seconde |Uitzondering-prestatiemeteritems |
| .NET CLR-geheugen (*globale*) |% Tijd in % |Prestatiemeteritems voor geheugen |
| ASP.NET |Toepassing opnieuw wordt gestart |Prestatiemeteritems voor ASP.NET |
| ASP.NET |Uitvoertijd van aanvraag |Prestatiemeteritems voor ASP.NET |
| ASP.NET |Verbroken aanvragen |Prestatiemeteritems voor ASP.NET |
| ASP.NET |Opnieuw gestarte werkprocessen |Prestatiemeteritems voor ASP.NET |
| ASP.NET-toepassingen (**totale**) |Totaal aantal aanvragen |Prestatiemeteritems voor ASP.NET |
| ASP.NET-toepassingen (**totale**) |Aanvragen per seconde |Prestatiemeteritems voor ASP.NET |
| ASP.NET v4.0.30319 |Uitvoertijd van aanvraag |Prestatiemeteritems voor ASP.NET |
| ASP.NET v4.0.30319 |Wachttijd van aanvraag |Prestatiemeteritems voor ASP.NET |
| ASP.NET v4.0.30319 |Huidige aanvragen |Prestatiemeteritems voor ASP.NET |
| ASP.NET v4.0.30319 |Aanvragen in wachtrij |Prestatiemeteritems voor ASP.NET |
| ASP.NET v4.0.30319 |Aanvragen dat is geweigerd |Prestatiemeteritems voor ASP.NET |
| Geheugen |Beschikbare megabytes (MB) |Prestatiemeteritems voor geheugen |
| Geheugen |Toegewezen Bytes |Prestatiemeteritems voor geheugen |
| Processor(_Totaal) |Percentage processortijd |Prestatiemeteritems voor ASP.NET |
| TCPv4 |Verbindingsfouten |TCP-Object |
| TCPv4 |Verbindingen |TCP-Object |
| TCPv4 |Verbindingen opnieuw instellen |TCP-Object |
| TCPv4 |Segmenten verzonden per seconde |TCP-Object |
| Netwerk Interface(*) |Ontvangen bytes per seconde |Netwerkinterface-Object |
| Netwerk Interface(*) |Verzonden bytes per seconde |Netwerkinterface-Object |
| Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2) |Ontvangen bytes per seconde |Netwerkinterface-Object |
| Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2) |Verzonden bytes per seconde |Netwerkinterface-Object |
| Netwerkinterface (Microsoft Virtual Machinebus netwerk Adapter _2) |Totaal aantal bytes per seconde |Netwerkinterface-Object |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Maken en aangepaste prestaties tellers tooyour toepassing toevoegen
Azure support toocreate heeft en aangepaste prestatiemeteritems voor webrollen en werkrollen wijzigen. Hallo tellers mogelijk gebruikte tootrack en monitor toepassingsspecifieke gedrag. U kunt maken en aangepaste categorieën voor prestatiemeteritems en specificaties verwijderen uit een starten van de taak, Webrol of werkrol met verhoogde machtigingen.

> [!NOTE]
> Code die gewijzigd toocustom prestatiemeteritems wordt moet wel verhoogde machtigingen toorun. Als Hallo code in een Webrol of werkrol is, Hallo rol Hallo-tag moet bevatten <Runtime executionContext="elevated" /> hello ServiceDefinition.csdef van de bestandsserver voor Hallo rol tooinitialize goed.
>
>

U kunt aangepaste prestaties teller tooAzure opslag van gegevens met de Hallo diagnostics agent verzenden.

Hallo standaard gegevens van prestatiemeteritems wordt gegenereerd door hello die Azure verwerkt. Aangepaste gegevens van prestatiemeteritems moeten worden gemaakt door de functie- of worker-rol webtoepassing. Zie [prestaties itemtypen](https://msdn.microsoft.com/library/z573042h.aspx) voor informatie over het Hallo typen gegevens die kunnen worden opgeslagen in de aangepaste prestatiemeteritems. Zie [PerformanceCounters voorbeeld](http://code.msdn.microsoft.com/azure/) voor een voorbeeld maakt en stelt u aangepaste prestatiemeteritem-gegevens in een Webrol.

## <a name="store-and-view-performance-counter-data"></a>Gegevens van prestatiemeteritems opslaan en weergeven
Azure in de cache opgeslagen gegevens met andere diagnostische gegevens van prestatiemeteritems. Deze gegevens is beschikbaar voor externe controle terwijl Hallo rolinstantie wordt uitgevoerd met toegang tot extern bureaublad tooview's zoals Prestatiemeter. toopersist hello buiten rolinstantie hello, Hallo diagnostics agent moet gegevensoverdracht Hallo tooAzure gegevensopslag. Hallo maximale grootte van Hallo in de cache opgeslagen gegevens van prestatiemeteritems kan worden geconfigureerd in Hallo diagnostics agent, of wordt mogelijk toobe deel uitmaken van een gedeelde limiet is geconfigureerd voor alle Hallo diagnostische gegevens. Zie voor meer informatie over het instellen van de buffergrootte Hallo [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) en [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Zie [Store en diagnostische gegevens weergeven in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) voor een overzicht van het Hallo-agent tootransfer gegevens tooa opslagaccount voor diagnostische gegevens in te stellen.

Elke geconfigureerde exemplaar van prestatiemeteritem wordt vastgelegd bij een opgegeven samplefrequentie en Hallo door actieve gegevens worden overgedragen toohello storage-account door een geplande aanvraag of een aanvraag voor op aanvraag. Automatische transfers kunnen zo vaak als één keer per minuut worden gepland. Prestatiemeteritemgegevens overgedragen door Hallo diagnostics agent wordt opgeslagen in een tabel WADPerformanceCountersTable, in Hallo storage-account. Deze tabel kan worden geopend en methoden die standaard Azure storage-API worden opgevraagd. Zie [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) voor een voorbeeld van het uitvoeren van query's en gegevens van prestatiemeteritems uit Hallo WADPerformanceCountersTable tabel weergeven.

> [!NOTE]
> Afhankelijk van Hallo diagnostics agent overdracht frequentie en wachtrij latentie, hello meest recente prestatiemeteritemgegevens in Hallo storage-account mogelijk enkele minuten verouderd.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Prestatiemeteritems configuratiebestand diagnostische gegevens inschakelen
Gebruik hello te volgen procedure tooenable-prestatiemeters in uw Azure-toepassing.

## <a name="prerequisites"></a>Vereisten
Deze sectie wordt ervan uitgegaan dat u hebt geïmporteerd Hallo diagnostische monitor in uw toepassing en Hallo diagnostics configuration file tooyour Visual Studio-oplossing (diagnostics.wadcfg en lagere niveaus in de SDK 2.4 of diagnostics.wadcfgx in SDK 2.5 en hoger) toegevoegd. Zie stap 1 en 2 in [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services-dotnet-diagnostics.md)) voor meer informatie.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Stap 1: Verzamelen en opslaan van gegevens van prestatiemeteritems
Nadat u hebt toegevoegd Hallo diagnostics bestand tooyour Visual Studio-oplossing, kunt u Hallo verzameling en de opslag van gegevens van prestatiemeteritems configureren in een Azure-toepassing. Dit wordt gedaan door prestaties tellers toohello diagnostics bestand toe te voegen. Diagnostics-gegevens, prestatiemeteritems, eerst worden verzameld op Hallo-exemplaar. Hallo gegevens vervolgens persistente toohello WADPerformanceCountersTable tabel in hello Azure Table-service, zodat u ook nodig toospecify Hallo storage-account in uw toepassing. Als u uw toepassing lokaal in Hallo Compute-Emulator testen bent, kunt u diagnostische gegevens ook lokaal opslaan in Hallo-Opslagemulator. Voordat u de diagnostics-gegevens opslaat, moet u eerst toohello gaan [Azure-portal](http://portal.azure.com/) en een klassieke opslagaccount maken. Een aanbevolen procedure is toolocate uw opslagaccount in dezelfde geografische locatie als uw Azure-toepassing hello. Door houden hello Azure toepassings- en storage-account zijn in Hallo dezelfde geografische locatie, u betaalt externe bandbreedtekosten voorkomen en de latentie te verminderen.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Prestaties tellers toohello diagnostics bestand toevoegen
Er zijn veel prestatiemeteritems die u kunt gebruiken. Hallo volgende voorbeeld ziet u enkele prestatiemeteritems die worden aanbevolen voor web- en bewaking van worker-rol.

Open Hallo diagnostics-bestand (diagnostics.wadcfg in 2.4 SDK en de onderliggende of diagnostics.wadcfgx in SDK 2.5 en hoger) en Hallo toohello DiagnosticMonitorConfiguration element volgende toevoegen:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

Hallo bufferQuotaInMB kenmerk Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo verzameling gegevenstype (Azure Logboeken, IIS-logboeken, enzovoort). Hallo standaardwaarde is 0. Wanneer Hallo quotum is bereikt, wordt de oudste gegevens Hallo verwijderd naarmate er nieuwe gegevens worden toegevoegd. Hallo som van alle Hallo bufferQuotaInMB eigenschappen moet groter dan Hallo-waarde van Hallo OverallQuotaInMB kenmerk. Zie voor meer informatie over om te bepalen hoeveel opslagruimte zijn vereist voor Hallo verzamelen van diagnostische gegevens, af van de Setup-sectie van Hallo [Best Practices probleemoplossing voor Azure-toepassingen ontwikkelen](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

Hallo scheduledTransferPeriod kenmerk hello-interval tussen de geplande overdrachten van gegevens bevat, afgerond naar toohello dichtstbijzijnde minuut. In de Hallo volgen voorbeelden, wordt deze ingesteld tooPT30M (30 minuten). Instelling Hallo overdracht periode tooa kleine waarde, zoals 1 minuut, zal negatieve invloed hebben op de prestaties van de toepassing in productie, maar is handig als u wilt zien van diagnostische gegevens snel te werken als u wilt testen. Hallo geplande overdracht periode moet klein genoeg tooensure diagnostische gegevens zijn niet op Hallo-exemplaar, maar groot genoeg is dat het heeft geen invloed op prestaties van uw toepassing hello overschreven.

Hallo counterSpecifier kenmerk geeft Hallo prestaties teller toocollect. Hallo sampleRate kenmerk geeft Hallo snelheid waarmee het prestatiemeteritem Hallo moet actieve, in dit geval 30 seconden.

Nadat u hebt toegevoegd Hallo prestatiemeteritems die u toocollect wilt, sla uw wijzigingen toohello diagnostics-bestand. Vervolgens moet u toospecify Hallo storage-account dat Hallo diagnostics-gegevens worden opgeslagen in.

### <a name="specify-hello-storage-account"></a>Hallo storage-account opgeven
toopersist uw diagnostische informatie tooyour Azure Storage-account, moet u een verbindingsreeks in uw serviceconfiguratiebestand (ServiceConfiguration.cscfg).

Voor de Azure SDK 2.5, kan Hallo Storage-Account in Hallo diagnostics.wadcfgx bestand worden opgegeven.

> [!NOTE]
> Deze instructies zijn alleen van toepassing tooAzure SDK 2.4 en lager. Voor de Azure SDK 2.5, kan Hallo Storage-Account in Hallo diagnostics.wadcfgx bestand worden opgegeven.
>
>

tooset hello verbindingsreeksen:

1. Open Hallo ServiceConfiguration.Cloud.cscfg bestand met uw favoriete teksteditor en de set Hallo-verbindingsreeks voor de opslag. Hallo *AccountName* en *AccountKey* waarden zijn gevonden in hello Azure-portal op Hallo storage account dashboard onder toegangstoetsen.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Hallo ServiceConfiguration.Cloud.cscfg bestand opslaan.
3. Hallo ServiceConfiguration.Local.cscfg bestand openen en controleren of UseDevelopmentStorage tootrue is ingesteld.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Nu dat de verbindingsreeksen Hallo zijn ingesteld, wordt uw toepassing opslagaccount voor diagnostische gegevens tooyour bewaard wanneer uw toepassing wordt geïmplementeerd.
4. Opslaan op het project bouwen en implementeren van uw toepassing.

## <a name="step-2-optional-create-custom-performance-counters"></a>Stap 2: (Optioneel) Maak aangepaste prestatiemeteritems
Bovendien toohello vooraf gedefinieerde prestatie-items, kunt u uw eigen aangepaste prestatiemeteritems toomonitor web- of worker rollen toevoegen. Aangepaste prestatiemeteritems kunnen gebruikte tootrack en monitor toepassingsspecifieke gedrag en kan worden gemaakt of verwijderd in een opstarttaak Webrol of een werkrol met verhoogde machtigingen.

Hello Azure diagnostics agent vernieuwt Hallo prestaties teller configuratie uit Hallo .wadcfg bestand een minuut na het starten.  Als u aangepaste prestatiemeteritems in Hallo OnStart-methode maken en uw opstarttaken langer dan een minuut tooexecute duurt, uw aangepaste prestatiemeteritems wordt niet gemaakt wanneer hello Azure Diagnostics agent tooload probeert ze.  In dit scenario ziet u dat Azure Diagnostics correct worden alle diagnostische gegevens, behalve van uw aangepaste prestatiemeteritems vastgelegd.  tooresolve dit probleem Hallo prestatie-items maken in een opstarttaak of verplaatsen werken sommige van uw opstarttaak toohello OnStart-methode na het maken van Hallo prestatiemeteritems.

Volgende stappen toocreate een eenvoudige aangepaste Prestatiemeter '\MyCustomCounterCategory\MyButton1Counter' hello uitvoeren:

1. Open Hallo servicedefinitiebestand (CSDEF) voor uw toepassing.
2. Hallo Runtime element toohello WebRole of WorkerRole element tooallow uitvoeren met verhoogde bevoegdheden toevoegen:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Hallo-bestand opslaan.
4. Open Hallo diagnostics-bestand (diagnostics.wadcfg in 2.4 SDK en de onderliggende of diagnostics.wadcfgx in SDK 2.5 en hoger) en Hallo na toohello DiagnosticMonitorConfiguration toevoegen

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Hallo-bestand opslaan.
6. Hallo aangepaste Prestatiemeteritem-categorie in Hallo OnStart-methode van uw rol maken voordat base wordt aangeroepen. OnStart. Hallo maakt volgende C#-voorbeeld u een aangepaste categorie als deze niet al bestaat:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Hallo-tellers in uw toepassing bijwerken. Hallo voorbeeld van de volgende updates van een aangepaste prestatiemeteritem op Button1_Click gebeurtenissen:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Hallo-bestand opslaan.  

Aangepaste prestatiemeteritemgegevens worden nu door hello Azure diagnostics monitor verzameld.

## <a name="step-3-query-performance-counter-data"></a>Stap 3: De gegevens van prestatiemeteritems opvragen
Als uw toepassing wordt geïmplementeerd en uitgevoerd, Hallo diagnostische monitor gaat verder met het verzamelen van prestatiemeteritems en persistent maken die tooAzure gegevensopslag. U hulpprogramma's zoals Server Explorer gebruiken in Visual Studio [Azure Opslagverkenner](http://azurestorageexplorer.codeplex.com/), of [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) door Cerebrata tooview Hallo prestatiemeteritems van de gegevens in Hallo WADPerformanceCountersTable tabel. U kunt ook programmatisch query service gebruikmaakt van Hallo tabel [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), of [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Hallo volgende C#-voorbeeld ziet u een eenvoudige query op Hallo WADPerformanceCountersTable tabel en Hallo diagnostische gegevens tooa CSV-bestand wordt opgeslagen. Wanneer Hallo-prestatiemeteritems tooa CSV-bestand opgeslagen zijn, kunt u Hallo mogelijkheden in Microsoft Excel of andere hulpprogramma toovisualize Hallo gegevens grafieken. Niet zeker tooadd een verwijzing tooMicrosoft.WindowsAzure.Storage.dll, die is opgenomen in hello Azure SDK voor .NET oktober 2012 en hoger. Hallo-assembly is geïnstalleerde toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version num\ref\-directory.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Entiteiten worden toegewezen tooC #-objecten met behulp van een aangepaste klasse die is afgeleid van **TableEntity**. Hallo volgende code definieert een entiteitsklasse die staat voor een prestatiemeteritem op Hallo **WADPerformanceCountersTable** tabel.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Volgende stappen
[Aanvullende artikelen op Azure Diagnostics weergeven](../azure-diagnostics.md)
