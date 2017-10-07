---
title: aaaUsing Elasticsearch als een Service Fabric-toepassingsarchief trace | Microsoft Docs
description: Beschrijft hoe Service Fabric-toepassingen kunnen gebruiken Elasticsearch en Kibana toostore, index en zoekmogelijkheid via toepassingstraceringen (Logboeken)
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Gebruik Elasticsearch als een tracering van de Service Fabric-toepassing opslaan
## <a name="introduction"></a>Inleiding
Dit artikel wordt beschreven hoe [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) toepassingen kunnen gebruikmaken van **Elasticsearch** en **Kibana** voor opslag voor servertoepassingen trace indexeren en zoeken. [Elasticsearch](https://www.elastic.co/guide/index.html) is een open source, gedistribueerde en schaalbare realtime zoekresultaten en analyse-engine die geschikt zijn voor deze taak. Deze kan worden geïnstalleerd op Windows- en Linux virtuele machines in Microsoft Azure wordt uitgevoerd. Elasticsearch kan efficiënt verwerken *gestructureerde* traceringen geproduceerd met behulp van technologieën zoals **Event Tracing voor Windows (ETW)**.

ETW wordt gebruikt door de Service Fabric-runtime toosource diagnostische gegevens (traceringen). Is Hallo aanbevolen methode voor het Service Fabric-toepassingen toosource hun diagnostische gegevens te. Met behulp van hetzelfde mechanisme voor correlatie tussen runtime verstrekt en toepassing opgegeven traceringen, en wordt probleemoplossing eenvoudiger kunt Hallo. Sjablonen voor service Fabric-project in Visual Studio een logboekregistratie API opnemen (op basis van Hallo .NET **EventSource** klasse) die ETW traceringen standaard verzendt. Voor een algemeen overzicht van Service Fabric-toepassing voor het traceren met behulp van ETW, Zie [controle en diagnose van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Voor Hallo traceringen tooshow omhoog in Elasticsearch moeten ze toobe vastgelegd op Hallo Service Fabric clusterknooppunten in realtime (tijdens het Hallo-toepassing wordt uitgevoerd) en tooan Elasticsearch eindpunt verzonden. Er zijn twee belangrijke opties voor het vastleggen van trace:

* **Proces trace vastleggen**  
  Hallo toepassings- of preciezer, serviceproces is verantwoordelijk voor het verzenden van Hallo diagnostische gegevens toohello trace store (Elasticsearch).
* **Out of process-trace vastleggen**  
  Een afzonderlijke agent is het vastleggen van traces van serviceproces Hallo of processen en ze toohello trace store te sturen.

Hierna beschreven hoe tooset up Elasticsearch in Azure, bespreken Hallo-professionals en nadelen voor beide opties vastleggen en wordt uitgelegd hoe een Service Fabric tooconfigure toosend gegevens tooElasticsearch service.

## <a name="set-up-elasticsearch-on-azure"></a>Instellen van Elasticsearch op Azure
Hallo meest directe manier tooset hello Elasticsearch service in Azure is via [ **Azure Resource Manager-sjablonen**](../azure-resource-manager/resource-group-overview.md). Een uitgebreide [Quick Start Azure Resource Manager-sjabloon voor Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) is beschikbaar via de Azure Quickstart-opslagplaats voor sjablonen. Deze sjabloon maakt gebruik van afzonderlijke storage-accounts voor schaaleenheden (groepen van knooppunten). Deze kan ook afzonderlijke client en serverknooppunten met verschillende configuraties en verschillende aantallen gegevensschijven gekoppeld inrichten.

Hier, gebruiken we een andere sjabloon, de zogeheten **ES MultiNode** van Hallo [Azure diagnostische hulpprogramma's voor opslagplaats](https://github.com/Azure/azure-diagnostics-tools). Deze sjabloon is eenvoudiger toouse en een beveiligd door HTTP basisverificatie Elasticsearch-cluster wordt gemaakt. Voordat u doorgaat, downloaden Hallo opslagplaats GitHub tooyour machine (met de Hallo opslagplaats klonen of downloaden van een zipbestand). Hallo ES MultiNode sjabloon bevindt zich in de map Hallo Hello dezelfde naam.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Voorbereiden van een machine toorun Elasticsearch installatiescripts
Hallo gemakkelijkste manier toouse Hallo ES MultiNode sjabloon is via een opgegeven Azure PowerShell-script aangeroepen `CreateElasticSearchCluster`. toouse dit script, moet u tooinstall PowerShell-modules en hulpprogramma **openssl**. Hallo laatstgenoemde is nodig voor het maken van een SSH-sleutel die gebruikt tooadminister worden kan uw cluster Elasticsearch op afstand.

`CreateElasticSearchCluster`script is ontworpen voor gebruiksgemak Hallo ES MultiNode sjabloon van een Windows-machine. Het is mogelijk toouse Hallo sjabloon op een niet-Windows-machine, maar in dit scenario ligt buiten bereik Hallo van dit artikel.

1. Als u dit nog niet hebt ze al hebt geïnstalleerd, installeert u [ **Azure PowerShell-modules**](http://aka.ms/webpi-azps). Wanneer u wordt gevraagd, klikt u op **uitvoeren**, klikt u vervolgens **installeren**. Azure PowerShell 1.3 of hoger is vereist.
2. Hallo **openssl** hulpprogramma is opgenomen in de distributie van Hallo [ **Git voor Windows**](http://www.git-scm.com/downloads). Als u dit nog niet hebt gedaan, installeert u [Git voor Windows](http://www.git-scm.com/downloads) nu. (Hallo standaard installatieopties zijn OK).
3. Ervan uitgaande dat Git is geïnstalleerd maar niet zijn opgenomen in het systeempad hello, een Microsoft Azure PowerShell-venster openen en Voer Hallo volgende opdrachten uit:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Vervang Hallo `<Git installation folder>` met Git-locatie op uw computer; Hallo Hallo standaardwaarde is **'C:\Program Files\Git'**. Houd er rekening mee Hallo puntkomma aan Hallo begin van de eerste Hallo-pad.
4. Zorg ervoor dat u bent aangemeld op tooAzure (via [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) en toocreate uw cluster elastische zoeken die u hebt geselecteerd dat Hallo-abonnement dat moet worden gebruikt. U kunt controleren of het juiste abonnement is geselecteerd met `Get-AzureRmContext` en `Get-AzureRmSubscription` cmdlets.
5. Als u dit nog niet hebt gedaan, wijzigt u Hallo huidige toohello ES MultiNode map.

### <a name="run-hello-createelasticsearchcluster-script"></a>Hallo CreateElasticSearchCluster script uitvoeren
Voordat u Hallo script uitvoert, open Hallo `azuredeploy-parameters.json` bestand en controleer of geef waarden op voor de scriptparameters Hallo. Hallo volgende parameters zijn beschikbaar:

| Parameternaam | Beschrijving |
| --- | --- |
| dnsNameForLoadBalancerIP |Hallo-naam die is gebruikt toocreate Hallo openbaar zichtbaar DNS-naam voor Hallo elastische zoeken cluster (door toe te voegen hello Azure-regio toohello opgegeven domeinnaam). Als deze parameterwaarde is 'myBigCluster' Hallo gekozen Azure-regio VS-West is, is Hallo resulterende DNS-naam voor de cluster Hallo myBigCluster.westus.cloudapp.azure.com. <br /><br />Deze naam fungeert ook als de naam van een basis voor veel artefacten die zijn gekoppeld aan Hallo elastische zoeken cluster, zoals gegevens knooppuntnamen. |
| adminUsername |Hallo-naam van Hallo administrator-account voor het beheren van Hallo elastische zoeken cluster (bijbehorende SSH-sleutels worden automatisch gegenereerd). |
| dataNodeCount |Hallo aantal knooppunten in cluster van Hallo elastische zoeken. huidige versie van script Hallo Hallo maakt geen onderscheid tussen knooppunten, gegevens en de query. alle knooppunten afspelen beide rollen. Standaardwaarden too3 knooppunten. |
| dataDiskSize |Hallo grootte van gegevensschijven (in GB) die voor elk gegevensknooppunt is toegewezen. Elk knooppunt ontvangt 4 gegevensschijven, exclusief toegewezen tooElastic Search-service. |
| Regio |Hallo-naam van de Azure-regio waar Hallo elastische zoeken cluster moet zich bevinden. |
| esUserName |Hallo gebruikersnaam van Hallo-gebruiker die is geconfigureerd toohave toegang tooES cluster (onderwerp tooHTTP basisverificatie). Hallo wachtwoord maakt geen deel uit van parameterbestand en moet worden opgegeven wanneer `CreateElasticSearchCluster` script wordt aangeroepen. |
| vmSizeDataNodes |Hallo grootte van de virtuele machine van Azure voor de clusterknooppunten elastische zoeken. Standaardwaarden tooStandard_D2. |

U bent nu klaar toorun Hallo script. Probleem Hallo volgende opdracht:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

waar 

| De parameternaam script | Beschrijving |
| --- | --- |
| `<es-group-name>` |Hallo-naam van hello Azure-resourcegroep die alle resources van elastische zoeken cluster bevat. |
| `<azure-region>` |Hallo-naam van hello Azure-regio waar Hallo elastische zoeken cluster moet worden gemaakt. |
| `<es-password>` |Hallo-wachtwoord voor gebruiker Hallo-elastische zoeken. |

> [!NOTE]
> Als u een NullReferenceException van de cmdlet Test-AzureResourceGroup hello krijgt, hebt u toolog op tooAzure vergeten (`Add-AzureRmAccount`).
> 
> 

Als u een fout krijgt van het Hallo-script wordt uitgevoerd en u bepalen dat Hallo-fout is veroorzaakt door een onjuiste sjabloon parameterwaarde, Hallo parameterbestand corrigeren en Hallo script opnieuw uitgevoerd met een andere Resourcegroepnaam in. U kunt ook opnieuw gebruiken dezelfde Resourcegroepnaam Hallo en Hallo script opschonen Hallo oude hebben door toe te voegen Hallo `-RemoveExistingResourceGroup` parameter toohello script aanroepen.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Resultaat van het Hallo CreateElasticSearchCluster script uitvoeren
Na het uitvoeren van Hallo `CreateElasticSearchCluster` script, volgen de belangrijkste artefacten hello wordt gemaakt. In dit voorbeeld gaan we ervan uit dat u 'myBigCluster' hebt gebruikt als de waarde Hallo Hallo `dnsNameForLoadBalancerIP` parameter en dat Hallo-regio waar u Hallo-cluster gemaakt is VS-West.

| Artefacten | De naam, locatie en opmerkingen |
| --- | --- |
| SSH-sleutel voor extern beheer |myBigCluster.key-bestand (in de map Hallo van welke Hallo CreateElasticSearchCluster wordt uitgevoerd). <br /><br />Bestand met deze sleutel kan worden gebruikt tooconnect toohello admin knooppunt en (via Hallo beheerder knooppunt) toodata knooppunten in Hallo-cluster. |
| Admin-knooppunt |myBigCluster admin.westus.cloudapp.azure.com <br /><br />Een speciale virtuele machine voor extern beheer van het cluster voor Elasticsearch--Hallo slechts één waarmee externe SSH-verbindingen. Deze wordt uitgevoerd op Hallo hetzelfde virtuele netwerk als alle clusterknooppunten van Hallo Elasticsearch, maar biedt niet alle Elasticsearch-services worden uitgevoerd. |
| Gegevensknooppunten |myBigCluster1... myBigCluster*N* <br /><br />Van gegevensknooppunten die fungeren als Elasticsearch en Kibana services worden uitgevoerd. U kunt verbinding maken via SSH tooeach knooppunt, maar alleen via Hallo beheerder knooppunt. |
| Elasticsearch cluster |http://myBigCluster.westus.cloudapp.Azure.com/ES/ <br /><br />Hallo primaire eindpunt voor Hallo Elasticsearch cluster (Opmerking Hallo /es achtervoegsel). Het is beveiligd met een eenvoudige HTTP-verificatie (Hallo referenties werden Hallo esUserName/esPassword parameters van de sjabloon Hallo ES MultiNode opgegeven). Hallo-cluster heeft ook Hallo head invoegtoepassing geïnstalleerd (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) voor het beheer van basiscluster. |
| Kibana-service |http://myBigCluster.westus.cloudapp.Azure.com <br /><br />Hallo Kibana-service is tooshow gegevens instellen van Hallo Elasticsearch cluster hebt gemaakt. Deze wordt beveiligd door Hallo dezelfde verificatiereferenties als Hallo cluster zelf. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>In-process versus out of process-trace vastleggen
In het Hallo-inleiding gezegd twee manieren om diagnostische gegevens te verzamelen: in-process- en out-of-process. Elk heeft sterke en zwakke punten.

Voordelen van Hallo **proces trace vastleggen** omvatten:

1. *Eenvoudige configuratie en implementatie*
   
   * Hallo-configuratie van verzamelen van diagnostische gegevens net is onderdeel van de configuratie van de toepassing hello. Het is gemakkelijk tooalways Houd deze 'synchroon' Hello rest van de toepassing hello.
   * Configuratie van per toepassing of per-service is eenvoudig haalbare.
   * Out of process-trace vastleggen moet meestal een afzonderlijke implementatie en configuratie van Hallo diagnostische agent, die een extra beheertaak en een mogelijke oorzaak van fouten is. Hallo bepaalde agent technologie kunnen vaak slechts één exemplaar van de agent Hallo per virtuele machine (knooppunt). Dit betekent dat de configuratie voor de verzameling van diagnostische configuratie Hallo Hallo wordt gedeeld door alle toepassingen en services die op dat knooppunt worden uitgevoerd.
2. *Flexibiliteit*
   
   * Hallo-toepassing kunt hello gegevens verzenden waar het toogo, moet, zolang er is een clientbibliotheek die ondersteuning biedt voor systeem voor gegevensopslag Hallo gericht. Nieuwe sinks kunnen worden toegevoegd naar wens.
   * Complexe regels voor het vastleggen, filteren en samenvoegen van gegevens kunnen worden geïmplementeerd.
   * Het vastleggen van een out-of-process trace wordt vaak beperkt door Hallo gegevens put die Hallo agent ondersteunt. Sommige agents worden uitgebreid.
3. *Toegang toointernal toepassingsgegevens en -context*
   
   * Hallo diagnostische subsysteem uitvoering binnen Hallo toepassing/service-proces kan eenvoudig hello traceringen met contextafhankelijke informatie verbeteren.
   * In Hallo out of process-methode, moet op Hallo gegevens tooan agent via een mechanisme voor communicatie tussen processen, zoals Event Tracing for Windows worden verzonden. Dit mechanisme kan aanvullende beperkingen opleggen.

Voordelen van Hallo **out of process-tracering vast te leggen** omvatten:

1. *Hallo mogelijkheid toomonitor toepassing hello en crashdumps verzamelen*
   
   * Tracering in-process vastleggen mogelijk mislukt als de toepassing hello toostart mislukt of is vastgelopen. Een onafhankelijke agent heeft een veel grotere kans van het vastleggen van cruciaal belang voor probleemoplossing.<br /><br />
2. *Vervaldatum, robuustheid en beproefde prestaties*
   
   * Een agent die is ontwikkeld door een leverancier platform (zoals Microsoft Azure Diagnostics-agent) is onderwerp toorigorous testen en strijd te beperken.
   * Met de in proces tracering vast te leggen, moet nauwkeurig tooensure dat Hallo activiteit van het verzenden van diagnostische gegevens van een toepassingsproces niet leiden tot met de belangrijkste taken van de toepassing hello problemen of problemen met timing- of Prestatieweergave veroorzaken. Een agent onafhankelijk uitgevoerd is minder gevoelig toothese problemen en is speciaal ontworpen toolimit het effect op Hallo-systeem.

Het is mogelijk toocombine en voordelen van beide benaderingen. Inderdaad, mogelijk de beste oplossing Hallo voor veel toepassingen.

Hier, gebruiken we Hallo **Microsoft.Diagnostic.Listeners bibliotheek** en Hallo in-process trace het vastleggen van gegevens uit een cluster Service Fabric-toepassing tooan Elasticsearch toosend.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Hallo-Listeners bibliotheek toosend diagnostische gegevens tooElasticsearch gebruiken
Hallo Microsoft.Diagnostic.Listeners bibliotheek maakt deel uit van de voorbeeldtoepassing Service Fabric PartyCluster. toouse het:

1. Download [hello PartyCluster voorbeeld](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) vanuit GitHub.
2. Hallo Microsoft.Diagnostics.Listeners en Microsoft.Diagnostics.Listeners.Fabric projecten (hele mappen) kopiëren van Hallo PartyCluster voorbeeld toohello oplossingenmap van Hallo-toepassing die toosend Hallo gegevens tooElasticsearch moet .
3. Open Hallo doel oplossing, met de rechtermuisknop op Hallo oplossing knooppunt in Hallo Solution Explorer en kiest u **bestaand Project toevoegen**. Hallo Microsoft.Diagnostics.Listeners project toohello oplossing toevoegen. Herhaal Hallo dezelfde voor Hallo Microsoft.Diagnostics.Listeners.Fabric project.
4. Voeg een projectverwijzing van uw projecten toohello twee toegevoegde serviceprojecten. (Elke service die toosend gegevens tooElasticsearch moet moet verwijzen naar Microsoft.Diagnostics.EventListeners en Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Project verwijst naar tooMicrosoft.Diagnostics.EventListeners en Microsoft.Diagnostics.EventListeners.Fabric bibliotheken][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Service Fabric algemene beschikbaarheid release en Microsoft.Diagnostics.Tracing Nuget-pakket
Toepassingen die zijn gemaakt met de release van Service Fabric algemene beschikbaarheid (2.0.135, en met 31 maart 2016 wordt uitgebracht) doel **.NET Framework 4.5.2**. Deze versie is de hoogste versie Hallo Hallo .NET Framework ondersteund door Azure bij Hallo Hallo GA-release. Deze versie van framework Hallo helaas beschikt niet over bepaalde EventListener APIs die Hallo Microsoft.Diagnostics.Listeners bibliotheek nodig heeft. Omdat nauw EventSource (Hallo-component die Hallo basis vormt van logboekregistratie van API's in de Fabric-toepassingen) en EventListener zijn gekoppeld, moet elk project dat gebruikmaakt van Hallo Microsoft.Diagnostics.Listeners bibliotheek een alternatieve implementatie van gebruiken EventSource. Deze implementatie wordt geleverd door Hallo **Microsoft.Diagnostics.Tracing Nuget-pakket**, opgestelde door Microsoft. Hallo-pakket is volledig achterwaarts compatibel met EventSource opgenomen in het Hallo-framework, dus geen codewijzigingen mag alleen waarnaar wordt verwezen naamruimte wijzigingen nodig.

toostart met Hallo Microsoft.Diagnostics.Tracing implementatie van Hallo EventSource klasse, als volgt te werk voor elk serviceproject dat toosend gegevens tooElasticsearch moet:

1. Met de rechtermuisknop op het Hallo-service-project en kies **Nuget-pakketten beheren**.
2. Overschakelen toohello nuget.org pakketbron (indien deze nog niet is geselecteerd) en zoek naar '**Microsoft.Diagnostics.Tracing**'.
3. Hallo installeren `Microsoft.Diagnostics.Tracing.EventSource` pakket (en de bijbehorende afhankelijkheden).
4. Open Hallo **ServiceEventSource.cs** of **ActorEventSource.cs** bestand in uw serviceproject en vervang Hallo `using System.Diagnostics.Tracing` richtlijn boven op het Hallo-bestand met de Hallo `using Microsoft.Diagnostics.Tracing` richtlijn.

Deze stappen worden niet nodig eenmaal Hallo **.NET Framework 4.6** wordt ondersteund door Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Elasticsearch listener instantiëring en configuratie
Hallo laatste stap voor het verzenden van diagnostische gegevens tooElasticsearch is toocreate een exemplaar van `ElasticSearchListener` en configureer deze met Elasticsearch verbindingsgegevens. Hallo-listener worden automatisch alle gebeurtenissen geregistreerd die zijn gegenereerd via EventSource klassen die zijn gedefinieerd in het Hallo-serviceproject. Moet toobe actief is tijdens de levensduur Hallo van Hallo-service, zodat Hallo aanbevolen toocreate in Hallo initialisatie servicecode plaatsen. Hallo initialisatie van de code voor een stateless service kan uitzien na de benodigde wijzigingen hello (toevoegingen die zijn uiteengezet in opmerkingen die beginnen met `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Elasticsearch verbindingsgegevens moeten worden geplaatst in een aparte sectie in het serviceconfiguratiebestand hello (**PackageRoot\Config\Settings.xml**). Hallo-naam van de sectie Hallo moet overeenkomen met toohello waarde doorgegeven toohello `FabricConfigurationProvider` -constructor aan, bijvoorbeeld:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
waarden van Hallo `serviceUri`, `userName` en `password` parameters toohello Elasticsearch cluster eindpuntadres Elasticsearch gebruikersnaam en wachtwoord, respectievelijk overeenkomen. `indexNamePrefix`Hallo-voorvoegsel voor Elasticsearch indexen; Hallo Microsoft.Diagnostics.Listeners bibliotheek maakt dagelijks een nieuwe index voor de gegevens.

### <a name="verification"></a>Verificatie
Dat is alles. Nu wanneer Hallo-service wordt uitgevoerd, begint traceringen toohello Elasticsearch service die is opgegeven in configuratie Hallo verzenden. U kunt dit controleren door openen Hallo die kibana UI Hallo Elasticsearch doelexemplaar gekoppeld. In ons voorbeeld is het adres pagina Hallo http://myBigCluster.westus.cloudapp.azure.com/. Controleer of de geïndexeerd met Hallo voorvoegsel voor Hallo gekozen `ElasticSearchListener` exemplaar inderdaad zijn gemaakt en gevuld met gegevens.

![Kibana tonen PartyCluster toepassingsgebeurtenissen][2]

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over het diagnosticeren en controleren van een Service Fabric-service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
