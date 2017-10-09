---
title: aaaDeep Duik in vehicle health voorspellen en die zorg draagt gewoonten - Azure | Microsoft Docs
description: Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende inzicht op vehicle health gebruiken en gewoonten besturen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Vehicle telemetrie analytics-oplossing playbook: diepgaand in Hallo-oplossing
Dit **menu** toohello secties van dit playbook koppelingen: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Deze sectie zoomt in op in elk van de fasen van het Hallo afgebeeld in Hallo oplossingsarchitectuur met instructies en verwijzingen voor aanpassing. 

## <a name="data-sources"></a>Gegevensbronnen
Hallo-oplossing maakt gebruik van twee verschillende gegevensbronnen:

* **gesimuleerde vehicle signalen en diagnostische gegevensset** en 
* **vehicle catalogus**

Er is een vehicle telematica simulator opgenomen als onderdeel van deze oplossing. Deze diagnostische gegevens verzendt en signalen bijbehorende toohello status van Hallo vehicle en toohello besturen patroon op een bepaald tijdstip. Klik op [Vehicle telematica Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle telematica Simulator Visual Studio-oplossing** voor aanpassingen op basis van uw vereisten. Hallo vehicle catalogus bevat een verwijzingsgegevensset met een Chassisnummer toomodel-toewijzing.

![Vehicle telematica simulator](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Afbeelding 1 – Vehicle telematica Simulator*

Dit is een JSON-indeling gegevensset met Hallo schema te volgen.

| Kolom | Beschrijving | Waarden |
| --- | --- | --- |
| CHASSISNUMMER |Willekeurig gegenereerde Vehicle id-nummer |Hiermee wordt opgehaald uit een master lijst 10.000 willekeurig gegenereerde vehicle-id's. |
| Externe temperatuur |Hallo buiten temperatuur waar Hallo vehicle wordt bestuurd |Willekeurig gegenereerd nummer tussen 0-100 |
| Engine temperatuur |Hallo-engine temperatuur van Hallo vehicle |Willekeurig gegenereerd nummer tussen 0-500 |
| Snelheid |Hallo-engine snelheid op welke Hallo vehicle wordt bestuurd. |Willekeurig gegenereerd nummer tussen 0-100 |
| Brandstof |Hallo brandstofpeil van Hallo vehicle |Willekeurig gegenereerd nummer tussen 0-100 (geeft brandstof niveau percentage) |
| EngineOil |Hallo-engine olie niveau van Hallo vehicle |Willekeurig gegenereerd nummer tussen 0-100 (geeft engine olie niveau percentage) |
| Druk band |Hallo band druk van Hallo vehicle |Willekeurig gegenereerde getal van 0 tot 50 (geeft band zware belasting op het niveau percentage) |
| Kilometerstand |Hallo kilometerstand van Hallo vehicle |Willekeurig gegenereerd nummer van 0 200000 |
| Accelerator_pedal_position |Hallo accelerator vorm positie van Hallo vehicle |Willekeurig gegenereerd nummer tussen 0-100 (geeft accelerator niveau percentage) |
| Parking_brake_status |Hiermee wordt aangegeven of Hallo vehicle geparkeerd of niet |True of False |
| Headlamp_status |Geeft aan waar Hallo licht op of niet |True of False |
| Brake_pedal_status |Hiermee wordt aangegeven of Hallo rempedaal wordt ingedrukt of niet |True of False |
| Transmission_gear_position |Hallo transmission tandwielpictogram positie van Hallo vehicle |Statussen: eerste, tweede, derde, vierde vijfde, zesde, zevende, achtste |
| Ignition_status |Hiermee wordt aangegeven of Hallo vehicle uitgevoerd of gestopt |True of False |
| Windshield_wiper_status |Hiermee wordt aangegeven of Hallo voorruit combinatie of niet is ingeschakeld |True of False |
| ABS |Hiermee wordt aangegeven of ABS is ingeschakeld of niet |True of False |
| tijdstempel |Hallo tijdstempel wanneer Hallo gegevenspunt wordt gemaakt |Date |
| Plaats |Hallo-locatie van Hallo vehicle |4 plaatsen zijn in deze oplossing: Bellevue, Redmond, Sammamish, Seattle |

Hallo vehicle model verwijzingsgegevensset bevat VIN toohello modeltoewijzing. 

| CHASSISNUMMER | Model |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Sedan |
| 8J0U8XCPRGW4Z3NQE |Hybride |
| WORG68Z2PLTNZDBI7 |Familie sedan |
| JTHMYHQTEPP4WBMRN |Sedan |
| W9FTHG27LZN1YWO0Y |Hybride |
| MHTP9N792PHK08WJM |Familie sedan |
| EI4QXI2AXVQQING4I |Sedan |
| 5KKR2VB4WHQH97PF8 |Hybride |
| W9NSZ423XZHAONYXB |Familie sedan |
| 26WJSGHX4MA5ROHNL |Converteerbaar |
| GHLUB6ONKMOSI7E77 |Station Wagon |
| 9C2RHVRVLMEJDBXLP |Compacte auto |
| BRNHVMZOUJ6EOCP32 |Kleine standaard |
| VCYVW0WUZNBTM594J |Sport auto |
| HNVCE6YFZSA5M82NY |Gemiddeld standaard |
| 4R30FOR7NUOBL05GJ |Station Wagon |
| WYNIIY42VKV6OQS1J |Grote standaard |
| 8Y5QKG27QET1RBK7I |Grote standaard |
| DF6OX2WSRA6511BVG |Coupé |
| Z2EOZWZBXAEW3E60T |Sedan |
| M4TV6IEALD5QDS3IR |Hybride |
| VHRA1Y2TGTA84F00H |Familie sedan |
| R0JAUHT1L1R3BIKI0 |Sedan |
| 9230C202Z60XX84AU |Hybride |
| T8DNDN5UDCWL7M72H |Familie sedan |
| 4WPYRUZII5YV7YA42 |Sedan |
| D1ZVY26UV2BFGHZNO |Hybride |
| XUF99EW9OIQOMV7Q7 |Familie sedan |
| 8OMCL3LGI7XNCC21U |Converteerbaar |
| ……. | |

### <a name="references"></a>Verwijzingen
[Vehicle telematica Simulator Visual Studio-oplossing](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Azure Event Hub](https://azure.microsoft.com/services/event-hubs/)

[Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Opname
Combinaties van Azure Event Hubs, Stream Analytics en Data Factory worden overgenomen tooingest Hallo vehicle signalen, Hallo diagnostische gebeurtenissen, en realtime en analytics batch. Al deze onderdelen zijn gemaakt en geconfigureerd als onderdeel van de implementatie van Hallo-oplossing. 

### <a name="real-time-analysis"></a>Realtime analyses
Hallo gebeurtenissen die worden gegenereerd door Hallo Vehicle telematica Simulator worden gepubliceerd toohello Event Hub gebruiken Hallo Event Hub SDK. Hallo Stream Analytics-taak opgenomen deze gebeurtenissen van Hallo Event Hub en processen Hallo gegevens in realtime tooanalyze Hallo vehicle health. 

![Event hub-dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Afbeelding 4: Event Hub-dashboard*

![Stream Analytics-taak verwerken van gegevens](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Afbeelding 5 - Stream Analytics-taak verwerken van gegevens*

Hallo Stream Analytics-taak;

* gegevens uit Event Hub Hallo opgenomen 
* voert een koppeling met Hallo verwijzing toomap Hallo vehicle VIN toohello bijbehorende gegevensmodel 
* persistente ze in Azure blob storage voor uitgebreide batch analytics. 

Hallo na Stream Analytics-query is gebruikt toopersist Hallo gegevens in Azure blob-opslag. 

![Stream Analytics-taak query voor gegevensopname](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Afbeelding 6 - Stream Analytics-taak query voor gegevensopname*

### <a name="batch-analysis"></a>Batchanalyse
Er zijn ook een extra volume van de gesimuleerde vehicle signalen en diagnostische gegevensset voor uitgebreidere batch analytics genereren. Dit is vereiste tooensure een goede representatief gegevensvolume voor batchverwerking. Voor dit doel gebruiken we een pijplijn met de naam 'PrepareSampleDataPipeline' in hello Azure Data Factory werkstroom toogenerate een jaar lang gesimuleerde vehicle signalen en diagnostische gegevensset. Klik op [Data Factory aangepaste activiteit](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload Hallo Data Factory aangepaste DotNet activiteit Visual Studio-oplossing voor aanpassingen op basis van uw vereisten. 

![Voorbeeldgegevens voor batchverwerking werkstroom voorbereiden](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Afbeelding 7: voorbeeldgegevens voorbereiden voor de werkstroom voor batch*

Hallo pijplijn bestaat uit een aangepaste ADF .net activiteit, hier weergeven:

![PrepareSampleDataPipeline activiteit](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Afbeelding 8 - PrepareSampleDataPipeline*

Hallo-pipeline met succes uitgevoerd als 'RawCarEventsTable' dataset is gemarkeerd als 'Gereed' één jaar waard gesimuleerde vehicle signalen en diagnostische worden gegevens geproduceerd. U ziet de volgende Hallo mappen en bestanden die zijn gemaakt in uw opslagaccount onder Hallo 'connectedcar' container:

![PrepareSampleDataPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Afbeelding 9 - PrepareSampleDataPipeline uitvoer*

### <a name="references"></a>Verwijzingen
[Azure Event Hub SDK voor streamopname](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Mogelijkheden van Azure Data Factory data movement](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet-activiteit](../data-factory/data-factory-use-custom-activities.md)

[Azure Data Factory DotNet activiteit visual studio-oplossing voor het voorbereiden van voorbeeldgegevens](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>Partitie Hallo gegevensset
Hallo onbewerkte semi-gestructureerde vehicle signalen en diagnostische gegevensset worden in Hallo gegevens voorbereiding stap naar een indeling maand/gepartitioneerd. Deze partitioneren bijdraagt aan het efficiënter uitvoeren van query's en schaalbare langdurige opslag vervolgens als eerste account Hallo doordat fault-over van een blob account toohello vol is. 

>[!NOTE] 
>Deze stap in Hallo-oplossing is van toepassing alleen toobatch verwerking.

Invoer en uitvoer gegevensbeheer gegevens:

* Hallo **uitvoergegevens** (met het label *PartitionedCarEventsTable*) is toobe gedurende een lange periode als Hallo fundamentele / 'rawest' vorm van gegevens in van de klant Hallo 'Data Lake'. 
* Hallo **invoergegevens** toothis pijplijn zou doorgaans worden verwijderd, omdat de uitvoergegevens Hallo volledige fidelity toohello invoer heeft-alleen wordt opgeslagen (gepartitioneerd) beter voor later gebruik.

![Partitie auto gebeurtenissen werkstroom](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Afbeelding 10 – partitie auto gebeurtenissen werkstroom*

de onbewerkte gegevens Hallo is gepartitioneerd met behulp van een HDInsight Hive-activiteit in 'PartitionCarEventsPipeline'. Hallo voorbeeldgegevens gegenereerd in stap 1 van een jaar is jaar/maand gepartitioneerd. Hallo-partities zijn gebruikte toogenerate vehicle signalen en diagnostische gegevens voor elke maand (totaal 12 partities) van een jaar. 

![PartitionCarEventsPipeline activiteit](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Afbeelding 11 - PartitionCarEventsPipeline*

***PartitionConnectedCarEvents Hive-Script***

Hallo volgende Hive-script met de naam 'partitioncarevents.hql' wordt gebruikt voor het partitioneren en bevindt zich in map van '\demo\src\connectedcar\scripts' Hallo van Hallo gedownloade zip. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.

![Gepartitioneerde uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Afbeelding 12 - gepartitioneerde uitvoer*

Hallo-gegevens nu is geoptimaliseerd, beter beheerbaar en gereed voor verdere verwerking toogain uitgebreide batch insights. 

## <a name="data-analysis"></a>Data-analyse
In deze sectie ziet u hoe toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory en Azure HDInsight voor rich geavanceerde analyses op de drager gezondheid en groot gewoonten. Er zijn drie subsecties hier:

1. **Machine Learning**: in deze subsectie bevat informatie over Hallo afwijkingsdetectie detectie experiment die wordt gebruikt in deze oplossing toopredict voertuigen vereisen onderhoud onderhoud en voertuigen teruggehaald vanwege problemen met toosafety vereisen.
2. **Analyse van realtime**: in deze subsectie bevat informatie over Hallo realtime-analyses met behulp van de Stream Analytics Query Language Hallo en operationele Hallo machine learning-experiment in realtime met een aangepaste toepassing.
3. **Batch-analyse**: in deze subsectie bevat informatie over Hallo transformeren en verwerking van Hallo batch gegevens met Azure HDInsight en Azure Machine Learning geoperationaliseerd door Azure Data Factory.

### <a name="machine-learning"></a>Machine Learning
Ons doel hier is toopredict Hallo voertuigen waarvoor onderhoud of intrekken op basis van bepaalde Health statistieken. Wij maken Hallo na veronderstellingen

* Als een van de Hallo na drie voorwaarden voldaan wordt, Hallo voertuigen vereisen **onderhoud onderhoud**:
  
  * Band druk is laag
  * Engine olie niveau is laag
  * Engine temperatuur is hoog
* Als een van de Hallo volgende voorwaarden voldaan wordt, Hallo voertuigen wellicht een **veiligheid probleem** en vereisen **intrekken**:
  
  * Engine temperatuur hoog is, maar externe temperatuur is laag
  * Engine temperatuur laag is, maar externe temperatuur is hoog

Op basis van de vorige vereisten hello, hebben we twee afzonderlijke modellen toodetect afwijkingen, één voor de detectie van vehicle onderhoud en één voor vehicle intrekken detectie gemaakt. In beide modellen, wordt Hallo ingebouwde Principal onderdeel Analysis (Pso)-algoritme gebruikt voor afwijkingsdetectie. 

**Model voor onderhoud**

Als een van drie indicatoren - band druk, engine olie of engine temperatuur - aan de respectieve voorwaarde voldoet, meldt Hallo onderhoud detectie model een afwijkingsdetectie. Als gevolg hiervan, alleen moet tooconsider deze drie variabelen bij het bouwen van Hallo-model. In ons experiment in Azure Machine Learning, gebruiken we eerst een **Select Columns in Dataset** module tooextract deze drie variabelen. We gebruiken naast Hallo PCA-gebaseerd anomaliedetectie detection module toobuild hello afwijkingsdetectie detectie model. 

Principal onderdeel analyse (Pso) is een techniek tot stand gebrachte in machine learning die toegepast toofeature selectie, classificatie en afwijkingsdetectie detectie worden kan. PCA zet een set krat met mogelijk gecorreleerde variabelen in een set waarden principal onderdelen genoemd. Hallo sleutel idee modellering PCA-gebaseerd is tooproject gegevens naar een lager dimensionale ruimte zodat functies en afwijkingen kunnen gemakkelijk worden geïdentificeerd.

Voor elke nieuwe invoer hello te detectie model, Hallo afwijkingsdetectie detectie eerst de projectie op Hallo eigenvectors wordt berekend en vervolgens berekent de Hallo herstel fout genormaliseerd. Deze fout genormaliseerde is Hallo afwijkingsdetectie score. Hallo hoger Hallo fout, hello meer afwijkende Hallo-exemplaar is. 

Hallo onderhoud detectie probleem kunt elke record worden beschouwd als een punt in een 3-dimensionale ruimte gedefinieerd door band druk, engine olie en temperatuur motor coördinaten. toocapture deze afwijkingen kunnen we Hallo oorspronkelijke gegevens in Hallo 3-dimensionale ruimte project naar een 2-dimensionale ruimte met behulp van Pso. We stellen dus Hallo parameter aantal onderdelen toouse in PCA toobe 2. Deze parameter speelt een belangrijke rol bij het toepassen van PCA-gebaseerd anomaliedetectie. Na projecteren gegevens met behulp van Pso, kunnen we deze afwijkingen gemakkelijker identificeren.

**Model voor afwijkingsdetectie intrekken** In Hallo intrekken afwijkingsdetectie detectie model gebruiken we Hallo Select Columns in Dataset en PCA-gebaseerd anomaliedetectie detectiemodules op soortgelijke wijze. In het bijzonder we drie variabelen - engine temperatuur, externe temperatuur en snelheid - hello gebruiken voor het eerst uitpakken **Select Columns in Dataset** module. We ook Hallo snelheid variabele omdat Hallo engine temperatuur meestal gecorreleerde toohello snelheid. We gebruiken naast PCA-gebaseerd anomaliedetectie module tooproject Hallo gegevens van 3-dimensionale ruimte Hallo naar een 2-dimensionale ruimte. Hallo intrekken criteria is voldaan en dus intrekken door Hallo vehicle is vereist wanneer engine temperatuur- en externe temperatuur maximaal negatieve worden gecorreleerd. PCA-gebaseerd anomaliedetectie-algoritme kunnen we Hallo afwijkingen vastleggen na het uitvoeren van Pso. 

Bij het model trainen, moeten we toouse normale gegevens, die geen onderhoud of intrekken als Hallo invoergegevens tootrain Hallo PCA-gebaseerd anomaliedetectie detectie model vereist. In Hallo score berekenen experiment, gebruiken we Hallo getraind afwijkingsdetectie detectie model toodetect al dan niet Hallo vehicle onderhoud of intrekken vereist. 

### <a name="real-time-analysis"></a>Realtime analyses
Hallo na Stream Analytics SQL-Query wordt gebruikt tooget Hallo gemiddelde van alle belangrijke vehicle parameters zoals vehicle snelheid, brandstofpeil engine temperatuur, kilometerstand, band druk, engine olie niveau en anderen Hallo. Hallo gemiddelde zijn gebruikte toodetect afwijkingen, waarschuwingen uitgeven, en bepalen Hallo algehele status voorwaarden van voertuigen in specifieke regio worden beheerd en die de correleren in toodemographics. 

![Stream Analytics query voor realtime verwerking](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Afbeelding 13-Stream Analytics query voor realtime verwerking*

Alle Hallo gemiddelden worden via een TumblingWindow 3 seconden berekend. We gebruiken TubmlingWindow in dit geval omdat we is vereist voor niet-overlappende en aaneengesloten tijdsintervallen. 

toolearn meer informatie over alle mogelijkheden van Hallo 'Windowing' in Azure Stream Analytics, klikt u op [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Realtime voorspelling**

Er is een toepassing in realtime opgenomen als onderdeel van Hallo oplossing toooperationalize Hallo machine learning-model. Deze toepassing met de naam 'RealTimeDashboardApp' is gemaakt en geconfigureerd als onderdeel van Hallo-oplossing implementatie. de toepassing Hello voert Hallo uit:

1. Tooan Event Hub-instantie waar Stream Analytics Hallo gebeurtenissen in een patroon continu publiceert luistert. ![Stream Analytics query voor het publiceren van gegevens Hallo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *afbeelding 14 – Stream Analytics query voor het publiceren van Hallo gegevens tooan uitvoer Event Hub-instantie* 
2. Voor elke gebeurtenis die deze toepassing ontvangt: 
   
   * Processen Hallo gegevens gebruik van het eindpunt van de Machine Learning aanvragen en antwoorden score berekenen (RR's). Hallo RRS eindpunt wordt automatisch gepubliceerd als onderdeel van Hallo-implementatie.
   * Hallo RRS uitvoer is gepubliceerde tooa Power BI gegevensset Hallo clientpush API's.

Dit patroon is ook van toepassing tooscenarios waaraan u een Line of Business (LoB)-toepassing met het Hallo realtime analyses flow, toointegrate voor scenario's zoals waarschuwingen, meldingen en messaging wilt.

Klik op [RealtimeDashboardApp downloaden](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio-oplossing voor aanpassingen. 

**tooexecute hello, realtime dashboardtoepassing**
1. Uitpakken en lokaal opslaan ![RealtimeDashboardApp map](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *afbeelding 16 – RealtimeDashboardApp map*  
2. Hallo toepassing RealtimeDashboardApp.exe uitvoeren
3. Geldige Power BI-referenties opgeven, meld u aan en klik op accepteren ![Realtime dashboard-app aanmelden tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Realtime dashboard-app aanmelden tooPower BI voltooien](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Afbeelding 17 – RealtimeDashboardApp: Aanmelden tooPower BI*

>[!NOTE] 
>Als u tooflush Hallo Power BI gegevensset wilt, uitvoeren Hallo RealtimeDashboardApp met Hallo 'flushdata' parameter: 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Batchanalyse
Hallo dient dit tooshow hoe Contoso motoren hello Azure compute mogelijkheden tooharness big data toogain veel inzichten gerichtheid patroon, gebruik gedrag en vehicle health gebruikmaakt. Dit maakt het mogelijk om te:

* Hallo klantervaring te verbeteren en goedkoper maken door op te geven inzicht gerichtheid gewoonten en efficiënte aangedreven gedrag brandstof
* Proactief meer over klanten en hun aangedreven patters toogovern zakelijke beslissingen te nemen en het beste Hallo op klasse-producten en services bieden

In deze oplossing ontwikkelt we Hallo metrische gegevens te volgen:

1. **Agressief gedrag besturen**: Hallo trend van Hallo modellen, locaties, aangedreven voorwaarden en tijd van Hallo jaar toogain inzicht in agressief aangedreven patronen identificeert. Contoso motoren kunnen deze inzichten gebruiken voor marketingcampagnes, nieuwe functies voor persoonlijke en verzekering op basis van informatie over het gebruik.
2. **Efficiënte aangedreven gedrag brandstof**: Hallo trend van Hallo modellen, locaties, aangedreven voorwaarden en tijd van Hallo jaar toogain inzicht op efficiënte aangedreven patronen brandstof identificeert. Contoso motoren kunt deze inzichten voor marketingcampagnes, kunnen nieuwe functies en proactieve reporting toohello stuurprogramma's voor kosten van kracht worden en de omgeving beschrijvende aangedreven gewoonten. 
3. **Intrekken van modellen**: identificeert modellen waarvoor teruggehaald operationele Hallo afwijkingsdetectie detectie machine learning-experiment

We bekijken in de details van elk van deze metrische gegevens, Hallo

**Agressieve aangedreven patroon**

Hallo vehicle signalen gepartitioneerd en diagnostische gegevens worden verwerkt in de pijplijn Hallo met de naam 'AggresiveDrivingPatternPipeline' met behulp van Hive toodetermine Hallo modellen, locatie, vehicle, besturen voorwaarden en andere parameters die vertoont agressieve aangedreven patroon.

![Agressieve aangedreven patroon werkstroom](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*figuur 18 – agressieve aangedreven patroon-werkstroom*


***Agressieve aangedreven patroon Hive-query***

Hallo Hive-script met de naam 'aggresivedriving.hql"gebruikt voor het analyseren van agressieve aangedreven voorwaarde patroon bevindt zich in de map '\demo\src\connectedcar\scripts' van Hallo gedownloade zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Hallo combinatie van drager van verzending tandwielpictogram positie, bedient vorm status en snelheid toodetect roekeloze/agressief gedrag op basis van het patroon met hoge snelheid remmen groot wordt gebruikt. 

Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.

![AggressiveDrivingPatternPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Afbeelding 19-AggressiveDrivingPatternPipeline uitvoer*

**Brandstof efficiënt aangedreven patroon**

Hallo vehicle signalen gepartitioneerd en diagnostische gegevens worden verwerkt in Hallo-pijplijn met de naam 'FuelEfficientDrivingPatternPipeline'. Hive is gebruikte toodetermine Hallo modellen, locatie, vehicle, aangedreven voorwaarden en andere eigenschappen die brandstof efficiënt aangedreven patroon vertonen.

![Fuel-Efficient aangedreven patroon](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Afbeelding 20 – Fuel-efficient aangedreven patroon-werkstroom*

***Brandstof efficiënt aangedreven patroon Hive-query***

Hallo Hive-script met de naam 'fuelefficientdriving.hql"gebruikt voor het analyseren van agressieve aangedreven voorwaarde patroon bevindt zich in de map '\demo\src\connectedcar\scripts' van Hallo gedownloade zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Hallo combinatie van de drager transmission tandwielpictogram positie, bedient vorm status snelheid en accelerator vorm positie toodetect brandstof efficiënt aangedreven gedrag op basis van versnelling, remmen, wordt gebruikt en patronen te versnellen. 

Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.

![FuelEfficientDrivingPatternPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Afbeelding 21 – FuelEfficientDrivingPatternPipeline uitvoer*

**Voorspellingen intrekken**

Hallo machine learning-experiment worden ingericht en gepubliceerd als een webservice als onderdeel van Hallo-oplossing implementatie. Hallo score-eindpunt wordt gebruikt in deze werkstroom geregistreerd als een data factory gekoppelde service en geoperationaliseerd met behulp van data factory batch activiteit voor score berekenen.

![Machine Learning-eindpunt](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Afbeelding 22 – Machine learning-eindpunt is geregistreerd als een gekoppelde service in de gegevensfactory*

Hallo wordt geregistreerde gekoppelde service gebruikt in Hallo DetectAnomalyPipeline tooscore Hallo gegevens met behulp van Hallo afwijkingsdetectie detectie model. 

![Machine Learning score activiteit in de gegevensfactory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Afbeelding 23: Azure Machine Learning-Batchscoreberekening activiteit in de gegevensfactory* 

Er zijn enkele stappen die worden uitgevoerd in deze pijplijn voor het voorbereiden van gegevens, zodat deze kan worden geoperationaliseerd met Hallo score-webservice. 

![DetectAnomalyPipeline voor het voorspellen van voertuigen terughalen vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Afbeelding 24 – DetectAnomalyPipeline voor het voorspellen van voertuigen terughalen vereisen* 

***Afwijkingsdetectie detectie Hive-query***

Zodra Hallo score berekenen is voltooid, wordt een HDInsight-activiteit is gebruikte tooprocess en Hallo statistische gegevens die zijn aangemerkt als afwijkingen door Hallo-model met een kans score van 0,60 of hoger.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Nadat het Hallo-pipeline met succes is uitgevoerd, ziet u Hallo partities die worden gegenereerd in uw opslagaccount onder Hallo 'connectedcar' container te volgen.

![DetectAnomalyPipeline uitvoer](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Afbeelding 25 – DetectAnomalyPipeline uitvoer*

## <a name="publish"></a>Publiceren

### <a name="real-time-analysis"></a>Realtime analyses
Een van de Hallo query's in de Stream Analytics-taak Hallo Hallo gebeurtenissen tooan uitvoer publiceert Event Hub-instantie. 

![Stream Analytics-taak publiceert tooan uitvoer Event Hub-instantie](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Afbeelding 26 – Stream Analytics-taak publiceert tooan uitvoer Event Hub-instantie*

![Stream Analytics query toopublish toohello uitvoer Event Hub-instantie](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Afbeelding 27 – Stream Analytics query toopublish toohello uitvoer Event Hub-instantie*

Deze stroom van gebeurtenissen wordt verbruikt door Hallo die realtimedashboardapp deel van Hallo-oplossing uitmaken. Deze toepassing maakt gebruik van de webservice van Hallo Machine Learning-reactie op aanvragen voor score berekenen voor realtime en publiceert Hallo resulterende gegevens tooa Power BI gegevensset voor verbruik. 

### <a name="batch-analysis"></a>Batchanalyse
Hallo Hallo batch en realtime verwerking zijn gepubliceerde toohello Azure SQL Database-tabellen voor verbruik. Hello Azure SQL-Server, Database en Hallo tabellen worden automatisch gemaakt als onderdeel van het installatiescript Hallo. 

![Batch verwerking resultaten kopiëren toodata datamart werkstroom](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Afbeelding 28 – batchverwerking resultaten kopiëren toodata datamart werkstroom*

![Stream Analytics-taak publiceert toodata datamart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Afbeelding 29 – Stream Analytics-taak publiceert toodata datamart*

![Datamart-instelling van Data in Stream Analytics-taak](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Afbeelding 30 – datamart instellen in Stream Analytics-taak*

## <a name="consume"></a>Gebruiken
Power BI biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics. 

Klik hier voor gedetailleerde instructies over het instellen van Hallo Power BI-rapporten en het Hallo-dashboard. Hallo laatste dashboard ziet er als volgt:

![Power BI-dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Afbeelding 31 - Power BI-Dashboard*

## <a name="summary"></a>Samenvatting
Dit document bevat een gedetailleerde inzoomen Hallo Vehicle telemetrie Analytics-oplossing. Dit patroon met een lambda-architectuur voor gepresenteerd realtime en batch-analyses met voorspellingen en acties. Dit patroon van toepassing is tooa breed scala aan gebruiksvoorbeelden waarvoor hot pad (real-time) en analyses van koude pad (batch). 

