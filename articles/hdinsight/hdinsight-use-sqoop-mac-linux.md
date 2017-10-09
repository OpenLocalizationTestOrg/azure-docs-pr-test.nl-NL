---
title: aaaApache Sqoop met Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Sqoop tooimport en exporteren tussen Hadoop in HDInsight en een Azure SQL Database.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop, sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Apache Sqoop tooimport gebruiken en exporteren van gegevens tussen Hadoop in HDInsight en SQL-Database

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Meer informatie over hoe toouse Apache Sqoop tooimport en exporteren tussen een Hadoop-cluster in Azure HDInsight en Azure SQL Database of Microsoft SQL Server-database. Hallo stappen in dit document gebruik Hallo `sqoop` opdracht rechtstreeks vanuit Hallo headnode van Hallo Hadoop-cluster. U gebruikt SSH tooconnect toohello hoofdknooppunt en Hallo opdrachten uitvoert in dit document.

> [!IMPORTANT]
> Hallo werken stappen in dit document alleen met HDInsight-clusters die gebruikmaken van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="install-freetds"></a>FreeTDS installeren

1. SSH tooconnect toohello HDInsight-cluster gebruiken. Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met primaire headnode toohello van een cluster met de naam `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Hallo opdracht tooinstall FreeTDS volgende gebruiken:

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    FreeTDS wordt gebruikt in verschillende stappen tooconnect tooSQL Database.

## <a name="create-hello-table-in-sql-database"></a>Hallo-tabel in SQL-Database maken

> [!IMPORTANT]
> Als u van Hallo HDInsight-cluster gebruikmaakt en SQL-Database gemaakt [cluster en SQL-database maken](hdinsight-use-sqoop.md), Hallo stappen in deze sectie overslaan. Hallo database en tabel zijn gemaakt als onderdeel van Hallo stappen voor het Hallo [cluster en SQL-database maken](hdinsight-use-sqoop.md) document.

1. Gebruik vanaf Hallo SSH-sessie, Hallo opdracht tooconnect toohello SQL Database-server te volgen.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    U ontvangt uitvoer vergelijkbare toohello volgende tekst:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. Op Hallo `1>` gevraagd, voert u Hallo query te volgen:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    Wanneer Hallo `GO` instructie wordt ingevoerd, Hallo vorige instructies worden geëvalueerd. Eerst Hallo **mobiledata** tabel is gemaakt en vervolgens een geclusterde index wordt toegevoegd tooit (vereist door de SQL-Database.)

    Gebruik Hallo na tooverify query die tabel Hallo is gemaakt:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Ziet u uitvoer vergelijkbare toohello volgende tekst:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Voer `exit` op Hallo `1>` vragen tooexit Hallo tsql-hulpprogramma.

## <a name="sqoop-export"></a>Sqoop exporteren

1. Gebruik van Hallo SSH-verbinding toohello cluster Hallo opdracht tooverify Sqoop ziet uw SQL-Database te volgen:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    Voer desgevraagd Hallo wachtwoord voor Hallo SQL Database-aanmelding.

    Met deze opdracht retourneert een lijst met databases, met inbegrip van Hallo **sqooptest** database die u eerder hebt gemaakt.

2. gegevens van tooexport **hivesampletable** toohello **mobiledata** tabel, gebruikt u Hallo volgende opdracht:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    Deze opdracht verwijdert Sqoop tooconnect toohello **sqooptest** database. Daarna exporteert gegevens uit Sqoop **wasb: / / / hive/datawarehouse/hivesampletable** toohello **mobiledata** tabel.

    > [!IMPORTANT]
    > Gebruik `wasb:///` als Hallo standaard opslagruimte voor uw cluster een Azure Storage-account is. Gebruik `adl:///` als het een Azure Data Lake Store.

3. Nadat het Hallo-opdracht is voltooid, gebruikt u Hallo opdracht tooconnect toohello database met TSQL te volgen:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    Eenmaal zijn verbonden, gebruik Hallo na instructies tooverify die gegevens Hallo geëxporteerde toohello is **mobiledata** tabel:

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    U ziet een lijst met gegevens in de tabel Hallo. Type `exit` tooexit Hallo tsql-hulpprogramma.

## <a name="sqoop-import"></a>Sqoop importeren

1. Gebruik Hallo volgende opdracht tooimport gegevens van Hallo **mobiledata** tabel in SQL-Database, toohello **wasb: / / / zelfstudies/usesqoop/importeddata** directory op HDInsight:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    Hallo-velden in Hallo gegevens worden gescheiden door een tab-teken en Hallo regels worden beëindigd door een nieuwe-regelteken.

2. Zodra Hallo importeren is voltooid, gebruikt u Hallo opdracht toolist Hallo-gegevens in de nieuwe map hello te volgen:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>Met behulp van SQL Server

U kunt ook tooimport Sqoop gebruiken en gegevens exporteren uit SQL Server in uw datacenter of op een virtuele Machine gehost in Azure. Hallo verschillen tussen het gebruik van SQL-Database en SQL Server zijn:

* Zowel HDInsight en SQL Server moet worden op Hallo hetzelfde virtuele Azure-netwerk.

    Zie voor een voorbeeld Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](./connect-on-premises-network.md) document.

    Zie voor meer informatie over het gebruik van HDInsight met een Azure Virtual Network Hallo [HDInsight uitbreiden met Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document. Zie voor meer informatie over Azure Virtual Network Hallo [Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md) document.

* SQL Server moet geconfigureerde tooallow SQL-verificatie. Zie voor meer informatie, Hallo [een verificatiemodus kiezen](https://msdn.microsoft.com/ms144284.aspx) document.

* Mogelijk hebt u tooconfigure SQL Server tooaccept externe verbindingen. Zie voor meer informatie, Hallo [hoe tootroubleshoot verbindende toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.

* Hallo maken **sqooptest** database in SQL-Server met een hulpprogramma zoals **SQL Server Management Studio** of **tsql**. Hallo-stappen voor het gebruik van hello Azure CLI werkt alleen voor Azure SQL Database.

    Gebruik Hallo volgende Transact-SQL-instructies toocreate hello **mobiledata** tabel:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* Wanneer u verbinding maakt toohello SQL Server uit HDInsight, mogelijk hebt u toouse Hallo IP-adres van Hallo SQL Server. Bijvoorbeeld:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Beperkingen

* Bulk-export - met Linux gebaseerde HDInsight, Hallo Sqoop connector die wordt gebruikt tooexport gegevens tooMicrosoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.

* Batchverwerking - met HDInsight op basis van Linux bij gebruik van Hallo `-batch` bij het uitvoeren van invoeg-switch, Sqoop maakt meerdere invoegen in plaats van batchverwerking Hallo insert-bewerkingen.

## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe toouse Sqoop. toolearn meer, Zie:

* [Oozie gebruiken met HDInsight][hdinsight-use-oozie]: Sqoop gebruiken in een werkstroom Oozie in te grijpen.
* [Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-data]: tooanalyze vlucht Hive gebruiken gegevens uit te stellen en vervolgens Sqoop tooexport tooan Azure SQL database te gebruiken.
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]: vinden van andere methoden voor het uploaden van gegevens tooHDInsight/Azure Blob-opslag.

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
