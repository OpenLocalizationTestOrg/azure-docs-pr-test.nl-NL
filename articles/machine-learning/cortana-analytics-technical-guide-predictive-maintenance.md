---
title: Onderhoud aaaPredictive momenteel met Azure - Cortana Intelligence technische handleiding | Microsoft Docs
description: Een technische handleiding toohello sjabloon met Microsoft Cortana Intelligence-oplossing voor voorspeld onderhoud in ruimtevaart, hulpprogramma's en transport.
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Technische handleiding toohello Cortana Intelligence oplossingssjabloon voor voorspeld onderhoud in ruimtevaart en andere bedrijven

## <a name="important"></a>**Belangrijk**
In dit artikel is afgeschaft. Hallo-informatie is nog steeds relevante toohello probleem bij de hand, dat wil zeggen voorspeld onderhoud momenteel, maar de meest recente artikel Hallo Hello meest up toodate informatie vindt u [hier](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Bevestigingen**
In dit artikel is geschreven door gegevenswetenschappers Yan Zhang, Gauher Shaheen, Fidan Boylu Uz en software engineer Dan Grecoe bij Microsoft.

## <a name="overview"></a>**Overzicht**
Oplossingssjablonen zijn zo ontworpen tooaccelerate Hallo proces van het bouwen van een demo E2E boven op de Cortana Intelligence Suite. Een geïmplementeerde sjabloon wordt uw abonnement met vereiste onderdelen van de Cortana Intelligence inrichten en Hallo onderlinge relaties bouwen. Deze ook seeding Hallo data pipeline met voorbeeldgegevens die zijn gegenereerd op basis van een toepassing voor de generator van gegevens die u downloaden en installeren op uw lokale computer na het implementeren van Hallo oplossingssjabloon. Hallo-gegevens gegenereerd op basis van Hallo generator hydrate Hallo gegevens pijplijn en gaan genereren van machine learning voorspellingen die vervolgens kunnen worden weergegeven op Hallo Power BI-dashboard. Hallo-implementatieproces leidt u door de verschillende stappen tooset van de referenties van uw oplossing. Zorg ervoor dat u deze referenties zoals oplossingsnaam, gebruikersnaam en wachtwoord dat u tijdens de implementatie van Hallo opgeeft vastleggen.  

Hallo-doel van dit document is tooexplain Hallo-referentiearchitectuur en verschillende onderdelen die zijn ingericht in uw abonnement als onderdeel van de oplossingssjabloon voor deze. Hallo document ook wordt gesproken over het tooreplace de voorbeeldgegevens met echte gegevens van uw eigen toobe kunnen toosee inzicht en de voorspellingen van uw eigen gegevens. Hallo document wordt bovendien de onderdelen van Hallo oplossingssjabloon waarvoor toobe gewijzigd als u deze toocustomize Hallo oplossing met uw eigen gegevens wilde beschreven. Hallo achter vindt u instructies over hoe toobuild Power BI-dashboard Hallo voor deze oplossingssjabloon.

> [!TIP]
> U kunt downloaden en afdrukken een [PDF-versie van dit document](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Grote afbeelding**
![Architectuur voor voorspeld onderhoud](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Wanneer het Hallo-oplossing is geïmplementeerd, verschillende Azure-services binnen Cortana-Analytics Suite zijn geactiveerd (*dat wil zeggen* Event Hub, Stream Analytics, HDInsight, Data Factory Machine Learning, *enzovoort*). Hallo Architectuurdiagram van de bovenstaande toont, op een hoog niveau hoe Hallo voorspeld onderhoud voor lucht oplossingssjabloon is samengesteld uit de end-to-end. U zult kunnen tooinvestigate deze services in hello azure-portal door erop te klikken op Hallo oplossing sjabloon diagram gemaakt met de Hallo implementeren van Hallo-oplossing met uitzondering van de Hallo van HDInsight als deze service is ingericht op verzoek als hello-gerelateerd Pipeline-activiteiten zijn vereiste toorun en daarna verwijderd.
U kunt downloaden via een [volledige versie van Hallo diagram](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Hallo volgende secties beschrijven elk gegeven.

## <a name="data-source-and-ingestion"></a>**Gegevensbron en opnamesnelheid**
### <a name="synthetic-data-source"></a>Synthetische gegevensbron
Bron gebruikt wordt voor deze sjabloon Hallo gegevens gegenereerd vanuit een bureaubladtoepassing die u wilt downloaden en lokaal uitvoeren na een geslaagde implementatie. U Hallo instructies toodownload vinden en installeren van deze toepassing op Hallo Eigenschappenbalk wanneer u de eerste knooppunt Hallo voorspeld onderhoud Gegevensgenerator aangeroepen op Hallo oplossing sjabloon diagram selecteert. Deze toepassing hello feeds [Azure Event Hub](#azure-event-hub) service met gegevenspunten of gebeurtenissen die worden gebruikt in de rest Hallo van Hallo oplossing stroom. Deze gegevensbron bestaat uit of afgeleid uit openbaar beschikbare gegevens uit de [NASA gegevensopslagplaats](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) met Hallo [Turbofan Engine Degradation Simulation Data Set](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

Hallo-toepassing voor het genereren van gebeurtenis vult hello Azure Event Hub alleen terwijl deze wordt uitgevoerd op uw computer.

### <a name="azure-event-hub"></a>Azure event hub
Hallo [Azure Event Hub](https://azure.microsoft.com/services/event-hubs/) service is Hallo geadresseerde van Hallo invoer geleverd door Hallo synthetische gegevensbron die hierboven worden beschreven.

## <a name="data-preparation-and-analysis"></a>**Voorbereiden van gegevens en analyse**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hallo [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) -service is gebruikte tooprovide bijna realtime analyses op Hallo invoerstroom van Hallo [Azure Event Hub](#azure-event-hub) service en publiceren van de resultaten naar een [Power BI](https://powerbi.microsoft.com) dashboard, evenals alle onbewerkte binnenkomende gebeurtenissen toohello archiveren [Azure Storage](https://azure.microsoft.com/services/storage/) service later worden verwerkt door Hallo [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service.

### <a name="hd-insights-custom-aggregation"></a>HD Insights aangepaste aggregatie
Hallo HD inzicht van Azure-service is gebruikte toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts (gedirigeerd door Azure Data Factory) tooprovide aggregaties op Hallo onbewerkte gebeurtenissen die zijn gearchiveerd met hello Azure Stream Analytics-service.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) -service wordt gebruikt (gedirigeerd door Azure Data Factory) toomake voorspellingen op Hallo resterende levensduur (resterende Levensduur) van een bepaalde vliegtuigmotor gegeven Hallo invoer ontvangen.

## <a name="data-publishing"></a>**Gegevens publiceren**
### <a name="azure-sql-database-service"></a>Azure SQL Database-Service
Hallo [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) -service is gebruikte toostore (beheerd door Azure Data Factory) Hallo voorspellingen ontvangen door hello Azure Machine Learning-service die worden gebruikt in Hallo [Power BI](https://powerbi.microsoft.com) dashboard.

## <a name="data-consumption"></a>**Gegevens verbruik**
### <a name="power-bi"></a>Power BI
Hallo [Power BI](https://powerbi.microsoft.com) -service is gebruikte tooshow een dashboard met aggregaties en waarschuwingen die worden geleverd door Hallo [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) service en de resterende Levensduur voorspellingen opgeslagen in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) die zijn geproduceerd met Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) service. Voor instructies over hoe toobuild Power BI-dashboard voor deze oplossingssjabloon Hallo, Raadpleeg toohello hieronder.

## <a name="how-toobring-in-your-own-data"></a>**Hoe toobring in uw eigen gegevens**
Deze sectie wordt beschreven hoe toobring uw eigen gegevens tooAzure en wat gebieden waarvoor wijzigingen voor gegevens Hallo u doen in deze architectuur.

Het lijkt onwaarschijnlijk dat een gegevensset die u brengt overeenkomen met Hallo gegevensset die wordt gebruikt door Hallo [Turbofan Engine Degradation Simulation Data Set](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) voor deze oplossingssjabloon gebruikt. Inzicht in uw gegevens en de vereisten is cruciaal belang bij hoe u deze sjabloon toowork met uw eigen gegevens wijzigen. Als dit uw eerste blootstelling toohello Azure Machine Learning-service is, kunt u een inleiding tooit krijgen met behulp van Hallo voorbeeld in [hoe toocreate uw eerste experiment](machine-learning-create-experiment.md).

Hallo uit te voeren behandeld Hallo secties van Hallo-sjabloon die wijzigingen is vereist wanneer een nieuwe gegevensset wordt geïntroduceerd.

### <a name="azure-event-hub"></a>Azure Event Hub
Hello Azure Event Hub-service is zeer algemene zodanig dat de gegevens kan toohello hub worden geplaatst in CSV- of JSON-indeling. Er is geen speciale verwerking treedt op Hallo van Azure Event Hub, maar het is belangrijk dat u begrijpt Hallo-gegevens die wordt ingevoerd.

Dit document beschrijft niet hoe tooingest uw gegevens, maar u eenvoudig gebeurtenissen verzenden kunt of gegevens tooan Azure Event Hub met Hallo Event Hub-API's.

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
gebruikte tooprovide bijna realtime analyses is Hello Azure Stream Analytics-service door het lezen van gegevensstromen en het uitvoeren van de gegevens tooany aantal bronnen.

Voor voorspeld onderhoud voor lucht oplossingssjabloon hello bestaat de Azure Stream Analytics query uit vier subquery's, elk consumerende gebeurtenissen van hello Azure Event Hub-service en hoeven uitvoer vier verschillende locaties. Deze uitvoer bestaan uit drie Power BI-gegevenssets en een Azure-opslaglocatie.

Hello Azure Stream Analytics query kan worden gevonden door:

* Aanmelden bij hello Azure-portal
* Zoeken naar Hallo Stream Analytics-taken ![Stream Analytics-pictogram](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) die zijn gegenereerd tijdens het Hallo-oplossing is geïmplementeerd (*bijvoorbeeld*, **maintenancesa02asapbi** en **maintenancesa02asablob** voor de oplossing voor voorspeld onderhoud)
* Selecteren
  
  * ***INVOER*** tooview Hallo query invoer
  * ***QUERY*** tooview Hallo query zelf
  * ***LEVERT*** tooview Hallo andere uitvoer

Informatie over het samenstellen van Azure Stream Analytics query vindt u in Hallo [Stream Analytics Query verwijzing](https://msdn.microsoft.com/library/azure/dn834998.aspx) op MSDN.

In deze oplossing uitvoergegevenssets Hallo query's drie met bijna realtime analyses informatie over Hallo binnenkomende gegevensstroom tooa Power BI-dashboard die wordt geleverd als onderdeel van de oplossingssjabloon voor deze. Omdat er impliciete kennis over binnenkomende gegevensindeling hello, moet deze query's toobe gewijzigd op basis van indeling van uw gegevens.

Hallo-query in de tweede Stream Analytics-taak Hallo **maintenancesa02asablob** levert gewoon alle [Event Hub](https://azure.microsoft.com/services/event-hubs/) gebeurtenissen die moeten worden [Azure Storage](https://azure.microsoft.com/services/storage/) en daarom geen wijziging vereist ongeacht de gegevensindeling van uw als hello wordt informatie over de volledige gebeurtenis toostorage gestreamd.

### <a name="azure-data-factory"></a>Azure Data Factory
Hallo [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service ingedeeld Hallo verplaatsing en verwerking van gegevens. In de voorspeld onderhoud voor lucht oplossingssjabloon Hallo data factory bestaat uit drie [pijplijnen](../data-factory/data-factory-create-pipelines.md) die verplaatsen en het Hallo-gegevens met behulp van verschillende technologieën worden verwerkt.  U kunt uw gegevensfactory openen door Hallo Hallo Data Factory-knooppunt onder Hallo van Hallo oplossing sjabloon diagram gemaakt met de implementatie van Hallo oplossing Hallo openen. Hiervoor gaat u toohello gegevensfactory in uw Azure-portal. Als u fouten onder uw gegevenssets ziet, kunt u die negeren omdat deze vanwege toodata factory worden geïmplementeerd voordat Hallo gegevensgenerator werd gestart. Deze fouten doen niet voorkomen dat uw data factory werkt.

![Data Factory-gegevensset fouten](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

Deze sectie wordt beschreven Hallo nodig [pijplijnen](../data-factory/data-factory-create-pipelines.md) en [activiteiten](../data-factory/data-factory-create-pipelines.md) opgenomen in Hallo [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Hieronder ziet u de diagramweergave Hallo Hallo-oplossing.

![Azure Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Twee Hallo pijplijnen van deze factory bevatten [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts die gebruikt toopartition en Hallo cumulatieve gegevens zijn. Wanneer vermeld, Hallo scripts bevindt zich in Hallo [Azure Storage](https://azure.microsoft.com/services/storage/) account gemaakt tijdens de installatie. De locatie zijn: maintenancesascript\\\\script\\\\hive\\ \\ (of https://[Your oplossing name].blob.core.windows.net/maintenancesascript).

Vergelijkbare toohello [Azure Stream Analytics](#azure-stream-analytics-1) query's de [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts hebben impliciete kennis over binnenkomende gegevensindeling hello, deze query's moet toobe gewijzigd op basis van de indeling van gegevens en [functie-engineering](machine-learning-feature-selection-and-engineering.md) vereisten.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Dit [pijplijn](../data-factory/data-factory-create-pipelines.md) bevat een enkele activiteit - een [HDInsightHive](../data-factory/data-factory-hive-activity.md) activiteit met behulp van een [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) die wordt uitgevoerd een [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scriptgegevens toopartition Hallo plaatsen [Azure Storage](https://azure.microsoft.com/services/storage/) tijdens de [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) taak.

De [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script voor deze taak partitionering is ***AggregateFlightInfo.hql***

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Dit [pijplijn](../data-factory/data-factory-create-pipelines.md) bevat meerdere activiteiten en waarvan eindresultaat is berekend Hallo voorspellingen van Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) experimenten die zijn gekoppeld aan deze oplossingssjabloon.

Hallo-activiteiten die zijn opgenomen in dit zijn:

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) activiteit met behulp van een [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) die wordt uitgevoerd een [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script tooperform aggregaties en functie-engineering nodig zijn voor Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) experimenteren.
  De [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script voor deze taak partitionering is ***PrepareMLInput.hql***.
* [Kopiëren](https://msdn.microsoft.com/library/azure/dn835035.aspx) activiteit die wordt verplaatst Hallo resultaten van de [HDInsightHive](../data-factory/data-factory-hive-activity.md) activiteit tooa één [Azure Storage](https://azure.microsoft.com/services/storage/) blob die toegang op basis van worden kan de [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) activiteit.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) activiteit die Hallo aanroept [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) experiment, wat leidt tot Hallo resultaten worden opgeslagen in één [Azure Storage](https://azure.microsoft.com/services/storage/) blob.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Dit [pijplijn](../data-factory/data-factory-create-pipelines.md) bevat een enkele activiteit - een [kopie](https://msdn.microsoft.com/library/azure/dn835035.aspx) activiteit die wordt verplaatst Hallo resultaten van Hallo [Azure Machine Learning](#azure-machine-learning) experimenteren uit de *** MLScoringPipeline*** toohello [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) die als onderdeel van de installatie van de sjabloon oplossing is ingericht.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) experiment gebruikt voor de oplossingssjabloon voor deze biedt Hallo resterende nuttig Levensduur van een vliegtuigmotor. Hallo-experiment is specifiek toohello gegevensverzameling verbruikt en daarom moet wijziging of vervanging specifieke toohello gegevens die in gebracht.

Zie voor meer informatie over hoe hello Azure Machine Learning-experiment is gemaakt, [voorspeld onderhoud: stap 1 van 3, het voorbereiden van gegevens en functie-engineering](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**Voortgang van de monitor**
 Zodra het Hallo Gegevensgenerator wordt gestart, hello pijplijn begint tooget gehydrateerd en hello verschillende onderdelen van uw oplossing beginnen bij de start in de actie volgende Hallo opdrachten die zijn uitgegeven door Hallo Data Factory. Er zijn twee manieren die kunt u Hallo pijplijn bewaken.

1. Een van de Stream Analytics-taak Hallo schrijft Hallo onbewerkte binnenkomende tooblob gegevensopslag. Als u op voor Blob Storage-onderdeel van uw oplossing van welkomstscherm u de oplossing is geïmplementeerd Hallo en klik vervolgens op openen in het rechterpaneel hello, duurt het u toohello [beheerportal](https://portal.azure.com/). Klik op Blobs. In het volgende Configuratiescherm hello ziet u een lijst van Containers. Klik op **maintenancesadata**. In het volgende Configuratiescherm hello, ziet u Hallo **rawdata** map. Hallo rawdata-map, ziet u de mappen met de namen bijvoorbeeld uur = 17, uur = 18 enzovoort. Als u deze mappen ziet, betekent dit Hallo onbewerkte gegevens is voltooid wordt op uw computer wordt gegenereerd en opgeslagen in blob storage. U ziet de csv-bestanden die eindig grootte in MB in deze mappen moeten hebben.
2. laatste stap van de pijplijn Hallo Hallo is toowrite gegevens (bijvoorbeeld de voorspellingen van machine learning) in SQL-Database. Mogelijk hebt u toowait maximaal drie uur voor Hallo gegevens tooappear in SQL-Database. Eenzijdige toomonitor hoeveel gegevens zijn beschikbaar in de SQL-Database is via [azure-portal](https://manage.windowsazure.com/). Zoek in het linkerdeelvenster Hallo SQL-DATABASES ![SQL pictogram](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) en klik erop. Ga vervolgens naar de database **pmaintenancedb** en klik erop. Klik op volgende pagina Hallo Hallo onderaan op beheren
   
    ![Pictogram beheren](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    U kunt hier, klik op nieuwe Query en de query voor Hallo aantal rijen (bv. Selecteer count(*) van PMResult). Als uw database groeit, moet het aantal rijen in de tabel Hallo Hallo verhogen.

## <a name="power-bi-dashboard"></a>**Power BI-Dashboard**
### <a name="overview"></a>Overzicht
Deze sectie wordt beschreven hoe tooset van Power BI-dashboard toovisualize realtime gegevens uit Azure Stream Analytics (hot pad), evenals batch voorspelling resultaat is van een Azure machine learning (koude pad).

### <a name="setup-cold-path-dashboard"></a>Setup koude pad dashboard
Hallo essentiële doel is tooget de voorspellende resterende Levensduur (resterende gebruiksduur) van elke vliegtuigmotor in Hallo koude pad gegevens pijplijn zodra een vlucht (cyclus) is voltooid. Hallo voorspelling resultaat wordt elke drie uur voor het voorspellen van vliegtuigmotoren Hallo die u een vlucht Hallo tijdens de afgelopen drie uur hebt bijgewerkt.

Power BI verbinding tooan Azure SQL-database als de gegevensbron ervan, waar de voorspelling resultaten worden opgeslagen. Opmerking: 1) bij het implementeren van uw oplossing een echte voorspelling wordt weergegeven in de database Hallo binnen drie uur.
Hallo pbix-bestand met de Hallo Generator downloaden bevat enkele seedgegevens, zodat u meteen Hallo Power BI-dashboard kunt maken. 2) in deze stap Hallo vereiste toodownload en installeer Hallo gratis software is [van Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Hallo volgende stappen helpen u op hoe tooconnect hello pbix-bestand op Hallo van SQL Database die is geactiveerd op Hallo moment van implementatie van de oplossing met gegevens (*bijvoorbeeld*. resultaten van de voorspelling) voor visualisatie.

1. Hallo databasereferenties worden opgehaald.
   
   U moet **servernaam, databasenaam, gebruikersnaam en wachtwoord van de database** voordat u doorgaat toonext stappen. Hier volgen Hallo stappen tooguide u hoe toofind ze.
   
   * Eenmaal **'Azure SQL Database'** op uw oplossingssjabloon diagram wordt groen, klik hierop en klik op **'Openen'**.
   * Hier ziet u een nieuw tabblad/browservenster waarin hello Azure portal-pagina. Klik op **'Resourcegroepen'** in het linkerdeelvenster Hallo.
   * Hallo-abonnement u voor het implementeren van Hallo oplossing selecteren en selecteer vervolgens **' YourSolutionName\_ResourceGroup'**.
   * In Hallo nieuwe pop uit Configuratiescherm, klik op Hallo ![SQL pictogram](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) pictogram tooaccess uw database. De databasenaam van uw is de volgende toohello dit pictogram (*bijvoorbeeld*, **'pmaintenancedb'**), en Hallo **databaseservernaam** wordt vermeld onder Hallo Server name-eigenschap en moet worden gezocht vergelijkbare te**YourSoutionName.database.windows.net**.
   * Uw database **gebruikersnaam** en **wachtwoord** zijn Hallo hetzelfde als het Hallo-gebruikersnaam en wachtwoord eerder vastgelegd tijdens de implementatie van Hallo-oplossing.
2. De gegevensbron Hallo van Hallo koude pad rapportbestand bijwerken met Power BI Desktop.
   
   * In de map Hallo op uw PC waarop u hebt gedownload en het bestand Generator zijn uitgepakt, dubbelklikt u op de **PowerBI\\PredictiveMaintenanceAerospace.pbix** bestand. Als u eventuele waarschuwingsberichten ziet wanneer u Hallo bestand opent, deze negeren. Klik op Hallo bovenaan Hallo bestand **query's bewerken**.
     
     ![Query's bewerken](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Ziet u twee tabellen **RemainingUsefulLife** en **PMResult**. Selecteer de eerste tabel Hallo en klik op ![Query Instellingenpictogram](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) volgende te**'Source'** onder **'Toegepast stappen'** op Hallo rechts **Query instellingen**Configuratiescherm. Negeer eventuele waarschuwingsberichten die worden weergegeven.
   * Vervang in Hallo pop uit venster, **'Server'** en **'Database'** met uw eigen namen van de server en database en klik vervolgens op **'OK'**. Voor de servernaam van de, zorg ervoor dat u opgeeft Hallo-poort 1433 (**YourSoutionName.database.windows.net, 1433**). Laat het databaseveld Hallo als **pmaintenancedb**. Hallo waarschuwingsberichten die worden weergegeven op het welkomstscherm negeren.
   * In de volgende pop Hallo uit venster, ziet u twee opties in het linkerdeelvenster hello (**Windows** en **Database**). Klik op **'Database'**, vul uw **'Username'** en **'Password'** (dit is Hallo-gebruikersnaam en wachtwoord die u hebt ingevoerd toen u het eerst Hallo oplossing geïmplementeerd en gemaakt een Azure SQL database). In ***selecteren waarop deze instellingen tooapply niveau***, niveau databaseoptie controleren. Klik vervolgens op **'Connect'**.
   * Klik op de tweede tabel Hallo **PMResult** klikt u vervolgens op ![pictogram Navigatie](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) volgende te**'Source'** onder **'Toegepast stappen'** op Hallo rechts **Query-instellingen** deelvenster, en Hallo-server en databasenamen als in Hallo bovenstaande stappen bijwerken en klik op OK.
   * Als u de vorige pagina Begeleide back toohello bent, sluit u Hallo-venster. Een bericht verschijnt buiten: klik **toepassen**. Klik ten slotte Hallo **opslaan** knop toosave Hallo wijzigingen. Uw bestand Power BI heeft nu verbinding toohello server vastgesteld. Als uw visualisaties leeg zijn, moet dat u uitschakelen Hallo selecties op Hallo visualisaties toovisualize alle Hallo gegevens door te klikken op Hallo gum pictogram op Hallo rechtsboven Hallo legenda's. Hallo vernieuwen knop tooreflect nieuwe gegevens op Hallo visualisaties gebruiken. In eerste instantie alleen ziet u Hallo seedgegevens op uw visualisaties omdat de gegevensfactory Hallo geplande toorefresh elke drie uur. U ziet na drie uur nieuwe voorspellingen doorgevoerd in uw visualisaties Wanneer u Hallo gegevens vernieuwen.
3. (Optioneel) Hallo koude pad dashboard te publiceren[Power BI online](http://www.powerbi.com/). Houd er rekening mee dat deze stap moet een Power BI-account (of Office 365-account).
   
   * Klik op **'Publiceren'** en later enkele seconden verschijnt er een venster weergeven 'Publiceren tooPower BI geslaagd!' met een groen vinkje. Klik op onderstaande 'Open PredictiveMaintenanceAerospace.pbix in Power BI' Hallo-koppeling. toofind gedetailleerde instructies, Zie [publiceren vanuit Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * een nieuw dashboard toocreate: klikt u op Hallo  **+**  Meld u aan de volgende toothe **Dashboards** sectie in het linkerdeelvenster Hallo. Voer Hallo naam 'Voorspeld onderhoud Demo' voor dit nieuwe dashboard.
   * Nadat u Hallo rapport openen, klikt u op ![Punaisepictogram](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin het dashboard voor de tooyour visualisaties. toofind gedetailleerde instructies, Zie [een tegel tooa Power BI-dashboard uit een rapport vastmaken](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     De dashboardpagina toohello gaan en Hallo grootte en locatie van uw visualisaties aanpassen en hun titels bewerken. toofind gedetailleerde instructies over hoe tooedit uw tegels zien [bewerken een tegel--formaat, verplaatsen, wijzig de naam, pincode, verwijderen, voegt u hyperlink](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Hier volgt een voorbeeld van dashboard met sommige koude pad visualisaties vastgemaakt tooit.  Afhankelijk van hoe lang het uitvoeren van de gegevensgenerator van uw, kan de nummers op Hallo visualisaties afwijken.
     <br/>
     ![Laatste weergeven](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * tooschedule vernieuwing van het Hallo-gegevens, de muisaanwijzer op Hallo **PredictiveMaintenanceAerospace** gegevensset, klikt u op ![beletselteken pictogram](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) en kies vervolgens **schema vernieuwen**.
     <br/>
     **Opmerking:** als er een waarschuwing massage, klikt u op **referenties bewerken** en zorg ervoor dat de databasereferenties van uw Hallo zijn dezelfde als die wordt beschreven in stap 1.
     <br/>
     ![Geplande vernieuwing](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Vouw Hallo **schema vernieuwen** sectie. Schakel in 'uw gegevens up-to-date houden'.
     <br/>
   * Hallo vernieuwing op basis van de behoeften van uw plannen. toofind meer informatie Zie [gegevens vernieuwen in Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Hot pad dashboard instellen
volgende stappen uit Hallo leidt u hoe toovisualize realtime gegevens uitvoer van de Stream Analytics-taken die zijn gegenereerd op Hallo moment van implementatie van de oplossing. Een [Power BI online](http://www.powerbi.com/) -account is vereist tooperform Hallo stappen te volgen. Als u geen account hebt, kunt u [maken van een](https://powerbi.microsoft.com/pricing).

1. Power BI-uitvoer in Azure Stream Analytics (ASA) toevoegen.
   
   * U moet toofollow Hallo instructies in [Azure Stream Analytics & Power BI: een dashboard realtime analyses voor realtime zichtbaarheid van gegevensstromen](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset up Hallo-uitvoer van uw Azure Stream Analytics-taak als de stroom BI-dashboard.
   * Hallo ASA-query heeft drie uitvoer die **aircraftmonitor**, **aircraftalert**, en **flightsbyhour**. U kunt query Hallo weergeven door te klikken op het tabblad query. Bijbehorende tooeach van deze tabellen, moet u een uitvoer-tooASA tooadd. Bij het toevoegen van de eerste uitvoer hello (*bijvoorbeeld* **aircraftmonitor**) Zorg ervoor dat Hallo **Uitvoeraliassen**, **gegevenssetnaam** en  **Tabelnaam** zijn dezelfde Hallo (**aircraftmonitor**). Herhaal Hallo stappen tooadd levert voor **aircraftalert**, en **flightsbyhour**. Nadat u alle drie uitvoertabellen en Hallo ASA taak gestart hebt toegevoegd, krijgt u een bevestigingsbericht (*bijvoorbeeld*, 'Starten Stream Analytics-taak maintenancesa02asapbi is voltooid').
2. Meld u bij te[online in Power BI](http://www.powerbi.com)
   
   * Op Hallo links Configuratiescherm gegevenssets in mijn werkruimte de ***GEGEVENSSET*** namen **aircraftmonitor**, **aircraftalert**, en **flightsbyhour**moet worden weergegeven. Dit is Hallo streamen van gegevens die u vanuit Azure Stream Analytics in de vorige step.hello gegevensset Hallo gepusht **flightsbyhour** mogelijk niet weergegeven op Hallo dezelfde tijd als de andere twee gegevenssets vanwege toohello aard van de SQL-query Hallo achter Hallo het is. Echter, het weergegeven na een uur.
   * Zorg ervoor dat Hallo ***visualisaties*** deelvenster is geopend en wordt weergegeven aan de rechterkant van het welkomstscherm.
3. Wanneer u Hallo-gegevens die binnenkomen in Power BI hebt, kunt u beginnen Hallo streamen van gegevens te visualiseren. Hieronder volgt dat een voorbeeld-dashboard met visualisaties die bepaalde hot pad tooit vastgemaakt. U kunt andere dashboard tegels op basis van de juiste gegevenssets maken. Afhankelijk van hoe lang het uitvoeren van de gegevensgenerator van uw, kan de nummers op Hallo visualisaties afwijken.

    ![Dashboardweergave](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Hier volgen een aantal stappen-toocreate een van bovenstaande – Hallo-tegels Hallo 'vloot weergave van de vs Sensor 11. Drempelwaarde 48,26" tegel:
   
   * Klik op de gegevensset **aircraftmonitor** op Hallo links Configuratiescherm gegevenssets.
   * Klik op Hallo **lijndiagram** pictogram.
   * Klik op **verwerkte** in Hallo **velden** deelvenster zodat deze worden weergegeven onder 'As' in hello **visualisaties** deelvenster.
   * Klik op 's11' en ' s11\_waarschuwing ' zodat deze beide worden weergegeven onder "Waarden". Klik op het pijltje Hallo volgende te**s11** en **s11\_waarschuwing**, wijzigen van 'Sum' te 'Gemiddeld'.
   * Klik op **opslaan** op Hallo boven en noem Hallo rapport 'aircraftmonitor'. Het rapport met de naam 'aircraftmonitor' wordt weergegeven in Hallo **rapporten** sectie in Hallo **Navigator** in Hallo linkerdeelvenster.
   * Klik op Hallo **pincode Visual** pictogram op Hallo rechterbovenhoek van dit lijndiagram. Een venster 'Pincode tooDashboard' kan weergegeven voor u een dashboard te kiezen. Selecteer 'Voorspeld onderhoud Demo' en klik op 'Pincode'.
   * Hallo muisaanwijzer op deze tegel op Hallo dashboard, klikt u op Hallo "edit" pictogram op Hallo rechterbovenhoek toochange titel te 'vs wagenpark weergave van Sensor 11. Drempelwaarde 48,26" en subtitel te 'wordt gemiddeld over wagenpark na verloop van tijd'.

## <a name="how-toodelete-your-solution"></a>**Hoe toodelete uw oplossing**
Zorg ervoor dat de Hallo gegevensgenerator beëindigd als niet actief Hallo oplossing gebruiken zoals Hallo gegevensgenerator uitgevoerd wordt hogere kosten in rekening worden. Verwijder Hallo oplossing als u dit niet gebruikt. Uw oplossing verwijdert, worden alle Hallo-onderdelen in uw abonnement ingericht wanneer u Hallo oplossing hebt geïmplementeerd. toodelete hello oplossing, klikt u op de oplossingsnaam van uw in het linkerpaneel van oplossingssjabloon Hallo Hallo en klik op verwijderen.

## <a name="cost-estimation-tools"></a>**Schatting extra kosten**
Hallo zijn volgende twee hulpprogramma's beschikbaar toohelp beter begrip van de totale kosten die betrokken zijn bij Hallo voorspeld onderhoud voor lucht oplossingssjabloon in uw abonnement:

* [Microsoft Azure kosten Estimator Tool (online)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure kosten Estimator Tool (desktop)](http://www.microsoft.com/download/details.aspx?id=43376)

