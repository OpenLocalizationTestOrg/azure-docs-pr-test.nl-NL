---
title: 'Schaalbare Gegevenswetenschap met Azure Data Lake: een end-to-end-overzicht | Microsoft Docs'
description: Hoe taken toouse Azure Data Lake toodo gegevens te verkennen en binaire classificatie op een dataset.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Schaalbare Gegevenswetenschap met Azure Data Lake: een end-to-end-overzicht
Dit overzicht toont hoe toouse Azure Data Lake toodo gegevensverkenning en binaire classificatie taken van een steekproef van de NYC Hallo taxi reis en tarief gegevensset toopredict al dan niet een tip worden betaald door een tarief. Dit leidt u door de stappen Hallo Hallo [Team gegevens wetenschap proces](http://aka.ms/datascienceprocess)end-to- end, van gegevens overname toomodel training en toohello implementatie van een webservice die Hallo model publiceert.

### <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics
Hallo [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) heeft alle Hallo mogelijkheden vereist toomake gemakkelijk voor gegevens verzameld toostore gegevens van elke grootte, vorm en de snelheid en tooconduct gegevensverwerking advanced analytics en machine learning-model met hoge schaalbaarheid in een rendabele manier.   U betaalt op basis van per taak alleen wanneer de gegevens daadwerkelijk wordt verwerkt. Azure Data Lake Analytics bevat U-SQL, een taal of overvloeiingen Hallo declaratieve aard van SQL met Hallo expressieve voordelen van C# tooprovide schaalbare gedistribueerde query-mogelijkheden. Hiermee kunt u tooprocess ongestructureerde gegevens door het schema toepassen op lezen, plaatst u aangepaste regels en door de gebruiker gedefinieerde functies (UDF's) en omvat uitbreidbaarheid tooenable fijn gedetailleerde controle over hoe tooexecute op grote schaal. toolearn meer informatie over het Hallo-ontwerpplan achter de U-SQL, Zie [Visual Studio-blogbericht](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Data Lake Analytics is ook een belangrijk onderdeel van Cortana Analytics Suite en werkt met Azure SQL Data Warehouse, Power BI en Data Factory. Hierdoor krijgt u een volledig cloud big data en geavanceerde analyses platform.

In dit scenario begint met het Hallo-vereisten en bronnen die nodig toocomplete Hallo taken met Data Lake Analytics die Hallo gegevens wetenschappelijke processen vormen en hoe beschrijven tooinstall ze. Het bevat een overzicht van Hallo gegevensverwerking stappen met U-SQL en tot slot wordt weergegeven hoe toouse Python en Hive met Azure Machine Learning Studio toobuild en Hallo voorspellende modellen implementeren. 

### <a name="u-sql-and-visual-studio"></a>U-SQL en Visual Studio
In dit scenario raadt het gebruik van Visual Studio tooedit U-SQL-scripts tooprocess Hallo gegevensset. Hallo U-SQL-scripts zijn hier beschreven en vindt u in een afzonderlijk bestand. Hallo-proces omvat opnemen en steekproef nemen van Hallo gegevens verkennen. U ziet ook hoe toorun een U-SQL script taak in hello Azure-portal. Hive-tabellen worden gemaakt voor het Hallo-gegevens in een gekoppelde HDInsight-cluster toofacilitate Hallo bouwen en de implementatie van een model binaire classificatie in Azure Machine Learning Studio.  

### <a name="python"></a>Python
In dit scenario bevat ook een sectie die laat zien hoe toobuild en implementeren van een Voorspellend model met behulp van Python met Azure Machine Learning Studio.  We voorzien van een Jupyter-notebook Hallo Python-scripts voor de stappen in dit proces. Hallo-notebook bevat een code voor een aantal extra functie engineering stappen en de modellen constructie zoals multiklassen classificatie en regressie modelleren bovendien toohello binaire classificatie model die hier wordt beschreven. Hallo regressie taak is toopredict Hallo hoeveelheid Hallo tip op basis van andere functies tip. 

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning Studio is gebruikte toobuild en Hallo voorspellende modellen implementeren. Dit wordt gedaan met behulp van twee methoden: eerst met Python-scripts en klik vervolgens met de Hive-tabellen in een HDInsight (Hadoop)-cluster.

### <a name="scripts"></a>Scripts
Alleen Hallo principal stappen worden beschreven in dit scenario. U kunt downloaden Hallo volledige **U-SQL-script** en **Jupyter-Notebook** van [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Vereisten
Voordat u deze onderwerpen, moet u de volgende Hallo hebben:

* Een Azure-abonnement. Als u nog geen een, Zie [gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* (Aanbevolen) Visual Studio 2013 of later. Als u nog geen een van deze versies zijn geïnstalleerd, kunt u downloaden met een gratis versie van de Community van [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> U kunt hello Azure Portal toosubmit Azure Data Lake-query's ook gebruiken in plaats van Visual Studio. We geven instructies over hoe toodo dus met Visual Studio, en ook op de portal in de sectie Hallo Hallo met de titel **verwerken van gegevens met U-SQL**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Gegevens wetenschappelijke omgeving voor Azure Data Lake voorbereiden
tooprepare Hallo gegevens wetenschappelijke omgeving voor dit scenario maakt Hallo resources te volgen:

* Azure Data Lake Store (ADLS) 
* Azure Data Lake Analytics (ADLA)
* Azure Blob storage-account
* Azure Machine Learning Studio-account
* Azure Data Lake Tools voor Visual Studio (aanbevolen)

Deze sectie biedt instructies voor het toocreate van deze bronnen. Als u toouse Hive-tabellen met Azure Machine Learning, in plaats van Python, toobuild een model kiest, moet u ook tooprovision een HDInsight (Hadoop)-cluster. Deze alternatieve procedure in in de juiste sectie Hallo hieronder beschreven.


> [!NOTE]
> Hallo **Azure Data Lake Store** kunnen worden gemaakt van afzonderlijk of bij het maken van Hallo **Azure Data Lake Analytics** als Hallo standaard opslag. Instructies voor het maken van elk van deze resources afzonderlijk hieronder wordt verwezen, maar moet Hallo Data Lake storage-account niet afzonderlijk worden gemaakt.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Maken van een Azure Data Lake Store


Maken van een ADLS van Hallo [Azure Portal](http://portal.azure.com). Zie voor meer informatie [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Ervoor tooset up Hallo Cluster AAD-identiteit in Hallo worden **DataSource** blade Hallo **optionele configuratie** blade er beschreven. 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Een Azure Data Lake Analytics-account maken
Maken van een account ADLA van Hallo [Azure Portal](http://portal.azure.com). Zie voor meer informatie [zelfstudie: aan de slag met Azure Data Lake Analytics met Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Een Azure Blob storage-account maken
Een Azure Blob storage-account maken vanuit Hallo [Azure Portal](http://portal.azure.com). Zie voor meer informatie, Hallo maken een opslagaccount in sectie [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Een Azure Machine Learning Studio-account instellen
Aanmelden van/naar Azure Machine Learning Studio vanuit Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) pagina. Klik op Hallo **nu aan de slag** knop en kies vervolgens een 'Gratis werkruimte' of 'Standaard werkruimte'. Hierna kunt u zich kunt toocreate experimenten in Azure ML Studio.  

### <a name="install-azure-data-lake-tools-recommended"></a>Installeren van Azure Data Lake Tools (aanbevolen)
Azure Data Lake Tools installeren voor uw versie van Visual Studio van [Azure Data Lake Tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

Nadat het Hallo-installatie wordt voltooid, opent u van Visual Studio. U ziet Hallo Data Lake tabblad Hallo menu Hallo bovenaan. Uw Azure-resources moeten worden weergegeven in het linkerpaneel Hallo wanneer je je bij uw Azure-account aanmelden.

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a>Hallo NYC Taxi reizen gegevensset
Hallo gegevensset wordt hier gebruikt, is een openbaar gegevensset--hello [NYC Taxi reizen gegevensset](http://www.andresmh.com/nyctaxitrips/). Hallo NYC Taxi reis gegevens bestaat uit ongeveer 20GB gecomprimeerde CSV-bestanden (~ 48GB ongecomprimeerde), opnemen van meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald. Elke record reis omvat Hallo ophalen en inleverbibliotheek locaties en tijden, geanonimiseerde inbreken licentienummer (stuurprogramma van) en Hallo nummer straten (taxi van unieke id). Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:

* Hallo 'trip_data' CSV bevat reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis. Hier volgen enkele voorbeeldrecords:
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* Hello trip_fare CSV details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald bevat. Hier volgen enkele voorbeeldrecords:
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hallo unieke sleutel toojoin reis\_gegevens en reis\_tarief bestaat uit de volgende drie velden Hallo: straten, hack\_licentie en ophalen van\_datetime. Hallo onbewerkte CSV-bestanden kunnen worden geopend vanuit een openbare Azure-opslag-blob. Hallo U-SQL-script voor deze koppeling in Hallo is [tabellen reis en tarief samenvoegen](#join) sectie.

## <a name="process-data-with-u-sql"></a>Verwerken van gegevens met U-SQL
Hallo gegevensverwerkingstaken geïllustreerd in deze sectie bevatten opnemen, controleren van de kwaliteit, verkennen en steekproef nemen van Hallo-gegevens. Ook wordt gedemonstreerd hoe toojoin reis en tarief tabellen. het laatste gedeelte Hallo toont uitvoeren een U-SQL-script taak van hello Azure-portal. Hier vindt u koppelingen tooeach subsectie:

* [Gegevensopname: in van een openbare blob-gegevens lezen](#ingest)
* [Data quality controles](#quality)
* [Gegevensverkenning](#explore)
* [Tabellen reis en tarief samenvoegen](#join)
* [Gegevens steekproeven](#sample)
* [U-SQL-taken uitvoeren](#run)

Hallo U-SQL-scripts zijn hier beschreven en vindt u in een afzonderlijk bestand. U kunt downloaden Hallo volledige **U-SQL-scripts** van [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

tooexecute U-SQL Visual Studio openen, klikt u op **File--> Nieuw Project-->**, kies **U-SQL Project**, een naam en sla het tooa map.

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> Het is mogelijk toouse hello Azure Portal tooexecute U-SQL in plaats van Visual Studio. U kunt toohello Azure Data Lake Analytics-resource op Hallo portal navigeert en het verzenden van query's rechtstreeks als geïllustreerd in de volgende afbeelding Hallo.
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Gegevensopname: In van een openbare blob-gegevens lezen
Hallo-locatie van Hallo gegevens in Azure blob Hallo waarnaar wordt verwezen als  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  en kunnen worden geëxtraheerd met behulp van **Extractors.Csv()**. Vervangen door uw eigen containernaam en opslagaccountnaam in de volgende scripts voor container_name@blob_storage_account_name hello wasb adres. Aangezien Hallo bestandsnamen in dezelfde indeling zijn, kunnen we gebruiken **reis\_data_ {\*\}CSV** tooread in alle 12 reis-bestanden. 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

Omdat er in de eerste rij Hallo headers, we moet tooremove Hallo headers en kolomtypen wijzigen in de juiste waarden. We kunnen opslaan Hallo verwerkt gegevens tooAzure Data Lake Storage met **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ of tooAzure Blob storage-account met  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** . 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

We kunnen op dezelfde manier lezen in Hallo tarief gegevenssets. Klik met de rechtermuisknop op Azure Data Lake Store, kunt u toolook uw gegevens op **Azure Portal--> Data Explorer** of **Verkenner** vanuit Visual Studio. 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Data quality controles
Nadat reis en tarief tabellen zijn gelezen, kunnen data quality controles worden uitgevoerd in de volgende manieren Hallo. Hallo resulterende CSV-bestanden zijn uitvoer tooAzure Blob storage of Azure Data Lake Store. 

Hallo aantal medallions en uniek aantal medallions vinden:

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

Deze medallions waarop meer dan 100 reizen vinden:

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

Ongeldige records in termen van pickup_longitude vinden:

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

Ontbrekende waarden vinden voor sommige variabelen:

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Gegevensverkenning
Kan doen we enkele gegevens verkenning tooget beter inzicht te krijgen van Hallo gegevens.

Hallo-distributie van reizen Gekantelde en punt niet vinden:

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

Hallo-distributie van tip bedrag met afgekapte waarden vinden: 0,5,10 en 20 bedragen.

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

Elementaire statistische gegevens van reis afstand vinden:

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Hallo percentielen van reis afstand vinden:

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a>Tabellen reis en tarief samenvoegen
Reis en tarief tabellen kunnen worden gekoppeld door straten, hack_license en pickup_time.

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Voor elk niveau van het aantal passagiers Hallo aantal records, gemiddelde tip bedrag, afwijking van tip bedrag, percentage Gekantelde heen te berekenen.

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Gegevens steekproeven
Eerst wordt willekeurig selecteren 0,1% Hallo gegevens uit de gekoppelde tabel Hallo:

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

We doen vervolgens steekproeven toepassing stratificatie door binaire variabele tip_class:

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>U-SQL-taken uitvoeren
Wanneer u klaar bent U-SQL-scripts, kunt u deze met uw Azure Data Lake Analytics-account toohello-server verzenden. Klik op **Data Lake**, **Submit Job**, selecteer uw **Analytics-Account**, kies **parallelle uitvoering**, en klik op **verzenden**  knop.  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

Wanneer het Hallo-taak met succes is voldaan, wordt Hallo status van de taak weergegeven in Visual Studio voor bewaking. Nadat het Hallo-taak is voltooid, kunt u zelfs replay Hallo taak uitvoeringsproces en uitzoeken Hallo bottleneck stappen tooimprove de efficiëntie van uw taak. U kunt ook gaan tooAzure Portal toocheck Hallo status van uw U-SQL-taken.

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

U kunt nu de uitvoerbestanden Hallo in Azure Blob storage of Azure Portal controleren. We gebruiken de voorbeeldgegevens Hallo toepassing stratificatie voor onze modelleren in de volgende stap Hallo.

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Bouwen en implementeren van modellen in Azure Machine Learning
Ziet u twee opties die beschikbaar zijn voor uw toopull gegevens in Azure Machine Learning toobuild en 

* In de eerste optie Hallo, gebruikt u Hallo door actieve gegevens die is geschreven tooan Azure-Blob (in Hallo **gegevens steekproeven** bovenstaande stap) en gebruik van Python toobuild en modellen van Azure Machine Learning implementeren. 
* In de tweede optie Hallo kunt u een query Hallo-gegevens in Azure Data Lake rechtstreeks met behulp van een Hive-query. Deze optie vereist dat u een nieuwe HDInsight-cluster maken, of gebruik een bestaand HDInsight-cluster waar Hallo Hive punt toohello NY Taxi gegevens in Azure Data Lake Storage-tabellen.  Beide deze opties hieronder besproken. 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a>Optie 1: Gebruik Python toobuild en machine learning-modellen implementeren
toobuild en implementeren van machine learning-modellen met behulp van Python, een Jupyter-Notebook maken op uw lokale computer of in Azure Machine Learning Studio. Hallo Jupyter-Notebook opgegeven op [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) bevat volledige code tooexplore Hallo, visualiseren van gegevens, functie-engineering, modellering en implementatie. In dit artikel, laten we zien alleen Hallo modelleren en implementatie. 

### <a name="import-python-libraries"></a>Python-bibliotheken importeren
In de volgorde toorun Hallo steekproef Jupyter-Notebook of Python-scriptbestand Hallo, hello volgende Python pakketten zijn vereist. Als u Hallo service van AzureML-Notebook gebruikt, zijn deze pakketten vooraf worden geïnstalleerd.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a>Lees in Hallo gegevens uit blob
* Verbindingsreeks   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* Lees in als tekst
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* Toevoegen van kolomnamen en afzonderlijke kolommen
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Sommige kolommen toonumeric wijzigen
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Machine learning-modellen maken
Hier maken we een model binaire classificatie toopredict of een zakenreis is punt of niet. Hallo Jupyter-Notebook kunt u andere twee modellen: multiklassen classificatie en regressie-modellen.

* Eerst moet u toocreate dummy-variabelen die kunnen worden gebruikt in scikit-modellen meer
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Gegevens kader voor Hallo model maken
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* Trainings- en testdoeleinden 60 40 splitsen
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* Logistic Regression in trainingset
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* Score testen gegevensset
  
        Y_test_pred = logit_fit.predict(X_test)
* Evaluatie van metrische gegevens berekenen
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>API-webservice bouwen en deze wordt gebruikt in Python
We willen toooperationalize Hallo machine learning-model nadat deze is opgebouwd. We gebruiken hier Hallo binaire logistic model als voorbeeld. Zorg ervoor dat Hallo scikit-versie in uw lokale machine is 0.15.1 meer. U hebt geen tooworry over deze als u Azure ML studio service gebruiken.

* Uw werkruimte-referenties uit de instellingen voor Azure ML studio vinden. Klik op in Azure Machine Learning Studio **instellingen** --> **naam** --> **autorisatie Tokens**. 
  
    ![C3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* Web-Service maken
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* Web Servicereferenties ophalen
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* Web service API-aanroep. U hebt toowait 5 tot 10 seconden na de vorige stap Hallo.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Optie 2: Maken en implementeren van modellen rechtstreeks in Azure Machine Learning
Azure Machine Learning Studio kunt lezen van gegevens rechtstreeks vanuit de Azure Data Lake Store en vervolgens worden gebruikte toocreate en implementeren van modellen. Deze methode maakt gebruik van een Hive-tabel verwijst op Hallo Azure Data Lake Store. Dit vereist dat een aparte Azure HDInsight-cluster worden ingericht, op welke Hallo Hive tabel is gemaakt. Hallo van de volgende secties tonen hoe toodo dit. 

### <a name="create-an-hdinsight-linux-cluster"></a>Een HDInsight Linux-Cluster maken
Maken van een HDInsight-Cluster (Linux) van Hallo [Azure Portal](http://portal.azure.com). Zie voor meer informatie, Hallo **maken van een HDInsight-cluster met toegang tooAzure Data Lake Store** in sectie [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Hive-tabel maken in HDInsight
We maken nu Hive-tabellen toobe gebruikt in Azure Machine Learning Studio in Hallo HDInsight-cluster met behulp van Hallo-gegevens in de vorige stap Hallo opgeslagen in Azure Data Lake Store. Ga toohello HDInsight-cluster zojuist hebt gemaakt. Klik op **instellingen** --> **eigenschappen** --> **Cluster AAD-identiteit** --> **ADLS-toegang**, Zorg dat uw Azure Data Lake Store-account is toegevoegd in de lijst Hallo met lezen, schrijven en uitvoeren van rechten. 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

Klik vervolgens op **Dashboard** volgende toohello **instellingen** knop en een venster wordt weergegeven. Klik op **Hive-weergave** rechtsboven Hallo pagina en u ziet in Hallo Hallo **Query-Editor**.

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Een tabel in de volgende Hive scripts toocreate Hallo plakken. Hallo-locatie van de gegevensbron is in Azure Data Lake Store-documentatie op deze manier: **adl://data_lake_store_name.azuredatalakestore.net:443/mapnaam/bestandsnaam**.

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


Wanneer het Hallo-query is voltooid, ziet u Hallo resultaten als volgt:

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Bouwen en implementeren van modellen in Azure Machine Learning Studio
We zijn nu gereed toobuild en implementeren van een model dat voorspelt al dan niet een tip met Azure Machine Learning wordt betaald. Hallo toepassing stratificatie voorbeeldgegevens is gereed toobe gebruikt in deze binaire classificatie (tip of niet) probleem. Hallo voorspellende modellen met multiklassen classificatie (tip_class) en regressie (tip_amount) kan ook worden gemaakt en geïmplementeerd met Azure Machine Learning Studio maar hier alleen wordt gedemonstreerd hoe toohandle Hallo case met behulp van Hallo binaire classificatie model.

1. Hallo-gegevens ophalen voor Azure ML Hallo met **importgegevens** module beschikbaar in Hallo **gegevensinvoer en uitvoer** sectie. Zie voor meer informatie, Hallo [gegevens importeren-module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) -verwijzingspagina.
2. Selecteer **Hive-Query** als Hallo **gegevensbron** in Hallo **eigenschappen** Configuratiescherm.
3. Plakken Hallo volgende Hive-script in Hallo **Hive databasequery** editor
   
        select * from nyc_stratified_sample;
4. Voer Hallo URI van HDInsight-cluster (dit vindt u in Azure Portal), Hadoop-referenties, de locatie van uitvoergegevens en Azure storage-accountnaam naam/sleutelcontainer.
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

Een voorbeeld van een binaire indeling experiment lezen van gegevens van Hive-tabel wordt weergegeven in onderstaande afbeelding ziet Hallo.

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

Nadat het Hallo-experiment is gemaakt, klikt u op **webservice ingesteld** --> **Predictive-webservice**

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

Voer Hallo automatisch gemaakt score berekenen experiment, wanneer deze is voltooid, klikt u op **Web Service implementeren**

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

Hallo web servicedashboard wordt kort weergegeven:

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Samenvatting
U kunt een omgeving met wetenschappelijke gegevens voor het bouwen van schaalbare end-to-end-oplossingen in Azure Data Lake hebt gemaakt door de procedure is voltooid. Deze omgeving is gebruikte tooanalyze een grote openbare gegevensset, duurt deze stappen Hallo canonieke Hallo gegevens wetenschappelijke processen van aanschaf van gegevens via een model training, en vervolgens toohello implementatie van Hallo model als een webservice. U-SQL is gebruikte tooprocess, verkennen en Hallo voorbeeldgegevens. Python en Hive zijn gebruikt met Azure Machine Learning Studio toobuild en implementeren van voorspellende modellen.

## <a name="whats-next"></a>Volgende stappen
Hallo leertraject voor de [Team gegevens wetenschap proces (TDSP)](http://aka.ms/datascienceprocess) biedt koppelingen tootopics met een beschrijving van elke stap in Hallo advanced analytics-proces. Er zijn een aantal scenario's die worden gespecificeerd op Hallo [Team gegevens wetenschap proces scenario's](data-science-process-walkthroughs.md) die toepassingen hoe pagina toouse resources en services in verschillende predictive analytics-scenario's:

* [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Data Warehouse](machine-learning-data-science-process-sqldw-walkthrough.md)
* [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md)
* [Hallo Team gegevens wetenschappelijke processen: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Overzicht van het gebruik van Hallo gegevens wetenschap proces Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md)

