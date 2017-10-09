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
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="705a4-104">Oozie gebruiken met Hadoop toodefine en uitvoeren van een werkstroom op Linux gebaseerde HDInsight</span><span class="sxs-lookup"><span data-stu-id="705a4-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="705a4-105">Meer informatie over hoe toouse Apache Oozie met Hadoop op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="705a4-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="705a4-106">Apache Oozie is een werkstroom/coördinatie systeem waarmee Hadoop-taken worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="705a4-107">Oozie is geïntegreerd met Hadoop-stack Hallo en ondersteunt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="705a4-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="705a4-108">Apache MapReduce</span></span>
* <span data-ttu-id="705a4-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="705a4-109">Apache Pig</span></span>
* <span data-ttu-id="705a4-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="705a4-110">Apache Hive</span></span>
* <span data-ttu-id="705a4-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="705a4-111">Apache Sqoop</span></span>

<span data-ttu-id="705a4-112">Oozie kan ook worden gebruikt tooschedule taken die specifieke tooa systeem, zoals Java-programma's of shell-scripts zijn</span><span class="sxs-lookup"><span data-stu-id="705a4-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="705a4-113">Een andere optie voor het definiëren van werkstromen met HDInsight is Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="705a4-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="705a4-114">Zie toolearn meer informatie over Azure Data Factory [Use Pig en Hive met Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="705a4-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="705a4-115">Oozie is niet ingeschakeld op HDInsight domein.</span><span class="sxs-lookup"><span data-stu-id="705a4-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="705a4-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="705a4-116">Prerequisites</span></span>

* <span data-ttu-id="705a4-117">**Een HDInsight-cluster**: Zie [aan de slag met HDInsight op Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="705a4-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="705a4-118">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="705a4-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="705a4-119">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="705a4-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="705a4-120">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="705a4-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="705a4-121">Van de voorbeeldwerkstroom</span><span class="sxs-lookup"><span data-stu-id="705a4-121">Example workflow</span></span>

<span data-ttu-id="705a4-122">Hallo-werkstroom gebruikt in dit document bevat twee acties.</span><span class="sxs-lookup"><span data-stu-id="705a4-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="705a4-123">Acties zijn definities voor taken zoals het uitvoeren van Hive, Sqoop, MapReduce of ander proces:</span><span class="sxs-lookup"><span data-stu-id="705a4-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Werkstroomdiagram][img-workflow-diagram]

1. <span data-ttu-id="705a4-125">Een Hive-actie wordt uitgevoerd een HiveQL-script tooextract records uit Hallo **hivesampletable** opgenomen met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="705a4-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="705a4-126">Elke rij gegevens beschrijft een bezoek van een specifieke mobiele apparaat.</span><span class="sxs-lookup"><span data-stu-id="705a4-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="705a4-127">Hallo recordindeling weergegeven vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="705a4-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="705a4-128">Hallo Hive-script in dit document gebruikt telt Hallo totaal aantal bezoeken voor elk platform (zoals Android of iPhone) en slaat Hallo aantallen tooa nieuwe Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="705a4-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="705a4-129">Zie [Hive gebruiken met HDInsight][hdinsight-use-hive] voor meer informatie over Hive.</span><span class="sxs-lookup"><span data-stu-id="705a4-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="705a4-130">Een actie Sqoop exporteert Hallo inhoud van Hallo nieuwe Hive tooa tabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="705a4-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="705a4-131">Zie voor meer informatie over Sqoop [Hadoop-Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="705a4-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="705a4-132">Zie voor ondersteunde versies van de Oozie op HDInsight-clusters, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="705a4-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="705a4-133">Hallo-werkmap maken</span><span class="sxs-lookup"><span data-stu-id="705a4-133">Create hello working directory</span></span>

<span data-ttu-id="705a4-134">Oozie verwacht resources die vereist zijn voor een taak toobe die wordt opgeslagen in Hallo dezelfde directory.</span><span class="sxs-lookup"><span data-stu-id="705a4-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="705a4-135">In dit voorbeeld wordt **wasb: / / / zelfstudies/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="705a4-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="705a4-136">Gebruik Hallo opdracht toocreate na deze map en het Hallo-gegevensmap waarin Hallo nieuwe Hive-tabel is gemaakt door deze werkstroom:</span><span class="sxs-lookup"><span data-stu-id="705a4-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="705a4-137">Hallo `-p` parameter zorgt ervoor dat alle mappen in Hallo pad toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="705a4-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="705a4-138">Hallo **gegevens** map is gebruikte toohold gegevens die worden gebruikt door Hallo **useooziewf.hql** script.</span><span class="sxs-lookup"><span data-stu-id="705a4-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="705a4-139">Hallo na de opdracht die zorgt ervoor dat Oozie uw gebruikersaccount imiteren kan bij het uitvoeren van Hive en Sqoop taken ook uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="705a4-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="705a4-140">Vervang **gebruikersnaam** met de aanmeldingsnaam van uw:</span><span class="sxs-lookup"><span data-stu-id="705a4-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="705a4-141">U kunt fouten negeren die Hallo-gebruiker is al een lid van Hallo `users` groep.</span><span class="sxs-lookup"><span data-stu-id="705a4-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="705a4-142">Toevoegen van een databasestuurprogramma</span><span class="sxs-lookup"><span data-stu-id="705a4-142">Add a database driver</span></span>

<span data-ttu-id="705a4-143">Omdat deze werkstroom Sqoop tooexport gegevens tooSQL Database gebruikt, kunt u een kopie van Hallo JDBC-stuurprogramma gebruikt tootalk tooSQL Database moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="705a4-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="705a4-144">Gebruik Hallo na de opdracht toocopy deze werkmap toohello:</span><span class="sxs-lookup"><span data-stu-id="705a4-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="705a4-145">Als uw werkstroom andere resources, zoals een jar met een MapReduce-toepassingen gebruikt, moet u tooadd ook deze resources.</span><span class="sxs-lookup"><span data-stu-id="705a4-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="705a4-146">Hallo Hive-query definiëren</span><span class="sxs-lookup"><span data-stu-id="705a4-146">Define hello Hive query</span></span>

<span data-ttu-id="705a4-147">Gebruik Hallo stappen toocreate een HiveQL-script dat definieert u een query die wordt gebruikt in een werkstroom Oozie verderop in dit document te volgen.</span><span class="sxs-lookup"><span data-stu-id="705a4-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="705a4-148">Toohello-cluster via SSH verbinding.</span><span class="sxs-lookup"><span data-stu-id="705a4-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="705a4-149">Hallo volgende opdracht is een voorbeeld van het gebruik van Hallo `ssh` opdracht.</span><span class="sxs-lookup"><span data-stu-id="705a4-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="705a4-150">Vervang __gebruikersnaam__ met Hallo SSH-gebruiker voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="705a4-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="705a4-151">Vervang __CLUSTERNAME__ met de naam van de HDInsight-cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="705a4-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="705a4-152">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="705a4-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="705a4-153">Gebruik van Hallo SSH-verbinding, Hallo opdracht toocreate een bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="705a4-154">Zodra het Hallo nano-editor wordt geopend, gebruikt u Hallo query als Hallo inhoud van Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="705a4-155">Er zijn twee variabelen in Hallo script gebruikt:</span><span class="sxs-lookup"><span data-stu-id="705a4-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="705a4-156">**${hiveTableName}**: Hallo naam bevat van Hallo tabel toobe gemaakt</span><span class="sxs-lookup"><span data-stu-id="705a4-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="705a4-157">**${hiveDataFolder}**: Hallo locatie toostore Hallo-gegevensbestanden voor de tabel Hallo bevat</span><span class="sxs-lookup"><span data-stu-id="705a4-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="705a4-158">Hallo werkstroom-definitiebestand (workflow.xml in deze zelfstudie) geeft deze waarden toothis HiveQL-script tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="705a4-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="705a4-159">tooexit Hallo-editor, druk op Ctrl X.</span><span class="sxs-lookup"><span data-stu-id="705a4-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="705a4-160">Wanneer u wordt gevraagd, selecteert u **Y** toosave bestand Hallo en gebruik vervolgens **Enter** toouse hello **useooziewf.hql** bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="705a4-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="705a4-161">Gebruik Hallo deze opdrachten toocopy **useooziewf.hql** te**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="705a4-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="705a4-162">Deze opdrachten opslaan Hallo **useooziewf.hql** -bestand op Hallo HDFS-compatibele opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="705a4-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="705a4-163">Hallo werkstroom definiëren</span><span class="sxs-lookup"><span data-stu-id="705a4-163">Define hello workflow</span></span>

<span data-ttu-id="705a4-164">Oozie werkstromen definities worden geschreven in hPDL (een XML-proces Definition Language).</span><span class="sxs-lookup"><span data-stu-id="705a4-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="705a4-165">Gebruik Hallo stappen toodefine Hallo workflow volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="705a4-166">Na de instructie toocreate hello gebruiken en bewerken van een nieuw bestand:</span><span class="sxs-lookup"><span data-stu-id="705a4-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="705a4-167">Zodra Hallo nano-editor wordt geopend, Voer Hallo XML als Hallo bestandsinhoud te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

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

    <span data-ttu-id="705a4-168">Er zijn twee acties in de werkstroom Hallo gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="705a4-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="705a4-169">**RunHiveScript**: met deze actie Hallo startactie en wordt uitgevoerd Hallo **useooziewf.hql** Hive-script</span><span class="sxs-lookup"><span data-stu-id="705a4-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="705a4-170">**RunSqoopExport**: deze actie exporteert Hallo gegevens gemaakt op basis van Hallo Hive-script tooSQL Sqoop-Database.</span><span class="sxs-lookup"><span data-stu-id="705a4-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="705a4-171">Deze actie wordt alleen uitgevoerd als hello **RunHiveScript** actie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="705a4-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="705a4-172">Hallo werkstroom heeft enkele items zoals `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="705a4-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="705a4-173">Deze vermeldingen worden vervangen door waarden die u in de taakdefinitie hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="705a4-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="705a4-174">Hallo taakdefinitie wordt verderop in dit document gemaakt.</span><span class="sxs-lookup"><span data-stu-id="705a4-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="705a4-175">Ook Opmerking Hallo `<archive>sqljdbc4.jar</arcive>` vermelding in Hallo Sqoop-sectie.</span><span class="sxs-lookup"><span data-stu-id="705a4-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="705a4-176">Deze vermelding geeft opdracht Oozie toomake dit archief die beschikbaar zijn voor Sqoop wanneer deze actie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="705a4-177">Gebruik Ctrl X vervolgens **Y** en **Enter** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="705a4-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="705a4-178">Gebruik Hallo volgende opdracht toocopy hello **workflow.xml** bestand te**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="705a4-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="705a4-179">Hallo-database maken</span><span class="sxs-lookup"><span data-stu-id="705a4-179">Create hello database</span></span>

<span data-ttu-id="705a4-180">een Azure SQL Database toocreate Hallo stappen in Hallo [maken van een SQL-Database](../sql-database/sql-database-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="705a4-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="705a4-181">Gebruik bij het maken van database Hallo `oozietest` als Hallo databasenaam.</span><span class="sxs-lookup"><span data-stu-id="705a4-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="705a4-182">Maak ook een notitie van Hallo-naam van de databaseserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="705a4-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="705a4-183">Hallo-tabel maken</span><span class="sxs-lookup"><span data-stu-id="705a4-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="705a4-184">Er zijn veel manieren tooconnect tooSQL Database toocreate een tabel.</span><span class="sxs-lookup"><span data-stu-id="705a4-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="705a4-185">Hallo na gebruik van de stappen [FreeTDS](http://www.freetds.org/) van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="705a4-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="705a4-186">Gebruik Hallo opdracht tooinstall FreeTDS op Hallo HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="705a4-187">Zodra FreeTDS is geïnstalleerd, opdracht gebruik Hallo volgende uit tooconnect toohello SQL Database-server die u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="705a4-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="705a4-188">U ontvangt uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="705a4-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="705a4-189">Op Hallo `1>` gevraagd, voert u Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="705a4-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="705a4-190">Wanneer Hallo `GO` instructie wordt ingevoerd, Hallo vorige instructies worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="705a4-191">Deze instructies maken van een tabel met de naam **mobiledata** dat wordt gebruikt door het Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="705a4-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="705a4-192">Gebruik Hallo na tooverify die Hallo tabel is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="705a4-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="705a4-193">Ziet u uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="705a4-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="705a4-194">Voer `exit` op Hallo `1>` vragen tooexit Hallo tsql-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="705a4-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="705a4-195">Hallo taakdefinitie maken</span><span class="sxs-lookup"><span data-stu-id="705a4-195">Create hello job definition</span></span>

<span data-ttu-id="705a4-196">Hallo taakdefinitie beschrijft waar toofind workflow.xml Hallo.</span><span class="sxs-lookup"><span data-stu-id="705a4-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="705a4-197">Ook wordt beschreven waar toofind andere bestanden die worden gebruikt door de werkstroom hello (zoals useooziewf.hql.) Het definieert ook Hallo waarden voor eigenschappen binnen de werkstroom Hallo gebruikt en bestanden bijbehorende.</span><span class="sxs-lookup"><span data-stu-id="705a4-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="705a4-198">Hallo volgende opdracht tooget Hallo volledige adres Hallo standaard opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="705a4-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="705a4-199">Dit adres wordt gebruikt in het configuratiebestand hello later:</span><span class="sxs-lookup"><span data-stu-id="705a4-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="705a4-200">Met deze opdracht retourneert informatie vergelijkbare toohello XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="705a4-201">Als Azure-opslag Hallo HDInsight-cluster als Hallo standaard opslag gebruikt, Hallo `<value>` element inhoud beginnen met `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="705a4-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="705a4-202">Als Azure Data Lake Store in plaats daarvan wordt gebruikt, deze begint met `adl://`.</span><span class="sxs-lookup"><span data-stu-id="705a4-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="705a4-203">Hallo-inhoud van Hallo opslaan `<value>` element, zoals deze wordt gebruikt in de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="705a4-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="705a4-204">Gebruik hello opdracht tooget FQDN-naam van Hallo cluster headnode te volgen.</span><span class="sxs-lookup"><span data-stu-id="705a4-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="705a4-205">Deze informatie wordt gebruikt voor Hallo JobTracker adres voor Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="705a4-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="705a4-206">Hiermee wordt informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="705a4-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="705a4-207">Hallo poort gebruikt voor Hallo JobTracker is 8050, waardoor de Hallo volledig adres toouse voor Hallo JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="705a4-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="705a4-208">Gebruik Hallo toocreate hello Oozie-taakconfiguratie definitie te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="705a4-209">Zodra het Hallo nano-editor wordt geopend, gebruikt u Hallo XML als Hallo inhoud van Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

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

   * <span data-ttu-id="705a4-210">Vervang alle exemplaren van  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  met Hallo-waarde die u eerder hebt ontvangen voor de opslag van de standaard.</span><span class="sxs-lookup"><span data-stu-id="705a4-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="705a4-211">Als het Hallo-pad is een `wasb` pad, moet u het volledige pad hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="705a4-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="705a4-212">Kan geen moet u deze toojust `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="705a4-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="705a4-213">Vervang **JOBTRACKERADDRESS** Hello JobTracker/ResourceManager adres die u eerder hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="705a4-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="705a4-214">Vervang **uwnaam** met de aanmeldingsnaam van uw voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="705a4-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="705a4-215">Vervang **serverName**, **adminLogin**, en **adminPassword** met Hallo-informatie voor uw Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="705a4-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="705a4-216">De meeste Hallo-informatie in dit bestand is gebruikte toopopulate Hallo waarden gebruikt in Hallo workflow.xml of ooziewf.hql-bestanden (bijvoorbeeld ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="705a4-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="705a4-217">Hallo **oozie.wf.application.path** vermelding definieert waar toofind hello workflow.xml bestand, dat Hallo workflow bevat die worden uitgevoerd door deze taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="705a4-218">Gebruik Ctrl X vervolgens **Y** en **Enter** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="705a4-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="705a4-219">Indienen en Hallo taak beheren</span><span class="sxs-lookup"><span data-stu-id="705a4-219">Submit and manage hello job</span></span>

<span data-ttu-id="705a4-220">Hallo volgt gebruik Hallo Oozie opdracht toosubmit en Oozie-werkstromen op Hallo cluster beheren.</span><span class="sxs-lookup"><span data-stu-id="705a4-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="705a4-221">Hallo Oozie-opdracht is een beschrijvende interface via Hallo [Oozie REST-API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="705a4-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="705a4-222">Wanneer u Hallo Oozie-opdracht, moet u Hallo FQDN voor Hallo HDInsight headnode.</span><span class="sxs-lookup"><span data-stu-id="705a4-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="705a4-223">Deze FDQN-naam is alleen toegankelijk is vanaf Hallo cluster of als hello cluster zich op een virtueel netwerk in Azure vanuit andere machines op Hallo van hetzelfde netwerk.</span><span class="sxs-lookup"><span data-stu-id="705a4-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="705a4-224">Hallo tooobtain Hallo URL toohello Oozie service volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="705a4-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="705a4-225">Hiermee wordt informatie vergelijkbare toohello XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="705a4-226">Hallo `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` gedeelte Hallo URL toouse Hello Oozie-opdracht is.</span><span class="sxs-lookup"><span data-stu-id="705a4-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="705a4-227">Gebruik Hallo na toocreate een omgevingsvariabele voor Hallo-URL, zodat er geen tootype voor elke opdracht:</span><span class="sxs-lookup"><span data-stu-id="705a4-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="705a4-228">Hallo URL vervangen door Hallo een die u eerder hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="705a4-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="705a4-229">Hallo toosubmit Hallo taak volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="705a4-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="705a4-230">Met deze opdracht wordt geladen Hallo taakgegevens uit **job.xml** en verstuurt tooOozie maken, maar niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="705a4-231">Zodra het Hallo-opdracht is voltooid, moet het Hallo-ID van Hallo taak retourneren.</span><span class="sxs-lookup"><span data-stu-id="705a4-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="705a4-232">Bijvoorbeeld `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="705a4-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="705a4-233">Deze ID is gebruikte toomanage Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="705a4-234">Hallo-status van Hallo-taak met behulp van de volgende opdracht Hallo weergeven:</span><span class="sxs-lookup"><span data-stu-id="705a4-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="705a4-235">Vervang `<JOBID>` Hello ID in de vorige stap Hallo die wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="705a4-236">Hiermee wordt informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="705a4-236">This returns information similar toohello following text:</span></span>

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

    <span data-ttu-id="705a4-237">Deze taak heeft status `PREP`.</span><span class="sxs-lookup"><span data-stu-id="705a4-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="705a4-238">Deze status geeft aan dat Hallo-taak is gemaakt, maar is niet gestart.</span><span class="sxs-lookup"><span data-stu-id="705a4-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="705a4-239">Hallo opdracht toostart Hallo taak volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="705a4-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="705a4-240">Vervang `<JOBID>` Hello ID eerder geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="705a4-241">Als u Hallo status na deze opdracht controleren, actief is en gegevens worden geretourneerd voor Hallo-acties in Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="705a4-242">Zodra het Hallo-taak is voltooid, kunt u controleren dat Hallo gegevens is gegenereerd en geëxporteerd, toohello SQL Database-tabel met behulp van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="705a4-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="705a4-243">Op Hallo `1>` gevraagd, voert u Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="705a4-244">Hallo-informatie die wordt geretourneerd is vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="705a4-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="705a4-245">Zie voor meer informatie over Hallo Oozie opdracht [Oozie-opdrachtregelprogramma](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="705a4-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="705a4-246">Oozie REST-API</span><span class="sxs-lookup"><span data-stu-id="705a4-246">Oozie REST API</span></span>

<span data-ttu-id="705a4-247">Hallo Oozie REST-API kunt u toobuild uw eigen hulpprogramma's die met Oozie werken.</span><span class="sxs-lookup"><span data-stu-id="705a4-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="705a4-248">Hallo volgen HDInsight specifieke informatie over het gebruik van Hallo Oozie REST-API:</span><span class="sxs-lookup"><span data-stu-id="705a4-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="705a4-249">**URI**: Hallo REST-API toegankelijk is vanaf externe Hallo-cluster op`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="705a4-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="705a4-250">**Verificatie**: toohello API met Hallo cluster HTTP-account (admin) en het wachtwoord verifiëren.</span><span class="sxs-lookup"><span data-stu-id="705a4-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="705a4-251">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="705a4-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="705a4-252">Zie voor meer informatie over het gebruik van Hallo Oozie REST-API [Oozie-webservices-API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="705a4-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="705a4-253">Oozie-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="705a4-253">Oozie Web UI</span></span>

<span data-ttu-id="705a4-254">Hallo Oozie-Webgebruikersinterface biedt een webweergave in Hallo status van de Oozie taken op Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="705a4-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="705a4-255">Hallo-webgebruikersinterface kunt u tooview Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="705a4-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="705a4-256">De status van taak</span><span class="sxs-lookup"><span data-stu-id="705a4-256">Job status</span></span>
* <span data-ttu-id="705a4-257">Taakdefinitie</span><span class="sxs-lookup"><span data-stu-id="705a4-257">Job definition</span></span>
* <span data-ttu-id="705a4-258">Configuratie</span><span class="sxs-lookup"><span data-stu-id="705a4-258">Configuration</span></span>
* <span data-ttu-id="705a4-259">Een grafiek van Hallo-acties in Hallo-taak</span><span class="sxs-lookup"><span data-stu-id="705a4-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="705a4-260">Logboeken voor de taak Hallo</span><span class="sxs-lookup"><span data-stu-id="705a4-260">Logs for hello job</span></span>

<span data-ttu-id="705a4-261">U kunt ook details voor acties in een taak weergeven.</span><span class="sxs-lookup"><span data-stu-id="705a4-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="705a4-262">tooaccess hello Oozie-Webgebruikersinterface, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="705a4-263">Maak een SSH-tunnel toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="705a4-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="705a4-264">Zie voor informatie Hallo [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="705a4-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="705a4-265">Zodra een tunnel is gemaakt, opent u Hallo Ambari-webgebruikersinterface in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="705a4-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="705a4-266">Hallo URI voor Hallo Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="705a4-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="705a4-267">Vervang **CLUSTERNAME** met Hallo-naam van uw Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="705a4-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="705a4-268">Selecteer in de Hallo linkerkant van de pagina hello, **Oozie**, vervolgens **snelkoppelingen**, en tot slot **Oozie-Webgebruikersinterface**.</span><span class="sxs-lookup"><span data-stu-id="705a4-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![afbeelding van menu's Hallo](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="705a4-270">Hallo Oozie-Webgebruikersinterface standaardwaarden toodisplaying werkstroomtaken uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="705a4-271">alle werkstroomtaken, selecteert u toosee **alle taken**.</span><span class="sxs-lookup"><span data-stu-id="705a4-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Alle taken die worden weergegeven](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="705a4-273">Selecteer een taak tooview meer informatie over het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-273">Select a job tooview more information about hello job.</span></span>

    ![Taakinformatie](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="705a4-275">Hallo taakinformatie tabblad ziet u informatie over basic taak en Hallo afzonderlijke acties in Hallo job.</span><span class="sxs-lookup"><span data-stu-id="705a4-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="705a4-276">Hallo tabbladen boven Hallo die kunt u weergeven met taakdefinitie, configuratie van de taak, toegang Hallo taaklogboek hello of een omgeleid acyclische grafiek (DAG) van Hallo-taak weergeven.</span><span class="sxs-lookup"><span data-stu-id="705a4-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="705a4-277">**Taaklogboek**: Selecteer Hallo **GetLogs** tooget alle logboeken voor de Hallo taak, of gebruikt u Hallo **zoekfilter Voer** veld toofilter Logboeken</span><span class="sxs-lookup"><span data-stu-id="705a4-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![Logboekbestand van taak](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="705a4-279">**JobDAG**: Hallo DAG is een grafisch overzicht van de gegevenspaden Hallo doorlopen Hallo-werkstroom</span><span class="sxs-lookup"><span data-stu-id="705a4-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![Taak DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="705a4-281">Een van de acties Hallo selecteren in Hallo **taakinformatie** tabblad opstart, wordt informatie voor Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="705a4-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="705a4-282">Selecteer bijvoorbeeld Hallo **RunHiveScript** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="705a4-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Actie-info](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="705a4-284">Ziet u details voor Hallo actie, zoals een koppeling toohello **Console URL**.</span><span class="sxs-lookup"><span data-stu-id="705a4-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="705a4-285">Deze koppeling kan worden gebruikt tooview JobTracker informatie voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="705a4-286">Plannen van taken</span><span class="sxs-lookup"><span data-stu-id="705a4-286">Scheduling jobs</span></span>

<span data-ttu-id="705a4-287">Hallo-coördinator kunt u toospecify een begin en einde exemplaar frequentie voor taken.</span><span class="sxs-lookup"><span data-stu-id="705a4-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="705a4-288">toodefine een planning voor Hallo werkstroom, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="705a4-289">Gebruik Hallo na een bestand met de naam toocreate **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="705a4-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="705a4-290">Gebruik Hallo XML als Hallo inhoud van Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-290">Use hello following XML as hello contents of hello file:</span></span>

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
    > <span data-ttu-id="705a4-291">Hallo `${...}` variabelen zijn vervangen door waarden in de taakdefinitie Hallo tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="705a4-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="705a4-292">Hallo-variabelen zijn:</span><span class="sxs-lookup"><span data-stu-id="705a4-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="705a4-293">`${coordFrequency}`: Tijd tussen sessies van Hallo taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="705a4-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="705a4-294">** `${coordStart}`: de begintijd van taak Hallo.</span><span class="sxs-lookup"><span data-stu-id="705a4-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="705a4-295">`${coordEnd}`: eindtijd Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="705a4-296">`${coordTimezone}`: Coordinator taken zijn in een vaste tijdzone geen zomertijd (doorgaans weergegeven met behulp UTC).</span><span class="sxs-lookup"><span data-stu-id="705a4-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="705a4-297">Deze tijdzone wordt verwezen als Hallo 'Oozie verwerking tijdzone."</span><span class="sxs-lookup"><span data-stu-id="705a4-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="705a4-298">`${wfPath}`: Hallo pad toohello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="705a4-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="705a4-299">Hallo toosave gebruikt u Ctrl X **Y**, en **Enter**.</span><span class="sxs-lookup"><span data-stu-id="705a4-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="705a4-300">Gebruik Hallo opdracht toocopy Hallo bestand toohello werkmap voor deze taak te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="705a4-301">Gebruik Hallo na toomodify hello **job.xml** bestand:</span><span class="sxs-lookup"><span data-stu-id="705a4-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="705a4-302">Hallo volgende wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="705a4-302">Make hello following changes:</span></span>

   * <span data-ttu-id="705a4-303">tooinstruct oozie toorun Hallo coordinator bestand in plaats van Hallo werkstroom wijzigen `<name>oozie.wf.application.path</name>` te`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="705a4-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="705a4-304">tooset hello `workflowPath` variabele die wordt gebruikt door Hallo-coördinator toevoegen Hallo XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="705a4-305">Vervang Hallo `wasb://mycontainer@mystorageaccount.blob.core.windows` tekst met Hallo-waarde in de andere vermeldingen in Hallo job.xml bestand gebruikt.</span><span class="sxs-lookup"><span data-stu-id="705a4-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="705a4-306">toodefine hello start, einde en frequentie voor het Hallo-coördinator toevoegen Hallo XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

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

       <span data-ttu-id="705a4-307">Deze waarden ingesteld Hallo start tijd too12: 00 PM op 10 mei 2017 Hallo end tijd tooMay 12, 2017.</span><span class="sxs-lookup"><span data-stu-id="705a4-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="705a4-308">Hallo-interval voor het uitvoeren van deze taak dagelijks.</span><span class="sxs-lookup"><span data-stu-id="705a4-308">hello interval for running this job daily.</span></span> <span data-ttu-id="705a4-309">Hallo frequentie in minuten, wordt dus 24 uur x 60 minuten = 1440 minuten.</span><span class="sxs-lookup"><span data-stu-id="705a4-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="705a4-310">Ten slotte Hallo tijdzone tooUTC ingesteld.</span><span class="sxs-lookup"><span data-stu-id="705a4-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="705a4-311">Gebruik Ctrl X vervolgens **Y** en **Enter** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="705a4-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="705a4-312">toorun hello taak gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="705a4-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="705a4-313">Deze opdracht worden verzonden en Hallo taak start.</span><span class="sxs-lookup"><span data-stu-id="705a4-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="705a4-314">Als u Hallo Oozie-Webgebruikersinterface bezoeken en selecteer Hallo **coördinator taken** tabblad ziet u informatie vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![tabblad Coordinator-taken](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="705a4-316">Hallo **volgende Materialisatie** invoer bevat Hallo volgende keer dat Hallo taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="705a4-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="705a4-317">Vergelijkbare toohello eerdere werkstroomtaak Hallo taak vermelding selecteren in Hallo webgebruikersinterface geeft informatie weer op Hallo taak:</span><span class="sxs-lookup"><span data-stu-id="705a4-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![De taakinformatie Coordinator](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="705a4-319">Deze afbeelding ziet u alleen geslaagde wordt uitgevoerd van Hallo-taak niet afzonderlijke acties in de werkstroom Hallo gepland.</span><span class="sxs-lookup"><span data-stu-id="705a4-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="705a4-320">toosee die, selecteer een van de Hallo **actie** vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="705a4-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Actie-info](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="705a4-322">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="705a4-322">Troubleshooting</span></span>

<span data-ttu-id="705a4-323">Hallo Oozie UI kunt u tooview Oozie-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="705a4-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="705a4-324">Het bevat ook koppelingen tooJobTracker logboeken voor MapReduce-taken die zijn gestart door Hallo werkstroom.</span><span class="sxs-lookup"><span data-stu-id="705a4-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="705a4-325">Hallo-patroon voor het oplossen van moet zijn:</span><span class="sxs-lookup"><span data-stu-id="705a4-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="705a4-326">Hallo-taak weergeven in Oozie-Webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="705a4-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="705a4-327">Als er een fout of een fout voor een specifieke actie, selecteer de actie toosee Hallo als hello **foutbericht** veld bevat meer informatie over het Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="705a4-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="705a4-328">Indien beschikbaar, Hallo URL gebruiken van Hallo actie tooview meer informatie (zoals JobTracker Logboeken) voor Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="705a4-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="705a4-329">Hallo hieronder vindt u specifieke fouten optreden kunnen, en hoe tooresolve ze.</span><span class="sxs-lookup"><span data-stu-id="705a4-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="705a4-330">JA009: Cluster kan niet worden geïnitialiseerd</span><span class="sxs-lookup"><span data-stu-id="705a4-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="705a4-331">**Symptomen**: verandert de status van taak te Hallo**onderbroken**.</span><span class="sxs-lookup"><span data-stu-id="705a4-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="705a4-332">Details voor de taak Hallo Hallo RunHiveScript status als weergeven **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="705a4-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="705a4-333">Hallo actie selecteren weergegeven Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="705a4-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="705a4-334">**Oorzaak**: WASB-adressen die worden gebruikt in Hallo Hallo **job.xml** bestand bevatten geen Hallo storage-container of de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="705a4-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="705a4-335">Hallo WASB adresindeling moet `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="705a4-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="705a4-336">**Resolutie**: Hallo WASB adressen die worden gebruikt door Hallo taak wijzigen.</span><span class="sxs-lookup"><span data-stu-id="705a4-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="705a4-337">JA002: Oozie is niet toegestaan voor tooimpersonate &lt;gebruiker ></span><span class="sxs-lookup"><span data-stu-id="705a4-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="705a4-338">**Symptomen**: verandert de status van taak te Hallo**onderbroken**.</span><span class="sxs-lookup"><span data-stu-id="705a4-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="705a4-339">Details voor de taak Hallo Hallo RunHiveScript status als weergeven **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="705a4-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="705a4-340">Hallo actie selecteren toont Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="705a4-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="705a4-341">**Oorzaak**: huidige machtigingsinstellingen staan geen Oozie tooimpersonate Hallo opgegeven gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="705a4-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="705a4-342">**Resolutie**: Oozie tooimpersonate gebruikers is toegestaan in Hallo **gebruikers** groep.</span><span class="sxs-lookup"><span data-stu-id="705a4-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="705a4-343">Gebruik Hallo `groups USERNAME` toosee Hallo groepen die Hallo gebruikersaccount lid van is.</span><span class="sxs-lookup"><span data-stu-id="705a4-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="705a4-344">Als het Hallo-gebruiker is geen lid is van Hallo **gebruikers** groep, gebruikt u Hallo opdracht tooadd Hallo-gebruikersgroep toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="705a4-345">Het kan enkele minuten duren voordat HDInsight herkent dat die gebruiker Hallo toohello groep is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="705a4-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="705a4-346">FOUT (Sqoop) starten</span><span class="sxs-lookup"><span data-stu-id="705a4-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="705a4-347">**Symptomen**: verandert de status van taak te Hallo**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="705a4-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="705a4-348">Details voor de taak Hallo Hallo RunSqoopExport status als weergeven **fout**.</span><span class="sxs-lookup"><span data-stu-id="705a4-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="705a4-349">Hallo actie selecteren toont Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="705a4-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="705a4-350">**Oorzaak**: Sqoop is kan niet tooload Hallo database stuurprogramma vereist tooaccess Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="705a4-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="705a4-351">**Resolutie**: wanneer u Sqoop uit een taak Oozie, moet u opnemen Hallo databasestuurprogramma Hello andere bronnen (zoals Hallo workflow.xml) gebruikt door Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="705a4-352">Ook verwijzen naar Hallo-archief met databasestuurprogramma Hallo van Hallo `<sqoop>...</sqoop>` sectie van Hallo workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="705a4-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="705a4-353">Voor de taak Hallo in dit document gebruikt u bijvoorbeeld Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="705a4-354">Kopieer Hallo sqljdbc4.1.jar toohello /tutorials/useoozie map:</span><span class="sxs-lookup"><span data-stu-id="705a4-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="705a4-355">Hallo workflow.xml tooadd Hallo XML volgen op een nieuwe regel bovenstaande wijzigen `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="705a4-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="705a4-356">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="705a4-356">Next steps</span></span>

<span data-ttu-id="705a4-357">In deze zelfstudie hebt u geleerd hoe toodefine een Oozie-werkstroom en hoe toorun een Oozie-taak.</span><span class="sxs-lookup"><span data-stu-id="705a4-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="705a4-358">toolearn meer informatie over het werken met HDInsight, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="705a4-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="705a4-359">[Tijd gebaseerde Oozie-coördinator gebruiken met HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="705a4-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="705a4-360">[Uploaden van gegevens voor Hadoop-taken in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="705a4-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="705a4-361">[Sqoop gebruiken met Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="705a4-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="705a4-362">[Hive gebruiken met Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="705a4-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="705a4-363">[Pig gebruiken met Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="705a4-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="705a4-364">[Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="705a4-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
