---
title: Ambari-weergaven gebruiken om te werken met Hive in HDInsight (Hadoop) - Azure | Microsoft Docs
description: Informatie over het gebruik van de Hive-weergave van uw webbrowser Hive-query's verzenden. Het Hive-weergave maakt deel uit van de Ambari-Webgebruikersinterface voorzien van uw Linux gebaseerde HDInsight-cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 80df3da4d62feb814ea2dd97c96e57954093c5c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a>De weergave Hive gebruiken met Hadoop in HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Informatie over het uitvoeren van Hive-query's met Ambari Hive-weergave. Ambari is een beheer en controle hulpprogramma met HDInsight op basis van Linux-clusters. Een van de functies die worden geleverd via Ambari is een Web-UI die kan worden gebruikt voor het uitvoeren van Hive-query's.

> [!NOTE]
> Ambari heeft veel mogelijkheden die niet in dit document worden besproken. Zie voor meer informatie [HDInsight-clusters beheren met behulp van de Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Vereisten

* Een Linux gebaseerde HDInsight-cluster. Zie voor meer informatie over het maken van de cluster [aan de slag met HDInsight op basis van Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> De stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="open-the-hive-view"></a>Open de Hive-weergave

Kunt u Ambari-weergaven uit de Azure portal; Selecteer uw HDInsight-cluster en selecteer vervolgens **Ambari-weergaven** van de **snelkoppelingen** sectie.

![Snelle koppelingen sectie van de portal](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Selecteer in de lijst met weergaven, de __Hive-weergave__.

![De Hive-weergave geselecteerd](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Bij het openen van Ambari, wordt u gevraagd om de site te verifiëren. Voer de beheerder (standaard `admin`) account naam en het wachtwoord die u hebt gebruikt bij het maken van het cluster.

Hier ziet u een pagina zoals in de volgende afbeelding:

![Afbeelding van het werkblad query voor de Hive-weergave](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Een query uitvoeren

Als u wilt een hive-query uitvoert, gebruik de volgende stappen uit de Hive-weergave.

1. Van de __Query__ tabblad, plak de volgende HiveQL-instructies in het werkblad:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Deze instructies uitvoeren de volgende acties:

   * `DROP TABLE`-Hiermee verwijdert u de tabel en het gegevensbestand als de tabel al bestaat.

   * `CREATE EXTERNAL TABLE`-Maakt een nieuwe tabel 'extern' in Hive.
   Externe tabellen worden de definitie van de tabel in Hive opslaan. De gegevens blijft op de oorspronkelijke locatie.

   * `ROW FORMAT`-Hoe de gegevens zijn ingedeeld. In dit geval worden de velden in elk logboek gescheiden door een spatie.

   * `STORED AS TEXTFILE LOCATION`-Waar de gegevens worden opgeslagen en dat deze is opgeslagen als tekst.

   * `SELECT`: Hiermee kunt u een telling van alle rijen waarin t4 kolom de waarde [fout bevat].

     > [!NOTE]
     > Externe tabellen moeten worden gebruikt wanneer u de onderliggende gegevens wordt bijgewerkt door een externe bron verwacht. Bijvoorbeeld, een geautomatiseerde uploaden van gegevens verwerken, of door een andere MapReduce-bewerking. Verwijderen van een externe tabel komt *niet* de gegevens, de definitie van de tabel verwijderen.

    > [!IMPORTANT]
    > Laat de __Database__ selectie __standaard__. De voorbeelden in dit document gebruikt de standaarddatabase die is opgenomen in HDInsight.

2. Voor het starten van de query gebruikt de **Execute** knop onder het werkblad. Het oranje verandert en verandert de tekst in **stoppen**.

3. Nadat de query is voltooid, de **resultaten** tabblad geeft de resultaten van de bewerking. De volgende tekst is het resultaat van de query:

        sev       cnt
        [ERROR]   3

    De **logboeken** tabblad kan worden gebruikt om gegevens in het logboek wordt gemaakt door de taak weer te geven.

   > [!TIP]
   > De **resultaten opslaan** dialoogvenster van de vervolgkeuzelijst in de linkerbovenhoek links van de **resultaten queryproces** sectie kunt u downloaden of het opslaan van resultaten.

4. Selecteer de eerste vier regels van deze query en vervolgens **Execute**. U ziet dat er geen resultaten zijn wanneer de taak is voltooid. Met behulp van de **Execute** knop als deel van de query is geselecteerd. alleen de geselecteerde instructies wordt uitgevoerd. De selectie bevatten niet in dit geval wordt de laatste instructie die rijen opgehaald uit de tabel. Als u alleen die regel selecteren en gebruik **Execute**, ziet u de verwachte resultaten.

5. U kunt een werkblad toevoegen met de **nieuw werkblad** knop aan de onderkant van de **Query-Editor**. Voer de volgende HiveQL-instructies in het nieuwe werkblad:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Deze instructies uitvoeren de volgende acties:

   * **MAKEN van tabel als niet bestaat** -maakt een tabel, als deze niet al bestaat. Aangezien de **externe** trefwoord wordt niet gebruikt, een interne tabel is gemaakt. Een interne tabel wordt opgeslagen in het datawarehouse Hive en volledig wordt beheerd door Hive. In tegenstelling tot externe tabellen voor het verwijderen van een interne tabel worden verwijderd en de onderliggende gegevens.

   * **OPGESLAGEN AS ORC** -slaat de gegevens geoptimaliseerd rij kolommen (ORC)-indeling. ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.

   * **INSERT OVERSCHRIJVEN... Selecteer** -selecteert rijen uit de **log4jLogs** tabel met `[ERROR]`, en vervolgens voegt u de gegevens in de **foutenlogboeken** tabel.

     Gebruik de **Execute** knop deze query uit te voeren. De **resultaten** tabblad bevat geen gegevens wanneer de query nul rijen retourneert. De status moet worden weergegeven als **geslaagd** zodra de query is voltooid.

### <a name="visual-explain"></a>Visual wordt uitgelegd

Als u wilt een visualisatie van het queryplan weergeven, selecteert u de **Visual uitgelegd** tabblad onder het werkblad.

De **Visual uitgelegd** weergave van de query kan nuttig zijn bij het begrijpen van de stroom van complexe query's zijn. U kunt een tekstuele equivalent van deze weergave weergeven met behulp van de **uitleg** knop in de Query-Editor.

### <a name="tez-ui"></a>Tez-gebruikersinterface

Als u wilt de Tez UI voor de query weergeven, selecteert u de **Tez** tabblad onder het werkblad.

> [!IMPORTANT]
> Tez wordt niet gebruikt voor het omzetten van alle query's. Groot aantal query's kunnen worden opgelost zonder Tez. 

Als Tez is gebruikt voor het omzetten van de query, wordt de omgeleid acyclische grafiek (DAG) weergegeven. Als u weergeven van de DAG wilt voor query's in het verleden hebt uitgevoerd, of het proces Tez voor foutopsporing gebruiken de [Tez weergave](hdinsight-debug-ambari-tez-view.md) in plaats daarvan.

## <a name="view-job-history"></a>Taakgeschiedenis weergeven

De __taken__ tabblad geeft een geschiedenis van Hive-query's.

![Afbeelding van de taakgeschiedenis](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Databasetabellen

U kunt de __tabellen__ tabblad om te werken met tabellen in een Hive-database.

![Afbeelding van het tabblad tabellen](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Opgeslagen query 's

U kunt eventueel query's opslaan op het tabblad Query. Wanneer opgeslagen, kunt u de query van hergebruiken de __opgeslagen query's__ tabblad.

![Afbeelding van tabblad opgeslagen query 's](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Gebruiker gedefinieerde functies

Hive kan ook worden uitgebreid door de gebruiker gedefinieerde functies (UDF). Een UDF, kunt u functionaliteit of logica die eenvoudig niet is gemodelleerd in HiveQL implementeren.

De UDF boven op het tabblad van de weergave Hive kunt u declareren en een reeks UDF's op te slaan. Deze UDF's kunnen worden gebruikt met de **Query-Editor**.

![Afbeelding van tabblad UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

Nadat u hebt een UDF toegevoegd aan de weergave Hive, een **invoegen UDF's** knop wordt weergegeven aan de onderkant van de **Query-Editor**. Als u deze vermelding geeft een vervolgkeuzelijst van de UDF's gedefinieerd in de weergave Hive weer. Als u een UDF, voegt HiveQL-instructies toe aan uw query voor het inschakelen van de UDF.

Bijvoorbeeld, als u hebt gedefinieerd een UDF met de volgende eigenschappen:

* Naam van bron: myudfs

* Bronpad: /myudfs.jar

* {UDF-naam: myawesomeudf

* {UDF-klassenaam: com.myudfs.Awesome

Met behulp van de **invoegen UDF's** knop wordt weergegeven voor een item met de naam **myudfs**, met een andere vervolgkeuzelijst voor elke UDF gedefinieerd voor die bron. In dit geval **myawesomeudf**. Dit item te selecteren, worden de volgende toegevoegd aan het begin van de query:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

U kunt vervolgens de UDF gebruiken in uw query. Bijvoorbeeld `SELECT myawesomeudf(name) FROM people;`.

Zie de volgende documenten voor meer informatie over het gebruik van UDF's met Hive in HDInsight:

* [Met behulp van Python met Hive en Pig in HDInsight](hdinsight-python.md)
* [Het toevoegen van een aangepaste Hive UDF naar HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Hive-instellingen

Instellingen kunnen worden gebruikt om verschillende Hive-instellingen te wijzigen. Bijvoorbeeld wijzigen van de engine voor het uitvoeren voor MapReduce onderdeel van Tez (de standaardinstelling).

## <a id="nextsteps"></a>Volgende stappen

Voor algemene informatie over Hive in HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)
