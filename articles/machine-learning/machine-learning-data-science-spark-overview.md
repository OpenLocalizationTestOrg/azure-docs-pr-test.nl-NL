---
title: aaaOverview van Gegevenswetenschap met Spark op Azure HDInsight | Microsoft Docs
description: Hallo Spark MLlib toolkit biedt aanzienlijke machine learning modelleren mogelijkheden toohello gedistribueerd HDInsight-omgeving.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Overzicht van gegevenswetenschap met Spark op Azure HDInsight
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Deze reeks onderwerpen ziet u hoe toouse HDInsight Spark toocomplete algemene gegevenswetenschap taken zoals gegevensopname, functie-engineering, modellering en evaluatie van het model. Hallo-gegevens die worden gebruikt, is een voorbeeld van Hallo 2013 NYC taxi reis en tarief gegevensset. Hallo-modellen gebouwd bevatten logistic en lineaire regressie, willekeurige forests en kleurovergang gestimuleerd structuren. Hallo onderwerpen ook laten zien hoe toostore deze modellen in Azure blob storage (WASB) en hoe tooscore en evalueren hun voorspellende prestaties. Meer geavanceerde onderwerpen wordt uitgelegd hoe modellen kunnen worden getraind met sweeping kruisvalidatie en hyper-parameter. In dit onderwerp verwijst ook naar Hallo onderwerpen waarin wordt beschreven hoe tooset up Hallo Spark-cluster die u nodig hebt toocomplete Hallo stappen in Hallo-scenario's. 

## <a name="spark-and-mllib"></a>Spark en MLlib
[Spark](http://spark.apache.org/) is een parallelle verwerking van open-source framework die ondersteuning biedt voor in het geheugen verwerkingsprestaties tooboost Hallo van analytische big data-toepassingen. Hallo Spark-verwerkingsengine is gebouwd voor snelheid, gebruiksgemak en geavanceerde analyses. De Spark in-memory gedistribueerde rekencapaciteiten kunnen u een goede keuze voor Hallo zich herhalende algoritmen in machine learning- en grafiekberekeningen gebruikt. [MLlib](http://spark.apache.org/mllib/) is modelleren van Spark schaalbare machine learning-bibliotheek waardoor het Hallo algoritmische mogelijkheden toothis gedistribueerde omgeving. 

## <a name="hdinsight-spark"></a>Spark in HDInsight
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure gehoste aanbieden van open-source Spark. Biedt ook ondersteuning voor **Jupyter PySpark-notebooks** op Hallo Spark-cluster dat Spark SQL interactieve query's voor het transformeren, te filteren en visualiseren van gegevens die zijn opgeslagen in Azure BLOB's (WASB) kan worden uitgevoerd. PySpark is hello Python-API voor Spark. Hallo-codefragmenten die Hallo-oplossingen bieden en weergeven van de relevante Hallo gegevenspunten toovisualize Hallo hier uitvoeren in Jupyter-notebooks geïnstalleerd op Hallo Spark-clusters. Hallo modellering stappen in de volgende onderwerpen bevatten code die laat zien hoe tootrain, evalueren, opslaan en gebruiken van elk type model. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Instellen: De Spark-clusters en Jupyter-notebooks
Instellingsstappen en code vindt u in dit scenario voor het gebruik van een HDInsight Spark 1.6. Maar Jupyter-notebooks zijn opgegeven voor zowel HDInsight Spark 1.6 en 2.0 Spark-clusters. Een beschrijving van het Hallo-notitieblokken en -koppelingen toothem vindt u in Hallo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) voor Hallo GitHub-opslagplaats met ze. Bovendien Hallo code hier en in notitieblokken Hallo gekoppeld is algemeen en moet werken op een Spark-cluster. Als u geen van HDInsight Spark, Hallo clusterinstallatie gebruikmaakt en management stappen mogelijk enigszins afwijken van wat hier moet worden weergegeven. Voor het gemak vindt hier u koppelingen Hallo toohello Jupyter-notebooks voor Spark 1.6 (toobe worden uitgevoerd in de pySpark-kernel Hallo Hallo Jupyter-Notebook server) en Spark 2.0 (toobe in Hallo pySpark3 kernel Hallo Jupyter-Notebook server worden uitgevoerd):

### <a name="spark-16-notebooks"></a>Spark 1.6 laptops
Deze laptops zijn toobe in Hallo pySpark-kernel van Jupyter-notebook server worden uitgevoerd.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): bevat informatie over het tooperform gegevensverkenning, modelleren en batchscoreberekening met diverse verschillende algoritmen.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): bevat onderwerpen in de notebook #1 en de ontwikkeling van het model met hyperparameter afstemmen en kruisvalidatie.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): ziet u hoe toooperationalize een opgeslagen model met behulp van Python op HDInsight-clusters.

### <a name="spark-20-notebooks"></a>Spark 2.0-laptops
Deze laptops zijn toobe in Hallo pySpark3 kernel van Jupyter-notebook server worden uitgevoerd.

- [Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): dit bestand bevat informatie over hoe tooperform gegevensverkenning, modelleren en scores in Spark 2.0 opslagclusters die gebruikmaken van Hallo NYC Taxi reis en tarief gegevensset-beschreven [hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Deze laptop is mogelijk een goed uitgangspunt voor het snel verkennen Hallo-code die we voor Spark 2.0 hebt opgegeven. Voor een meer gedetailleerde notebook Hallo NYC Taxi gegevens analyseert, Zie de volgende notebook Hallo in deze lijst. Zie na deze lijst Hallo-opmerkingen die deze laptops vergelijken. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): dit bestand ziet u hoe tooperform gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van Hallo NYC Taxi reis en tarief set gegevens die worden beschreven [ Hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): dit bestand ziet u hoe tooperform gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van bekende luchtvaartmaatschappij tijdige vertrek Hallo de gegevensset van 2011 en 2012. We Hallo luchtvaartmaatschappij gegevensset geïntegreerd met Hallo luchthaven weer gegevens (bijvoorbeeld windsnelheid, temperatuur en hoogte enz.) voorafgaande toomodeling, zodat deze weer-functies kunnen worden opgenomen in het Hallo-model.

<!-- -->

> [!NOTE]
> Hallo luchtvaartmaatschappij dataset is toegevoegd toohello Spark 2.0 notitieblokken toobetter illustreren Hallo gebruik van de classificatie-algoritmen. Zie Hallo koppelingen voor meer informatie over luchtvaartmaatschappij tijdige vertrek gegevensset en weer gegevensset te volgen:

>- Luchtvaartmaatschappij tijdige vertrek gegevens: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Luchthaven weergegevens: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Hallo Spark 2.0 notitieblokken op Hallo NYC taxi en luchtvaartmaatschappij vlucht vertraging-gegevenssets duurt 10 minuten of meer toorun (afhankelijk van de grootte van de Hallo van uw HDI-cluster). Hallo eerste laptop in Hallo boven lijst geeft veel aspecten van Hallo gegevensverkenning, visualisatie en ML-model training in een laptop die minder tijd toorun met een lagere actieve NYC gegevensset duurt, in welke Hallo taxi en tarief bestanden vooraf lid zijn: [ Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) deze notebook neemt een veel kortere tijd toofinish (2-3 minuten) en kan worden een goed startpunt voor Hallo code snel verkennen we hebben opgegeven voor Spark 2.0. 

<!-- -->

Zie voor instructies over Hallo uitoefening van een model voor Spark 2.0 en de model-verbruik voor score berekenen, Hallo [Spark 1.6 document over het verbruik](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) voor een voorbeeld waarin wordt beschreven Hallo stappen die nodig zijn. toouse op Spark 2.0, vervang Hallo Python code-bestand met [dit bestand](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Vereisten
Hallo volgen procedures zijn verwante tooSpark 1.6. Voor Hallo Spark 2.0-versie: gebruik Hallo notitieblokken beschreven en toopreviously gekoppeld. 

1. u moet een Azure-abonnement hebben. Als u nog geen een, Zie [gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

2. u moet een toocomplete 1.6 Spark-cluster in dit scenario. toocreate, Zie Hallo instructies in [aan de slag: maken van Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Hallo-clustertype en -versie is opgegeven vanuit Hallo **clustertype Selecteer** menu. 

![Cluster configureren](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Zie voor een onderwerp waarin wordt uitgelegd hoe toouse Scala in plaats van Python toocomplete taken voor een end-to-end gegevens wetenschap proces, Hallo [Gegevenswetenschap met Spark op Azure met behulp van Scala](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Hallo NYC 2013 Taxi gegevens
Hallo NYC Taxi reis gegevens is ongeveer 20 GB gecomprimeerde door komma's gescheiden waarden (CSV)-bestanden (~ 48 GB ongecomprimeerde), die bestaat uit meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald. Elke record reis omvat Hallo ophalen en afgiftepunt en tijd, geanonimiseerde hack (van stuurprogramma) licentienummer, en nummer straten (taxi van unieke id). Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:

1. Hallo 'trip_data' CSV-bestanden reis details, zoals het aantal passagiers bevatten, kunnen worden opgepikt en dropoff verwijst, krachtvoertuigen duur en reis lengte. Hier volgen enkele voorbeeldrecords:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hallo 'trip_fare' CSV-bestanden bevatten details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald. Hier volgen enkele voorbeeldrecords:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

We hebben een steekproef 0,1% van deze bestanden en gekoppelde Hallo reis genomen\_gegevens en reis\_ritbedrag CSV-bestanden in een toouse één gegevensset als Hallo invoergegevensset voor dit scenario. Hallo unieke sleutel toojoin reis\_gegevens en reis\_tarief dat bestaat uit Hallo velden: straten, hack\_en ophalen van certificaat\_datetime. Elke record van Hallo gegevensset bevat Hallo kenmerken die vertegenwoordigt een reis NYC Taxi te volgen:

| Veld | Korte beschrijving |
| --- | --- |
| straten |Geanonimiseerde taxi straten (taxi unieke id) |
| hack_license |Geanonimiseerde Hackney regeleinde licentienummer |
| vendor_id |Taxi leveranciers-id |
| rate_code |Snelheid van de NYC taxi van tarief |
| store_and_fwd_flag |Store en voorwaarts markering |
| pickup_datetime |Datum en tijd kunnen worden opgepikt |
| dropoff_datetime |Dropoff datum en tijd |
| pickup_hour |Uur ophalen |
| pickup_week |Week van jaar Hallo ophalen |
| werkdag |Werkdag (bereik 1-7) |
| passenger_count |Aantal passagiers in een reis taxi |
| trip_time_in_secs |Reis tijd in seconden |
| trip_distance |Reis afstand afgelegd in mijl |
| pickup_longitude |Lengtegraad ophalen |
| pickup_latitude |Breedtegraad ophalen |
| dropoff_longitude |Lengtegraad Dropoff |
| dropoff_latitude |Dropoff breedtegraad |
| direct_distance |Afstand tussen pick up directe en dropoff locaties |
| payment_type |Betalingstype (CA's, creditcard enz.) |
| fare_amount |Tarief bedrag in |
| Extra kosten |Extra kosten |
| mta_tax |MTA belasting |
| tip_amount |Tip bedrag |
| tolls_amount |Tolgelden bedrag |
| total_amount |Totale hoeveelheid |
| punt |Gekantelde (0/1 voor Nee of Ja) |
| tip_class |Tip klasse (0: $0, 1: $0-5, 2: $6-10, 3: $11-20, 4: > $20) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Code van een Jupyter-notebook in Spark-cluster Hallo uitvoeren
U kunt starten Hallo Jupyter-Notebook van hello Azure-portal. Zoek uw Spark-cluster op uw dashboard en klik op de pagina voor het beheer voor uw cluster tooenter. tooopen hello laptop die is gekoppeld aan Hallo Spark-cluster, klik op **Clusterdashboards** -> **Jupyter-Notebook** .

![Clusterdashboards](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

U kunt ook te bladeren***https://CLUSTERNAME.azurehdinsight.NET/jupyter*** tooaccess Hallo Jupyter-Notebooks. Hallo CLUSTERNAME deel uitmaken van deze URL vervangen door Hallo-naam van uw eigen cluster. Hallo-wachtwoord moet u voor uw admin-account tooaccess Hallo laptops.

![Jupyter-Notebooks bladeren](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

Selecteer PySpark toosee een map met een paar voorbeelden van vooraf verpakte laptops die gebruikmaken van de PySpark API.hello laptops die de codevoorbeelden Hallo voor dit pakket van Spark onderwerp bevatten zijn beschikbaar op Hallo [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

U kunt uploaden Hallo notitieblokken rechtstreeks vanuit [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) toohello Jupyter-notebook server op uw Spark-cluster. Klik op de introductiepagina Hallo van uw Jupyter, Hallo **uploaden** knop op Hallo rechts deel uit van welkomstscherm. Hiermee opent u een Windows Verkenner. Hier kunt u Hallo GitHub (onbewerkte inhoud)-URL van hello laptop- en klik op Plakken **Open**. 

U ziet Hallo-bestandsnaam in de lijst met Jupyter-bestand met een **uploaden** knop opnieuw. Klik hierop **uploaden** knop. U hebt nu Hallo notebook geïmporteerd. Herhaal deze stappen tooupload Hallo andere notitieblokken van dit scenario.

> [!TIP]
> U kunt met de rechtermuisknop op Hallo koppelingen in de browser en selecteer **koppeling kopiëren** tooget Hallo github onbewerkte URL van inhoud. U kunt deze URL plakken in Hallo Jupyter uploaden bestand explorer in het dialoogvenster.
> 
> 

U kunt nu:

* Hallo code door te klikken op Hallo notebook bekijken.
* elke cel uitvoeren door te drukken **SHIFT + ENTER**.
* Hallo gehele notebook uitvoeren door te klikken op **cel** -> **uitvoeren**.
* Gebruik automatische visualisatie Hallo van query's.

> [!TIP]
> Hallo PySpark-kernel visualiseren automatisch Hallo-uitvoer van SQL (HiveQL)-query's. U krijgt u Hallo optie tooselect tussen verschillende soorten visualisaties (tabel-, cirkel, regel, gebied of balk) met behulp van Hallo **Type** menuknoppen in de notebook Hallo:
> 
> 

![Logistic regression ROC-curve voor algemene methode](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>Volgende stappen
Nu u een HDInsight Spark-cluster is ingesteld en Hallo Jupyter-notebooks met licentie zijn geüpload, bent u klaar toowork door Hallo-onderwerpen die overeenkomen met toohello drie PySpark laptops. Ze geven weer hoe tooexplore uw gegevens en vervolgens het toocreate en modellen in beslag nemen. Hallo geavanceerde gegevensverkenning en laptop toont hoe modelleren tooinclude kruisvalidatie, hyper-parameter sweeping en evaluatie van het model. 

**Gegevensverkenning en modellering met Spark:** Hallo gegevensset verkennen en maken, beoordelen en evalueren Hallo machine learning-modellen doorloopt Hallo [binaire classificatie en regressie modellen voor gegevens met Hallo Spark maken MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md) onderwerp.

**Model verbruik:** toolearn hoe tooscore Hallo classificatie en regressie modellen gemaakt in dit onderwerp raadpleegt [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md).

**Kruisvalidatie en hyperparameter sweeping**: Zie [geavanceerde gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) over de manier waarop modellen kunnen getraind met behulp van kruisvalidatie en hyper-parameter sweeping

