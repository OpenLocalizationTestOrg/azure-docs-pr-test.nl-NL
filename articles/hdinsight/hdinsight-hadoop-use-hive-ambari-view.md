---
title: aaaUse Ambari-weergaven toowork met Hive in HDInsight (Hadoop) - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hive-weergave Hallo van uw web browser toosubmit Hive-query's. Hallo Hive-weergave maakt deel uit van Hallo die ambari-Webgebruikersinterface is voorzien van uw Linux gebaseerde HDInsight-cluster.
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
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Hallo Hive-weergave gebruiken met Hadoop in HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Meer informatie over hoe toorun Hive van query's met Ambari Hive-weergave. Ambari is een beheer en controle hulpprogramma met HDInsight op basis van Linux-clusters. Een van de Hallo functies via Ambari is een Webgebruikersinterface die gebruikte toorun Hive-query's kunnen worden.

> [!NOTE]
> Ambari heeft veel mogelijkheden die niet in dit document worden besproken. Zie voor meer informatie [HDInsight-clusters beheren met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Vereisten

* Een Linux gebaseerde HDInsight-cluster. Zie voor meer informatie over het maken van de cluster [aan de slag met HDInsight op basis van Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="open-hello-hive-view"></a>Open Hallo Hive-weergave

U kunt Ambari-weergaven van hello Azure-portal; Selecteer uw HDInsight-cluster en selecteer vervolgens **Ambari-weergaven** van Hallo **snelkoppelingen** sectie.

![sectie Snelle koppelingen van Hallo-portal](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Selecteer in de lijst van de Hallo van weergaven, Hallo __Hive-weergave__.

![Hallo Hive-weergave geselecteerd](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Bij het openen van Ambari zijn na vragen aan gebruiker tooauthenticate toohello site. Hallo beheerder invoeren (standaard `admin`) en het wachtwoord die u hebt gebruikt bij het maken van de cluster Hallo account.

Hier ziet u een pagina vergelijkbaar toohello installatiekopie te volgen:

![Afbeelding van Hallo query werkblad voor Hallo Hive-weergave](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Een query uitvoeren

een hive-query toorun gebruiken Hallo volgende stappen uit Hallo Hive-weergave.

1. Van Hallo __Query__ tabblad, Hallo HiveQL-instructies te volgen in Hallo werkblad plakken:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Deze instructies uitvoeren Hallo volgende acties:

   * `DROP TABLE`-Verwijdert Hallo tabel en Hallo-gegevensbestand als Hallo tabel al bestaat.

   * `CREATE EXTERNAL TABLE`-Maakt een nieuwe tabel 'extern' in Hive.
   Alleen de tabeldefinitie Hallo opslaan externe tabellen in Hive. Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.

   * `ROW FORMAT`-Hoe Hallo gegevens zijn opgemaakt. In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.

   * `STORED AS TEXTFILE LOCATION`-Waar Hallo gegevens worden opgeslagen en dat deze is opgeslagen als tekst.

   * `SELECT`: Hiermee kunt u een telling van alle rijen waarin kolom t4 Hallo waarde [fout] bevat.

     > [!NOTE]
     > Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent. Bijvoorbeeld, een geautomatiseerde uploaden van gegevens verwerken, of door een andere MapReduce-bewerking. Verwijderen van een externe tabel komt *niet* Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.

    > [!IMPORTANT]
    > Hallo laat __Database__ selectie __standaard__. Hallo-voorbeelden in dit document Hallo-standaarddatabase die is opgenomen in HDInsight gebruiken.

2. toostart hello query, gebruik Hallo **Execute** knop onder Hallo werkblad. Tekstwijzigingen oranje en hello te wordt**stoppen**.

3. Zodra het Hallo-query is voltooid, Hallo **resultaten** tabblad Hallo resultaten van Hallo bewerking weer. na de tekst Hello is Hallo resultaat van het Hallo-query:

        sev       cnt
        [ERROR]   3

    Hallo **logboeken** tabblad kan worden gemaakt door de taak Hallo Hallo-logboekgegevens voor gebruikte tooview.

   > [!TIP]
   > Hallo **resultaten opslaan** dialoogvenster vervolgkeuzelijst in het bovenste Hallo links van de Hallo **resultaten queryproces** sectie kunt u toodownload of resultaten opslaan.

4. Selecteer de eerste vier regels Hallo van deze query Selecteer **Execute**. U ziet dat er geen resultaten zijn wanneer Hallo-taak is voltooid. Met behulp van Hallo **Execute** knop indien deel van de query Hallo alleen wordt uitgevoerd Hallo geselecteerde instructies is geselecteerd. Hallo selectie bevatten niet in dit geval Hallo laatste instructie waarmee rijen worden opgehaald uit de tabel Hallo. Als u alleen die regel selecteren en gebruik **Execute**, ziet u resultaten Hallo verwacht.

5. tooadd een werkblad gebruiken Hallo **nieuw werkblad** knop onderin Hallo Hallo **Query-Editor**. Voer in nieuw werkblad Hallo Hallo HiveQL-instructies te volgen:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Deze instructies uitvoeren Hallo volgende acties:

   * **MAKEN van tabel als niet bestaat** -maakt een tabel, als deze niet al bestaat. Sinds Hallo **externe** trefwoord wordt niet gebruikt, een interne tabel is gemaakt. Een interne tabel wordt opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive. In tegenstelling tot externe tabellen verwijdert de Hallo onderliggende gegevens ook een interne tabel verwijderen.

   * **OPGESLAGEN AS ORC** -Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling. ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.

   * **INSERT OVERSCHRIJVEN... Selecteer** -rijen uit Hallo geselecteerd **log4jLogs** tabel met `[ERROR]`, en vervolgens voegt de gegevens in Hallo Hallo **foutenlogboeken** tabel.

     Gebruik Hallo **Execute** knop toorun deze query. Hallo **resultaten** tabblad bevat geen gegevens wanneer Hallo query nul rijen retourneert. Hallo status moet worden weergegeven als **geslaagd** zodra Hallo-query is voltooid.

### <a name="visual-explain"></a>Visual wordt uitgelegd

een visualisatie van queryplan hello, selecteer Hallo toodisplay **Visual uitgelegd** tabblad onder Hallo werkblad.

Hallo **Visual uitgelegd** -weergave van Hallo query kan nuttig zijn bij het begrijpen van de stroom Hallo van complexe query's zijn. U kunt een tekstuele equivalent van deze weergave weergeven met behulp van Hallo **uitleg** knop in Hallo Query-Editor.

### <a name="tez-ui"></a>Tez-gebruikersinterface

toodisplay hello Tez UI voor Hallo query, selecteer Hallo **Tez** tabblad onder Hallo werkblad.

> [!IMPORTANT]
> Tez wordt niet gebruikt tooresolve alle query's. Groot aantal query's kunnen worden opgelost zonder Tez. 

Als Tez gebruikte tooresolve Hallo query, wordt Hallo gestuurde acyclische grafiek (DAG) weergegeven. Als u tooview Hallo DAG wilt voor query's in de afgelopen Hallo hebt uitgevoerd, of fouten opsporen in Tez proces hello, gebruikt u Hallo [Tez weergave](hdinsight-debug-ambari-tez-view.md) in plaats daarvan.

## <a name="view-job-history"></a>Taakgeschiedenis weergeven

Hallo __taken__ tabblad geeft een geschiedenis van Hive-query's.

![Afbeelding van de taakgeschiedenis Hallo](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Databasetabellen

U kunt Hallo __tabellen__ tabblad toowork met tabellen in een Hive-database.

![Afbeelding van tabblad Hallo-tabellen](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Opgeslagen query 's

Vanaf het tabblad Query hello, kunt u eventueel query's opslaan. Wanneer opgeslagen, kunt u de query voor Hallo van Hallo hergebruiken __opgeslagen query's__ tabblad.

![Afbeelding van tabblad opgeslagen query 's](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Gebruiker gedefinieerde functies

Hive kan ook worden uitgebreid door de gebruiker gedefinieerde functies (UDF). Een UDF kunt u de functionaliteit van tooimplement of logica die eenvoudig niet is gemodelleerd in HiveQL.

Hallo UDF-tabblad bovenaan Hallo Hallo Hive-weergave kunt u toodeclare en een set UDF's opslaan. Deze UDF's kunnen worden gebruikt met Hallo **Query-Editor**.

![Afbeelding van tabblad UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

Nadat u een UDF toohello Hive-weergave hebt toegevoegd een **invoegen UDF's** knop wordt weergegeven aan de onderkant Hallo Hallo **Query-Editor**. Als u dit item selecteert, geeft een lijst vervolgkeuzelijst Hallo UDF's die zijn gedefinieerd in Hallo Hive-weergave. Als u een UDF, voegt HiveQL-instructies tooyour query tooenable Hallo UDF.

Bijvoorbeeld, als u hebt een UDF gedefinieerd Hello volgende eigenschappen:

* Naam van bron: myudfs

* Bronpad: /myudfs.jar

* {UDF-naam: myawesomeudf

* {UDF-klassenaam: com.myudfs.Awesome

Met behulp van Hallo **invoegen UDF's** knop wordt weergegeven voor een item met de naam **myudfs**, met een andere vervolgkeuzelijst voor elke UDF gedefinieerd voor die bron. In dit geval **myawesomeudf**. Dit item te selecteren, wordt na toohello begin van de query Hallo Hallo toegevoegd:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

U kunt vervolgens Hallo UDF gebruiken in uw query. Bijvoorbeeld `SELECT myawesomeudf(name) FROM people;`.

Zie voor meer informatie over het gebruik van UDF's met Hive in HDInsight Hallo documenten te volgen:

* [Met behulp van Python met Hive en Pig in HDInsight](hdinsight-python.md)
* [Hoe een aangepaste Hive UDF-tooHDInsight tooadd](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Hive-instellingen

Instellingen kunnen worden gebruikt toochange diverse Hive-instellingen. Engine voor het uitvoeren van Hallo voor Hive bijvoorbeeld gewijzigd van tooMapReduce Tez (Hallo standaard).

## <a id="nextsteps"></a>Volgende stappen

Voor algemene informatie over Hive in HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)
