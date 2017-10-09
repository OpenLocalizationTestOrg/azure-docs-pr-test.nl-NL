---
title: aaaExplore gegevens in een Hadoop-cluster en modellen maken in Azure Machine Learning | Microsoft Docs
description: Hallo Team gegevens wetenschappelijke processen voor een end-to-end-scenario die gebruikmaakt van een HDInsight Hadoop toobuild cluster en implementeren van een model met behulp van een openbaar gegevensset.
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>Hallo Team gegevens wetenschappelijke processen in actie: gebruik Azure HDInsight Hadoop-clusters
In dit scenario, gebruiken we Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md) aan een end-to-end-scenario met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/) toostore, verkennen en gegevens van de engineer van Hallo openbaar functies beschikbare [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset en toodown voorbeeldgegevens Hallo. Modellen van het Hallo-gegevens zijn gebouwd met Azure Machine Learning toohandle binaire en multiklassen classificatie en regressie voorspellende taken.

Zie voor een overzicht dat toont hoe toohandle een grotere gegevensset (1 terabyte) voor een vergelijkbaar scenario met behulp van HDInsight Hadoop-clusters voor gegevensverwerking, [Team gegevens wetenschap proces - met behulp van Azure HDInsight Hadoop-Clusters op een gegevensset 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).

Het is ook mogelijk toouse een IPython notebook tooaccomplish Hallo aangeboden Hallo scenario Hallo 1 TB gegevensset met taken. Gebruikers die zou zoals tootry contact met deze aanpak opnemen moet Hallo [Criteo scenario met behulp van een verbinding Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) onderwerp.

## <a name="dataset"></a>Beschrijving van de NYC Taxi reizen gegevensset
Hallo NYC Taxi reis gegevens is ongeveer 20GB gecomprimeerde door komma's gescheiden waarden (CSV)-bestanden (~ 48GB ongecomprimeerde), die bestaat uit meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald. Elke record reis omvat Hallo ophalen en inleverbibliotheek locatie en tijd, geanonimiseerde hack (van stuurprogramma) licentienummer en nummer straten (taxi van unieke id). Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:

1. Hallo 'trip_data' CSV-bestanden bevatten reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis. Hier volgen enkele voorbeeldrecords:
   
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

Hallo unieke sleutel toojoin reis\_gegevens en reis\_tarief dat bestaat uit Hallo velden: straten, hack\_en ophalen van certificaat\_datetime.

alle tooget Hallo details relevante tooa bepaalde reis is voldoende toojoin met drie sleutels: 'straten' Hallo ' inbreken\_licentie ' en ' ophalen\_datetime '.

Wanneer we deze opslaan in de Hive-tabellen kort beschreven sommige meer details van Hallo-gegevens.

## <a name="mltasks"></a>Voorbeelden van voorspelling taken
Wanneer gegevens nadert, helpt Hallo soort voorspellingen dat u toomake op basis van de analyse wilt bepalen verduidelijken Hallo taken dat u tooinclude van het proces moet.
Hier volgen drie voorbeelden van voorspelling problemen die we in dit overzicht waarvan formulering is gebaseerd op Hallo oplossen *tip\_bedrag*:

1. **Binaire classificatie**: voorspellen of een tip betaald is voor een reis, dat wil zeggen een *tip\_bedrag* die groter is dan $0 een voorbeeld van een positieve is, terwijl een *tip\_bedrag* van $0 is een voorbeeld van een negatief.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Multiklassen classificatie**: toopredict Hallo bereik van tip bedragen Hallo reis betaald. We delen Hallo *tip\_bedrag* in vijf opslaglocaties of klassen:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Regressie taak**: toopredict Hallo hoeveelheid Hallo tip voor een reis betaald.  

## <a name="setup"></a>Instellen van een HDInsight Hadoop-cluster voor geavanceerde analyses
> [!NOTE]
> Dit is doorgaans een **Admin** taak.
> 
> 

U kunt instellen wanneer er een Azure-omgeving voor geavanceerde analyses die gebruikmaakt van een HDInsight-cluster in drie stappen:

1. [Een opslagaccount maken](../storage/common/storage-create-storage-account.md): dit opslagaccount wordt gebruikt voor het opslaan van gegevens in Azure Blob Storage. Hallo-gegevens in HDInsight-clusters gebruikt ook bevinden zich hier.
2. [Aanpassen van Azure HDInsight Hadoop-clusters voor Hallo Advanced Analytics-proces en de technologie](machine-learning-data-science-customize-hadoop-cluster.md). Deze stap maakt een Azure HDInsight Hadoop-cluster met 64-bits Anaconda Python 2.7 geïnstalleerd op alle knooppunten. Er zijn twee belangrijke stappen tooremember tijdens het aanpassen van uw HDInsight-cluster.
   
   * Houd er rekening mee toolink Hallo storage-account gemaakt in stap 1 met uw HDInsight-cluster bij het maken van deze. Dit opslagaccount wordt gebruikt tooaccess gegevens dat wordt verwerkt binnen Hallo-cluster.
   * Nadat het Hallo-cluster is gemaakt, schakelt u RAS toohello hoofdknooppunt van Hallo-cluster. Navigeer toohello **configuratie** tabblad en klik op **externe inschakelen**. Deze stap bevat Hallo gebruikersreferenties gebruikt voor externe aanmelding.
3. [Maken van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md): deze Azure Machine Learning-werkruimte is gebruikte toobuild machine learning-modellen. Deze taak is gericht, na het voltooien van een initiële gegevensverkenning en omlaag steekproeven van Hallo HDInsight-cluster.

## <a name="getdata"></a>Hallo-gegevens ophalen uit een openbare bron
> [!NOTE]
> Dit is doorgaans een **Admin** taak.
> 
> 

Hallo tooget [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset van de openbare locatie, mag u Hallo-methoden die zijn beschreven in [gegevens verplaatsen tooand uit Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy Hallo gegevens tooyour machine.

Hier worden beschreven hoe gebruik AzCopy tootransfer Hallo bestanden met gegevens. toodownload en installeer AzCopy instructies Hallo op [aan de slag met het AzCopy-opdrachtregelprogramma Hallo](../storage/common/storage-use-azcopy.md).

1. Vanuit een opdrachtpromptvenster uitgeven Hallo AzCopy opdrachten te volgen en vervangt *< path_to_data_folder >* met de gewenste bestemming Hallo:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Wanneer Hallo kopie is voltooid, zijn in totaal 24 ZIP-bestanden in de map data Hallo gekozen. Pak Hallo gedownloade bestanden toohello dezelfde map op uw lokale machine. Noteer Hallo map waar Hallo ongecomprimeerde bestanden zich bevinden. Deze map worden waarnaar wordt verwezen tooas hello *< pad\_naar\_unzipped_data\_bestanden\>*  is het volgende.

## <a name="upload"></a>Hallo gegevens toohello standaardcontainer van Azure HDInsight Hadoop-cluster uploaden
> [!NOTE]
> Dit is doorgaans een **Admin** taak.
> 
> 

Volgende AzCopy opdrachten Vervang in Hallo Hallo parameters met Hallo werkelijke waarden die u hebt opgegeven bij het maken van Hallo Hadoop-cluster te volgen en ritsen Hallo gegevensbestanden worden opgeslagen.

* ***&#60; path_to_data_folder >*** Hallo-directory (samen met het pad) op uw computer met bestanden die zijn uitgepakt Hallo gegevens  
* ***&#60; opslagaccountnaam van Hadoop-cluster >*** Hallo storage-account die is gekoppeld aan uw HDInsight-cluster
* ***&#60; standaardcontainer van Hadoop-cluster >*** Hallo standaardcontainer gebruikt door het cluster. Houd er rekening mee dat Hallo-naam van de standaard Hallo container is meestal Hallo dezelfde naam als Hallo cluster zelf. Als het Hallo-cluster wordt 'abc123.azurehdinsight.net' genoemd, is de standaardcontainer Hallo abc123.
* ***&#60; opslagaccountsleutel >*** Hallo-sleutel voor Hallo storage-account die wordt gebruikt door het cluster

Hallo na twee AzCopy opdrachten vanaf een opdrachtprompt of een Windows PowerShell-venster op de computer worden uitgevoerd.

Met deze opdracht Hallo reis gegevens te uploaden***nyctaxitripraw*** map in de standaardcontainer Hallo van Hallo Hadoop-cluster.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

Met deze opdracht Hallo tarief gegevens te uploaden***nyctaxifareraw*** map in de standaardcontainer Hallo van Hallo Hadoop-cluster.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

Hallo gegevens moet nu in Azure Blob Storage en gereed toobe verbruikt binnen Hallo HDInsight-cluster.

## <a name="#download-hql-files"></a>Meld u aan bij de hoofdknooppunt Hallo van Hadoop-cluster en en voorbereiden voor experimentele data-analyse
> [!NOTE]
> Dit is doorgaans een **Admin** taak.
> 
> 

tooaccess hello hoofdknooppunt van Hallo cluster voor experimentele data-analyse en omlaag steekproeven van het Hallo-gegevens, volgt u Hallo procedure beschreven in [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

In dit scenario, gebruiken we voornamelijk query's die zijn geschreven [Hive](https://hive.apache.org/), een querytaal SQL-achtige, tooperform voorlopige gegevens explorations. Hallo Hive-query's worden opgeslagen in .hql bestanden. We vervolgens steekproef deze gegevens toobe in Azure Machine Learning gebruikt voor het bouwen van modellen omlaag.

tooprepare hello cluster voor experimentele data-analyse, we downloaden Hallo .hql bestanden met relevante Hive-scripts Hallo van [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa lokale map (C:\temp) op Hallo hoofdknooppunt. toodo deze, open Hallo **opdrachtprompt** vanuit Hallo hoofdknooppunt Hallo-cluster en probleem Hallo volgende twee opdrachten:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Deze twee opdrachten zal alle .hql bestanden downloaden die nodig zijn in dit scenario toohello lokale directory ***C:\temp &#92;*** in Hallo hoofdknooppunt.

## <a name="#hive-db-tables"></a>Hive-database en per maand gepartitioneerde tabellen maken
> [!NOTE]
> Dit is doorgaans een **Admin** taak.
> 
> 

Er zijn nu gereed toocreate Hive-tabellen voor onze NYC taxi dataset.
Open in hoofdknooppunt Hallo van Hadoop-cluster Hallo Hallo ***Hadoop-opdrachtregel*** op bureaublad van hoofdknooppunt Hallo Hallo en Voer Hallo Hive directory door te voeren opdracht Hallo

    cd %hive_home%\bin

> [!NOTE]
> **Alle Hive-opdrachten uitvoeren in dit overzicht van Hallo hierboven Hive bin / directory prompt. Dit zorgt voor problemen die pad automatisch. We gebruiken Hallo termen 'Hive directory prompt', ' Hive bin / directory prompt ', en "Hadoop-opdrachtregel ' door elkaar in dit scenario.**
> 
> 

Voer vanaf Hallo Hive directory prompt Hallo opdracht in Hadoop opdrachtregel van Hallo hoofdknooppunt toosubmit Hallo Hive query toocreate Hive-database en tabellen te volgen:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Hier volgt Hallo inhoud Hallo ***C:\temp\sample\_hive\_maken\_db\_en\_tables.hql*** -bestand dat wordt gemaakt van Hive database ***nyctaxidb *** en tabellen ***reis*** en ***tarief***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Deze Hive-script maakt twee tabellen:

* Hallo 'trip' tabel bevat reis details van elke rijpositie (stuurprogrammagegevens, ophalen tijd, reis afstand en tijden)
* Hallo 'tarief' tabel bevat tarief details (tarief, tip bedrag, tolgelden en toeslagen).

Als u extra hulp nodig hebt met deze procedures of tooinvestigate alternatieve waarden wilt, raadpleegt u Hallo sectie [indienen Hive-query's rechtstreeks vanuit Hallo Hadoop-opdrachtregel ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Laad tooHive gegevenstabellen door partities
> [!NOTE]
> Dit is doorgaans een **Admin** taak.
> 
> 

Hallo NYC taxi gegevensset heeft een natuurlijke partitioneren per maand, die we tooenable verwerking en queryprestaties sneller worden gebruikt. Hallo onderstaande PowerShell-opdrachten (uitgegeven door Hallo Hive directory via Hallo **Hadoop-opdrachtregel**) laden van gegevens toohello 'trip' en 'tarief' Hive-tabellen gepartitioneerd per maand.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Hallo *voorbeeld\_hive\_laden\_gegevens\_door\_partitions.hql* bestand bevat de volgende Hallo **laden** opdrachten.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Opmerking een aantal Hive-query's die we hier in Hallo exploratie proces gebruiken betrekking hebben op slechts één partitie of op een aantal partities opzoeken. Maar deze query's over Hallo volledige gegevens kunnen worden uitgevoerd.

### <a name="#show-db"></a>Databases weergeven in Hallo HDInsight Hadoop-cluster
tooshow hello databases die zijn gemaakt in HDInsight Hadoop-cluster in Hallo Hadoop opdrachtregelvenster, Hallo volgende opdracht in de Hadoop-opdrachtregel uitvoeren:

    hive -e "show databases;"

### <a name="#show-tables"></a>Hallo Hive-tabellen in Hallo nyctaxidb database weergeven
tooshow hello tabellen in Hallo nyctaxidb database Hallo volgende opdracht in de Hadoop-opdrachtregel uitvoeren:

    hive -e "show tables in nyctaxidb;"

We kunt bevestigen dat Hallo tabellen worden gepartitioneerd door onderstaande Hallo-opdracht:

    hive -e "show partitions nyctaxidb.trip;"

Hallo verwachte uitvoer wordt hieronder weergegeven:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

Op deze manier kunnen we dat die Hallo tarief tabel is gepartitioneerd door onderstaande Hallo-opdracht:

    hive -e "show partitions nyctaxidb.fare;"

Hallo verwachte uitvoer wordt hieronder weergegeven:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Gegevensverkenning en functie-engineering in component
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Hallo gegevensverkenning en functies van technische taken voor Hallo gegevens geladen in de Hive-tabellen Hallo kan worden gerealiseerd met Hive-query's. Hier volgen enkele voorbeelden van dergelijke taken dat we in deze sectie doorlopen:

* Hallo bovenste 10 records weergeven in beide tabellen.
* Verken de gegevens distributies van enkele velden in verschillende tijdvensters.
* Onderzoek de kwaliteit van de gegevens van Hallo breedtegraad velden.
* Genereren van binaire en multiklassen classificatielabels op basis van Hallo **tip\_bedrag**.
* Functies door Hallo directe trip afstanden computing genereren.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Exploratie: Hallo bovenste 10 records in de tabel reis weergeven
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

toosee hoe gegevens Hallo zien eruit, we naar de 10 records uit elke tabel. Hallo twee query's afzonderlijk volgende uit Hallo Hive directory prompt in Hallo Hadoop-opdrachtregel console tooinspect Hallo records worden uitgevoerd.

tooget hello bovenste 10 records in de tabel Hallo 'trip' van de eerste maand Hallo:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello bovenste 10 records in de tabel Hallo 'tarief' van de eerste maand Hallo:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

Het is vaak nuttig toosave Hallo records tooa bestand om handige weer te geven. Een kleine wijziging toohello hierboven query bewerkstelligt dit:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Exploratie: Hallo aantal records dat in alle Hallo 12 partities weergeven
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Is van belang hoe Hallo aantal reizen tijdens kalenderjaar Hallo varieert Hallo. Groeperen per maand, kunnen wij toosee hoe deze verdeling van reizen eruit ziet.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Hierdoor hebt ons Hallo uitvoer:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

Hier de eerste kolom Hallo Hallo maand en Hallo tweede Hallo aantal reizen voor die maand.

We kunnen ook Hallo kunt u het totale aantal records in onze gegevensset reis tellen door uitgifte van de volgende opdracht bij de opdrachtprompt van de map Hallo Hive Hallo.

    hive -e "select count(*) from nyctaxidb.trip;"

Dit levert:

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

Opdrachten vergelijkbare toothose weergegeven voor Hallo reis gegevensset kunnen we Hive-query's uit Hallo Hive directory prompt voor Hallo tarief gegevensset toovalidate Hallo aantal records uitgeven.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Hierdoor hebt ons Hallo uitvoer:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Houd er rekening mee dat Hallo exact hetzelfde aantal bezoeken per maand wordt geretourneerd voor beide gegevenssets. Dit biedt Hallo eerste validatie die Hallo gegevens correct zijn geladen.

Hallo kunt u het totale aantal records in de gegevensset voor Hallo tarief tellen kan worden gedaan met de opdracht Hallo hieronder uit Hallo Hive directory opdrachtprompt:

    hive -e "select count(*) from nyctaxidb.fare;"

Dit levert:

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

Totaal aantal records in beide tabellen Hallo is ook Hallo dezelfde. Dit biedt een tweede validatie die Hallo gegevens correct zijn geladen.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploratie: Reis distributie door straten
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

In dit voorbeeld identificeert Hallo straten (taxi getallen) met meer dan 100 reizen binnen een bepaalde periode. Hallo query voordelen van Hallo gepartitioneerd tabeltoegang omdat deze wordt waarbij door Hallo partitie variabele **maand**. Hallo-queryresultaten tooa lokaal bestand queryoutput.tsv zijn geschreven in `C:\temp` op Hallo hoofdknooppunt.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Hier is Hallo inhoud van *voorbeeld\_hive\_reis\_aantal\_door\_medallion.hql* -bestand voor inspectie.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Hallo straten in Hallo NYC taxi gegevensset identificeert een unieke CAB-bestand. We kunnen identificeren welke cab-bestanden zijn 'bezet' door vragen aan welke u meer dan een bepaald aantal reizen aangebracht in een bepaalde periode. Hallo volgende voorbeeld identificeert cabinetbestanden die uit meer dan honderd reizen Hallo eerste drie maanden, en slaat Hallo query resultaten tooa lokaal bestand C:\temp\queryoutput.tsv.

Hier is Hallo inhoud van *voorbeeld\_hive\_reis\_aantal\_door\_medallion.hql* -bestand voor inspectie.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Component van Hallo directory prompt onderstaande probleem Hallo-opdracht:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploratie: Reis distributie door straten en hack_license
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Wanneer een dataset verkennen, willen we vaak tooexamine Hallo aantal co-exemplaren van groepen van waarden. Deze sectie vindt u een voorbeeld van hoe toodo dit voor CAB-bestanden en stuurprogramma's.

Hallo *voorbeeld\_hive\_reis\_aantal\_door\_straten\_license.hql* bestandsgroepen Hallo tarief gegevens is ingesteld op 'straten' en 'hack_license' en retourneert de aantallen voor elke combinatie. Hieronder vindt u de inhoud ervan.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Deze query retourneert CAB-bestand en een bepaald stuurprogramma combinaties gesorteerd op aflopende aantal heen.

Component van Hallo directory prompt, uitvoeren:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

Hallo-queryresultaten worden tooa lokaal bestand C:\temp\queryoutput.tsv geschreven.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Exploratie: Beoordeling van de kwaliteit van de gegevens door te controleren op Ongeldige lengtegraad/breedtegraad records
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Een algemene doelstelling van experimentele gegevensanalyse is tooweed ongeldige of onjuiste records. Hallo bepaalt voorbeeld in deze sectie of ofwel hello lengte of breedte velden een waarde ver buiten Hallo NYC gebied bevatten. Aangezien het waarschijnlijk dat dergelijke records een onjuiste lengtegraad-breedtegraadwaarden hebben, willen we tooeliminate van alle gegevens die toobe is gebruikt voor het model.

Hier is Hallo inhoud van *voorbeeld\_hive\_kwaliteit\_assessment.hql* -bestand voor inspectie.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


Component van Hallo directory prompt, uitvoeren:

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Hallo *-S* argument dat is opgenomen in deze opdracht wordt onderdrukt Hallo status scherm afdruk van Hallo kaart/verminderen Hive-taken. Dit is nuttig omdat op deze manier Hallo scherm afdrukken Hallo voor Hive-query-uitvoer beter leesbaar.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Exploratie: Binaire klasse distributies reis tips
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Voor binair klassificatieprobleem Hallo die worden beschreven in Hallo [voorbeelden van voorspelling taken](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sectie is nuttig tooknow of een tip of niet is opgegeven. Deze verdeling van tips is binaire:

* Tip gegeven (klasse 1, tip\_bedrag > $0)  
* Er is geen tip (klasse 0, tip\_bedrag = $0).

Hallo *voorbeeld\_hive\_punt\_frequencies.hql* bestand hieronder wordt weergegeven, wordt dit.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

Component van Hallo directory prompt, uitvoeren:

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>Exploratie: Klasse distributies in multiklassen Hallo-instelling
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Voor multiklassen klassificatieprobleem Hallo die worden beschreven in Hallo [voorbeelden van voorspelling taken](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sectie deze gegevensset ook gepaard tooa natuurlijke classificatie waar willen we graag toopredict Hallo hoeveelheid Hallo tips gegeven. We kunnen opslaglocaties toodefine tip bereiken in Hallo query gebruiken. tooget Hallo klasse Distributies voor Hallo verschillende tip bereiken, gebruiken we Hallo *voorbeeld\_hive\_tip\_bereik\_frequencies.hql* bestand. Hieronder vindt u de inhoud ervan.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Voert de volgende opdracht uit vanaf de opdrachtregel Hadoop console Hallo:

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Exploratie: Compute Direct afstand tussen twee lengtegraad breedtegraad-locaties
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Met een meting van Hallo direct afstand kunt ons toofind uit Hallo discrepantie is tussen deze en Hallo werkelijke krachtvoertuigen afstand. We deze functie stimuleren door wijzen dat een passagiers kleiner kan zijn waarschijnlijk tootip als ze dat stuurprogramma Hallo achterhalen ze opzettelijk heeft genomen door een veel langer route.

toosee hello vergelijking tussen de werkelijke reis afstand en Hallo [Haversine afstand](http://en.wikipedia.org/wiki/Haversine_formula) tussen twee lengtegraad breedtegraad punten (afstand Hallo 'groot cirkel'), gebruiken we Hallo trigonometrische functies beschikbaar binnen Hive, dus:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

In bovenstaande Hallo query, R is Hallo radius Hallo Earth in mijl en pi geconverteerde tooradians is. Houd er rekening mee dat Hallo lengtegraad breedtegraad punten zijn 'gefilterde' tooremove-waarden die verre Hallo NYC gebied zijn.

In dit geval schrijven we onze resultaten tooa map met de naam 'queryoutputdir'. Hallo reeks opdrachten die hieronder wordt weergegeven maakt eerst deze uitvoermap en Hallo Hive-opdracht wordt uitgevoerd.

Component van Hallo directory prompt, uitvoeren:

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Hallo queryresultaten worden geschreven too9 Azure blobs ***queryoutputdir/000000\_0*** te ***queryoutputdir/000008\_0*** onder de standaardcontainer Hallo van Hallo Hadoop-cluster.

toosee hello grootte van afzonderlijke blobs hello, we Hallo volgende opdracht uit Hallo Hive directory prompt uitvoeren:

    hdfs dfs -ls wasb:///queryoutputdir

toosee hello inhoud van een bepaald bestand spreken 000000\_0, gebruiken we de Hadoop `copyToLocal` opdracht dus.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> `copyToLocal`erg langzaam voor grote bestanden en wordt niet aanbevolen voor gebruik met deze.  
> 
> 

Een groot voordeel van deze gegevens zich bevinden in een Azure-blob is dat mogelijk besproken voor het Hallo-gegevens in Azure Machine Learning met Hallo [importgegevens] [ import-data] module.

## <a name="#downsample"></a>Omlaag gegevens en build samplemodellen in Azure Machine Learning
> [!NOTE]
> Dit is doorgaans een **gegevens wetenschappelijk** taak.
> 
> 

Na analysefase Hallo experimentele gegevens zijn er nu klaar toodown voorbeeldgegevens Hallo voor het bouwen van modellen in Azure Machine Learning. In deze sectie laten we zien hoe toouse een Hive query toodown Hallo voorbeeldgegevens, die vervolgens toegankelijk is vanuit Hallo [importgegevens] [ import-data] -module in Azure Machine Learning.

### <a name="down-sampling-hello-data"></a>Omlaag steekproef nemen van Hallo-gegevens
Er zijn twee stappen in deze procedure. Eerst we Hallo toevoegen **nyctaxidb.trip** en **nyctaxidb.fare** tabellen op de drie sleutels die aanwezig in alle records zijn: 'straten', ' inbreken\_licentie ', en "ophalen\_datetime-waarde '. Er vervolgens een label binaire classificatie gegenereerd **punt** en een label met meerdere klasse classificatie **tip\_klasse**.

toobe kunnen toouse Hallo omlaag steekproefgegevens rechtstreeks vanuit Hallo [importgegevens] [ import-data] module in Azure Machine Learning, is het nodig toostore Hallo resultaten van Hallo hierboven query tooan interne Hive-tabel. In het volgende, we een interne Hive-tabel maken en de inhoud ervan te vullen met Hallo die lid zijn van en naar beneden steekproefgegevens.

Hallo query geldt Hive standaardfuncties rechtstreeks toogenerate Hallo uur van de dag, week van jaar werkdag (1 staat voor maandag en 7 staat voor zondag) van Hallo ' ophalen\_datetime ' veld en Hallo direct afstand tussen Hallo ophalen en dropoff locaties. Gebruikers kunnen verwijzen, te[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) voor een volledige lijst van deze functies.

Hallo query daarna naar beneden voorbeelden Hallo gegevens zodat Hallo queryresultaten in hello Azure Machine Learning Studio inpassen kunnen. Alleen ongeveer 1% van de oorspronkelijke gegevensset hello wordt geïmporteerd in Hallo Studio.

Hieronder vindt u de inhoud Hallo van *voorbeeld\_hive\_voorbereiden\_voor\_aml\_full.hql* worden gegevens voorbereid voor model bouwen in Azure Machine Learning-bestand.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

toorun deze query uit Hallo Hive directory vragen:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Nu er een interne tabel 'nyctaxidb.nyctaxi_downsampled_dataset', wat kan worden geopend met behulp van Hallo [importgegevens] [ import-data] module op basis van Azure Machine Learning. We kunnen deze gegevensset bovendien gebruiken voor het bouwen van Machine Learning-modellen.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Hallo gegevens importeren-module gebruiken in Azure Machine Learning tooaccess Hallo omlaag steekproefgegevens
Vereisten voor het uitgeven van Hive-query's in Hallo [importgegevens] [ import-data] -module van Azure Machine Learning, moeten we tooan Azure Machine Learning-werkruimte te openen en toegang tot de referenties toohello Hallo cluster en de bijbehorende opslagaccount.

Sommige gegevens op Hallo [importgegevens] [ import-data] module en Hallo parameters tooinput:

**HCatalog server-URI**: als Hallo clusternaam abc123, wordt dit eenvoudig is: https://abc123.azurehdinsight.net

**Hadoop-gebruikersaccountnaam** : gebruikersnaam Hallo gekozen voor Hallo-cluster (**niet** Hallo RAS-gebruikersnaam)

**Hadoop ser accountwachtwoord** : Hallo wachtwoord gekozen voor Hallo-cluster (**niet** Hallo-wachtwoord voor externe toegang)

**Locatie van uitvoergegevens** : dit toobe Azure is gekozen.

**Naam van het Azure-opslagaccount** : naam van Hallo standaardopslagaccount die zijn gekoppeld aan het Hallo-cluster.

**Azure containernaam** : dit Hallo standaard containernaam voor Hallo-cluster is en wordt dezelfde doorgaans als clusternaam Hallo Hallo. Voor een cluster 'abc123' genoemd, is dit alleen abc123.

> [!IMPORTANT]
> **Een tabel die we willen tooquery Hallo met [importgegevens] [ import-data] module in Azure Machine Learning een interne tabel moet zijn.** Een tip om te bepalen of een tabel T in een database D.db een interne tabel is is als volgt.
> 
> 

Component van Hallo directory prompt probleem Hallo-opdracht:

    hdfs dfs -ls wasb:///D.db/T

Als Hallo-tabel een interne tabel is en dit ingevuld, wordt de inhoud moeten hier weergegeven. Een andere manier toodetermine toouse hello Azure Storage Explorer of een tabel een interne tabel is is. Gebruik deze toonavigate toohello standaard containernaam van Hallo cluster en vervolgens filteren op Hallo tabelnaam. Als Hallo tabel en de inhoud ervan wordt getoond, bevestigt dit dat het is een interne tabel.

Hier volgt een momentopname van Hallo Hive-query en Hallo [importgegevens] [ import-data] module:

![Hive-query voor gegevens importeren-module](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Sinds onze omlaag steekproefgegevens bevindt zich in de standaardcontainer hello, Hallo resulterende Hive-query uit Azure Machine Learning is zeer eenvoudig en is alleen een "Selecteer * uit nyctaxidb.nyctaxi\_verkleind\_gegevens '.

Hallo dataset kan nu worden gebruikt als startpunt voor het bouwen van Machine Learning-modellen Hallo.

### <a name="mlmodel"></a>Bouwen van modellen in Azure Machine Learning
Er wordt nu kunnen tooproceed toomodel gebouw en implementatie van het model in [Azure Machine Learning](https://studio.azureml.net). Hallo-gegevens is gereed voor ons toouse in Hallo voorspelling problemen hierboven adressering:

**1. Binaire classificatie**: toopredict al dan niet een tip voor een zakenreis is betaald.

**Cursist gebruikt:** Two-class logistic regression

a. Voor dit probleem op door is onze label doel (of een klasse) "punt". Onze oorspronkelijke omlaag actieve gegevensset heeft een aantal kolommen die doel lekken voor dit experiment classificatie. Met name: tip\_klasse, tip\_bedrag en totaal\_bedrag onthullen informatie over Hallo doellabel dat is niet beschikbaar voor het testen van tijd. We deze kolommen verwijderen uit met behulp van Hallo overweging [Select Columns in Dataset] [ select-columns] module.

Hallo momentopname hieronder ziet u onze toopredict experiment al dan niet een tip voor een bepaalde reis is betaald.

![Experiment momentopname](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. Ons doel label distributies zijn voor dit experiment ongeveer 1:1.

Hallo momentopname hieronder toont de distributie Hallo van tip klasse labels voor Hallo binair klassificatieprobleem.

![Distributie van tip klasse labels](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

Als gevolg hiervan krijgen we een AUC van 0.987 zoals weergegeven in onderstaande afbeelding ziet Hallo.

![AUC waarde](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Multiklassen classificatie**: toopredict Hallo bereik van tip bedragen betaald Hallo reis Hallo eerder gebruikte klassen gedefinieerd.

**Cursist gebruikt:** Multiklassen logistic regression

a. Voor dit probleem op door het label voor onze doel (of een klasse) is ' tip\_klasse ' die kan duren voordat een van vijf waarden (0,1,2,3,4). Net als bij Hallo binaire classificatie hebben we enkele kolommen die doel lekken voor dit experiment. Met name: punt, tip\_bedrag totale\_bedrag onthullen informatie over Hallo doellabel dat is niet beschikbaar voor het testen van tijd. Verwijderen we deze kolommen met Hallo [Select Columns in Dataset] [ select-columns] module.

Hallo momentopname hieronder bevat onze experiment toopredict in welke opslaglocatie een tip waarschijnlijk toofall is (klasse 0: tip = $0, 1 klasse: tip > $0 en tip < = $5, klasse 2: tip > $5 en tip < = $10, klasse 3: tip > $10 en tip < = $20 Klasse 4: tip > $20)

![Experiment momentopname](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Nu zien hoe de distributie van onze werkelijke test klasse eruit ziet. Zien we dat klasse 0 en 1 van de klasse gangbare zijn, hello andere klassen zijn zeldzame.

![Klasse distributie testen](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. We gebruiken een matrix verwarring toolook op onze accuratesse voorspelling voor dit experiment. Dit wordt hieronder weergegeven.

![Verwarring matrix](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Houd er rekening mee dat hoewel onze accuratesse klasse op Hallo gangbare klassen behoorlijk geschikt, Hallo model wordt niet goed werk 'learning' op Hallo zeldzame klassen.

**3. Regressie taak**: toopredict Hallo hoeveelheid tip voor een reis betaald.

**Cursist gebruikt:** Boosted decision tree

a. Voor dit probleem op door het label voor onze doel (of een klasse) is ' tip\_bedrag '. Ons doel lekken in dit geval zijn: punt, tip\_klasse, totale\_bedrag; deze variabelen die zijn op basis van informatie over Hallo tip hoeveelheid die doorgaans niet beschikbaar voor het testen van tijd duidelijk. Verwijderen we deze kolommen met Hallo [Select Columns in Dataset] [ select-columns] module.

Hallo momentopname belows bevat onze experiment toopredict Hallo hoeveelheid Hallo tip gegeven.

![Experiment momentopname](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. Regressie problemen, we Hallo accuratesse van onze voorspelling meten door te kijken Hallo kwadraat fout in Hallo voorspellingen Hallo determinatiecoëfficiënt en Hallo zoals. We weergegeven deze hieronder.

![Voorspelling statistieken](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Zien we dat de determinatiecoëfficiënt over Hallo 0.709, is door onze coëfficiënten model: de overdracht van ongeveer 71% van de variantie hello wordt uitgelegd.

> [!IMPORTANT]
> meer informatie over Azure Machine Learning toolearn en hoe tooaccess en deze gebruiken, raadpleegt u te[wat is Machine Learning?](machine-learning-what-is-machine-learning.md). Een zeer nuttig resource voor het afspelen van met een aantal Machine Learning-experimenten in Azure Machine Learning is Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/). Hallo-galerie bevat informatie over een kleurenbereik van experimenten en biedt een uitgebreide inleiding in Hallo scala aan mogelijkheden van Azure Machine Learning.
> 
> 

## <a name="license-information"></a>Licentie-informatie
In dit voorbeeld scenario en de bijbehorende scripts worden gedeeld door Microsoft onder Hallo MIT-licentie. Controleer de Hallo LICENSE.txt bestand in de directory Hallo van Hallo voorbeeldcode op GitHub voor meer informatie.

## <a name="references"></a>Verwijzingen
• [Andrés Monroy NYC Taxi reizen downloadpagina](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC Taxi reis gegevens door Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi en Limousine Commissie onderzoek en statistieken](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
