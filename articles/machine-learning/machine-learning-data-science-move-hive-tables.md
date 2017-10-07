---
title: aaaCreate Hive-tabellen en laden van gegevens uit Azure Blob Storage | Microsoft Docs
description: Hive-tabellen maken en te laden van gegevens in blob toohive tabellen
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Hive-tabellen maken en gegevens uit Azure Blob-opslag laden
Dit onderwerp bevat algemene Hive-query's die Hive-tabellen maken en gegevens uit Azure blob-opslag laden. Sommige richtlijnen is ook beschikbaar op het Hive-tabellen te partitioneren en over het gebruik van Hallo geoptimaliseerd rij kolommen (ORC) opmaak tooimprove prestaties van query's.

Dit **menu** koppelingen tootopics waarin wordt beschreven hoe tooingest gegevens in de doel-omgevingen waar Hallo gegevens kunnen worden opgeslagen en verwerkt tijdens Hallo Team gegevens wetenschap proces (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt:

* Een Azure storage-account gemaakt. Als u instructies nodig hebt, raadpleegt u [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).
* Een aangepaste Hadoop-cluster met Hallo HDInsight-service wordt ingericht.  Als u instructies nodig hebt, raadpleegt u [aanpassen Azure HDInsight Hadoop-clusters voor geavanceerde analyses](machine-learning-data-science-customize-hadoop-cluster.md).
* Ingeschakelde RAS toohello cluster aangemeld en Hallo Hadoop opdrachtregelconsole geopend. Als u instructies nodig hebt, raadpleegt u [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Uploaden van gegevens tooAzure blob-opslag
Als u een virtuele machine in Azure gemaakt op basis van Hallo instructies in [instellen van een virtuele machine van Azure voor geavanceerde analyses](machine-learning-data-science-setup-virtual-machine.md), dit scriptbestand had moet zijn gedownloade toohello *C:\\ Gebruikers\\\<gebruikersnaam\>\\documenten\\gegevens wetenschappelijke Scripts* map op Hallo virtuele machine. Deze Hive-query's vereisen alleen plug-in uw eigen gegevensschema en de Azure blob storage-configuratie in Hallo juiste velden toobe gereed voor verzending.

Er wordt ervan uitgegaan dat Hallo-gegevens voor Hive-tabellen een **niet-gecomprimeerde** tabelvorm en dat Hallo gegevens zijn geüpload toohello standaard (of extra tooan) container van Hallo storage-account die wordt gebruikt door Hallo Hadoop-cluster.

Als u wilt dat toopractice op Hallo **NYC Taxi reis gegevens**, moet u:

* **Download** Hallo 24 [NYC Taxi reis gegevens](http://www.andresmh.com/nyctaxitrips) -bestanden (12 reis bestanden en 12 tarief-bestanden)
* **Pak** alle bestanden in CSV-bestanden, en vervolgens
* **uploaden** ze toohello standaard (of juiste container) van Azure storage-account dat is gemaakt door Hallo procedure beschreven in Hallo Hallo [aanpassen Azure HDInsight Hadoop-clusters voor Advanced Analytics-proces en technologie ](machine-learning-data-science-customize-hadoop-cluster.md) onderwerp. Hallo proces tooupload Hallo .csv-bestanden toohello standaardcontainer op Hallo opslagaccount vindt u op dit [pagina](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>Hoe toosubmit Hive-query's
Hive-query's kunnen worden verzonden met behulp van:

1. [Indienen van Hive-query's via de opdrachtregel voor Hadoop in headnode van Hadoop-cluster](#headnode)
2. [Indienen van Hive-query's met Hallo Hive-Editor](#hive-editor)
3. [Indienen van Hive-query's met Azure PowerShell-opdrachten](#ps)

Hive-query's zijn SQL-achtige. Als u bekend met SQL bent, vindt u Hallo [Hive voor SQL gebruikers cheats blad](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) nuttig.

Bij het indienen van een Hive-query kunt u Hallo bestemming van Hallo-uitvoer van Hive-query's ook bepalen of deze nu op Hallo scherm of tooa lokaal bestand op het hoofdknooppunt Hallo of tooan Azure-blob.

### <a name="headnode"></a> 1. Indienen van Hive-query's via de opdrachtregel voor Hadoop in headnode van Hadoop-cluster
Als Hallo Hive-is query complex is of verzenden dat deze rechtstreeks in het hoofdknooppunt van het Hadoop-cluster Hallo Hallo doorgaans toofaster Schakel rond dan verzendt, wordt deze met een Hive-Editor of Azure PowerShell-scripts leidt.

Hoofdknooppunt van het Hadoop-cluster Hallo toohello aanmelden, opent u Hallo Hadoop vanaf de opdrachtregel op Hallo bureaublad van hoofdknooppunt Hallo en voer de opdracht `cd %hive_home%\bin`.

Hebt u drie manieren toosubmit Hive-query's in Hallo Hadoop-opdrachtregel:

* rechtstreeks
* met behulp van .hql bestanden
* Hello Hive opdrachtconsole

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Indienen van Hive-query's rechtstreeks in Hadoop vanaf de opdrachtregel.
U kunt een opdracht zoals uitvoeren `hive -e "<your hive query>;` toosubmit eenvoudige Hive-query's rechtstreeks in Hadoop vanaf de opdrachtregel. Hier volgt een voorbeeld, waarbij Hallo rode vak overzichten Hallo opdracht die is ingediend door Hallo Hive-query en Hallo groene vak overzichten Hallo uitvoer van Hallo Hive-query.

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Indienen van Hive-query's in .hql bestanden
Wanneer Hallo Hive-query gecompliceerdere is en meerdere regels heeft, is query's in de opdrachtregel of Hive-opdrachtconsole bewerken het niet praktisch. Een alternatief is toouse een teksteditor in het hoofdknooppunt van Hallo Hadoop-cluster toosave Hallo Hive-query's in een bestand .hql in een lokale map van het hoofdknooppunt Hallo Hallo. Vervolgens Hallo Hive-query in Hallo .hql bestand kan worden verzonden met behulp van Hallo `-f` argument als volgt:

    hive -f "<path toohello .hql file>"

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Onderdrukken voortgang Statusoverzicht scherm van Hive-query 's**

Standaard nadat Hive-query wordt verzonden in Hadoop opdrachtregel wordt Hallo voortgang van Hallo kaart/verminderen taak afgedrukt op het scherm. toosuppress Hallo scherm afdrukken van de voortgang van de taak kaart/verminderen hello, kunt u een argument `-S` ("S" in hoofdletters) in Hallo opdrachtregel als volgt:

    hive -S -f "<path toohello .hql file>"
.    hive -S -e '<Hive queries>'

#### <a name="submit-hive-queries-in-hive-command-console"></a>Indienen van Hive-query's in de opdrachtconsole Hive.
U kunt ook eerst Hallo Hive opdrachtconsole invoeren door de opdracht uit te voeren `hive` in Hadoop vanaf de opdrachtregel, en verzend Hive-query's in de opdrachtconsole Hive. Hier volgt een voorbeeld. In dit voorbeeld Hallo twee rode vakken markeren Hallo-opdrachten gebruikt tooenter Hallo Hive opdrachtconsole en Hallo Hive-query verzonden in de Hive-opdrachtconsole, respectievelijk. Hallo groen vak licht Hallo-uitvoer van Hallo Hive-query.

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

de eerdere voorbeelden Hallo uitvoerresultaten rechtstreeks Hallo Hive-query op het scherm. U kunt ook Hallo tooa lokale uitvoerbestand op Hallo hoofdknooppunt of tooan Azure blob schrijven. Vervolgens gebruikt u andere hulpprogramma's toofurther analyseren Hallo-uitvoer van Hive-query's.

**Hive query resultaten tooa lokale bestand voor uitvoer.**
toooutput Hive query resultaten tooa lokale map op het hoofdknooppunt hello, hebt u toosubmit Hallo Hive-query in Hallo Hadoop vanaf de opdrachtregel als volgt:

    hive -e "<hive query>" > <local path in hello head node>

In Hallo voorbeeld te volgen, Hallo-uitvoer van Hive-query is geschreven in een bestand `hivequeryoutput.txt` in directory `C:\apps\temp`.

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Uitvoer Hive query resultaten tooan Azure-blobopslag**

U kunt ook Hallo Hive query resultaten tooan Azure blob, binnen de standaardcontainer Hallo van Hadoop-cluster Hallo uitvoeren. Hallo Hive-query voor deze is als volgt:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

In de Hallo voorbeeld te volgen, Hallo uitvoer van Hive-query tooa blob directory geschreven `queryoutputdir` binnen de standaardcontainer Hallo van Hallo Hadoop-cluster. Hier hoeft u alleen tooprovide Hallo mapnaam, zonder Hallo blob-naam. Een fout gegenereerd als u zowel de directory en de blob-namen, zoals opgeeft `wasb:///queryoutputdir/queryoutput.txt`.

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Als u de standaardcontainer Hallo van Hallo Hadoop-cluster met behulp van Azure Storage Explorer opent, ziet u uitvoer Hallo van Hallo Hive-query zoals weergegeven in de volgende afbeelding Hallo. U kunt toepassen Hallo filter (gemarkeerd met een rood kader) tooonly ophalen Hallo blob met de opgegeven letters in namen.

![Werkruimte maken](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Indienen van Hive-query's met Hallo Hive-Editor
U kunt ook Hallo Query Console (Hive-Editor) gebruiken door een URL van Hallo formulier *https://&#60; De naam van de Hadoop-cluster >.azurehdinsight.net/Home/HiveEditor* in een webbrowser. U moet zijn geregistreerd in Hallo Zie deze console en dus moet u uw hier Hadoop-cluster-referenties.

### <a name="ps"></a> 3. Indienen van Hive-query's met Azure PowerShell-opdrachten
U kunt ook PowerShell toosubmit Hive-query's gebruiken. Zie voor instructies [indienen Hive-taken met behulp van PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Hive-database en tabellen maken
Hallo Hive-query's gedeeld in Hallo [GitHub-opslagplaats](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) en van daaruit kan worden gedownload.

Hier volgt Hallo Hive-query waarmee een Hive-tabel.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Hier volgen beschrijvingen van Hallo Hallo velden die u nodig hebt tooplug in en andere configuraties:

* **&#60; databasenaam >**: Hallo-naam van Hallo-database die u toocreate wilt. Desgewenst kunt u alleen toouse Hallo standaarddatabase Hallo query *database maken...*  kunnen worden weggelaten.
* **&#60; tabelnaam >**: Hallo-naam van de gewenste toocreate binnen de opgegeven database Hallo Hallo-tabel. Als u toouse Hallo standaarddatabase wilt, Hallo tabel rechtstreeks kan worden verwezen door *&#60; tabelnaam >* zonder &#60; databasenaam >.
* **&#60; veldscheidingsteken >**: Hallo scheidingsteken die velden in Hallo gegevens bestand toobe begrenst geüpload toohello Hive-tabel.
* **&#60; regelscheiding >**: regels in het gegevensbestand Hallo begrenst Hallo scheidingsteken.
* **&#60; opslaglocatie >**: hello Azure storage toosave Hallo locatiegegevens van Hive-tabellen. Als u geen opgeeft *locatie &#60; opslaglocatie >*, Hallo database en hello tabellen zijn opgeslagen in *hive/datawarehouse/* map in de standaardcontainer Hallo van Hallo Hive cluster standaard. Als u toospecify Hallo-opslaglocatie wilt, heeft de opslaglocatie Hallo toobe binnen de standaardcontainer Hallo voor Hallo-database en tabellen. Deze locatie heeft een toobe verwezen als locatie relatieve toohello standaardcontainer van Hallo-cluster op Hallo-indeling van *' wasb: / / / &#60; map 1 > / "* of *' wasb: / / / &#60; map 1 > / &#60; map 2 > / "*, enzovoort. Nadat het Hallo-query wordt uitgevoerd, worden Hallo relatieve mappen in Hallo standaardcontainer gemaakt.
* **TBLPROPERTIES("SKIP.header.line.Count"="1")**: als het gegevensbestand Hallo een kopregel heeft, hebt u tooadd deze eigenschap **aan Hallo einde** Hallo *tabel maken* query. Anders is Hallo kopregel geladen als een tabel, record toohello. Als het Hallo-gegevensbestand geen een kopregel heeft, kan deze configuratie worden weggelaten in Hallo-query.

## <a name="load-data"></a>TooHive gegevenstabellen laden
Hier volgt Hallo Hive-query die gegevens in een Hive-tabel laadt.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; pad tooblob gegevens >**: als Hallo blob bestand geüpload toobe toohello Hive-tabel in de standaardcontainer Hallo Hallo HDInsight Hadoop-cluster, Hallo *&#60; pad tooblob gegevens >* moet Hallo-indeling *' wasb: / / / &#60; directory in deze container > / &#60; blob-bestandsnaam >'*. Hallo blob-bestand kan ook worden in een extra container Hallo HDInsight Hadoop-cluster. In dit geval *&#60; pad tooblob gegevens >* moet Hallo indeling *' wasb: / / &#60; containernaam > @&#60; opslagaccountnaam >.blob.core.windows.net/ &#60; blob-bestandsnaam >'*.

  > [!NOTE]
  > Hallo heeft toobe geüpload blob-tooHive gegevenstabel toobe in Hallo standaard of extra container van Hallo storage-account voor Hallo Hadoop-cluster. Anders Hallo *gegevens laden* klagen dat deze geen toegang gegevens Hallo tot query is mislukt.
  >
  >

## <a name="partition-orc"></a>Onderwerpen over geavanceerde: gepartitioneerde tabel en archief Hive-gegevens in ORC-indeling
Als Hallo gegevens groot is, is partitioneren van tabel Hallo nuttig is voor query's die u alleen tooscan enkele partities van Hallo tabel hoeft. Het is bijvoorbeeld redelijke toopartition Hallo logboekgegevens van een website door datums.

In aanvulling toopartitioning Hive-tabellen, het is ook nuttig toostore Hallo Hive gegevens in Hallo geoptimaliseerd rij kolommen (ORC)-indeling. Zie voor meer informatie over het ORC opmaak <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">met behulp van ORC-bestanden verbetert de prestaties wanneer Hive lezen, schrijven en verwerken van gegevens</a>.

### <a name="partitioned-table"></a>Gepartitioneerde tabel
Hier volgt Hallo Hive-query die een gepartitioneerde tabel maakt en gegevens worden geladen in de App.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Tijdens het opvragen van gepartitioneerde tabellen, verdient het tooadd Hallo partitie voorwaarde in Hallo **begin** Hallo `where` component deze verbetert Hallo effectiviteit aanzienlijk te zoeken.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Hive-gegevens opslaat in ORC-indeling
U kan niet rechtstreeks gegevens uit blob-opslag laden in de Hive-tabellen die zijn opgeslagen in Hallo ORC-indeling. Hier volgen de stappen Hallo die Hallo moet u tootake tooload gegevens van Azure blobs tooHive tabellen die zijn opgeslagen in ORC-indeling.

Maken van een externe tabel **opgeslagen AS TEXTFILE** en laden van gegevens uit blob storage toohello tabel.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Een interne tabel maken met de Hallo Hallo hetzelfde schema als externe tabel Hallo in stap 1, hello dezelfde veldscheidingsteken en op te slaan Hive-gegevens in Hallo ORC-indeling.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Selecteer de gegevens uit de externe tabel Hallo in stap 1 en invoegen in Hallo ORC tabel

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Als Hallo TEXTFILE tabel *&#60; databasenaam >. &#60; externe textfile tabelnaam >* partities bevat, in stap 3 hello `SELECT * FROM <database name>.<external textfile table name>` opdracht selecteert Hallo partitie variabele een veld in Hallo gegevensset geretourneerd. Opneemt in Hallo *&#60; databasenaam >. &#60; ORC-tabelnaam >* mislukt sinds *&#60; databasenaam >. &#60; ORC-tabelnaam >* heeft geen Hallo partitie variabele als een veld in het tabelschema Hallo. In dit geval moet u toospecifically Selecteer Hallo velden toobe ingevoegd te*&#60; databasenaam >. &#60; ORC-tabelnaam >* als volgt:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

Het is veilig toodrop hello *&#60; externe textfile tabelnaam >* wanneer met behulp van de query te volgen nadat alle gegevens Hallo is ingevoegd in *&#60; databasenaam >. &#60; ORC-tabelnaam >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Na deze procedure uitvoert, moet u een tabel met gegevens in Hallo ORC indeling gereed toouse hebben.  
