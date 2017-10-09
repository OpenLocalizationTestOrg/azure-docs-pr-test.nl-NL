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
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="d2172-104">Apache Sqoop tooimport gebruiken en exporteren van gegevens tussen Hadoop in HDInsight en SQL-Database</span><span class="sxs-lookup"><span data-stu-id="d2172-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="d2172-105">Meer informatie over hoe toouse Apache Sqoop tooimport en exporteren tussen een Hadoop-cluster in Azure HDInsight en Azure SQL Database of Microsoft SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="d2172-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="d2172-106">Hallo stappen in dit document gebruik Hallo `sqoop` opdracht rechtstreeks vanuit Hallo headnode van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2172-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="d2172-107">U gebruikt SSH tooconnect toohello hoofdknooppunt en Hallo opdrachten uitvoert in dit document.</span><span class="sxs-lookup"><span data-stu-id="d2172-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2172-108">Hallo werken stappen in dit document alleen met HDInsight-clusters die gebruikmaken van Linux.</span><span class="sxs-lookup"><span data-stu-id="d2172-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="d2172-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d2172-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d2172-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d2172-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="d2172-111">FreeTDS installeren</span><span class="sxs-lookup"><span data-stu-id="d2172-111">Install FreeTDS</span></span>

1. <span data-ttu-id="d2172-112">SSH tooconnect toohello HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2172-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="d2172-113">Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met primaire headnode toohello van een cluster met de naam `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="d2172-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d2172-114">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d2172-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d2172-115">Hallo opdracht tooinstall FreeTDS volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d2172-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="d2172-116">FreeTDS wordt gebruikt in verschillende stappen tooconnect tooSQL Database.</span><span class="sxs-lookup"><span data-stu-id="d2172-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="d2172-117">Hallo-tabel in SQL-Database maken</span><span class="sxs-lookup"><span data-stu-id="d2172-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2172-118">Als u van Hallo HDInsight-cluster gebruikmaakt en SQL-Database gemaakt [cluster en SQL-database maken](hdinsight-use-sqoop.md), Hallo stappen in deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="d2172-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="d2172-119">Hallo database en tabel zijn gemaakt als onderdeel van Hallo stappen voor het Hallo [cluster en SQL-database maken](hdinsight-use-sqoop.md) document.</span><span class="sxs-lookup"><span data-stu-id="d2172-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="d2172-120">Gebruik vanaf Hallo SSH-sessie, Hallo opdracht tooconnect toohello SQL Database-server te volgen.</span><span class="sxs-lookup"><span data-stu-id="d2172-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="d2172-121">U ontvangt uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d2172-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="d2172-122">Op Hallo `1>` gevraagd, voert u Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2172-122">At hello `1>` prompt, enter hello following query:</span></span>

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

    <span data-ttu-id="d2172-123">Wanneer Hallo `GO` instructie wordt ingevoerd, Hallo vorige instructies worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="d2172-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="d2172-124">Eerst Hallo **mobiledata** tabel is gemaakt en vervolgens een geclusterde index wordt toegevoegd tooit (vereist door de SQL-Database.)</span><span class="sxs-lookup"><span data-stu-id="d2172-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="d2172-125">Gebruik Hallo na tooverify query die tabel Hallo is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="d2172-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="d2172-126">Ziet u uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d2172-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="d2172-127">Voer `exit` op Hallo `1>` vragen tooexit Hallo tsql-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="d2172-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="d2172-128">Sqoop exporteren</span><span class="sxs-lookup"><span data-stu-id="d2172-128">Sqoop export</span></span>

1. <span data-ttu-id="d2172-129">Gebruik van Hallo SSH-verbinding toohello cluster Hallo opdracht tooverify Sqoop ziet uw SQL-Database te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2172-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="d2172-130">Voer desgevraagd Hallo wachtwoord voor Hallo SQL Database-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d2172-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="d2172-131">Met deze opdracht retourneert een lijst met databases, met inbegrip van Hallo **sqooptest** database die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d2172-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="d2172-132">gegevens van tooexport **hivesampletable** toohello **mobiledata** tabel, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d2172-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="d2172-133">Deze opdracht verwijdert Sqoop tooconnect toohello **sqooptest** database.</span><span class="sxs-lookup"><span data-stu-id="d2172-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="d2172-134">Daarna exporteert gegevens uit Sqoop **wasb: / / / hive/datawarehouse/hivesampletable** toohello **mobiledata** tabel.</span><span class="sxs-lookup"><span data-stu-id="d2172-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d2172-135">Gebruik `wasb:///` als Hallo standaard opslagruimte voor uw cluster een Azure Storage-account is.</span><span class="sxs-lookup"><span data-stu-id="d2172-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="d2172-136">Gebruik `adl:///` als het een Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d2172-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="d2172-137">Nadat het Hallo-opdracht is voltooid, gebruikt u Hallo opdracht tooconnect toohello database met TSQL te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2172-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="d2172-138">Eenmaal zijn verbonden, gebruik Hallo na instructies tooverify die gegevens Hallo geëxporteerde toohello is **mobiledata** tabel:</span><span class="sxs-lookup"><span data-stu-id="d2172-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="d2172-139">U ziet een lijst met gegevens in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2172-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="d2172-140">Type `exit` tooexit Hallo tsql-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="d2172-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="d2172-141">Sqoop importeren</span><span class="sxs-lookup"><span data-stu-id="d2172-141">Sqoop import</span></span>

1. <span data-ttu-id="d2172-142">Gebruik Hallo volgende opdracht tooimport gegevens van Hallo **mobiledata** tabel in SQL-Database, toohello **wasb: / / / zelfstudies/usesqoop/importeddata** directory op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d2172-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="d2172-143">Hallo-velden in Hallo gegevens worden gescheiden door een tab-teken en Hallo regels worden beëindigd door een nieuwe-regelteken.</span><span class="sxs-lookup"><span data-stu-id="d2172-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="d2172-144">Zodra Hallo importeren is voltooid, gebruikt u Hallo opdracht toolist Hallo-gegevens in de nieuwe map hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2172-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="d2172-145">Met behulp van SQL Server</span><span class="sxs-lookup"><span data-stu-id="d2172-145">Using SQL Server</span></span>

<span data-ttu-id="d2172-146">U kunt ook tooimport Sqoop gebruiken en gegevens exporteren uit SQL Server in uw datacenter of op een virtuele Machine gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="d2172-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="d2172-147">Hallo verschillen tussen het gebruik van SQL-Database en SQL Server zijn:</span><span class="sxs-lookup"><span data-stu-id="d2172-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="d2172-148">Zowel HDInsight en SQL Server moet worden op Hallo hetzelfde virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="d2172-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="d2172-149">Zie voor een voorbeeld Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](./connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="d2172-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="d2172-150">Zie voor meer informatie over het gebruik van HDInsight met een Azure Virtual Network Hallo [HDInsight uitbreiden met Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="d2172-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="d2172-151">Zie voor meer informatie over Azure Virtual Network Hallo [Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md) document.</span><span class="sxs-lookup"><span data-stu-id="d2172-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="d2172-152">SQL Server moet geconfigureerde tooallow SQL-verificatie.</span><span class="sxs-lookup"><span data-stu-id="d2172-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="d2172-153">Zie voor meer informatie, Hallo [een verificatiemodus kiezen](https://msdn.microsoft.com/ms144284.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="d2172-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="d2172-154">Mogelijk hebt u tooconfigure SQL Server tooaccept externe verbindingen.</span><span class="sxs-lookup"><span data-stu-id="d2172-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="d2172-155">Zie voor meer informatie, Hallo [hoe tootroubleshoot verbindende toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="d2172-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="d2172-156">Hallo maken **sqooptest** database in SQL-Server met een hulpprogramma zoals **SQL Server Management Studio** of **tsql**.</span><span class="sxs-lookup"><span data-stu-id="d2172-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="d2172-157">Hallo-stappen voor het gebruik van hello Azure CLI werkt alleen voor Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d2172-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="d2172-158">Gebruik Hallo volgende Transact-SQL-instructies toocreate hello **mobiledata** tabel:</span><span class="sxs-lookup"><span data-stu-id="d2172-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

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

* <span data-ttu-id="d2172-159">Wanneer u verbinding maakt toohello SQL Server uit HDInsight, mogelijk hebt u toouse Hallo IP-adres van Hallo SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d2172-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="d2172-160">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d2172-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="d2172-161">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="d2172-161">Limitations</span></span>

* <span data-ttu-id="d2172-162">Bulk-export - met Linux gebaseerde HDInsight, Hallo Sqoop connector die wordt gebruikt tooexport gegevens tooMicrosoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.</span><span class="sxs-lookup"><span data-stu-id="d2172-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="d2172-163">Batchverwerking - met HDInsight op basis van Linux bij gebruik van Hallo `-batch` bij het uitvoeren van invoeg-switch, Sqoop maakt meerdere invoegen in plaats van batchverwerking Hallo insert-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d2172-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2172-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d2172-164">Next steps</span></span>

<span data-ttu-id="d2172-165">Nu u hebt geleerd hoe toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="d2172-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="d2172-166">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="d2172-166">toolearn more, see:</span></span>

* <span data-ttu-id="d2172-167">[Oozie gebruiken met HDInsight][hdinsight-use-oozie]: Sqoop gebruiken in een werkstroom Oozie in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="d2172-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="d2172-168">[Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-data]: tooanalyze vlucht Hive gebruiken gegevens uit te stellen en vervolgens Sqoop tooexport tooan Azure SQL database te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2172-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="d2172-169">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]: vinden van andere methoden voor het uploaden van gegevens tooHDInsight/Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d2172-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

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
