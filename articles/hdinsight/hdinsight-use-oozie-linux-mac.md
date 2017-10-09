---
title: aaaUse Hadoop Oozie werkstromen in Linux gebaseerde HDInsight | Microsoft Docs
description: Gebruik Hadoop Oozie in HDInsight op basis van Linux. Meer informatie over hoe toodefine een Oozie-werkstroom en het verzenden van een Oozie-taak.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Oozie gebruiken met Hadoop toodefine en uitvoeren van een werkstroom op Linux gebaseerde HDInsight

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Meer informatie over hoe toouse Apache Oozie met Hadoop op HDInsight. Apache Oozie is een werkstroom/coördinatie systeem waarmee Hadoop-taken worden beheerd. Oozie is geïntegreerd met Hadoop-stack Hallo en ondersteunt Hallo taken te volgen:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie kan ook worden gebruikt tooschedule taken die specifieke tooa systeem, zoals Java-programma's of shell-scripts zijn

> [!NOTE]
> Een andere optie voor het definiëren van werkstromen met HDInsight is Azure Data Factory. Zie toolearn meer informatie over Azure Data Factory [Use Pig en Hive met Data Factory][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Oozie is niet ingeschakeld op HDInsight domein.

## <a name="prerequisites"></a>Vereisten

* **Een HDInsight-cluster**: Zie [aan de slag met HDInsight op Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="example-workflow"></a>Van de voorbeeldwerkstroom

Hallo-werkstroom gebruikt in dit document bevat twee acties. Acties zijn definities voor taken zoals het uitvoeren van Hive, Sqoop, MapReduce of ander proces:

![Werkstroomdiagram][img-workflow-diagram]

1. Een Hive-actie wordt uitgevoerd een HiveQL-script tooextract records uit Hallo **hivesampletable** opgenomen met HDInsight. Elke rij gegevens beschrijft een bezoek van een specifieke mobiele apparaat. Hallo recordindeling weergegeven vergelijkbaar toohello volgende tekst:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Hallo Hive-script in dit document gebruikt telt Hallo totaal aantal bezoeken voor elk platform (zoals Android of iPhone) en slaat Hallo aantallen tooa nieuwe Hive-tabel.

    Zie [Hive gebruiken met HDInsight][hdinsight-use-hive] voor meer informatie over Hive.

2. Een actie Sqoop exporteert Hallo inhoud van Hallo nieuwe Hive tooa tabel in een Azure SQL database. Zie voor meer informatie over Sqoop [Hadoop-Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Zie voor ondersteunde versies van de Oozie op HDInsight-clusters, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Hallo-werkmap maken

Oozie verwacht resources die vereist zijn voor een taak toobe die wordt opgeslagen in Hallo dezelfde directory. In dit voorbeeld wordt **wasb: / / / zelfstudies/useoozie**. Gebruik Hallo opdracht toocreate na deze map en het Hallo-gegevensmap waarin Hallo nieuwe Hive-tabel is gemaakt door deze werkstroom:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Hallo `-p` parameter zorgt ervoor dat alle mappen in Hallo pad toobe gemaakt. Hallo **gegevens** map is gebruikte toohold gegevens die worden gebruikt door Hallo **useooziewf.hql** script.

Hallo na de opdracht die zorgt ervoor dat Oozie uw gebruikersaccount imiteren kan bij het uitvoeren van Hive en Sqoop taken ook uitvoeren. Vervang **gebruikersnaam** met de aanmeldingsnaam van uw:

```
sudo adduser USERNAME users
```

> [!NOTE]
> U kunt fouten negeren die Hallo-gebruiker is al een lid van Hallo `users` groep.

## <a name="add-a-database-driver"></a>Toevoegen van een databasestuurprogramma

Omdat deze werkstroom Sqoop tooexport gegevens tooSQL Database gebruikt, kunt u een kopie van Hallo JDBC-stuurprogramma gebruikt tootalk tooSQL Database moet opgeven. Gebruik Hallo na de opdracht toocopy deze werkmap toohello:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

Als uw werkstroom andere resources, zoals een jar met een MapReduce-toepassingen gebruikt, moet u tooadd ook deze resources.

## <a name="define-hello-hive-query"></a>Hallo Hive-query definiëren

Gebruik Hallo stappen toocreate een HiveQL-script dat definieert u een query die wordt gebruikt in een werkstroom Oozie verderop in dit document te volgen.

1. Toohello-cluster via SSH verbinding. Hallo volgende opdracht is een voorbeeld van het gebruik van Hallo `ssh` opdracht. Vervang __gebruikersnaam__ met Hallo SSH-gebruiker voor Hallo-cluster. Vervang __CLUSTERNAME__ met de naam van de HDInsight-cluster Hallo Hallo.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Gebruik van Hallo SSH-verbinding, Hallo opdracht toocreate een bestand te volgen:

    ```
    nano useooziewf.hql
    ```

3. Zodra het Hallo nano-editor wordt geopend, gebruikt u Hallo query als Hallo inhoud van Hallo-bestand te volgen:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Er zijn twee variabelen in Hallo script gebruikt:

    * **${hiveTableName}**: Hallo naam bevat van Hallo tabel toobe gemaakt

    * **${hiveDataFolder}**: Hallo locatie toostore Hallo-gegevensbestanden voor de tabel Hallo bevat

    Hallo werkstroom-definitiebestand (workflow.xml in deze zelfstudie) geeft deze waarden toothis HiveQL-script tijdens runtime

4. tooexit Hallo-editor, druk op Ctrl X. Wanneer u wordt gevraagd, selecteert u **Y** toosave bestand Hallo en gebruik vervolgens **Enter** toouse hello **useooziewf.hql** bestandsnaam.

5. Gebruik Hallo deze opdrachten toocopy **useooziewf.hql** te**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Deze opdrachten opslaan Hallo **useooziewf.hql** -bestand op Hallo HDFS-compatibele opslag voor Hallo-cluster.

## <a name="define-hello-workflow"></a>Hallo werkstroom definiëren

Oozie werkstromen definities worden geschreven in hPDL (een XML-proces Definition Language). Gebruik Hallo stappen toodefine Hallo workflow volgen:

1. Na de instructie toocreate hello gebruiken en bewerken van een nieuw bestand:

    ```
    nano workflow.xml
    ```

2. Zodra Hallo nano-editor wordt geopend, Voer Hallo XML als Hallo bestandsinhoud te volgen:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    Er zijn twee acties in de werkstroom Hallo gedefinieerd:

   * **RunHiveScript**: met deze actie Hallo startactie en wordt uitgevoerd Hallo **useooziewf.hql** Hive-script

   * **RunSqoopExport**: deze actie exporteert Hallo gegevens gemaakt op basis van Hallo Hive-script tooSQL Sqoop-Database. Deze actie wordt alleen uitgevoerd als hello **RunHiveScript** actie is geslaagd.

     Hallo werkstroom heeft enkele items zoals `${jobTracker}`. Deze vermeldingen worden vervangen door waarden die u in de taakdefinitie hello gebruiken. Hallo taakdefinitie wordt verderop in dit document gemaakt.

     Ook Opmerking Hallo `<archive>sqljdbc4.jar</arcive>` vermelding in Hallo Sqoop-sectie. Deze vermelding geeft opdracht Oozie toomake dit archief die beschikbaar zijn voor Sqoop wanneer deze actie wordt uitgevoerd.

3. Gebruik Ctrl X vervolgens **Y** en **Enter** toosave Hallo-bestand.

4. Gebruik Hallo volgende opdracht toocopy hello **workflow.xml** bestand te**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Hallo-database maken

een Azure SQL Database toocreate Hallo stappen in Hallo [maken van een SQL-Database](../sql-database/sql-database-get-started.md) document. Gebruik bij het maken van database Hallo `oozietest` als Hallo databasenaam. Maak ook een notitie van Hallo-naam van de databaseserver Hallo.

### <a name="create-hello-table"></a>Hallo-tabel maken

> [!NOTE]
> Er zijn veel manieren tooconnect tooSQL Database toocreate een tabel. Hallo na gebruik van de stappen [FreeTDS](http://www.freetds.org/) van Hallo HDInsight-cluster.


1. Gebruik Hallo opdracht tooinstall FreeTDS op Hallo HDInsight-cluster te volgen:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Zodra FreeTDS is geïnstalleerd, opdracht gebruik Hallo volgende uit tooconnect toohello SQL Database-server die u eerder hebt gemaakt:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    U ontvangt uitvoer vergelijkbare toohello volgende tekst:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. Op Hallo `1>` gevraagd, voert u Hallo volgende regels:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Wanneer Hallo `GO` instructie wordt ingevoerd, Hallo vorige instructies worden geëvalueerd. Deze instructies maken van een tabel met de naam **mobiledata** dat wordt gebruikt door het Hallo-werkstroom.

    Gebruik Hallo na tooverify die Hallo tabel is gemaakt:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Ziet u uitvoer vergelijkbare toohello volgende tekst:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Voer `exit` op Hallo `1>` vragen tooexit Hallo tsql-hulpprogramma.

## <a name="create-hello-job-definition"></a>Hallo taakdefinitie maken

Hallo taakdefinitie beschrijft waar toofind workflow.xml Hallo. Ook wordt beschreven waar toofind andere bestanden die worden gebruikt door de werkstroom hello (zoals useooziewf.hql.) Het definieert ook Hallo waarden voor eigenschappen binnen de werkstroom Hallo gebruikt en bestanden bijbehorende.

1. Hallo volgende opdracht tooget Hallo volledige adres Hallo standaard opslag gebruiken. Dit adres wordt gebruikt in het configuratiebestand hello later:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Met deze opdracht retourneert informatie vergelijkbare toohello XML te volgen:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Als Azure-opslag Hallo HDInsight-cluster als Hallo standaard opslag gebruikt, Hallo `<value>` element inhoud beginnen met `wasb://`. Als Azure Data Lake Store in plaats daarvan wordt gebruikt, deze begint met `adl://`.

    Hallo-inhoud van Hallo opslaan `<value>` element, zoals deze wordt gebruikt in de volgende stappen Hallo.

2. Gebruik hello opdracht tooget FQDN-naam van Hallo cluster headnode te volgen. Deze informatie wordt gebruikt voor Hallo JobTracker adres voor Hallo-cluster:

    ```
    hostname -f
    ```

    Hiermee wordt informatie vergelijkbare toohello volgende tekst:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Hallo poort gebruikt voor Hallo JobTracker is 8050, waardoor de Hallo volledig adres toouse voor Hallo JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Gebruik Hallo toocreate hello Oozie-taakconfiguratie definitie te volgen:

    ```
    nano job.xml
    ```

4. Zodra het Hallo nano-editor wordt geopend, gebruikt u Hallo XML als Hallo inhoud van Hallo-bestand te volgen:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * Vervang alle exemplaren van  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  met Hallo-waarde die u eerder hebt ontvangen voor de opslag van de standaard.

     > [!WARNING]
     > Als het Hallo-pad is een `wasb` pad, moet u het volledige pad hello gebruiken. Kan geen moet u deze toojust `wasb:///`.

   * Vervang **JOBTRACKERADDRESS** Hello JobTracker/ResourceManager adres die u eerder hebt ontvangen.
   * Vervang **uwnaam** met de aanmeldingsnaam van uw voor Hallo HDInsight-cluster.
   * Vervang **serverName**, **adminLogin**, en **adminPassword** met Hallo-informatie voor uw Azure SQL Database.

     De meeste Hallo-informatie in dit bestand is gebruikte toopopulate Hallo waarden gebruikt in Hallo workflow.xml of ooziewf.hql-bestanden (bijvoorbeeld ${nameNode}.)

     > [!NOTE]
     > Hallo **oozie.wf.application.path** vermelding definieert waar toofind hello workflow.xml bestand, dat Hallo workflow bevat die worden uitgevoerd door deze taak.

5. Gebruik Ctrl X vervolgens **Y** en **Enter** toosave Hallo-bestand.

## <a name="submit-and-manage-hello-job"></a>Indienen en Hallo taak beheren

Hallo volgt gebruik Hallo Oozie opdracht toosubmit en Oozie-werkstromen op Hallo cluster beheren. Hallo Oozie-opdracht is een beschrijvende interface via Hallo [Oozie REST-API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Wanneer u Hallo Oozie-opdracht, moet u Hallo FQDN voor Hallo HDInsight headnode. Deze FDQN-naam is alleen toegankelijk is vanaf Hallo cluster of als hello cluster zich op een virtueel netwerk in Azure vanuit andere machines op Hallo van hetzelfde netwerk.


1. Hallo tooobtain Hallo URL toohello Oozie service volgende gebruiken:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Hiermee wordt informatie vergelijkbare toohello XML te volgen:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Hallo `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` gedeelte Hallo URL toouse Hello Oozie-opdracht is.

2. Gebruik Hallo na toocreate een omgevingsvariabele voor Hallo-URL, zodat er geen tootype voor elke opdracht:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Hallo URL vervangen door Hallo een die u eerder hebt ontvangen.
3. Hallo toosubmit Hallo taak volgende gebruiken:

    ```
    oozie job -config job.xml -submit
    ```

    Met deze opdracht wordt geladen Hallo taakgegevens uit **job.xml** en verstuurt tooOozie maken, maar niet worden uitgevoerd.

    Zodra het Hallo-opdracht is voltooid, moet het Hallo-ID van Hallo taak retourneren. Bijvoorbeeld `0000005-150622124850154-oozie-oozi-W`. Deze ID is gebruikte toomanage Hallo taak.

4. Hallo-status van Hallo-taak met behulp van de volgende opdracht Hallo weergeven:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Vervang `<JOBID>` Hello ID in de vorige stap Hallo die wordt geretourneerd.

    Hiermee wordt informatie vergelijkbare toohello volgende tekst:

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    Deze taak heeft status `PREP`. Deze status geeft aan dat Hallo-taak is gemaakt, maar is niet gestart.

5. Hallo opdracht toostart Hallo taak volgende gebruiken:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Vervang `<JOBID>` Hello ID eerder geretourneerd.

    Als u Hallo status na deze opdracht controleren, actief is en gegevens worden geretourneerd voor Hallo-acties in Hallo-taak.

6. Zodra het Hallo-taak is voltooid, kunt u controleren dat Hallo gegevens is gegenereerd en geëxporteerd, toohello SQL Database-tabel met behulp van de volgende opdrachten Hallo:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    Op Hallo `1>` gevraagd, voert u Hallo query te volgen:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    Hallo-informatie die wordt geretourneerd is vergelijkbaar toohello volgende tekst:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Zie voor meer informatie over Hallo Oozie opdracht [Oozie-opdrachtregelprogramma](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>Oozie REST-API

Hallo Oozie REST-API kunt u toobuild uw eigen hulpprogramma's die met Oozie werken. Hallo volgen HDInsight specifieke informatie over het gebruik van Hallo Oozie REST-API:

* **URI**: Hallo REST-API toegankelijk is vanaf externe Hallo-cluster op`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Verificatie**: toohello API met Hallo cluster HTTP-account (admin) en het wachtwoord verifiëren. Bijvoorbeeld:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Zie voor meer informatie over het gebruik van Hallo Oozie REST-API [Oozie-webservices-API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Oozie-webgebruikersinterface

Hallo Oozie-Webgebruikersinterface biedt een webweergave in Hallo status van de Oozie taken op Hallo cluster. Hallo-webgebruikersinterface kunt u tooview Hallo volgende informatie:

* De status van taak
* Taakdefinitie
* Configuratie
* Een grafiek van Hallo-acties in Hallo-taak
* Logboeken voor de taak Hallo

U kunt ook details voor acties in een taak weergeven.

tooaccess hello Oozie-Webgebruikersinterface, gebruikt u Hallo stappen te volgen:

1. Maak een SSH-tunnel toohello HDInsight-cluster. Zie voor informatie Hallo [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

2. Zodra een tunnel is gemaakt, opent u Hallo Ambari-webgebruikersinterface in uw webbrowser. Hallo URI voor Hallo Ambari site is **https://CLUSTERNAME.azurehdinsight.net**. Vervang **CLUSTERNAME** met Hallo-naam van uw Linux gebaseerde HDInsight-cluster.

3. Selecteer in de Hallo linkerkant van de pagina hello, **Oozie**, vervolgens **snelkoppelingen**, en tot slot **Oozie-Webgebruikersinterface**.

    ![afbeelding van menu's Hallo](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Hallo Oozie-Webgebruikersinterface standaardwaarden toodisplaying werkstroomtaken uitgevoerd. alle werkstroomtaken, selecteert u toosee **alle taken**.

    ![Alle taken die worden weergegeven](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Selecteer een taak tooview meer informatie over het Hallo-taak.

    ![Taakinformatie](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. Hallo taakinformatie tabblad ziet u informatie over basic taak en Hallo afzonderlijke acties in Hallo job. Hallo tabbladen boven Hallo die kunt u weergeven met taakdefinitie, configuratie van de taak, toegang Hallo taaklogboek hello of een omgeleid acyclische grafiek (DAG) van Hallo-taak weergeven.

   * **Taaklogboek**: Selecteer Hallo **GetLogs** tooget alle logboeken voor de Hallo taak, of gebruikt u Hallo **zoekfilter Voer** veld toofilter Logboeken

       ![Logboekbestand van taak](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: Hallo DAG is een grafisch overzicht van de gegevenspaden Hallo doorlopen Hallo-werkstroom

       ![Taak DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Een van de acties Hallo selecteren in Hallo **taakinformatie** tabblad opstart, wordt informatie voor Hallo actie. Selecteer bijvoorbeeld Hallo **RunHiveScript** in te grijpen.

    ![Actie-info](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Ziet u details voor Hallo actie, zoals een koppeling toohello **Console URL**. Deze koppeling kan worden gebruikt tooview JobTracker informatie voor Hallo-taak.

## <a name="scheduling-jobs"></a>Plannen van taken

Hallo-coördinator kunt u toospecify een begin en einde exemplaar frequentie voor taken. toodefine een planning voor Hallo werkstroom, gebruik Hallo stappen te volgen:

1. Gebruik Hallo na een bestand met de naam toocreate **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Gebruik Hallo XML als Hallo inhoud van Hallo-bestand te volgen:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > Hallo `${...}` variabelen zijn vervangen door waarden in de taakdefinitie Hallo tijdens runtime. Hallo-variabelen zijn:
    >
    > * `${coordFrequency}`: Tijd tussen sessies van Hallo taak uitvoeren.
    > ** `${coordStart}`: de begintijd van taak Hallo.
    > * `${coordEnd}`: eindtijd Hallo-taak.
    > * `${coordTimezone}`: Coordinator taken zijn in een vaste tijdzone geen zomertijd (doorgaans weergegeven met behulp UTC). Deze tijdzone wordt verwezen als Hallo 'Oozie verwerking tijdzone."
    > * `${wfPath}`: Hallo pad toohello workflow.xml.

2. Hallo toosave gebruikt u Ctrl X **Y**, en **Enter**.

3. Gebruik Hallo opdracht toocopy Hallo bestand toohello werkmap voor deze taak te volgen:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Gebruik Hallo na toomodify hello **job.xml** bestand:

    ```
    nano job.xml
    ```

    Hallo volgende wijzigingen aanbrengen:

   * tooinstruct oozie toorun Hallo coordinator bestand in plaats van Hallo werkstroom wijzigen `<name>oozie.wf.application.path</name>` te`<name>oozie.coord.application.path</name>`.

   * tooset hello `workflowPath` variabele die wordt gebruikt door Hallo-coördinator toevoegen Hallo XML te volgen:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Vervang Hallo `wasb://mycontainer@mystorageaccount.blob.core.windows` tekst met Hallo-waarde in de andere vermeldingen in Hallo job.xml bestand gebruikt.

   * toodefine hello start, einde en frequentie voor het Hallo-coördinator toevoegen Hallo XML te volgen:

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       Deze waarden ingesteld Hallo start tijd too12: 00 PM op 10 mei 2017 Hallo end tijd tooMay 12, 2017. Hallo-interval voor het uitvoeren van deze taak dagelijks. Hallo frequentie in minuten, wordt dus 24 uur x 60 minuten = 1440 minuten. Ten slotte Hallo tijdzone tooUTC ingesteld.

5. Gebruik Ctrl X vervolgens **Y** en **Enter** toosave Hallo-bestand.

6. toorun hello taak gebruik Hallo volgende opdracht:

    ```
    oozie job -config job.xml -run
    ```

    Deze opdracht worden verzonden en Hallo taak start.

7. Als u Hallo Oozie-Webgebruikersinterface bezoeken en selecteer Hallo **coördinator taken** tabblad ziet u informatie vergelijkbare toohello installatiekopie te volgen:

    ![tabblad Coordinator-taken](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Hallo **volgende Materialisatie** invoer bevat Hallo volgende keer dat Hallo taak wordt uitgevoerd.

8. Vergelijkbare toohello eerdere werkstroomtaak Hallo taak vermelding selecteren in Hallo webgebruikersinterface geeft informatie weer op Hallo taak:

    ![De taakinformatie Coordinator](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Deze afbeelding ziet u alleen geslaagde wordt uitgevoerd van Hallo-taak niet afzonderlijke acties in de werkstroom Hallo gepland. toosee die, selecteer een van de Hallo **actie** vermeldingen.

    ![Actie-info](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Problemen oplossen

Hallo Oozie UI kunt u tooview Oozie-Logboeken. Het bevat ook koppelingen tooJobTracker logboeken voor MapReduce-taken die zijn gestart door Hallo werkstroom. Hallo-patroon voor het oplossen van moet zijn:

1. Hallo-taak weergeven in Oozie-Webgebruikersinterface.

2. Als er een fout of een fout voor een specifieke actie, selecteer de actie toosee Hallo als hello **foutbericht** veld bevat meer informatie over het Hallo-fout.

3. Indien beschikbaar, Hallo URL gebruiken van Hallo actie tooview meer informatie (zoals JobTracker Logboeken) voor Hallo actie.

Hallo hieronder vindt u specifieke fouten optreden kunnen, en hoe tooresolve ze.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: Cluster kan niet worden geïnitialiseerd

**Symptomen**: verandert de status van taak te Hallo**onderbroken**. Details voor de taak Hallo Hallo RunHiveScript status als weergeven **START_MANUAL**. Hallo actie selecteren weergegeven Hallo volgende foutbericht weergegeven:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Oorzaak**: WASB-adressen die worden gebruikt in Hallo Hallo **job.xml** bestand bevatten geen Hallo storage-container of de naam van het opslagaccount. Hallo WASB adresindeling moet `wasb://containername@storageaccountname.blob.core.windows.net`.

**Resolutie**: Hallo WASB adressen die worden gebruikt door Hallo taak wijzigen.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie is niet toegestaan voor tooimpersonate &lt;gebruiker >

**Symptomen**: verandert de status van taak te Hallo**onderbroken**. Details voor de taak Hallo Hallo RunHiveScript status als weergeven **START_MANUAL**. Hallo actie selecteren toont Hallo volgende foutbericht weergegeven:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Oorzaak**: huidige machtigingsinstellingen staan geen Oozie tooimpersonate Hallo opgegeven gebruikersaccount.

**Resolutie**: Oozie tooimpersonate gebruikers is toegestaan in Hallo **gebruikers** groep. Gebruik Hallo `groups USERNAME` toosee Hallo groepen die Hallo gebruikersaccount lid van is. Als het Hallo-gebruiker is geen lid is van Hallo **gebruikers** groep, gebruikt u Hallo opdracht tooadd Hallo-gebruikersgroep toohello te volgen:

    sudo adduser USERNAME users

> [!NOTE]
> Het kan enkele minuten duren voordat HDInsight herkent dat die gebruiker Hallo toohello groep is toegevoegd.

### <a name="launcher-error-sqoop"></a>FOUT (Sqoop) starten

**Symptomen**: verandert de status van taak te Hallo**KILLED**. Details voor de taak Hallo Hallo RunSqoopExport status als weergeven **fout**. Hallo actie selecteren toont Hallo volgende foutbericht weergegeven:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Oorzaak**: Sqoop is kan niet tooload Hallo database stuurprogramma vereist tooaccess Hallo-database.

**Resolutie**: wanneer u Sqoop uit een taak Oozie, moet u opnemen Hallo databasestuurprogramma Hello andere bronnen (zoals Hallo workflow.xml) gebruikt door Hallo-taak. Ook verwijzen naar Hallo-archief met databasestuurprogramma Hallo van Hallo `<sqoop>...</sqoop>` sectie van Hallo workflow.xml.

Voor de taak Hallo in dit document gebruikt u bijvoorbeeld Hallo stappen te volgen:

1. Kopieer Hallo sqljdbc4.1.jar toohello /tutorials/useoozie map:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Hallo workflow.xml tooadd Hallo XML volgen op een nieuwe regel bovenstaande wijzigen `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe toodefine een Oozie-werkstroom en hoe toorun een Oozie-taak. toolearn meer informatie over het werken met HDInsight, Zie Hallo artikelen te volgen:

* [Tijd gebaseerde Oozie-coördinator gebruiken met HDInsight][hdinsight-oozie-coordinator-time]
* [Uploaden van gegevens voor Hadoop-taken in HDInsight][hdinsight-upload-data]
* [Sqoop gebruiken met Hadoop in HDInsight][hdinsight-use-sqoop]
* [Hive gebruiken met Hadoop in HDInsight][hdinsight-use-hive]
* [Pig gebruiken met Hadoop in HDInsight][hdinsight-use-pig]
* [Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
