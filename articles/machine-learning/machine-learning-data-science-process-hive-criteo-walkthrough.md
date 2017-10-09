---
title: Hallo Team gegevens wetenschappelijke processen in actie - met een Azure HDInsight Hadoop-Cluster van een gegevensset 1 TB | Microsoft Docs
description: Hallo Team gegevens wetenschappelijke processen voor een end-to-end-scenario die gebruikmaakt van een HDInsight Hadoop toobuild cluster en implementeren van een model met behulp van een grote (1 TB) openbaar gegevensset
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Hallo Team gegevens wetenschappelijke processen in actie - met een Azure HDInsight Hadoop-Cluster van een gegevensset 1 TB

In dit overzicht wordt gedemonstreerd met behulp van Hallo Team gegevens wetenschappelijke processen in een end-to-end-scenario met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/) toostore, verkennen, functie engineering en voorbeeldgegevens uit een Hallo openbaar omlaag beschikbare [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) gegevenssets. Azure Machine Learning toobuild een model binaire classificatie gebruiken we gegevens. Ook laten we zien hoe toopublish een van deze modellen als een webservice.

Het is ook mogelijk toouse een IPython notebook tooaccomplish Hallo taken die zijn gepresenteerd in dit scenario. Gebruikers die zou zoals tootry contact met deze aanpak opnemen moet Hallo [Criteo scenario met behulp van een verbinding Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) onderwerp.

## <a name="dataset"></a>Beschrijving van de gegevensset Criteo
Hallo Criteo gegevens is een klik voorspelling gegevensset die ongeveer 370GB gecomprimeerde gzip TSV-bestanden (~1.3TB ongecomprimeerde), die bestaat uit meer dan 4.3 miljard records. Het is afkomstig uit 24 dagen van klik dan op gegevens die de [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Voor het gemak van gegevenswetenschappers Hallo hebben we gegevens beschikbaar toous tooexperiment met uitgepakt.

Elke record in deze gegevensset bevat 40 kolommen:

* de eerste kolom Hallo is een labelkolom waarin wordt aangegeven of een gebruiker klikt op een **toevoegen** (waarde 1) of niet op een (waarde 0)
* naast 13 kolommen zijn numerieke, en
* laatste 26 zijn categorische kolommen

Hallo-kolommen zijn geanonimiseerde en gebruiken van een reeks geïnventariseerde namen: "Col1' (voor kolom Hallo-label) te ' Col40 ' (voor Hallo laatste categorische kolom).            

Hier volgt een fragment van Hallo eerst 20 kolommen uit twee rapporten (rijen) van deze gegevensset:

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Er zijn ontbreken waarden in beide Hallo numerieke en categorische kolommen in deze dataset. Een eenvoudige methode voor het verwerken van de ontbrekende waarden Hallo worden beschreven. Aanvullende details van Hallo gegevens worden verkend wanneer we ze opslaan in de Hive-tabellen.

**Definitie:** *Clickthrough-snelheid (CTR):* dit percentage Hallo muisklikken in Hallo gegevens is. In deze dataset Criteo is Hallo CTR ongeveer 3.3% of 0.033.

## <a name="mltasks"></a>Voorbeelden van voorspelling taken
Twee voorbeeld voorspelling problemen worden in dit scenario behandeld:

1. **Binaire classificatie**: voorspelt of een gebruiker een add geklikt:
   
   * Klasse 0: Er is geen Klik
   * Klasse 1: klik op
2. **Regressie**: voorspelt Hallo waarschijnlijkheid van een ad-klik van functies voor gebruikers.

## <a name="setup"></a>Instellen van een HDInsight Hadoop-cluster voor gegevenswetenschap
**Opmerking:** dit is doorgaans een **Admin** taak.

Instellen van uw Azure-Gegevenswetenschap-omgeving voor het bouwen van predictive analytics-oplossingen met HDInsight-clusters in drie stappen:

1. [Een opslagaccount maken](../storage/common/storage-create-storage-account.md): dit opslagaccount wordt gebruikt toostore gegevens in Azure Blob Storage. Hallo-gegevens in HDInsight-clusters gebruikt, wordt hier opgeslagen.
2. [Azure HDInsight Hadoop-Clusters aanpassen voor Gegevenswetenschap](machine-learning-data-science-customize-hadoop-cluster.md): deze stap maakt u een Azure HDInsight Hadoop-cluster met 64-bits Anaconda Python 2.7 is geïnstalleerd op alle knooppunten. Er zijn twee belangrijke stappen die u (in dit onderwerp beschreven) toocomplete bij het aanpassen van Hallo HDInsight-cluster.
   
   * Hallo storage-account is gemaakt in stap 1 met uw HDInsight-cluster wanneer deze wordt gemaakt, moet u koppelen. Dit opslagaccount wordt gebruikt voor toegang tot gegevens die kunnen worden verwerkt binnen Hallo-cluster.
   * Nadat deze is gemaakt, moet u externe toegang toohello hoofdknooppunt van Hallo cluster inschakelen. Hallo RAS-referenties die u hier opgeeft (anders dan die zijn opgegeven voor de cluster Hallo bij het maken ervan) onthouden: u moet ze toocomplete Hallo volgende procedures.
3. [Maken van een Azure ML-werkruimte](machine-learning-create-workspace.md): deze Azure Machine Learning-werkruimte wordt gebruikt voor het bouwen van machine learning-modellen na een initiële gegevensverkenning en omlaag steekproeven op Hallo HDInsight-cluster.

## <a name="getdata"></a>Ophalen van gegevens en gebruiken van een openbare bron
Hallo [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset kan worden geopend door te klikken op de koppeling hello, Hallo gebruiksvoorwaarden accepteren en een naam geven. Hier ziet u een momentopname van wat ziet deze als eruit:

![Criteo voorwaarden accepteren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Klik op **doorgaan tooDownload** tooread meer over Hallo gegevensset en de beschikbaarheid.

Hallo gegevens bevinden zich in een openbare [Azure blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md) locatie: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. Hallo 'wasb' verwijst tooAzure Blob Storage-locatie. 

1. Hallo-gegevens in deze openbare blob-opslag bestaat uit drie submappen van uitgepakte gegevens.
   
   1. Hallo submap *Onbewerkte/telling/* bevat Hallo eerste 21 dagen aan gegevens - vanaf dag\_00 tooday\_20
   2. Hallo submap *onbewerkte/train/* bestaat uit één dag van gegevens, dag\_21
   3. Hallo submap *onbewerkte en testen/* bestaat uit twee dagen aan gegevens, dag\_22 en dag\_23
2. Voor die willen toostart met Hallo gzip onbewerkte gegevens, zijn ook beschikbaar in de hoofdmap Hallo *onbewerkte /* als day_NN.gz, waarbij NN van 00 too23 gaat.

Een alternatieve methode-tooaccess verkennen en model van deze gegevens waarvoor lokale downloads verderop in dit scenario wordt uitgelegd wanneer we Hive-tabellen maakt geen nodig.

## <a name="login"></a>Meld u bij toohello cluster headnode
toolog in toohello headnode van Hallo-cluster, gebruik Hallo [Azure-portal](https://ms.portal.azure.com) toolocate Hallo-cluster. Klik op Hallo HDInsight plaats pictogram op Hallo links en dubbelklik vervolgens op Hallo-naam van het cluster. Navigeer toohello **configuratie** tabblad, dubbelklik op Hallo CONNECT op Hallo onder aan Hallo pagina en geef uw referenties voor externe toegang als u wordt gevraagd. Hiermee gaat u toohello headnode van Hallo-cluster.

Hier volgt een typisch eerst aanmelden toohello cluster headnode ziet er als:

![Meld u bij toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

Aan de linkerkant hello ziet u Hallo ' Hadoop opdrachtregel ', die onze werkpaard voor Hallo gegevensverkenning is. Ook ziet u twee nuttig URL's - 'Hadoop Yarn Status' en 'Hadoop de naam van knooppunt'. Hallo yarn status URL ziet u de voortgang van de taak en Hallo naam knooppunt URL geeft informatie over het Hallo-clusterconfiguratie.

Nu we worden ingesteld en klaar toobegin eerste deel van Hallo rondleiding: gegevensverkenning gebruik van Hive en voorbereiden van gegevens voor Azure Machine Learning.

## <a name="hive-db-tables"></a>Hive-database en tabellen maken
toocreate Hive-tabellen voor onze gegevensset Criteo open Hallo ***Hadoop-opdrachtregel*** op bureaublad van hoofdknooppunt Hallo Hallo en Voer Hallo Hive directory door te voeren opdracht Hallo

    cd %hive_home%\bin

> [!NOTE]
> Alle Hive-opdrachten uitvoeren in dit overzicht van Hallo Hive bin / directory prompt. Dit zorgt voor problemen die pad automatisch. We gebruiken Hallo termen 'Hive directory prompt', ' Hive bin / directory prompt ', en ' Hadoop opdrachtregel ' door elkaar.
> 
> [!NOTE]
> tooexecute Hive-query op een altijd gebruiken Hallo volgende opdrachten:
> 
> 

        cd %hive_home%\bin
        hive

Na het Hallo Hive REPL wordt weergegeven met een ' hive > "aanmelden, gewoon knippen en plakken Hallo query tooexecute deze.

Hallo volgende code maakt een database 'criteo' en genereert vervolgens 4 tabellen:

* een *tabel voor het genereren van aantallen* gebouwd op dagen dag\_00 tooday\_20,
* een *tabel voor gebruik als de trein gegevensset Hallo* gebouwd op dag\_21, en
* twee *tabellen voor gebruik als Hallo testen gegevenssets* gebouwd op dag\_22 en dag\_23 respectievelijk.

We onze testgegevensset opgesplitst in twee verschillende tabellen omdat een van de Hallo dagen een feestdag is, en kunt u toodetermine als Hallo model verschillen tussen een feestdag en niet met Hallo clickthrough snelheid kan detecteren.

Hallo script [voorbeeld &#95; hive &#95; maken &#95; criteo &#95; database &#95; en &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) voor het gemak Hier wordt weergegeven:

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

Er rekening mee dat alle tabellen in deze externe als we gewoon punt tooAzure Blob Storage (wasb)-locaties.

**Er zijn twee manieren tooexecute ANY Hive-query die we nu vermeld.**

1. **Met behulp van Hive REPL opdrachtregelprogramma Hallo**: Hallo eerst tooissue is een opdracht 'hive' en kopieer en plak een query op Hallo Hive REPL vanaf de opdrachtregel. toodo deze, komen:
   
        cd %hive_home%\bin
        hive
   
     Nu op Hallo REPL opdrachtregelprogramma, knippen en plakken wordt deze Hallo query uitvoert.
2. **Opslaan query tooa bestands- en uitvoeren van de opdracht Hallo**: Hallo tweede is toosave Hallo query's tooa .hql-bestand ([voorbeeld &#95; hive &#95; maken &#95; criteo &#95; database &#95; en &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) en vervolgens Hallo Geef de volgende opdracht tooexecute Hallo query:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Het maken van database en tabel bevestigen
Vervolgens we Hallo database maken van Hallo bevestigen met de volgende opdracht uit Hallo Hive bin Hallo / opdrachtprompt van de map:

        hive -e "show databases;"

Hierdoor hebt:

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Hiermee bevestigt u Hallo maken van een nieuwe database hello, 'criteo'.

toosee welke tabellen wordt gemaakt, we gewoon Hallo opdracht geven hier vanuit Hallo Hive bin / opdrachtprompt van de map:

        hive -e "show tables in criteo;"

Vervolgens ziet u Hallo volgende uitvoer:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a>Gegevensverkenning in component
We klaar toodo sommige basic gegevensverkenning in Hive. We beginnen door het aantal voorbeelden in de trein Hallo Hallo te tellen en gegevenstabellen testen.

### <a name="number-of-train-examples"></a>Aantal train-voorbeelden
inhoud van Hallo [voorbeeld &#95; hive &#95; & #95 tellen; train &#95; tabel &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) worden hier weergegeven:

        SELECT COUNT(*) FROM criteo.criteo_train;

Dit levert:

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

U kunt ook een ook afgeven Hallo volgende opdracht uit Hallo Hive bin / opdrachtprompt van de map:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Aantal voorbeelden van de test in Hallo twee test gegevenssets
We nu tellen Hallo aantal voorbeelden in Hallo twee test gegevenssets. inhoud van Hallo [voorbeeld &#95; hive &#95; & #95 tellen; criteo &#95; test &#95; dag &#95; 22 &#95; tabel &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) hier zijn:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

Dit levert:

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

Gebruikelijke we ook Hallo script kunnen aanroepen vanuit Hallo Hive bin / Active directory vragen door Hallo-opdracht:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Ten slotte we naar de Hallo aantal test voorbeelden in Hallo testgegevensset op basis van dag\_23.

Hallo opdracht toodo dit is vergelijkbaar toohello een slechts weergegeven (Raadpleeg te[voorbeeld &#95; hive &#95; & #95 tellen; criteo &#95; test &#95; dag &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Hierdoor hebt:

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Label verdeling in Hallo train gegevensset
Hallo label verdeling in Hallo train gegevensset is van belang. toosee, laten we zien inhoud van [voorbeeld &#95; hive &#95; criteo &#95; & #95 label; verdeling &#95; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Dit levert Hallo label distributie:

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Houd er rekening mee dat Hallo percentage positieve labels ongeveer 3.3% (consistent met de oorspronkelijke gegevensset Hallo is).

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Histogram distributies van sommige numerieke variabelen in Hallo trainen gegevensset
Kunnen we de Hive-systeemeigen gebruiken ' histogram\_numerieke ' toofind uit welke Hallo-distributie van de numerieke variabelen Hallo eruit werken. Hier vindt u de inhoud Hallo van [voorbeeld &#95; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

Dit levert Hallo volgende:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

Hallo LATERAL BEELD - vouwen combinatie in Hive fungeert tooproduce de uitvoer van een SQL-achtige in plaats van gebruikelijke Hallo-lijst. Opmerking dat in Hallo deze tabel, de eerste kolom Hallo komt overeen toohello bin center en Hallo tweede toohello bin frequentie.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Geschatte percentielen van sommige numerieke variabelen in Hallo trainen gegevensset
Ook is het van belang met numerieke variabelen Hallo berekening van de geschatte percentielen. Hive de systeemeigen ' percentiel\_ongeveer ' Dit wordt uitgevoerd voor ons. inhoud van Hallo [voorbeeld &#95; hive &#95; criteo &#95; geschatte &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) zijn:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

Dit levert:

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

We dat Hallo distributie van percentielen nauw verwante toohello histogram distributie van een numerieke variabele meestal wordt te schakelen.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Aantal unieke waarden vinden voor sommige categorische kolommen in Hallo train gegevensset
Nog steeds Hallo gegevensverkenning, we nu vinden voor sommige categorische kolommen, Hallo aantal unieke waarden die ze nemen. toodo, laten we zien inhoud van [voorbeeld &#95; hive &#95; criteo &#95; unieke &#95; waarden &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

Dit levert:

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

We Houd er rekening mee dat Col15 19M unieke waarden bevat. Met behulp van naïve technieken zoals 'één hot codering' tooencode dergelijke hoge dimensionale categorische variabelen onbruikbare is. In het bijzonder we uitleggen en demonstreren van een krachtige, robuuste techniek aangeroepen [Learning met telt](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) voor efficiënt aanpakken van dit probleem.

We eindigen deze subsectie door te kijken Hallo aantal unieke waarden voor sommige andere categorische kolommen ook. inhoud van Hallo [voorbeeld &#95; hive &#95; criteo &#95; unieke &#95; waarden &#95; meerdere &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) zijn:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

Dit levert:

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Opnieuw zien we dat, met uitzondering van Col20, alle Hallo andere kolommen hebben veel unieke waarden.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Aantal paren van categorische variabelen in Hallo mede exemplaar trainen gegevensset

Hallo mede exemplaar tellingen van paren van categorische variabelen is ook van belang. Dit kan worden bepaald met behulp van Hallo-code in [voorbeeld &#95; hive &#95; criteo &#95; gekoppeld &#95; categorische &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

We omgekeerde volgorde Hallo aantallen door hun exemplaar en bekijkt hello boven 15 in dit geval. Hierdoor hebt ons:

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Omlaag Hallo voorbeeldgegevenssets voor Azure Machine Learning
Met explored Hallo gegevenssets en gedemonstreerd hoe we dit soort exploratie geen variabelen (waaronder combinaties), wordt nu naar beneden voorbeeld Hallo gegevenssets kan zodat we modellen in Azure Machine Learning kunnen bouwen. Dat we richten op Hallo-probleem intrekken: gezien een set voorbeeld kenmerken (functie waarden van Col2 - Col40), we voorspellen als Col1 0 (geen klik) of 1 (klik is).

toodown steekproef onze train en gegevenssets too1% van de oorspronkelijke grootte Hallo testen, gebruiken we de Hive-functie voor systeemeigen RAND(). Hallo volgende script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) doet u dit voor Hallo train gegevensset:

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

Dit levert:

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Hallo script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; test &#95; dag &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) gebeurt dit voor testgegevens, dag\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

Dit levert:

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Ten slotte Hallo script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; test &#95; dag &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) gebeurt dit voor testgegevens, dag\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

Dit levert:

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

Dit zijn de gereed toouse onze omlaag door actieve trainen en te testen gegevenssets voor het bouwen van modellen in Azure Machine Learning.

Er is een definitieve belangrijk onderdeel voordat we op tooAzure Machine Learning, namelijk problemen Hallo aantal tabel verplaatsen. In Hallo volgende subsectie bespreken we dit sommige beschreven.

## <a name="count"></a>Een korte bespreking van de Hallo aantal tabel
Zoals u hebt gezien, hebben verschillende categorische variabelen een zeer hoge dimensionaliteit. In ons scenario we een krachtige methode aangeroepen in dit [Learning met telt](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode deze variabelen in een efficiënte en krachtige manier. Meer informatie over deze techniek wordt Hallo koppeling.

[!NOTE]
>In dit overzicht richten we op met het aantal tabellen tooproduce compact representaties van hoge-dimensionale categorische functies. Dit is geen Hallo alleen manier tooencode categorische functies; voor meer informatie over andere technieken geïnteresseerd gebruikers kunnen uitchecken [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) en [hash-functie](http://en.wikipedia.org/wiki/Feature_hashing).
>

toobuild aantal tabellen op Hallo aantal gegevens, gebruiken we Hallo gegevens in Hallo map onbewerkte/aantal. In Hallo modelleren sectie we gebruikers zien tabellen hoe toobuild die deze tellen voor categorische functies maakt, of u kunt ook toouse een tabel vooraf samengestelde telling voor hun explorations. In wat volgt, wanneer we verwijst te 'vooraf gemaakte aantal tabellen', bedoelen we Hallo aantal tabellen die wij verstrekken. Gedetailleerde instructies over hoe tooaccess deze tabellen u in de volgende sectie Hallo vindt.

## <a name="aml"></a>Een model met Azure Machine Learning bouwen
Het model bouwen proces in Azure Machine Learning verloopt als volgt:

1. [Hallo-gegevens ophalen uit de Hive-tabellen in Azure Machine Learning](#step1)
2. [Hallo-experiment maken: schone Hallo gegevens en featurize met aantal tabellen](#step2)
3. [Build en train Hallo score-model](#step3)
4. [Hallo model evalueren](#step4)
5. [Hallo model publiceren als een webservice](#step5)

We zijn nu gereed toobuild modellen in Azure Machine Learning studio. Onze omlaag steekproefgegevens wordt opgeslagen als Hive-tabellen in het Hallo-cluster. We gebruiken hello Azure Machine Learning **importgegevens** module tooread deze gegevens. Hallo referenties tooaccess Hallo storage-account van dit cluster zijn opgegeven in welke volgt.

### <a name="step1"></a>Stap 1: Gegevens ophalen uit de Hive-tabellen in Azure Machine Learning met Hallo gegevens importeren-module en selecteert u deze voor een machine learning-experiment
Begin met het selecteren een **+ nieuw** -> **EXPERIMENT** -> **leeg Experiment**. Vervolgens Hallo **Search** vak bovenaan Hallo links, zoek naar 'Gegevens importeren'. Slepen en neerzetten Hallo **importgegevens** -module op de toohello experiment canvas (Hallo middelste gedeelte welkomstscherm) toouse Hallo-module voor gegevenstoegang.

Dit is wat Hallo **importgegevens** lijkt tijdens het ophalen van gegevens uit Hallo Hive-tabel:

![Gegevens importeren gegevens worden opgehaald](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Voor Hallo **importgegevens** module Hallo waarden van Hallo-parameters die zijn opgegeven in Hallo afbeelding zijn alleen voorbeelden van Hallo sortering van waarden u moet tooprovide. Hier volgt een aantal algemene richtlijnen op hoe toofill Hallo uitvoerparameter ingesteld voor Hallo **importgegevens** module.

1. 'Hive-query' kiezen voor **gegevensbron**
2. In Hallo **Hive databasequery** vak een eenvoudige SELECT * FROM < uw\_database\_name.your\_tabel\_name >-voldoende is.
3. **Hcatalog server-URI**: als uw cluster "abc", wordt dit eenvoudig is: https://abc.azurehdinsight.net
4. **Hadoop-gebruikersaccountnaam**: Hallo-gebruikersnaam die is gekozen op het Hallo-tijd van het bedrijf stellen Hallo-cluster. (Geen Hallo RAS gebruikersnaam!)
5. **Het wachtwoord voor gebruikersaccount Hadoop**: Hallo wachtwoord voor Hallo-gebruikersnaam die is gekozen op het Hallo-tijd van het bedrijf stellen Hallo-cluster. (Geen Hallo RAS wachtwoord!)
6. **Locatie van uitvoergegevens**: 'Azure' kiezen
7. **Naam van het Azure-opslagaccount**: opslagaccount die is gekoppeld aan cluster Hallo Hallo
8. **Azure-toegangssleutel**: Hallo-sleutel van Hallo storage-account is gekoppeld aan het Hallo-cluster.
9. **Azure containernaam**: als de clusternaam Hallo "abc", wordt dit is meestal gewoon "abc",.

Eenmaal Hallo **importgegevens** ophalen van gegevens (ziet u Hallo groen maatstreepjes op Hallo Module), zijn voltooid deze gegevens opslaan als een Dataset (met een naam van uw keuze). Wat ziet deze eruit als:

![Gegevens importeren opslaan gegevens](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Klik met de rechtermuisknop Hallo uitvoerpoort Hallo **importgegevens** module. Dit blijkt een **opslaan als gegevensset** optie en een **Visualize** optie. Hallo **Visualize** optie, als u klikt, wordt weergegeven, 100 rijen van Hallo-gegevens, inclusief een rechterpaneel die nuttig is voor sommige samenvattende statistieken. toosave gegevens, schakelt u gewoon **opslaan als gegevensset** en volg de instructies.

tooselect hello opgeslagen gegevensset voor gebruik in een machine learning-experiment vinden Hallo gegevenssets Hallo met **Search** vak weergegeven in de volgende afbeelding Hallo. Klik gewoon type out Hallo-naam die u hebt opgegeven Hallo gegevensset gedeeltelijk tooaccess deze en sleep de gegevensset op Hallo Hallo hoofdpaneel. Neer te zetten naar Hallo hoofdpaneel de wordt geselecteerd voor gebruik in machine learning-model.

![Drage gegevensset naar het hoofdpaneel Hallo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Doe dit voor zowel Hallo trein en Hallo test gegevenssets. Denk eraan dat toouse Hallo databasenaam en tabelnamen die u hebt opgegeven voor dit doel. Hallo-waarden die worden gebruikt in de afbeelding Hallo dienen uitsluitend ter illustratie purposes.* *
> 
> 

### <a name="step2"></a>Stap 2: Een eenvoudig experiment maken in Azure Machine Learning toopredict klikken / geen klikken
Ons Azure ML-experiment ziet er als volgt:

![Machine Learning-experiment](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

We nu eens kijken hoe Hallo belangrijke onderdelen van dit experiment. Als een herinnering moeten we toodrag onze opgeslagen trainen en gegevenssets op tooour experimentcanvas eerst te testen.

#### <a name="clean-missing-data"></a>De ontbrekende gegevens opschonen
Hallo **Clean Missing Data** module biedt wat de naam al aangeeft: het ontbrekende gegevens op een manier die de gebruiker opgegeven kunnen worden schoongemaakt. In deze module zoekt, ziet u dit:

![Ontbrekende gegevens opschonen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

We gekozen hier alle ontbrekende waarden met een 0 tooreplace. Er zijn andere opties, die kunnen worden gezien door te kijken Hallo opgegeven waarin dropdowns in Hallo-module.

#### <a name="feature-engineering-on-hello-data"></a>Functie-engineering op Hallo-gegevens
Er zijn miljoenen unieke waarden voor sommige categorische functies van grote gegevenssets. Naïve-methoden zoals een hot codering voor het voorstellen van dergelijke hoge dimensionale categorische functies is volledig unfeasible. In dit overzicht ziet u hoe toouse aantal onderdelen met de ingebouwde Azure Machine Learning-modules toogenerate weergaven van deze hoge-dimensionale categorische variabelen comprimeren. Hallo-eindresultaat is een kleinere model, sneller training en maatstaven voor prestaties die erg vergelijkbaar toousing andere technieken.

##### <a name="building-counting-transforms"></a>Gebouw transformaties tellen
toobuild aantal functies, gebruiken we Hallo **bouwen tellen transformeren** module die beschikbaar is in Azure Machine Learning. Hallo module ziet er als volgt:

![Module tellen transformeren maken](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![module bouwen tellen transformeren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> In Hallo **tellen kolommen** vak we invoeren die we willen tooperform telt op kolommen. Dit zijn meestal (zoals vermeld) hoge dimensionale categorische kolommen. Aan begin hello wordt gezegd dat Hallo Criteo gegevensset heeft 26 categorische kolommen: van Col15 tooCol40. Hier we tellen op alle mappen en hun indexen geven (van 15 too40 gescheiden door komma's, zoals wordt weergegeven).
> 

toouse hello module Hallo MapReduce-modus (geschikt voor grote gegevenssets), wij toegang moet krijgen tot tooan HDInsight Hadoop-cluster (hello gebruikt voor de functie verkenning opnieuw kan worden gebruikt voor dit doel ook) en de referenties. Hallo vorige afbeeldingen laten zien welke Hallo ingevulde waarden eruit (vervangen Hallo waarden opgegeven voor de afbeelding met die relevant zijn voor uw eigen gebruiksvoorbeeld).

![Moduleparameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

In de bovenstaande Hallo afbeelding, laten we zien hoe tooenter Hallo blob invoer locatie. Deze locatie heeft gereserveerd voor het aantal tabellen maken op Hallo-gegevens.

Nadat deze module is voltooid, we kunt opslaan Hallo transformatie voor later met de rechtermuisknop op Hallo module Hallo selecteren **opslaan als transformatie** optie:

![Optie 'Opslaan als transformatie'](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

In onze experiment architectuur hierboven weergegeven, overeen Hallo gegevensset 'ytransform2' nauwkeurig tooa aantal transformatie opgeslagen. Hallo rest van dit experiment, gaan we ervan uit dat Hallo lezer gebruikt een **bouwen tellen transformeren** -module op sommige gegevens toogenerate tellingen en kan vervolgens die aantallen toogenerate aantal functies op Hallo train gebruiken en gegevenssets te testen.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>Kiezen wat functies tooinclude als onderdeel van de trein Hallo tellen en gegevenssets testen
Zodra er een aantal transformeren gereed hebt, Hallo-gebruiker kan kiezen welke tooinclude functies in hun trein, en testen met behulp van Hallo gegevenssets **wijzigen aantal tabel Parameters** module. We deze module alleen weergeven hier voor de volledigheid, maar uit oogpunt van eenvoud daadwerkelijk gebruik deze functie niet bij ons experiment.

![De parameters voor aantal wijzigen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

In dit geval zoals u kunt zien, we hebben ervoor gekozen toouse alleen Hallo logboek-kans en tooignore Hallo kolom uitgesteld. We kunnen ook parameters instellen, zoals Hallo garbagecollection bin drempelwaarde, hoeveel pseudo eerdere voorbeelden tooadd voor vloeiend maken, en of toouse eventuele Laplacian ruis of niet. Al deze functies zijn geavanceerde en is toobe aangegeven dat de standaardwaarden Hallo een goed uitgangspunt voor gebruikers die nieuwe toothis-type van het genereren van de functie zijn zijn.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Gegevenstransformatie vóór het genereren van Hallo aantal functies
Nu we zich richten op een belangrijk punt over onze train transformeren en testen van de gegevens van de voorafgaande tooactually genereren aantal functies. Houd er rekening mee dat er twee zijn **R-Script uitvoeren** modules die worden gebruikt voordat we Hallo aantal transformatie tooour gegevens toepassen.

![Modules R-Script uitvoeren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Dit is de eerste R-script Hallo:

![Eerste R-script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

In deze R-script wijzigen we onze toonames kolommen 'Col1' te 'Col40'. Dit is omdat Hallo aantal transformatie namen van deze indeling verwacht.

In de tweede R-script hello, we Hallo-verdeling tussen klassen positieve en negatieve saldo (respectievelijk klassen 1 en 0) door downsampling Hallo negatieve klasse. Hallo R script hoe hier toont toodo dit:

![Tweede R-script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

In dit eenvoudige R-script gebruiken we ' pos\_neg\_verhouding ' tooset Hallo hoeveelheid balans tussen Hallo positieve en negatieve Hallo-klassen. Dit is belangrijk toodo aangezien prestatievoordelen voor classificatie problemen meestal verbeteren van de klasse onbalans heeft waar Hallo klasse distributie is vervormd (intrekken dat in ons geval we 3.3% positief klasse en 96,7% negatief klasse hebben).

##### <a name="applying-hello-count-transformation-on-our-data"></a>Hallo aantal transformatie toepassen op onze gegevens
Ten slotte gebruiken we Hallo **transformatie toepassen** module tooapply aantal transformaties op onze train Hallo en gegevenssets te testen. Deze module wordt van Hallo opgeslagen aantal transformatie als één invoer- en Hallo trainen of gegevenssets testen als andere invoer Hallo en retourneert gegevens met een aantal functies. Hier wordt weergegeven:

![Transformatie module toepassen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Een fragment Hallo aantal onderdelen van het uiterlijk van
Het is instructieve toosee welke functies van de count Hallo in ons geval eruit. Hier wordt een fragment van deze weergeven:

![Aantal functies](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

In dit fragment zien we dat voor kolommen die we geteld op Hallo we Hallo aantallen ophalen en meld u kans toevoeging tooany relevante backoffs.

Er zijn nu gereed toobuild een Azure Machine Learning-model met behulp van deze getransformeerde gegevenssets. In de volgende sectie hello, laten we zien hoe u dit kunt doen.

### <a name="step3"></a>Stap 3: Maken, te trainen en Hallo model beoordelen

#### <a name="choice-of-learner"></a>Keuze van cursist
We moeten eerst een cursist toochoose. We zijn gaan toouse een beslissingsstructuur twee class boosted onze cursist. Hier volgen de standaardopties Hallo voor deze cursist:

![Two-Class Boosted Decision Tree parameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

Voor onze experiment zijn we continu toochoose Hallo standaardwaarden. We Houd er rekening mee dat Hallo standaardinstellingen zijn meestal zinvolle en voor een goede manier tooget snelle basislijnen op de prestaties. U kunt op de prestaties verbeteren door verstrekkende parameters als u ervoor kiest tooonce die u hebt een basislijn.

#### <a name="train-hello-model"></a>Hallo-model trainen
Voor training, roepen we gewoon een **Train Model** module. Hallo twee invoer tooit zijn Hallo Two-Class Boosted Decision Tree cursist en onze train-gegevensset. Dit wordt hier weergegeven:

![Module Train-Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Hallo-score-model
Zodra er een getraind model hebt, we klaar zijn tooscore op Hallo testen gegevensset en tooevaluate de prestaties. We doen dit met behulp van Hallo **Score Model** module weergegeven in de volgende afbeelding, samen met Hallo een **Evaluate Model** module:

![De module Score Model (Scoremodel)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>Stap 4: Hallo model evalueren
Willen we graag ten slotte tooanalyze model prestaties. Meestal is een goede indicatie voor twee klasse (binair) classificatie problemen, Hallo AUC. toovisualize, we Hallo aansluiten **Score Model** module tooan **Evaluate Model** -module voor dit. Te klikken op **Visualize** op Hallo **Evaluate Model** module resulteert in een afbeelding zoals Hallo volgt:

![Module BDT model evalueren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

Binair (of twee klasse) classificatie problemen met een goede indicatie van nauwkeurigheid is Hallo gebied onder Curve (AUC). In het volgende, laten we zien onze resultaten met dit model op onze testgegevensset. tooget deze, klik met de rechtermuisknop Hallo uitvoerpoort Hallo **Evaluate Model** module en vervolgens **Visualize**.

![Module Evaluate Model visualiseren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>Stap 5: Hallo model publiceren als een webservice
Hallo mogelijkheid toopublish een Azure Machine Learning-model als webservices met een minimum van fuss is een waardevolle functie algemeen beschikbaar te maken. Zodra u dat hebt gedaan, kan iedereen aanroepen toohello-webservice met invoergegevens dat ze nodig hebben voorspellingen voor en Hallo-webservice Hallo model tooreturn die voorspellingen gebruikt maken.

toodo, we eerst het getrainde model opslaan als een object van het getrainde Model. Dit wordt gedaan met de rechtermuisknop op Hallo **Train Model** module en met behulp van Hallo **opslaan als getrainde Model** optie.

Vervolgens moet toocreate invoer en uitvoer poorten voor onze webservice:

* een invoerpoort worden gegevens in dezelfde formulier als Hallo-gegevens die we nodig hebben voorspellingen voor Hallo
* een uitvoerpoort retourneert Hallo Scored Labels en kansen Hallo die zijn gekoppeld.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Selecteer een paar rijen van de gegevens voor invoerpoort Hallo
Het handige toouse is een **toepassen SQL transformatie** module tooselect NET 10 rijen tooserve als Hallo poort invoergegevens. Selecteer alleen deze rijen met gegevens voor onze invoerpoort met behulp van SQL-query Hallo hier weergegeven:

![Invoerpoort gegevens](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Webservice
We klaar toorun een kleine experiment die gebruikt toopublish worden kan onze webservice.

#### <a name="generate-input-data-for-webservice"></a>Genereren van de invoergegevens voor de webservice
Als een stap zeroth aangezien Hallo aantal tabel groot, we nemen van een paar regels testgegevens en uitvoergegevens genereren van het aantal functies. Dit kan fungeren als Hallo invoergegevens indeling voor de webservice. Dit wordt hier weergegeven:

![De invoergegevens BDT maken](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Voor de indeling van de invoergegevens hello, gebruiken we nu Hallo uitvoer Hallo **aantal Featurizer** module. Zodra dit is voltooid met experimenteren, Hallo uitvoer opslaan van Hallo **aantal Featurizer** module als een Dataset. Deze gegevensset wordt gebruikt voor Hallo invoergegevens in Hallo-webservice.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Score berekenen voor experiment voor de publicatie-webservice
Eerst laten we zien hoe dit eruitziet. Hallo essentiële structuur is een **Score Model** module die accepteert onze getrainde model-object en een paar regels met invoergegevens die wordt gegenereerd in de vorige stappen Hallo Hallo met **aantal Featurizer** module. We gebruiken de tooproject 'Kolommen in gegevensset selecteren' hello Scored labels en Hallo Score kansen.

![Kolommen in gegevensset selecteren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

U ziet hoe Hallo **Select Columns in Dataset** module kan worden gebruikt voor 'uitgefilterd' gegevens uit een gegevensset. We weergeven hier Hallo-inhoud:

![Filteren met hello Select Columns in Dataset-module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

tooget hello blauw invoer en uitvoer poorten, klikt u op **voorbereiden webservice** op Hallo rechtsonder. Dit experiment uitgevoerd kunt ook ons toopublish Hallo-webservice: klikt u op Hallo **WEBSERVICE PUBLICEERT** pictogram Hallo onderkant rechts, weergegeven hier:

![Webservice publiceren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Zodra het Hallo-webservice wordt gepubliceerd, krijgen we omgeleide tooa pagina die er zo uitziet:

![Web service-dashboard](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

Twee koppelingen voor webservices zien we aan de linkerkant Hallo:

* Hallo **aanvragen/reacties** Service (of RR's) zijn alleen bedoeld voor één voorspellingen en is er met deze workshop gebruiken.
* Hallo **BATCHUITVOERING** Service (BES) wordt gebruikt voor voorspellingen batch en vereist dat Hallo invoergegevens gebruikt toomake voorspellingen zich in Azure Blob Storage bevinden.

Te klikken op de koppeling Hallo **aanvragen/reacties** duurt tooa pagina waarmee ons blik vooraf code in C#, python en R. Deze code kan gemakkelijk worden gebruikt voor het maken van aanroepen toohello webservice. Houd er rekening mee dat Hallo API-sleutel op deze pagina moet toobe gebruikt voor verificatie.

Het is handige toocopy deze python via tooa nieuwe cel in Hallo IPython notebook code.

We weergeven hier een segment van python-code met de juiste API-sleutel Hallo.

![Python-code](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Houd er rekening mee dat we Hallo standaard API-sleutel hebt vervangen door onze webservices-API-sleutel. Te klikken op **uitvoeren** op deze cel in een IPython levert notebook Hallo antwoord te volgen:

![IPython antwoord](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

We zien dat voor Hallo twee voorbeelden die we gevraagd over (in JSON-framework Hallo van Hallo pythonscript) testen, we antwoorden terug in de vorm Hallo 'Scored Labels, Scored kansen'. Opmerking die in dit geval we hebt gekozen Hallo standaardwaarden die vooraf voorgedefinieerde Hallo-code bevat (0 voor alle numerieke kolommen en Hallo tekenreeks '' waarde '' voor alle categorische kolommen).

Hiermee is onze end-to-end-overzicht die laat zien hoe toohandle grootschalige gegevensset met Azure Machine Learning. We gestart met een terabyte van gegevens, een Voorspellend model samengesteld en wordt geïmplementeerd als een webservice in de cloud Hallo.

