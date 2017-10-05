---
title: Met Elasticsearch als een Service Fabric-toepassingsarchief trace | Microsoft Docs
description: Beschrijft hoe Service Fabric-toepassingen Elasticsearch en Kibana op te slaan, index, en doorzoeken toepassingstraceringen (Logboeken) kunnen gebruiken
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
ms.openlocfilehash: 2d2ceceea131b41ad1a1735aaa2a859d035ab098
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Gebruik Elasticsearch als een tracering van de Service Fabric-toepassing opslaan
## <a name="introduction"></a>Inleiding
Dit artikel wordt beschreven hoe [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) toepassingen kunnen gebruikmaken van **Elasticsearch** en **Kibana** voor opslag voor servertoepassingen trace indexeren en zoeken. [Elasticsearch](https://www.elastic.co/guide/index.html) is een open source, gedistribueerde en schaalbare realtime zoekresultaten en analyse-engine die geschikt zijn voor deze taak. Deze kan worden geïnstalleerd op Windows- en Linux virtuele machines in Microsoft Azure wordt uitgevoerd. Elasticsearch kan efficiënt verwerken *gestructureerde* traceringen geproduceerd met behulp van technologieën zoals **Event Tracing voor Windows (ETW)**.

ETW wordt gebruikt door de Service Fabric-runtime bron diagnostische gegevens (traceringen). Het is de aanbevolen methode voor Service Fabric-toepassingen met hun diagnostische gegevens te bron. Kan gebruikmaken van hetzelfde mechanisme voor correlatie tussen runtime verstrekt en toepassing opgegeven traceringen, en wordt probleemoplossing eenvoudiger. Sjablonen voor service Fabric-project in Visual Studio een logboekregistratie API opnemen (op basis van de .NET **EventSource** klasse) die ETW traceringen standaard verzendt. Voor een algemeen overzicht van Service Fabric-toepassing voor het traceren met behulp van ETW, Zie [controle en diagnose van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Voor de traceringen worden weergegeven in Elasticsearch moeten worden vastgelegd op de knooppunten van het Service Fabric in realtime (terwijl de toepassing wordt uitgevoerd) en verzonden naar een eindpunt Elasticsearch. Er zijn twee belangrijke opties voor het vastleggen van trace:

* **Proces trace vastleggen**  
  De toepassing of preciezer, serviceproces is verantwoordelijk voor het verzenden van de diagnostische gegevens naar de store trace (Elasticsearch).
* **Out of process-trace vastleggen**  
  Een afzonderlijke agent is het vastleggen van traces van de service of meer werkprocessen en ze worden verzonden naar de trace-store.

Hieronder, er wordt beschreven hoe u Elasticsearch op Azure instellen, de professionals bespreken en nadelen voor beide opties vastleggen en wordt uitgelegd hoe u een Service Fabric-service om gegevens te verzenden naar Elasticsearch configureren.

## <a name="set-up-elasticsearch-on-azure"></a>Instellen van Elasticsearch op Azure
De eenvoudigste manier voor het instellen van de service Elasticsearch in Azure is via [ **Azure Resource Manager-sjablonen**](../azure-resource-manager/resource-group-overview.md). Een uitgebreide [Quick Start Azure Resource Manager-sjabloon voor Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) is beschikbaar via de Azure Quickstart-opslagplaats voor sjablonen. Deze sjabloon maakt gebruik van afzonderlijke storage-accounts voor schaaleenheden (groepen van knooppunten). Deze kan ook afzonderlijke client en serverknooppunten met verschillende configuraties en verschillende aantallen gegevensschijven gekoppeld inrichten.

Hier, gebruiken we een andere sjabloon, de zogeheten **ES MultiNode** van de [Azure diagnostische hulpprogramma's voor opslagplaats](https://github.com/Azure/azure-diagnostics-tools). Deze sjabloon is eenvoudiger te gebruiken en een beveiligd door HTTP basisverificatie Elasticsearch-cluster wordt gemaakt. Voordat u doorgaat, download u de opslagplaats vanuit GitHub op uw computer (door de opslagplaats klonen of downloaden van een zipbestand). De sjabloon ES MultiNode bevindt zich in de map met dezelfde naam.

### <a name="prepare-a-machine-to-run-elasticsearch-installation-scripts"></a>Voorbereiden van een machine Elasticsearch installatiescripts uitvoeren
De eenvoudigste manier om het gebruik van de sjabloon ES MultiNode is via een opgegeven Azure PowerShell-script aangeroepen `CreateElasticSearchCluster`. Als u wilt dit script gebruiken, moet u PowerShell-modules en hulpprogramma installeren **openssl**. De laatste is nodig voor het maken van een SSH-sleutel die kan worden gebruikt voor het beheren van uw cluster Elasticsearch op afstand.

`CreateElasticSearchCluster`script is ontworpen voor eenvoudig te gebruiken met de sjabloon ES MultiNode van een Windows-machine. Het is mogelijk de sjabloon wilt gebruiken op een niet-Windows-machine, maar in dit scenario ligt buiten het bereik van dit artikel.

1. Als u dit nog niet hebt ze al hebt geïnstalleerd, installeert u [ **Azure PowerShell-modules**](http://aka.ms/webpi-azps). Wanneer u wordt gevraagd, klikt u op **uitvoeren**, klikt u vervolgens **installeren**. Azure PowerShell 1.3 of hoger is vereist.
2. De **openssl** hulpprogramma is opgenomen in de distributie van [ **Git voor Windows**](http://www.git-scm.com/downloads). Als u dit nog niet hebt gedaan, installeert u [Git voor Windows](http://www.git-scm.com/downloads) nu. (De standaard installatieopties zijn OK).
3. Ervan uitgaande dat Git is geïnstalleerd maar niet is opgenomen in het systeempad bevindt, opent u een Microsoft Azure PowerShell-venster en voer de volgende opdrachten:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Vervang de `<Git installation folder>` met de Git-locatie op uw computer; de standaardwaarde is **'C:\Program Files\Git'**. Noteer de puntkomma aan het begin van het eerste pad.
4. Zorg ervoor dat u bent aangemeld bij Azure (via [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) en dat u het abonnement dat moet worden gebruikt voor het maken van het cluster elastische Search hebt geselecteerd. U kunt controleren of het juiste abonnement is geselecteerd met `Get-AzureRmContext` en `Get-AzureRmSubscription` cmdlets.
5. Als u dit nog niet hebt gedaan, moet u de huidige map wijzigen naar de map ES MultiNode.

### <a name="run-the-createelasticsearchcluster-script"></a>Voer het script CreateElasticSearchCluster
Voordat u het script uitvoert, opent u de `azuredeploy-parameters.json` bestand en controleer of geef waarden op voor de scriptparameters. De volgende parameters zijn beschikbaar:

| Parameternaam | Beschrijving |
| --- | --- |
| dnsNameForLoadBalancerIP |De naam die wordt gebruikt voor het maken van de openbaar zichtbaar DNS-naam voor het cluster elastische zoeken (door het Azure-regio domein toe te voegen aan de opgegeven naam). Als deze parameterwaarde is 'myBigCluster' en de gekozen Azure-regio VS-West, is de resulterende DNS-naam voor het cluster myBigCluster.westus.cloudapp.azure.com. <br /><br />Deze naam fungeert ook als de naam van een basis voor veel artefacten die zijn gekoppeld aan het cluster elastische zoeken, zoals gegevens knooppuntnamen. |
| adminUsername |De naam van de administrator-account voor het beheren van het cluster elastische zoeken (bijbehorende SSH-sleutels worden automatisch gegenereerd). |
| dataNodeCount |Het aantal knooppunten in het cluster elastische zoeken. De huidige versie van het script wordt geen onderscheid gemaakt tussen knooppunten, gegevens en de query. alle knooppunten afspelen beide rollen. Standaard ingesteld op 3 knooppunten. |
| dataDiskSize |De grootte van gegevensschijven (in GB) die voor elk gegevensknooppunt is toegewezen. Elk knooppunt ontvangt 4 gegevensschijven exclusief toegewezen aan elastische Search-service. |
| Regio |De naam van de Azure-regio waar het cluster elastische zoeken moet zich bevinden. |
| esUserName |De gebruikersnaam van de gebruiker die is geconfigureerd voor toegang tot cluster ES (afhankelijk van de basisverificatie voor HTTP). Het wachtwoord is geen onderdeel van het parameterbestand en moet worden opgegeven wanneer `CreateElasticSearchCluster` script wordt aangeroepen. |
| vmSizeDataNodes |De grootte van de virtuele machine van Azure voor de clusterknooppunten elastische zoeken. De standaardwaarde Standard_D2. |

U bent nu klaar om uit te voeren van het script. Geef de volgende opdracht:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

waar 

| De parameternaam script | Beschrijving |
| --- | --- |
| `<es-group-name>` |De naam van de Azure-resourcegroep die alle resources van elastische zoeken cluster bevat. |
| `<azure-region>` |De naam van de Azure-regio waar het cluster elastische zoeken moet worden gemaakt. |
| `<es-password>` |Het wachtwoord voor de gebruiker elastische zoeken. |

> [!NOTE]
> Als u een NullReferenceException van de cmdlet Test-AzureResourceGroup krijgt, u aanmelden bij Azure bent vergeten (`Add-AzureRmAccount`).
> 
> 

Als u krijgt een fout in het script wordt uitgevoerd en u bepalen dat de fout is veroorzaakt door een parameterwaarde verkeerde sjabloon, het parameterbestand corrigeren en het script opnieuw uitgevoerd met een andere Resourcegroepnaam in. U kunt ook opnieuw gebruiken dezelfde naam van de resourcegroep en het script opruimen van de oude heeft door toe te voegen de `-RemoveExistingResourceGroup` parameter voor het aanroepen van het script.

### <a name="result-of-running-the-createelasticsearchcluster-script"></a>Resultaat van het uitvoeren van het script CreateElasticSearchCluster
Nadat u de `CreateElasticSearchCluster` script, de volgende belangrijke artefacten worden gemaakt. In dit voorbeeld gaan we ervan uit dat u 'myBigCluster' hebt gebruikt als de waarde van de `dnsNameForLoadBalancerIP` parameter en of de regio waar u het cluster hebt gemaakt VS-West.

| Artefacten | De naam, locatie en opmerkingen |
| --- | --- |
| SSH-sleutel voor extern beheer |myBigCluster.key-bestand (in de map van waaruit de CreateElasticSearchCluster wordt uitgevoerd). <br /><br />Deze sleutel bestand kan verbinding maken (via het knooppunt admin) en het knooppunt beheer worden gebruikt voor gegevensknooppunten in het cluster. |
| Admin-knooppunt |myBigCluster admin.westus.cloudapp.azure.com <br /><br />Een speciale virtuele machine voor extern beheer van het cluster voor Elasticsearch--het enige dat externe SSH-verbindingen toestaat. Deze wordt uitgevoerd op hetzelfde virtuele netwerk als alle knooppunten van het Elasticsearch, maar kunnen de services Elasticsearch kan niet worden uitgevoerd. |
| Gegevensknooppunten |myBigCluster1... myBigCluster*N* <br /><br />Van gegevensknooppunten die fungeren als Elasticsearch en Kibana services worden uitgevoerd. U kunt verbinding maken via SSH op elk knooppunt, maar alleen via het knooppunt beheer. |
| Elasticsearch cluster |http://myBigCluster.westus.cloudapp.Azure.com/ES/ <br /><br />Het primaire eindpunt voor het cluster Elasticsearch (Let op het achtervoegsel /es). Het is beveiligd met eenvoudige HTTP-verificatie (de referenties zijn de opgegeven esUserName/esPassword parameters van de sjabloon ES MultiNode). Het cluster heeft ook de kop invoegtoepassing geïnstalleerd (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) voor elementaire Clusterbeheer. |
| Kibana-service |http://myBigCluster.westus.cloudapp.Azure.com <br /><br />De service Kibana is ingesteld om gegevens uit het gemaakte Elasticsearch cluster weer te geven. Het is beveiligd door de dezelfde referenties voor verificatie als het cluster zelf. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>In-process versus out of process-trace vastleggen
In de inleiding gezegd twee manieren om diagnostische gegevens te verzamelen: in-process- en out-of-process. Elk heeft sterke en zwakke punten.

Voordelen van de **proces trace vastleggen** omvatten:

1. *Eenvoudige configuratie en implementatie*
   
   * De configuratie van verzamelen van diagnostische gegevens net is onderdeel van de configuratie van de toepassing. Het is gemakkelijk altijd het ' om synchroon te houden "met de rest van de toepassing.
   * Configuratie van per toepassing of per-service is eenvoudig haalbare.
   * Out of process-trace vastleggen moet meestal een afzonderlijke implementatie en configuratie van de diagnostische agent, die een extra beheertaak en een mogelijke oorzaak van fouten is. De agent op bepaalde technologie kunt vaak slechts één exemplaar van de agent per virtuele machine (knooppunt). Dit betekent dat de configuratie voor het verzamelen van diagnostische configuratie wordt gedeeld door alle toepassingen en services die op dat knooppunt worden uitgevoerd.
2. *Flexibiliteit*
   
   * De toepassing de gegevens kan verzenden, waar nodig om te gaan, zolang er is een clientbibliotheek die ondersteuning biedt voor het opslagsysteem van gerichte gegevens. Nieuwe sinks kunnen worden toegevoegd naar wens.
   * Complexe regels voor het vastleggen, filteren en samenvoegen van gegevens kunnen worden geïmplementeerd.
   * Het vastleggen van een out-of-process trace wordt vaak beperkt door de gegevens put die ondersteuning biedt voor de agent. Sommige agents worden uitgebreid.
3. *Toegang tot interne toepassingsgegevens en -context*
   
   * Het diagnostische subsysteem uitvoering binnen het proces van de toepassing/service kan eenvoudig de traceringen met contextafhankelijke informatie verbeteren.
   * In de out-of-process-methode, moet de gegevens worden verzonden naar een agent via een mechanisme voor communicatie tussen processen, zoals Event Tracing voor Windows. Dit mechanisme kan aanvullende beperkingen opleggen.

Voordelen van de **out of process-tracering vast te leggen** omvatten:

1. *De mogelijkheid voor het bewaken van de toepassing en verzamelen crashdumps*
   
   * Tracering in-process vastleggen mogelijk mislukt als de toepassing niet kan worden gestart of is vastgelopen. Een onafhankelijke agent heeft een veel grotere kans van het vastleggen van cruciaal belang voor probleemoplossing.<br /><br />
2. *Vervaldatum, robuustheid en beproefde prestaties*
   
   * Een agent die is ontwikkeld door een leverancier platform (zoals Microsoft Azure Diagnostics-agent) is onderworpen aan strengere testen en strijd te beperken.
   * Met de in proces tracering vast te leggen, extra op worden gelet om ervoor te zorgen dat de activiteit van het verzenden van diagnostische gegevens van een toepassingsproces niet leiden tot met de belangrijkste taken van de toepassing problemen of problemen met timing- of Prestatieweergave veroorzaken. Een agent onafhankelijk uitgevoerd minder gevoelig is voor deze problemen en is speciaal ontworpen voor het beperken van de invloed ervan op het systeem.

Het is mogelijk om te combineren en profiteren van beide benaderingen. Inderdaad, mogelijk de beste oplossing voor veel toepassingen.

Hier, gebruiken we de **Microsoft.Diagnostic.Listeners bibliotheek** en de in-process-tracering vastleggen om gegevens te verzenden vanuit een Service Fabric-toepassing naar een cluster Elasticsearch.

## <a name="use-the-listeners-library-to-send-diagnostic-data-to-elasticsearch"></a>Gebruik van de bibliotheek Listeners diagnostische gegevens verzenden naar Elasticsearch
De bibliotheek Microsoft.Diagnostic.Listeners maakt deel uit van de voorbeeldtoepassing Service Fabric PartyCluster. Om deze te gebruiken:

1. Download [het voorbeeld PartyCluster](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) vanuit GitHub.
2. De projecten Microsoft.Diagnostics.Listeners en Microsoft.Diagnostics.Listeners.Fabric (hele mappen) kopiëren vanuit de map van de steekproef PartyCluster naar de oplossingenmap van de toepassing die u moet de gegevens verzenden naar Elasticsearch.
3. Open de doel-oplossing, met de rechtermuisknop op het knooppunt van de oplossing in Solution Explorer en kiest u **bestaand Project toevoegen**. Het project Microsoft.Diagnostics.Listeners toevoegen aan de oplossing. Herhaal dezelfde voor het project Microsoft.Diagnostics.Listeners.Fabric.
4. Project een verwijzing van uw service-projecten toevoegen aan de twee projecten toegevoegd. (Elke service die u moet gegevens verzenden naar Elasticsearch moet verwijzen naar Microsoft.Diagnostics.EventListeners en Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Projectverwijzingen aan Microsoft.Diagnostics.EventListeners en Microsoft.Diagnostics.EventListeners.Fabric tapewisselaars][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Service Fabric algemene beschikbaarheid release en Microsoft.Diagnostics.Tracing Nuget-pakket
Toepassingen die zijn gemaakt met de release van Service Fabric algemene beschikbaarheid (2.0.135, en met 31 maart 2016 wordt uitgebracht) doel **.NET Framework 4.5.2**. Deze versie is de hoogste versie van .NET Framework ondersteund door Azure op het moment van de GA-release. Deze versie van het framework helaas beschikt niet over bepaalde EventListener APIs die de bibliotheek Microsoft.Diagnostics.Listeners nodig heeft. Omdat nauw EventSource (het onderdeel dat de basis vormt van de logboekregistratie van API's in de Fabric-toepassingen) en EventListener zijn gekoppeld, moet elk project dat gebruikmaakt van de bibliotheek Microsoft.Diagnostics.Listeners een alternatieve implementatie van EventSource gebruiken. Deze implementatie wordt geleverd door de **Microsoft.Diagnostics.Tracing Nuget-pakket**, opgestelde door Microsoft. Het pakket is volledig achterwaarts compatibel met EventSource opgenomen in het kader, dus er zijn geen codewijzigingen mag alleen waarnaar wordt verwezen naamruimte wijzigingen nodig.

Om te starten met de Microsoft.Diagnostics.Tracing-implementatie van de klasse EventSource, volg deze stappen voor elk serviceproject dat u moet gegevens verzenden naar Elasticsearch:

1. Met de rechtermuisknop op de service-project en kies **Nuget-pakketten beheren**.
2. Overschakelen naar de pakketbron nuget.org (indien deze nog niet is geselecteerd) en zoek naar '**Microsoft.Diagnostics.Tracing**'.
3. Installeer de `Microsoft.Diagnostics.Tracing.EventSource` -pakket (en de bijbehorende afhankelijkheden).
4. Open de **ServiceEventSource.cs** of **ActorEventSource.cs** bestand in uw serviceproject en vervang de `using System.Diagnostics.Tracing` richtlijn boven op het bestand met de `using Microsoft.Diagnostics.Tracing` richtlijn.

Deze stappen worden niet nodig eenmaal de **.NET Framework 4.6** wordt ondersteund door Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Elasticsearch listener instantiëring en configuratie
De laatste stap voor het verzenden van diagnostische gegevens naar Elasticsearch is geen exemplaar maken van `ElasticSearchListener` en configureer deze met Elasticsearch verbindingsgegevens. De listener worden automatisch alle gebeurtenissen geregistreerd die zijn gegenereerd via EventSource klassen die zijn gedefinieerd in het serviceproject. Het moet actief zijn tijdens de levensduur van de service, zodat de beste plaats om deze te maken in de code van de initialisatie van de service. De van de initialisatiecode voor een stateless service kan uitzien na de benodigde wijzigingen (toevoegingen die zijn uiteengezet in opmerkingen die beginnen met `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add the following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is the entry point of the service host process.
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

                // The ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name to a .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of the class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that the ElasticSearchListner instance is not garbage-collected prematurely
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

Elasticsearch verbindingsgegevens moeten worden geplaatst in een aparte sectie in het configuratiebestand van de service (**PackageRoot\Config\Settings.xml**). De naam van de sectie moet overeenkomen met de waarde die is doorgegeven aan de `FabricConfigurationProvider` -constructor aan, bijvoorbeeld:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
De waarden van `serviceUri`, `userName` en `password` parameters overeenkomen met de Elasticsearch cluster eindpuntadres, Elasticsearch gebruikersnaam en wachtwoord, respectievelijk. `indexNamePrefix`is het voorvoegsel voor Elasticsearch indexen; de bibliotheek Microsoft.Diagnostics.Listeners maakt dagelijks een nieuwe index voor de gegevens.

### <a name="verification"></a>Verificatie
Dat is alles. Nu wanneer de service wordt uitgevoerd, wordt er gestart traceringen verzenden naar de Elasticsearch-service dat is opgegeven in de configuratie. U kunt controleren of dit door het openen van de UI Kibana die zijn gekoppeld aan de doelinstantie Elasticsearch. In ons voorbeeld is het adres van de pagina http://myBigCluster.westus.cloudapp.azure.com/. Controleer of de geïndexeerd met het voorvoegsel van de gekozen voor de `ElasticSearchListener` exemplaar inderdaad zijn gemaakt en gevuld met gegevens.

![Kibana tonen PartyCluster toepassingsgebeurtenissen][2]

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over het diagnosticeren en controleren van een Service Fabric-service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
