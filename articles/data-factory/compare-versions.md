---
title: Versies 1 en 2 van Azure Data Factory vergelijken | Microsoft Docs
description: In dit artikel worden versies 1 en 2 van Azure Data Factory vergeleken.
services: data-factory
documentationcenter: 
author: kromerm
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/24/2018
ms.author: makromer
ms.openlocfilehash: 83065e6cacd784a3914cfac3ff2552a712688366
ms.sourcegitcommit: 79683e67911c3ab14bcae668f7551e57f3095425
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/25/2018
---
# <a name="compare-azure-data-factory-v1-and-v2"></a>Versies 1 en 2 van Azure Data Factory vergelijken
In dit artikel wordt versie 2 (V2) van Azure Data Factory vergeleken met versie 1 (V1). Zie voor meer informatie over V1 [Inleiding tot Azure Data Factory](v1/data-factory-introduction.md). Zie voor meer informatie over V2 [Inleiding tot Data Factory (V2 - preview)](introduction.md).

## <a name="feature-comparison"></a>Vergelijking van functies
In de volgende tabel worden de functies van V1 en V2 vergeleken. 

| Functie | Versie 1 | Versie 2 | 
| ------- | --------- | --------- | 
| Gegevenssets | Een benoemde weergave van gegevens met een verwijzing naar de gegevens die u als in- en uitvoer wilt gebruiken in uw activiteiten. Met gegevenssets worden gegevens binnen andere gegevensarchieven geïdentificeerd, waaronder tabellen, bestanden, mappen en documenten. Een Azure Blob-gegevensset benoemt bijvoorbeeld de blobcontainer en -map in de Azure Blob-opslag van waaruit de activiteit de gegevens moet lezen.<br/><br/>**Beschikbaarheid** definieert het segmenteringsmodel voor het verwerkingsvenster voor de gegevensset (bijvoorbeeld elk uur, dagelijks, enzovoort). | In V2 zijn de gegevenssets dezelfde. U hoeft echter geen **beschikbaarheidsschema's** voor gegevenssets te definiëren. U kunt een triggerbron definiëren waarmee pijplijnen kunnen worden gepland op basis van een klokplannermodel. Zie [Triggers](concepts-pipeline-execution-triggers.md#triggers) en [Gegevenssets](concepts-datasets-linked-services.md) voor meer informatie. | 
| Gekoppelde services | Gekoppelde services zijn te vergelijken met verbindingsreeksen, die de verbindingsinformatie bevatten die Data Factory nodig heeft om verbinding te maken met externe bronnen. | Gekoppelde services zijn hetzelfde als in Data Factory V1, maar met een nieuwe **connectVia**-eigenschap voor het gebruik van de Data Factory V2 Integration Runtime-rekenomgeving. Zie [Integration Runtime in Azure Data Factory](concepts-integration-runtime.md) en [Eigenschappen van de gekoppelde service voor Azure Blob-opslag](connector-azure-blob-storage.md#linked-service-properties) voor meer informatie. |
| Pijplijnen | Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn is een logische groep activiteiten die samen een taak uitvoeren. U gebruikt startTime, endTime en isPaused voor het plannen en uitvoeren van pijplijnen. | Pijplijnen zijn groepen met activiteiten die op gegevens moeten worden uitgevoerd. Het plannen van activiteiten in de pijplijn is echter gescheiden in nieuwe triggerbronnen. In Data Factory V2 kunt u zich pijplijnen voorstellen als 'werkstroomeenheden' die u afzonderlijk via triggers plant. <br/><br/>In Data Factory V2 hebben pijplijnen geen 'vensters' voor uitvoering in de tijd. De concepten startTime, endTime en isPaused van Data Factory V1 zijn niet meer aanwezig in Data Factory V2. Zie [Pijplijnuitvoering en triggers](concepts-pipeline-execution-triggers.md) en [Pijplijnen en activiteiten](concepts-pipelines-activities.md) voor meer informatie. |
| Activiteiten | Activiteiten definiëren welke acties binnen een pijplijn moeten worden uitgevoerd op uw gegevens. Activiteiten als het verplaatsen van gegevens (kopieeractiviteit) en het transformeren van gegevens (zoals Hive, Pig en MapReduce) worden ondersteund. | In Data Factory V2 zijn activiteiten nog steeds gedefinieerde acties binnen een pijplijn. In V2 worden nieuwe [controlestroomactiviteiten](concepts-pipelines-activities.md#control-activities) geïntroduceerd. U gebruikt deze activiteiten in een controlestroom (lussen en vertakkingen). Gegevensverplaatsings- en gegevenstransformatieactiviteiten die in V1 werden ondersteund, worden in V2 ondersteund. In V2 kunt u transformatieactiviteiten definiëren zonder gegevenssets te gebruiken. |
| Hybride verplaatsing van gegevens en verzenden van activiteiten | [Gegevensbeheergateway](v1/data-factory-data-management-gateway.md), nu bekend als Integration Runtime, bood ondersteuning voor het verplaatsen van gegevens tussen on-premises en de cloud.| Gegevensbeheergateway wordt nu zelf-hostende Integration Runtime genoemd. Het biedt dezelfde mogelijkheden als in V1. <br/><br/> Azure-SSIS Integration Runtime in V2 ondersteunt teven het implementeren en uitvoeren van SSIS-pakketten (SQL Server Integration Services) in de cloud. Zie voor meer informatie [Integration Runtime in Azure Data Factory](concepts-integration-runtime.md).|
| Parameters | N.v.t. | Parameters zijn sleutel-waardeparen van alleen-lezen-configuratie-instellingen die in pijplijnen worden gedefinieerd. U kunt argumenten voor de parameters doorgeven als u de pijplijn handmatig uitvoert. Als u een scheduler-trigger gebruikt, kan de trigger ook waarden voor de parameters doorgeven. Activiteiten binnen de pijplijn gebruiken de parameterwaarden.  |
| Expressies | In Data Factory V1 kunt u functies en systeemvariabelen gebruiken in gegevensselectiequery's en activiteits-/gegevensseteigenschappen. | In Data Factory V2 kunt u overal in een JSON-tekenreekswaarde gebruikmaken van expressies. Zie [Expressies en functies in V2](control-flow-expression-language-functions.md) voor meer informatie.|
| Pijplijnuitvoeringen | N.v.t. | Eén instantie van een uitvoeringsbewerking van een pijplijn. Stel dat u een pijplijn hebt die wordt uitgevoerd om 8 uur, 9 uur en 10 uur. In dit geval wordt de pijplijn drie keer afzonderlijk uitgevoerd (pijplijnuitvoeringen). Elke pijplijnuitvoering heeft een unieke id. De id is een unieke GUID die de betreffende specifieke pijplijnuitvoering definieert. Pijplijnuitvoeringen worden doorgaans geïnstantieerd doordat argumenten worden doorgegeven aan parameters die zijn gedefinieerd in de pijplijnen. |
| Uitvoering van activiteiten | N.v.t. | Een instantie van een uitvoerbewerking van een activiteit binnen een pijplijn. | 
| Triggeruitvoeringen | N.v.t. | Een instantie van een uitvoerbewerking van een trigger. Zie [Triggers](concepts-pipeline-execution-triggers.md) voor meer informatie. |
| Planning | Planning is gebaseerd op de begin-/eindtijd van een pijplijn en de beschikbaarheid van gegevenssets. | Scheduler-trigger of uitvoering via externe planner. Zie [Pijplijnen uitvoeren en triggers](concepts-pipeline-execution-triggers.md) voor meer informatie. |

De volgende gedeelten bevatten meer informatie over de mogelijkheden van V2. 

## <a name="control-flow"></a>Controlestroom  
Data Factory V2 heeft een nieuw flexibel gegevenspijplijnmodel dat niet langer is gekoppeld aan tijdseriegegevens ter ondersteuning van diverse integratiestromen en -patronen in het moderne datawarehouse. Dit zijn enkele veelvoorkomende stromen die nu mogelijk zijn geworden. Deze worden gedetailleerd beschreven in de volgende gedeelten.   

### <a name="chaining-activities"></a>Koppelingsactiviteiten
In V1 moest u de uitvoer van een activiteit configureren als de invoer van een andere activiteit om ze te koppelen. In V2 kunt u activiteiten in een reeks binnen een pijplijn koppelen. U kunt de eigenschap **dependsOn** in een activiteitsdefinitie gebruiken om deze te koppelen aan een upstream-activiteit. Zie [Pijplijnen en activiteiten](concepts-pipelines-activities.md#multiple-activities-in-a-pipeline) en [Vertakkings- en koppelingsactiviteiten](tutorial-control-flow.md) voor meer informatie en een voorbeeld. 

### <a name="branching-activities"></a>Vertakkingsactiviteiten
In V2 kunt u activiteiten binnen een pijplijn koppelen. De [activiteit Als-voorwaarde](control-flow-if-condition-activity.md) biedt dezelfde functionaliteit als een `if`-instructie in een programmeertaal. Er wordt een reeks activiteiten mee geëvalueerd als de voorwaarde resulteert in `true` en een andere reeks activiteiten als de voorwaarde resulteert in `false`. Zie [Vertakkings- en koppelingsactiviteiten](tutorial-control-flow.md) voor een voorbeeld van vertakkingsactiviteiten.

### <a name="parameters"></a>Parameters 
U kunt parameters definiëren op pijplijnniveau en de argumenten doorgeven tijdens het aanroepen van de pijplijn op aanvraag of vanuit een trigger. Activiteiten kunnen de argumenten die zijn doorgegeven aan de pijplijn gebruiken. Zie [Pijplijnen en triggers](concepts-pipeline-execution-triggers.md) voor meer informatie. 

### <a name="custom-state-passing"></a>Aangepaste status doorgeven
Activiteituitvoer zoals de status kan worden gebruikt door een volgende activiteit in de pijplijn. In de JSON-definitie van een activiteit bijvoorbeeld, hebt u toegang tot de uitvoer van de vorige activiteit door middel van de volgende syntaxis: `@activity('NameofPreviousActivity').output.value`. Met deze functie kunt u werkstromen bouwen waar waarden activiteiten kunnen passeren.

### <a name="looping-containers"></a>Herhalende containers
De [activiteit ForEach](control-flow-for-each-activity.md) definieert een herhalende controlestroom in de pijplijn. Deze activiteit wordt gebruikt om een verzameling te herhalen en voert opgegeven activiteiten uit in een lus. De lusimplementatie van deze activiteit is vergelijkbaar met Foreach-lusstructuur in computertalen. 

De activiteit [Until](control-flow-until-activity.md) biedt dezelfde functionaliteit als de lusstructuur do-until in een programmeertaal. Er wordt een reeks activiteiten uitgevoerd totdat de voorwaarde die aan de activiteit is gekoppeld, resulteert in `true`. U kunt in Data Factory een time-outwaarde voor de Until-activiteit opgeven.  

### <a name="trigger-based-flows"></a>Op triggers gebaseerde stromen
Pijplijnen kunnen op aanvraag of volgens wandklokplanningen worden geactiveerd. In het artikel [Pijplijnen en triggers](concepts-pipeline-execution-triggers.md) vindt u meer informatie over triggers. 

### <a name="invoking-a-pipeline-from-another-pipeline"></a>Een pijplijn aanroepen vanaf een andere pijplijn
De [activiteit Execute Pipeline](control-flow-execute-pipeline-activity.md) stelt een Data Factory-pijplijn in staat om een andere pijplijn aan te roepen.

### <a name="delta-flows"></a>Deltastromen
Een belangrijke use case in ETL-patronen zijn 'deltaladingen', waarin alleen gegevens worden geladen die zijn gewijzigd sinds de laatste iteratie van een pijplijn. Nieuwe mogelijkheden in V2, zoals de [activiteit lookup](control-flow-lookup-activity.md), flexibele planning en controlestroom maken deze use case op een natuurlijke manier mogelijk. Zie [Zelfstudie: stapsgewijs kopiëren](tutorial-incremental-copy-powershell.md) voor een zelfstudie met stapsgewijze instructies.

### <a name="other-control-flow-activities"></a>Andere controlestroomactiviteiten
Hier volgen nog enkele controlestroomactiviteiten die door Data Factory V2 worden ondersteund. 

Controleactiviteit | Beschrijving
---------------- | -----------
[Activiteit ForEach](control-flow-for-each-activity.md) | Deze activiteit definieert een herhalende controlestroom in de pijplijn. Deze activiteit wordt gebruikt om een verzameling te herhalen en voert opgegeven activiteiten uit in een lus. De lusimplementatie van deze activiteit is vergelijkbaar met Foreach-lusstructuur in computertalen.
[Activiteit Web](control-flow-web-activity.md) | Deze roept een aangepast REST-eindpunt aan vanaf een Data Factory-pijplijn. U kunt gegevenssets en gekoppelde services doorgeven die moten worden verbruikt door en die toegankelijk zijn voor de activiteit. 
[Activiteit Lookup](control-flow-lookup-activity.md) | Deze activiteit leest of zoekt de waarde op van een record op tabelnaamwaarde in een externe bron. Er kan naar deze uitvoer worden verwezen door volgende activiteiten. 
[Activiteit Metagegevens ophalen](control-flow-get-metadata-activity.md) | Haalt de metagegevens op van de gegevens in Azure Data Factory. 
[Activiteit Wait](control-flow-wait-activity.md) | Onderbreekt de pijplijn voor een opgegeven periode.

## <a name="deploy-ssis-packages-to-azure"></a>SSIS-pakketten implementeren in Azure 
U gebruikt Azure-SSIS als u de SSIS-werkbelastingen naar de cloud wilt verplaatsen, een data factory wilt maken met V2 en een Azure-SSIS Integration Runtime wilt inrichten.

Azure-SSIS Integration Runtime is een volledig beheerd cluster met virtuele Azure-machines (knooppunten) die uw SSIS-pakketten uitvoeren in de cloud. Als u Azure-SSIS Integration Runtime hebt ingericht, kunt u dezelfde hulpmiddelen gebruiken die u hebt gebruikt voor het implementeren van SSIS-pakketten in een on-premises SSIS-omgeving. 

U kunt bijvoorbeeld SQL Server Data Tools of SQL Server Management Studio gebruiken om SSIS-pakketten te implementeren in deze runtime op Azure. Zie de zelfstudie [Pakketten van SQL Server Integration Services implementeren in Azure](tutorial-deploy-ssis-packages-azure.md) voor stapsgewijze instructies. 

## <a name="flexible-scheduling"></a>Flexibel plannen
In Data Factory V2 hoeft u geen beschikbaarheidschema's voor gegevenssets te definiëren. U kunt een triggerbron definiëren waarmee pijplijnen kunnen worden gepland op basis van een klokplannermodel. U kunt ook vanuit een trigger parameters aan pijplijnen doorgeven voor een flexibel plannings- en uitvoeringsmodel. 

In Data Factory V2 hebben pijplijnen geen 'vensters' voor uitvoering in de tijd. De concepten startTime, endTime en isPaused van Data Factory V1 bestaan niet in Data Factory V2. Zie [Pijplijnen uitvoeren en triggers](concepts-pipeline-execution-triggers.md) voor meer informatie over het bouwen en plannen van een pijplijn in Data Factory V2.

## <a name="support-for-more-data-stores"></a>Ondersteuning voor meer gegevensarchieven
V2 ondersteunt het kopiëren van gegevens van en naar meer gegevensarchieven dan V1. Zie de volgende artikelen voor een lijst met ondersteunde gegevensarchieven:

- [V1: ondersteunde gegevensarchieven](v1/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
- [V2: ondersteunde gegevensarchieven](copy-activity-overview.md#supported-data-stores-and-formats)

## <a name="support-for-on-demand-spark-cluster"></a>Ondersteuning voor Apache Spark-cluster op aanvraag
V2 ondersteunt het maken van een Azure HDInsight Spark-cluster op aanvraag. Als u een Spark-cluster op aanvraag wilt maken, geeft u het clustertype op als Spark in uw definitie van uw gekoppelde HDInsight-service op aanvraag. Vervolgens configureert u de Spark-activiteit in de pijplijn voor het gebruik van deze gekoppelde service. 

Tijdens runtime, als de activiteit wordt uitgevoerd, maakt de data factory-service automatisch de Apache Spark-cluster. Raadpleeg voor meer informatie de volgende artikelen:

- [Apache Spark-activiteit in V2](transform-data-using-spark.md)
- [Een gekoppelde Azure HDInsight-service op aanvraag](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)

## <a name="custom-activities"></a>Aangepaste activiteiten
In V1 implementeert u (aangepaste) DotNet-activiteitscode door een .NET-klassebibliotheekproject te maken met een klasse die de methode Execute van de IDotNetActivity-interface implementeert. Daarom moet de aangepaste code worden geschreven in .NET Framework 4.5.2 en worden uitgevoerd op Batch-poolknooppunten van Azure onder Windows. 

In een aangepaste V2-activiteit hoeft u geen .NET-interface te implementeren. U kunt rechtstreeks opdrachten en scripts uitvoeren en uw eigen, aangepaste code uitvoeren die als een uitvoerbaar bestand is gecompileerd. 

Zie [Verschil tussen aangepaste activiteit in V1 en V2](transform-data-using-dotnet-custom-activity.md#difference-between-custom-activity-in-azure-data-factory-v2-and-custom-dotnet-activity-in-azure-data-factory-v1) voor meer informatie.

## <a name="sdks"></a>SDK's
 Data Factory V2 biedt een meer uitgebreide set SDK's, die kan worden gebruikt voor het ontwerpen, beheren en bewaken van pijplijnen.

- **.NET SDK**: de .NET SDK is bijgewerkt voor V2.

- **PowerShell**: de PowerShell-cmdlets zijn bijgewerkt voor V2. De V2-cmdlets hebben **DataFactoryV2** in de naam, bijvoorbeeld: Get-AzureRmDataFactoryV2. 

- **Python SDK**: deze SDK is nieuw in V2.

- **REST API**: de REST-API is bijgewerkt voor V2. 

De SDK's die zijn bijgewerkt voor V2 zijn niet achterwaarts compatibel met V1-clients. 

## <a name="authoring-experience"></a>Ontwerpen

| &nbsp; | V2 | V1 |
| ------ | -- | -- | 
| Azure Portal | [Ja](quickstart-create-data-factory-portal.md) | [Ja](data-factory-build-your-first-pipeline-using-editor.md) |
| Azure PowerShell | [Ja](quickstart-create-data-factory-powershell.md) | [Ja](data-factory-build-your-first-pipeline-using-powershell.md) |
| .NET SDK | [Ja](quickstart-create-data-factory-dot-net.md) | [Ja](data-factory-build-your-first-pipeline-using-vs.md) |
| REST-API | [Ja](quickstart-create-data-factory-rest-api.md) | [Ja](data-factory-build-your-first-pipeline-using-rest-api.md) |
| Python-SDK | [Ja](quickstart-create-data-factory-python.md) | Nee |
| Resource Manager-sjabloon | [Ja](quickstart-create-data-factory-resource-manager-template.md) | [Ja](data-factory-build-your-first-pipeline-using-arm.md) | 


## <a name="monitoring-experience"></a>Bewaken
In V2 kunt u ook data factory's bewaken met behulp van [Azure Monitor](monitor-using-azure-monitor.md). De nieuwe PowerShell-cmdlets bieden ondersteuning voor het bewaken van [integratie-runtimes](monitor-integration-runtime.md). Zowel V1 als V2 ondersteunen visueel bewaken via bewakingstoepassingen die vanuit Azure Portal kunnen worden gestart.


## <a name="next-steps"></a>Volgende stappen
In de volgende QuickStarts vindt u informatie over het maken van een data factory door het volgen van stapsgewijze instructies: [PowerShell](quickstart-create-data-factory-powershell.md), [.NET](quickstart-create-data-factory-dot-net.md), [Python](quickstart-create-data-factory-python.md) en [REST-API](quickstart-create-data-factory-rest-api.md). 
