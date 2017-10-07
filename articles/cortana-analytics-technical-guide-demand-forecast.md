---
title: aaaDemand prognose in technische handleiding energie | Microsoft Docs
description: Een technische handleiding toohello oplossingssjabloon met Microsoft Cortana Intelligence voor vraag prognose in energie.
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>Technische handleiding toohello Cortana Intelligence oplossingssjabloon voor vraag prognose in energie
## <a name="overview"></a>**Overzicht**
Oplossingssjablonen zijn zo ontworpen tooaccelerate Hallo proces van het bouwen van een demo E2E boven op de Cortana Intelligence Suite. Een geïmplementeerde sjabloon wordt uw abonnement met de benodigde Cortana Intelligence-onderdeel inrichten en Hallo relaties tussen bouwen. Deze ook seeding Hallo data pipeline met voorbeeldgegevens ophalen gegenereerd op basis van een toepassing simuleren. Hallo gegevens simulator van Hallo koppeling downloaden en installeren op uw lokale computer, raadpleeg dan toohello Leesmij-bestand voor instructies over het gebruik van Hallo simulator. Gegevens die zijn gegenereerd uit Hallo simulator wordt hydrate Hallo gegevens pijplijn en start het genereren van machine learning voorspelling die vervolgens kan worden weergegeven op Hallo Power BI-dashboard.

Hallo oplossingssjabloon vindt [hier](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

Hallo-implementatieproces leidt u door de verschillende stappen tooset van de referenties van uw oplossing. Zorg ervoor dat u deze referenties zoals oplossingsnaam, gebruikersnaam en wachtwoord dat u tijdens de implementatie van Hallo opgeeft vastleggen.

Hallo-doel van dit document is tooexplain Hallo-referentiearchitectuur en verschillende onderdelen die zijn ingericht in uw abonnement als onderdeel van de sjabloon voor deze oplossing. Hallo-document is ook wordt gesproken over hoe tooreplace Hallo voorbeeldgegevens met echte gegevens van uw eigen toobe kunnen toosee insights/voorspellingen van u gewonnen gegevens. Bovendien Hallo document vertelt over Hallo delen van Hallo oplossingssjabloon waarvoor toobe gewijzigd als u wilt dat toocustomize Hallo oplossing met uw eigen gegevens. Hallo achter vindt u instructies over hoe toobuild Power BI-dashboard Hallo voor deze oplossingssjabloon.

## <a name="big-picture"></a>**Grote afbeelding**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Architectuur uitgelegd
Wanneer het Hallo-oplossing is geïmplementeerd, verschillende Azure-services binnen Cortana-Analytics Suite zijn geactiveerd (*dat wil zeggen* Event Hub, Stream Analytics, HDInsight, Data Factory Machine Learning, *enzovoort*). Hallo Architectuurdiagram van de bovenstaande toont, op een hoog niveau hoe Hallo voorspellen van de vraag voor energie-oplossingssjabloon is samengesteld uit de end-to-end. U zult kunnen tooinvestigate deze services door erop te klikken op Hallo oplossing sjabloon diagram gemaakt met de Hallo implementeren van Hallo-oplossing. Hallo volgende secties beschrijven elk gegeven.

## <a name="data-source-and-ingestion"></a>**Gegevensbron en opnamesnelheid**
### <a name="synthetic-data-source"></a>Synthetische gegevensbron
Bron gebruikt wordt voor deze sjabloon Hallo gegevens gegenereerd vanuit een bureaubladtoepassing die u wilt downloaden en lokaal uitvoeren na een geslaagde implementatie. U Hallo instructies toodownload vinden en installeren van deze toepassing op Hallo Eigenschappenbalk wanneer u de eerste knooppunt Hallo energie prognose gegevens Simulator aangeroepen op Hallo oplossing sjabloon diagram selecteert. Deze toepassing hello feeds [Azure Event Hub](#azure-event-hub) service met gegevenspunten of gebeurtenissen die worden gebruikt in de rest Hallo van Hallo oplossing stroom.

Hallo-toepassing voor het genereren van gebeurtenis vult hello Azure Event Hub alleen terwijl deze wordt uitgevoerd op uw computer.

### <a name="azure-event-hub"></a>Azure Event Hub
Hallo [Azure Event Hub](https://azure.microsoft.com/services/event-hubs/) service is Hallo geadresseerde van Hallo invoer geleverd door Hallo synthetische gegevensbron die hierboven worden beschreven.

## <a name="data-preparation-and-analysis"></a>**Voorbereiden van gegevens en analyse**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hallo [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) -service is gebruikte tooprovide bijna realtime analyses op Hallo invoerstroom van Hallo [Azure Event Hub](#azure-event-hub) service en publiceren van de resultaten naar een [Power BI](https://powerbi.microsoft.com) dashboard, evenals alle onbewerkte binnenkomende gebeurtenissen toohello archiveren [Azure Storage](https://azure.microsoft.com/services/storage/) service later worden verwerkt door Hallo [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service.

### <a name="hd-insights-custom-aggregation"></a>HD Insights aangepaste aggregatie
Hallo HD inzicht van Azure-service is gebruikte toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts (gedirigeerd door Azure Data Factory) tooprovide aggregaties op Hallo onbewerkte gebeurtenissen die zijn gearchiveerd met hello Azure Stream Analytics-service.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) -service wordt gebruikt (gedirigeerd door Azure Data Factory) toomake prognose op toekomstige energieverbruik van een bepaald gebied opgegeven Hallo invoer ontvangen.

## <a name="data-publishing"></a>**Gegevens publiceren**
### <a name="azure-sql-database-service"></a>Azure SQL Database-Service
Hallo [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) -service is gebruikte toostore (beheerd door Azure Data Factory) Hallo voorspellingen ontvangen door hello Azure Machine Learning-service die worden gebruikt in Hallo [Power BI](https://powerbi.microsoft.com) dashboard.

## <a name="data-consumption"></a>**Gegevens verbruik**
### <a name="power-bi"></a>Power BI
Hallo [Power BI](https://powerbi.microsoft.com) -service is gebruikte tooshow een dashboard met aggregaties geleverd door Hallo [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) service als vraag forecast resultaten opgeslagen in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) die zijn geproduceerd met Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) service. Voor instructies over hoe toobuild Power BI-dashboard voor deze oplossingssjabloon Hallo, Raadpleeg toohello hieronder.

## <a name="how-toobring-in-your-own-data"></a>**Hoe toobring in uw eigen gegevens**
Deze sectie wordt beschreven hoe toobring uw eigen gegevens tooAzure en wat gebieden waarvoor wijzigingen voor gegevens Hallo u doen in deze architectuur.

Het lijkt onwaarschijnlijk dat een gegevensset die u brengt overeenkomen met Hallo gegevensset voor deze oplossingssjabloon gebruikt. Inzicht in uw gegevens en de vereisten is cruciaal belang bij hoe u deze sjabloon toowork met uw eigen gegevens wijzigen. Als dit uw eerste blootstelling toohello Azure Machine Learning-service is, kunt u een inleiding tooit krijgen met behulp van Hallo voorbeeld in [hoe toocreate uw eerste experiment](machine-learning/machine-learning-create-experiment.md).

Hallo uit te voeren behandeld Hallo secties van Hallo-sjabloon die wijzigingen is vereist wanneer een nieuwe gegevensset wordt geïntroduceerd.

### <a name="azure-event-hub"></a>Azure Event Hub
Hallo [Azure Event Hub](https://azure.microsoft.com/services/event-hubs/) -service is zeer algemeen, zodat gegevens kan toohello hub worden geplaatst in CSV- of JSON-indeling. Er is geen speciale verwerking optreedt in hello Azure Event Hub, maar het is belangrijk dat u begrijpt Hallo-gegevens die is ingevoerd.

Dit document beschrijft niet hoe tooingest uw gegevens, maar een eenvoudig gebeurtenissen of gegevens tooan Azure Event Hub verzenden kan, met behulp van Hallo [Event Hub API](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hallo [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) service gebruikte tooprovide bijna realtime analyses op lezen van gegevensstromen en uitvoeren van de gegevens tooany aantal bronnen is.

Voor Hallo voorspellen van de vraag voor oplossingssjabloon energie bestaat hello Azure Stream Analytics query uit twee subquery's, elk verbruikt gebeurtenissen van hello Azure Event Hub-service als invoer en uitvoer tootwo verschillende locaties hebben. Deze uitvoer bestaan uit één gegevensset met Power BI en een Azure-opslaglocatie.

Hallo [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) query kan worden gevonden door:

* Aanmelden bij Hallo [Azure-beheerportal](https://manage.windowsazure.com/)
* Zoeken naar Hallo stream analytics-taken ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) die zijn gegenereerd tijdens het Hallo-oplossing is geïmplementeerd. Een is voor het pushen van tooblob gegevensopslag (bijvoorbeeld mytest1streaming432822asablob) en Hallo andere een is voor het pushen van gegevens tooPower BI (bijvoorbeeld mytest1streaming432822asapbi).
* Selecteren

  * ***INVOER*** tooview Hallo query invoer
  * ***QUERY*** tooview Hallo query zelf
  * ***LEVERT*** tooview Hallo andere uitvoer

Informatie over het samenstellen van Azure Stream Analytics query vindt u in Hallo [Stream Analytics Query verwijzing](https://msdn.microsoft.com/library/azure/dn834998.aspx) op MSDN.

In deze oplossing hello Azure Stream Analytics-taak, die de gegevensset met bijna realtime analyses informatie over Hallo binnenkomende gegevensstroom tooa Power BI-dashboard wordt geleverd als onderdeel van deze oplossingssjabloon levert. Omdat er impliciete kennis over binnenkomende gegevensindeling hello, moet deze query's toobe gewijzigd op basis van indeling van uw gegevens.

Hallo andere Azure Stream Analytics-taak levert alle [Event Hub](https://azure.microsoft.com/services/event-hubs/) gebeurtenissen die moeten worden [Azure Storage](https://azure.microsoft.com/services/storage/) en daarom geen wijziging ongeacht de indeling van uw gegevens vereist als de volledige gebeurtenisgegevens Hallo gestreamd toostorage.

### <a name="azure-data-factory"></a>Azure Data Factory
Hallo [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service ingedeeld Hallo verplaatsing en verwerking van gegevens. In Hallo voorspellen van de vraag voor energie oplossingssjabloon Hallo data factory bestaat uit twaalf [pijplijnen](data-factory/data-factory-create-pipelines.md) die verplaatsen en het Hallo-gegevens met behulp van verschillende technologieën worden verwerkt.

  U kunt toegang tot uw gegevensfactory door het openen van de Data Factory-knooppunt Hallo HALLO hallo oplossing sjabloon diagram gemaakt met de implementatie van Hallo oplossing Hallo onderaan in. Hiervoor gaat u toohello gegevensfactory op uw Azure-beheerportal. Als u fouten onder uw gegevenssets ziet, kunt u die negeren omdat deze vanwege toodata factory worden geïmplementeerd voordat Hallo gegevensgenerator werd gestart. Deze fouten doen niet voorkomen dat uw data factory werkt.

Deze sectie wordt beschreven Hallo nodig [pijplijnen](data-factory/data-factory-create-pipelines.md) en [activiteiten](data-factory/data-factory-create-pipelines.md) opgenomen in Hallo [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Hieronder ziet u de diagramweergave Hallo Hallo-oplossing.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Vijf Hallo pijplijnen van deze factory bevatten [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts die gebruikt toopartition en Hallo cumulatieve gegevens zijn. Wanneer vermeld, Hallo scripts bevindt zich in Hallo [Azure Storage](https://azure.microsoft.com/services/storage/) account gemaakt tijdens de installatie. De locatie zijn: demandforecasting\\\\script\\\\hive\\ \\ (of https://[Your oplossing name].blob.core.windows.net/demandforecasting).

Vergelijkbare toohello [Azure Stream Analytics](#azure-stream-analytics-1) query's de [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts hebben impliciete kennis over binnenkomende gegevensindeling hello, deze query's moet toobe gewijzigd op basis van de indeling van gegevens en [functie-engineering](machine-learning/machine-learning-feature-selection-and-engineering.md) vereisten.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
Dit [pijplijn](data-factory/data-factory-create-pipelines.md) pijplijn bevat een enkele activiteit - een [HDInsightHive](data-factory/data-factory-hive-activity.md) activiteit met behulp van een [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) die wordt uitgevoerd een [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)script tooaggregate Hallo elke 10 seconden gegevens van de aanvraag in onderstation niveau toohourly regioniveau, worden stroomsgewijs ingevoegd en plaatsen [Azure Storage](https://azure.microsoft.com/services/storage/) via hello Azure Stream Analytics-taak.

De [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script voor deze taak partitionering is ***AggregateDemandRegion1Hr.hql***

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
Dit [pijplijn](data-factory/data-factory-create-pipelines.md) bevat twee activiteiten:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) activiteit met behulp van een [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) dat wordt uitgevoerd een component tooaggregate Hallo per uur vraag geschiedenisgegevens in onderstation niveau toohourly regioniveau script en in Azure Storage tijdens hello Azure plaatsen Stream Analytics-taak
* [Kopiëren](https://msdn.microsoft.com/library/azure/dn835035.aspx) activiteit die wordt verplaatst Hallo cumulatieve gegevens uit Azure Storage-blob toohello Azure SQL Database die als onderdeel van de installatie van de servicesjabloon oplossing Hallo is ingericht.

Hallo [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script voor deze taak is ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Deze [pijplijnen](data-factory/data-factory-create-pipelines.md) verschillende activiteiten bevatten en waarvan eindresultaat is Hallo gewaardeerd voorspellingen van hello Azure Machine Learning-experimenten die zijn gekoppeld aan deze oplossingssjabloon. Ze zijn bijna identiek, met uitzondering van elk van deze verwerkt alleen Hallo andere regio die wordt uitgevoerd door verschillende RegionID doorgegeven Hallo ADF-pijplijn en Hallo hive-script voor elke regio.  
Hallo-activiteiten die zijn opgenomen in dit zijn:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) activiteit met behulp van een [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) dat wordt uitgevoerd een component tooperform aggregaties script en functie-engineering nodig zijn voor hello Azure Machine Learning-experiment. Hallo Hive scripts voor deze taak zijn respectieve ***PrepareMLInputRegionX.hql***.
* [Kopiëren](https://msdn.microsoft.com/library/azure/dn835035.aspx) activiteit die wordt verplaatst Hallo resultaten van Hallo [HDInsightHive](data-factory/data-factory-hive-activity.md) activiteit tooa één Azure Storage-blob die toegang door Hallo worden kan [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) activiteit.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) die aanroept hello Azure Machine Learning-experiment wat tot Hallo leidt resulteert in een enkel Azure Storage-blob worden opgeslagen.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Deze [pijplijnen](data-factory/data-factory-create-pipelines.md) een enkele activiteit - bevatten een [kopie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activiteit die Hallo resultaten van hello Azure Machine Learning-experiment van Hallo respectieve verplaatst ***MLScoringRegionXPipeline *** toohello Azure SQL Database die als onderdeel van de installatie van de servicesjabloon oplossing Hallo is ingericht.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
Dit [pijplijnen](data-factory/data-factory-create-pipelines.md) een enkele activiteit - bevatten een [kopie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activiteit die wordt verplaatst Hallo geaggregeerd gegevens van actieve aanvraag ***LoadHistoryDemandDataPipeline*** toohello Azure SQL-Database die als onderdeel van de installatie van de servicesjabloon oplossing Hallo is ingericht.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
Deze [pijplijnen](data-factory/data-factory-create-pipelines.md) een enkele activiteit - bevatten een [kopie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activiteit die wordt verplaatst Hallo referentiegegevens voor onderstation-regio/Topologygeo die zijn geüpload tooAzure Storage-blob als onderdeel van Hallo-oplossing sjabloon installatie toohello Azure SQL Database die als onderdeel van de installatie van de servicesjabloon oplossing Hallo is ingericht.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) experimenteren gebruikt voor de oplossingssjabloon voor deze Hallo voorspelling van de vraag van de regio biedt. Hallo-experiment is specifiek toohello gegevensverzameling verbruikt en daarom moet wijziging of vervanging specifieke toohello gegevens die in is gebracht.

## <a name="monitor-progress"></a>**Voortgang van de monitor**
Zodra het Hallo Gegevensgenerator wordt gestart, hello pijplijn begint tooget gehydrateerd en hello verschillende onderdelen van uw oplossing beginnen bij de start in de actie volgende Hallo opdrachten die zijn uitgegeven door Hallo Data Factory. Er zijn twee manieren die kunt u Hallo pijplijn bewaken.

1. Controleer Hallo gegevens uit Azure Blob Storage.

    Een van de Stream Analytics-taak Hallo schrijft Hallo onbewerkte binnenkomende tooblob gegevensopslag. Als u op klikt **Azure Blob Storage** onderdeel van uw oplossing van Hallo u de oplossing is geïmplementeerd Hallo scherm en klik vervolgens op **Open** in het rechterpaneel hello, duurt het u toohello [Azure-beheerportal](https://portal.azure.com). Klik op **Blobs**. In het volgende Configuratiescherm hello ziet u een lijst van Containers. Klik op **'energysadata'**. In het volgende Configuratiescherm hello, ziet u Hallo **'demandongoing'** map. Hallo rawdata-map, ziet u mappen met namen zoals datum = 2016-01-28 enzovoort. Als u deze mappen ziet, betekent dit Hallo onbewerkte gegevens is voltooid wordt op uw computer wordt gegenereerd en opgeslagen in blob storage. Hier ziet u bestanden met moeten eindig grootte in MB in deze mappen.
2. Hallo-gegevens van Azure SQL Database controleren.

    laatste stap van de pijplijn Hallo Hallo is toowrite gegevens (bijvoorbeeld de voorspellingen van machine learning) in SQL-Database. Mogelijk hebt u toowait maximaal 2 uur voor Hallo gegevens tooappear in SQL-Database. Eenzijdige toomonitor hoeveel gegevens zijn beschikbaar in de SQL-Database is via [Azure-beheerportal](https://manage.windowsazure.com/). Zoek in het linkerdeelvenster Hallo SQL-DATABASES![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) en klik erop. Zoek uw database (dat wil zeggen demo123456db) en vervolgens klikt u op. Op de volgende pagina Hallo onder **'Connect tooyour database'** sectie, klikt u op **' Uitvoeren Transact-SQL-query's op uw SQL-database'**.

    Hier kunt u klikken op nieuwe Query en de query voor het aantal rijen (bijvoorbeeld ' select count(*) van DemandRealHourly) Hallo ' wanneer de database groeit, het aantal rijen in de tabel Hallo Hallo moet verhogen.)
3. Controleer Hallo gegevens van Power BI-dashboard.

    U kunt Power BI hot pad dashboard toomonitor Hallo onbewerkte binnenkomende gegevens instellen. Volg de instructies Hallo in de sectie 'Power BI-Dashboard' Hallo.

## <a name="power-bi-dashboard"></a>**Power BI-Dashboard**
### <a name="overview"></a>Overzicht
Deze sectie wordt beschreven hoe tooset van Power BI-dashboard toovisualize uw realtime-gegevens van Azure stream analytics (hot pad) als goed als prognose resultaten van Azure machine learning (koude pad).

### <a name="setup-hot-path-dashboard"></a>Hot pad Dashboard instellen
volgende stappen uit Hallo leidt u hoe toovisualize realtime gegevens uitvoer van de Stream Analytics-taken die zijn gegenereerd op Hallo moment van implementatie van de oplossing. Een [Power BI online](http://www.powerbi.com/) -account is vereist tooperform Hallo stappen te volgen. Als u geen account hebt, kunt u [maken van een](https://powerbi.microsoft.com/pricing).

1. Power BI-uitvoer in Azure Stream Analytics (ASA) toevoegen.

   * U moet toofollow Hallo instructies in [Azure Stream Analytics & Power BI: een dashboard realtime analyses voor realtime zichtbaarheid van gegevensstromen](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset up Hallo-uitvoer van uw Azure Stream Analytics-taak als de stroom BI-dashboard.
   * Zoek Hallo stream analytics-taak in uw [Azure-beheerportal](https://manage.windowsazure.com). Hallo-naam van de taak Hallo moet: YourSolutionName + "streamingjob" + willekeurig getal + "asapbi' (dat wil zeggen demostreamingjob123456asapbi).
   * De uitvoer van een Power BI voor Hallo ASA taak toevoegen. Set Hallo **Uitvoeraliassen** als **'PBIoutput'**. Stel uw **gegevenssetnaam** en **tabelnaam** als **'EnergyStreamData'**. Nadat u de uitvoer Hallo hebt toegevoegd, klikt u op **'Start'** onderaan Hallo Hallo pagina toostart Hallo Stream Analytics-taak. Krijgt u een bevestigingsbericht (*bijvoorbeeld*, 'starten stream analytics-taak myteststreamingjob12345asablob is voltooid').
2. Meld u bij te[online in Power BI](http://www.powerbi.com)

   * U moet op Hallo links Configuratiescherm gegevenssets in mijn werkruimte, kunnen toosee een nieuwe gegevensset wordt weergegeven op Hallo linkerpaneel van Power BI. Dit is Hallo streamen van gegevens die u vanuit Azure Stream Analytics in de vorige stap Hallo gepusht.
   * Zorg ervoor dat Hallo ***visualisaties*** deelvenster is geopend en wordt weergegeven aan de rechterkant van het welkomstscherm.
3. Hallo 'Vraag door tijdstempel' tegel maken:

   * Klik op de gegevensset **'EnergyStreamData'** op Hallo links Configuratiescherm gegevenssets.
   * Klik op **'Lijndiagram'** pictogram ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * Klik op 'EnergyStreamData' in **velden** Configuratiescherm.
   * Klik op **'Tijdstempel'** en zorg ervoor dat er onder 'As' wordt weergegeven. Klik op **'Load'** en zorg ervoor dat er wordt weergegeven onder "Waarden".
   * Klik op **opslaan** op Hallo boven en geef de naam Hallo rapport als 'EnergyStreamDataReport'. Hallo-rapport met de naam 'EnergyStreamDataReport' wordt weergegeven in de sectie rapporten in Hallo Navigator deelvenster aan de linkerkant.
   * Klik op **'Pincode Visual'** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) pictogram in de rechterbovenhoek van dit lijndiagram een venster 'Pincode tooDashboard' mogelijk weergegeven voor toochoose u een dashboard. Selecteer 'EnergyStreamDataReport' en klik vervolgens op 'Pincode'.
   * Hallo muisaanwijzer via deze tegel op Hallo dashboard, klikt u op '' pictogram bewerken op rechterbovenhoek toochange titel als 'Vraag door tijdstempel'
4. Andere dashboard tegels op basis van de juiste gegevenssets maken. de laatste dashboardweergave Hallo worden hieronder weergegeven.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Setup koude pad Dashboard
In de pijplijn voor koude pad gegevens streeft Hallo essentiële tooget Hallo vraag forecast van elke regio. Power BI verbinding tooan Azure SQL-database als de gegevensbron ervan, waarbij Hallo voorspelling resultaten worden opgeslagen.

> [!NOTE]
> 1) Het duurt enkele uren toocollect genoeg prognose resultaten voor het Hallo-dashboard. U wordt aangeraden de start van dit proces 2-3 uur nadat u Hallo gegevensgenerator lunch. 2) in deze stap Hallo vereiste toodownload en installeer Hallo gratis software is [van Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Hallo databasereferenties worden opgehaald.

   U moet **servernaam, databasenaam, gebruikersnaam en wachtwoord van de database** voordat u doorgaat toonext stappen. Hier volgen Hallo stappen tooguide u hoe toofind ze.

   * Eenmaal **'Azure SQL Database'** op uw oplossingssjabloon diagram wordt groen, klik hierop en klik op **'Open'**. U zult de begeleide tooAzure-beheerportal en uw databasepagina-informatie ook wordt geopend.
   * Op de pagina hello vindt u een sectie 'Database'. Geeft het Hallo-database die u hebt gemaakt. Hallo-naam van uw database moet **'Uw oplossingsnaam willekeurig getal + 'database' '** (bijvoorbeeld ' mytest12345db').
   * Klik op de database, in de nieuwe dat pop uit Configuratiescherm, vindt u de naam van uw database-server op Hallo boven Hallo. De naam van uw database-server moet **'Uw oplossingsnaam willekeurig getal + 'database.windows.net,1433' '** (bijvoorbeeld ' mytest12345.database.windows.net,1433').
   * Uw database **gebruikersnaam** en **wachtwoord** zijn Hallo hetzelfde als het Hallo-gebruikersnaam en wachtwoord eerder vastgelegd tijdens de implementatie van Hallo-oplossing.
2. De gegevensbron Hallo van Hallo koude pad Power BI-bestand bijwerken

   * Zorg ervoor dat u de meest recente versie van Hallo hebt geïnstalleerd [van Power BI desktop](https://powerbi.microsoft.com/desktop).
   * In Hallo **'DemandForecastingDataGeneratorv1.0'** map die u hebt gedownload, dubbelklikt u op Hallo **'Power BI Template\DemandForecastPowerBI.pbix'** bestand. Hallo initiële visualisaties zijn gebaseerd op dummy-gegevens. **Opmerking:** als er een fout Massageolie, zorg dat u de meest recente versie van Power BI Desktop Hallo hebt geïnstalleerd.

     Nadat u deze, bovenaan Hallo van Hallo-bestand opent, klikt u op **query's bewerken**. Klik in het pop uit venster hello, dubbelklik op **'Source'** in het rechterdeelvenster Hallo.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * Vervang in Hallo pop uit venster, **'Server'** en **'Database'** met uw eigen namen van de server en database en klik vervolgens op **'OK'**. Voor de servernaam van de, zorg ervoor dat u opgeeft Hallo-poort 1433 (**YourSolutionName.database.windows.net, 1433**). Hallo waarschuwingsberichten die worden weergegeven op het welkomstscherm negeren.
   * In de volgende pop Hallo uit venster, ziet u twee opties in het linkerdeelvenster hello (**Windows** en **Database**). Klik op **'Database'**, vul uw **'Gebruikersnaam'** en **'Password'** (dit is Hallo-gebruikersnaam en wachtwoord die u hebt ingevoerd toen u het eerst Hallo oplossing geïmplementeerd en gemaakt een Azure SQL database). In ***selecteren waarop deze instellingen tooapply niveau***, niveau databaseoptie controleren. Klik vervolgens op **'Connect'**.
   * Als u de vorige pagina Begeleide back toohello bent, sluit u Hallo-venster. Een bericht verschijnt buiten: klik **toepassen**. Klik ten slotte Hallo **opslaan** knop toosave Hallo wijzigingen. Uw bestand Power BI heeft nu verbinding toohello server vastgesteld. Als uw visualisaties leeg zijn, moet dat u uitschakelen Hallo selecties op Hallo visualisaties toovisualize alle Hallo gegevens door te klikken op Hallo gum pictogram op Hallo rechtsboven Hallo legenda's. Hallo vernieuwen knop tooreflect nieuwe gegevens op Hallo visualisaties gebruiken. In eerste instantie alleen ziet u Hallo seedgegevens op uw visualisaties omdat de gegevensfactory Hallo geplande toorefresh elke drie uur. U ziet na drie uur nieuwe voorspellingen doorgevoerd in uw visualisaties Wanneer u Hallo gegevens vernieuwen.
3. (Optioneel) Hallo koude pad dashboard te publiceren[Power BI online](http://www.powerbi.com/). Houd er rekening mee dat deze stap moet een Power BI-account (of Office 365-account).

   * Klik op **'Publiceren'** en later enkele seconden verschijnt er een venster weergeven 'Publiceren tooPower BI geslaagd!' met een groen vinkje. Klik op onderstaande 'Open demoprediction.pbix in Power BI' Hallo-koppeling. toofind gedetailleerde instructies, Zie [publiceren vanuit Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * een nieuw dashboard toocreate: klikt u op Hallo  **+**  Meld u aan de volgende toothe **Dashboards** sectie in het linkerdeelvenster Hallo. Voer Hallo naam 'Vraag prognose Demo' voor dit nieuwe dashboard.
   * Nadat u Hallo rapport openen, klikt u op ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin het dashboard voor de tooyour visualisaties. toofind gedetailleerde instructies, Zie [een tegel tooa Power BI-dashboard uit een rapport vastmaken](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     De dashboardpagina toohello gaan en Hallo grootte en locatie van uw visualisaties aanpassen en hun titels bewerken. toofind gedetailleerde instructies over hoe tooedit uw tegels zien [bewerken een tegel--formaat, verplaatsen, wijzig de naam, pincode, verwijderen, voegt u hyperlink](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Hier volgt een voorbeeld van dashboard met sommige koude pad visualisaties vastgemaakt tooit.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (Optioneel) Geplande vernieuwing van Hallo-gegevensbron.

   * tooschedule vernieuwing van het Hallo-gegevens, de muisaanwijzer op Hallo **EnergyBPI Final** gegevensset, klikt u op ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) en kies vervolgens **schema vernieuwen**.
     **Opmerking:** als er een waarschuwing massage, klikt u op **referenties bewerken** en zorg ervoor dat de databasereferenties van uw Hallo zijn dezelfde als die wordt beschreven in stap 1.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Vouw Hallo **schema vernieuwen** sectie. Schakel in 'uw gegevens up-to-date houden'.
   * Hallo vernieuwing op basis van de behoeften van uw plannen. toofind meer informatie Zie [gegevens vernieuwen in Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**Hoe toodelete uw oplossing**
Zorg ervoor dat de Hallo gegevensgenerator beëindigd als niet actief Hallo oplossing gebruiken zoals Hallo gegevensgenerator uitgevoerd wordt hogere kosten in rekening worden. Verwijder Hallo oplossing als u dit niet gebruikt. Uw oplossing verwijdert, worden alle Hallo-onderdelen in uw abonnement ingericht wanneer u Hallo oplossing hebt geïmplementeerd. toodelete hello oplossing, klikt u op de oplossingsnaam van uw in het linkerpaneel van oplossingssjabloon Hallo Hallo en klik op verwijderen.

## <a name="cost-estimation-tools"></a>**Schatting extra kosten**
Hallo zijn volgende twee hulpprogramma's beschikbaar toohelp beter begrip van de totale kosten die betrokken zijn bij Hallo voorspellen van de vraag voor oplossingssjabloon energie in uw abonnement:

* [Microsoft Azure kosten Estimator Tool (online)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure kosten Estimator Tool (desktop)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Bevestigingen**
In dit artikel is geschreven door gegevens wetenschappelijk Yijing Chen en software engineer Qiu Min bij Microsoft.
