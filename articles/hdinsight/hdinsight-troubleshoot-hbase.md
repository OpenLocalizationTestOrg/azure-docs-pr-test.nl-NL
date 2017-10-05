---
title: HBase oplossen met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op veelgestelde vragen over het werken met HBase en Azure HDInsight.
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 15412c3853a2b8436c5e96034c9a92a2a1094662
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="a3053-103">HBase oplossen met behulp van Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a3053-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="a3053-104">Meer informatie over de meest voorkomende problemen en hun oplossingen bij het werken met Apache HBase nettoladingen in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="a3053-104">Learn about the top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="a3053-105">Hoe voer hbck opdracht rapporten met meerdere niet-toegewezen gebieden</span><span class="sxs-lookup"><span data-stu-id="a3053-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="a3053-106">Een algemene foutmelding dat u mogelijk zien bij het uitvoeren van de `hbase hbck` opdracht is "meerdere regio's wordt niet-toegewezen of gaten in de keten van regio's."</span><span class="sxs-lookup"><span data-stu-id="a3053-106">A common error message that you might see when you run the `hbase hbck` command is "multiple regions being unassigned or holes in the chain of regions."</span></span>

<span data-ttu-id="a3053-107">In de UI HBase Master ziet u het aantal regio's die zijn op alle servers van de regio in onbalans gebracht.</span><span class="sxs-lookup"><span data-stu-id="a3053-107">In the HBase Master UI, you can see the number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="a3053-108">U kunt vervolgens uitvoert `hbase hbck` opdracht om te zien gaten in de keten regio.</span><span class="sxs-lookup"><span data-stu-id="a3053-108">Then, you can run `hbase hbck` command to see holes in the region chain.</span></span>

<span data-ttu-id="a3053-109">Gaten wordt mogelijk veroorzaakt door de offline-regio's, de toewijzingen dus eerst los.</span><span class="sxs-lookup"><span data-stu-id="a3053-109">Holes might be caused by the offline regions, so fix the assignments first.</span></span> 

<span data-ttu-id="a3053-110">Voor het maken van de niet-toegewezen gebieden terug naar een normale status, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a3053-110">To bring the unassigned regions back to a normal state, complete the following steps:</span></span>

1. <span data-ttu-id="a3053-111">Meld u aan het HDInsight HBase-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="a3053-111">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="a3053-112">Voor verbinding met de ZooKeeper-shell, voer de `hbase zkcli` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a3053-112">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="a3053-113">Voer de `rmr /hbase/regions-in-transition` opdracht of het `rmr /hbase-unsecure/regions-in-transition` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a3053-113">Run the `rmr /hbase/regions-in-transition` command or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="a3053-114">Om af te sluiten van de `hbase zkcli` -shell, gebruikt u de `exit` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a3053-114">To exit from the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="a3053-115">Open de Apache Ambari-gebruikersinterface en start de service actief HBase Master opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a3053-115">Open the Apache Ambari UI, and then restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="a3053-116">Voer de `hbase hbck` opdracht (zonder opties) opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a3053-116">Run the `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="a3053-117">Controleer de uitvoer van deze opdracht om ervoor te zorgen dat alle regio's worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a3053-117">Check the output of this command to ensure that all regions are being assigned.</span></span>


## <span data-ttu-id="a3053-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Hoe los ik problemen time-out bij gebruik van hbck opdrachten voor toewijzingen regio</span><span class="sxs-lookup"><span data-stu-id="a3053-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="a3053-119">Probleem</span><span class="sxs-lookup"><span data-stu-id="a3053-119">Issue</span></span>

<span data-ttu-id="a3053-120">Een mogelijke oorzaak voor time-out van problemen wanneer u de `hbck` opdracht mogelijk verschillende regio's zijn in de status 'in de overgangsfase' gedurende een lange periode.</span><span class="sxs-lookup"><span data-stu-id="a3053-120">A potential cause for timeout issues when you use the `hbck` command might be that several regions are in the "in transition" state for a long time.</span></span> <span data-ttu-id="a3053-121">Deze regio's kunt u zien als offline in de HBase-Master-UI.</span><span class="sxs-lookup"><span data-stu-id="a3053-121">You can see those regions as offline in the HBase Master UI.</span></span> <span data-ttu-id="a3053-122">Omdat een groot aantal gebieden om een overgang probeert, HBase Master time-out mogelijk en geen regio's weer online brengen.</span><span class="sxs-lookup"><span data-stu-id="a3053-122">Because a high number of regions are attempting to transition, HBase Master might timeout and be unable to bring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="a3053-123">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="a3053-123">Resolution steps</span></span>

1. <span data-ttu-id="a3053-124">Meld u aan het HDInsight HBase-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="a3053-124">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="a3053-125">Voor verbinding met de ZooKeeper-shell, voer de `hbase zkcli` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a3053-125">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="a3053-126">Voer de `rmr /hbase/regions-in-transition` of de `rmr /hbase-unsecure/regions-in-transition` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a3053-126">Run the `rmr /hbase/regions-in-transition` or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="a3053-127">Om af te sluiten de `hbase zkcli` -shell, gebruikt u de `exit` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a3053-127">To exit the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="a3053-128">In de Ambari-UI de actieve HBase Master-service opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="a3053-128">In the Ambari UI, restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="a3053-129">Voer de `hbase hbck -fixAssignments` opdracht opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a3053-129">Run the `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="a3053-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Hoe ik geforceerde-/ uitschakelen HDFS veilige modus in een cluster</span><span class="sxs-lookup"><span data-stu-id="a3053-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="a3053-131">Probleem</span><span class="sxs-lookup"><span data-stu-id="a3053-131">Issue</span></span>

<span data-ttu-id="a3053-132">De lokale Hadoop Distributed File System (HDFS) is vastgelopen in de veilige modus op het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="a3053-132">The local Hadoop Distributed File System (HDFS) is stuck in safe mode on the HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="a3053-133">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3053-133">Detailed description</span></span>

<span data-ttu-id="a3053-134">Deze fout kan zijn veroorzaakt door een fout opgetreden tijdens het uitvoeren van de volgende HDFS-opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3053-134">This error might be caused by a failure when you run the following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="a3053-135">De fout die u tegenkomen kunt wanneer u probeert uit te voeren van de opdracht ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="a3053-135">The error you might see when you try to run the command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" to turn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="a3053-136">Mogelijke oorzaak</span><span class="sxs-lookup"><span data-stu-id="a3053-136">Probable cause</span></span>

<span data-ttu-id="a3053-137">De grootte van het HDInsight-cluster is gewijzigd om een zeer weinig knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a3053-137">The HDInsight cluster has been scaled down to a very few nodes.</span></span> <span data-ttu-id="a3053-138">Het aantal knooppunten is lager dan of dicht bij de replicatie HDFS factor.</span><span class="sxs-lookup"><span data-stu-id="a3053-138">The number of nodes is below or close to the HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="a3053-139">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="a3053-139">Resolution steps</span></span> 

1. <span data-ttu-id="a3053-140">De status van de HDFS ophalen op het HDInsight-cluster met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a3053-140">Get the status of the HDFS on the HDInsight cluster by running the following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="a3053-141">U kunt ook de integriteit van de HDFS op het HDInsight-cluster controleren met behulp van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a3053-141">You also can check the integrity of the HDFS on the HDInsight cluster by using the following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting to namenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   The filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="a3053-142">Als u dat vaststelt er zijn geen ontbreekt, beschadigd of under-gerepliceerde blokken of dat deze blokken kunnen worden genegeerd, voer de volgende opdracht te laten de naam van knooppunt buiten de veilige modus:</span><span class="sxs-lookup"><span data-stu-id="a3053-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run the following command to take the name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="a3053-143">Hoe los JDBC of SQLLine verbinding problemen met Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="a3053-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="a3053-144">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="a3053-144">Resolution steps</span></span>

<span data-ttu-id="a3053-145">Als u wilt verbinden met Phoenix, moet u het IP-adres van een actief ZooKeeper-knooppunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="a3053-145">To connect with Phoenix, you must provide the IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="a3053-146">Zorg ervoor dat de service ZooKeeper welke sqlline.py verbinding probeert te maken is actief.</span><span class="sxs-lookup"><span data-stu-id="a3053-146">Ensure that the ZooKeeper service to which sqlline.py is trying to connect is up and running.</span></span>
1. <span data-ttu-id="a3053-147">Meld u aan het HDInsight-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="a3053-147">Sign in to the HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="a3053-148">Voer de volgende opdracht in:</span><span class="sxs-lookup"><span data-stu-id="a3053-148">Enter the following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="a3053-149">Het IP-adres van het actieve knooppunt van de ZooKeeper kunt u krijgen via de UI Ambari.</span><span class="sxs-lookup"><span data-stu-id="a3053-149">You can get the IP address of the active ZooKeeper node from the Ambari UI.</span></span> <span data-ttu-id="a3053-150">Ga naar **HBase** > **snelle koppelingen** > **ZK\* (actief)** > **Zookeeper Info**.</span><span class="sxs-lookup"><span data-stu-id="a3053-150">Go to **HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="a3053-151">Als de sqlline.py met Phoenix verbindt en geen time-out biedt, voert u de volgende opdracht om de beschikbaarheid en de status van Phoenix valideren:</span><span class="sxs-lookup"><span data-stu-id="a3053-151">If the sqlline.py connects to Phoenix and does not timeout, run the following command to validate the availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="a3053-152">Als deze opdracht werkt, is er geen probleem.</span><span class="sxs-lookup"><span data-stu-id="a3053-152">If this command works, there is no issue.</span></span> <span data-ttu-id="a3053-153">Het IP-adres opgegeven door de gebruiker is mogelijk onjuist.</span><span class="sxs-lookup"><span data-stu-id="a3053-153">The IP address provided by the user might be incorrect.</span></span> <span data-ttu-id="a3053-154">Echter, als de opdracht voor langere tijd wordt onderbroken en wordt vervolgens de volgende fout weergegeven, verder met stap 5.</span><span class="sxs-lookup"><span data-stu-id="a3053-154">However, if the command pauses for an extended time and then displays the following error, continue to step 5.</span></span>

   ```apache
           Error while connecting to sqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting to jdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="a3053-155">De volgende opdrachten uitvoeren vanaf het hoofdknooppunt (hn0) voor het vaststellen van de voorwaarde van het systeem Phoenix. Catalogustabel:</span><span class="sxs-lookup"><span data-stu-id="a3053-155">Run the following commands from the head node (hn0) to diagnose the condition of the Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="a3053-156">De opdracht moet retourneren een foutmelding ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="a3053-156">The command should return an error similar to the following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="a3053-157">Voer de volgende stappen uit om de service HMaster op alle knooppunten van de ZooKeeper opnieuw te starten in de UI Ambari:</span><span class="sxs-lookup"><span data-stu-id="a3053-157">In the Ambari UI, complete the following steps to restart the HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="a3053-158">In de **samenvatting** sectie van HBase, gaat u naar **HBase** > **actieve HBase Master**.</span><span class="sxs-lookup"><span data-stu-id="a3053-158">In the **Summary** section of HBase, go to **HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="a3053-159">In de **onderdelen** sectie, opnieuw opstarten van de HBase-hoofdservice.</span><span class="sxs-lookup"><span data-stu-id="a3053-159">In the **Components** section, restart the HBase Master service.</span></span>
    3. <span data-ttu-id="a3053-160">Herhaal deze stappen voor alle resterende **stand-by HBase Master** services.</span><span class="sxs-lookup"><span data-stu-id="a3053-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="a3053-161">Het kan tot vijf minuten duren voordat de HBase-Master service stabiel en het herstelproces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="a3053-161">It can take up to five minutes for the HBase Master service to stabilize and finish the recovery process.</span></span> <span data-ttu-id="a3053-162">Herhaal de sqlline.py-opdrachten om te bevestigen dat het systeem na een paar minuten. Catalogustabel actief is en dat deze kan worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="a3053-162">After a few minutes, repeat the sqlline.py commands to confirm that the SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="a3053-163">Wanneer het systeem. Catalogustabel is weer in de normale, het connectiviteitsprobleem naar Phoenix moet worden automatisch opgelost.</span><span class="sxs-lookup"><span data-stu-id="a3053-163">When the SYSTEM.CATALOG table is back to normal, the connectivity issue to Phoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-to-fail-to-start"></a><span data-ttu-id="a3053-164">Wat zorgt ervoor dat een master server niet worden gestart</span><span class="sxs-lookup"><span data-stu-id="a3053-164">What causes a master server to fail to start</span></span>

### <a name="error"></a><span data-ttu-id="a3053-165">Fout</span><span class="sxs-lookup"><span data-stu-id="a3053-165">Error</span></span> 

<span data-ttu-id="a3053-166">Een atomic naamswijzigingen fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="a3053-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="a3053-167">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3053-167">Detailed description</span></span>

<span data-ttu-id="a3053-168">Tijdens het opstarten voltooid HMaster veel initialisatiestappen.</span><span class="sxs-lookup"><span data-stu-id="a3053-168">During the startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="a3053-169">Deze omvatten het verplaatsen van gegevens uit de map maken (TMP) naar de map data.</span><span class="sxs-lookup"><span data-stu-id="a3053-169">These include moving data from the scratch (.tmp) folder to the data folder.</span></span> <span data-ttu-id="a3053-170">HMaster ook gekeken naar de map schrijven-ahead logs (WALs) om te zien of er niet-reagerende regio-servers zijn, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="a3053-170">HMaster also looks at the write-ahead logs (WALs) folder to see if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="a3053-171">Tijdens het opstarten HMaster biedt een eenvoudige `list` opdracht op deze mappen.</span><span class="sxs-lookup"><span data-stu-id="a3053-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="a3053-172">Als HMaster op elk gewenst moment een onverwacht bestand in een van deze mappen ziet, er een uitzondering gegenereerd en niet kan worden gestart.</span><span class="sxs-lookup"><span data-stu-id="a3053-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="a3053-173">Mogelijke oorzaak</span><span class="sxs-lookup"><span data-stu-id="a3053-173">Probable cause</span></span>

<span data-ttu-id="a3053-174">Probeer om te bepalen van de tijdlijn van het maken van het bestand en controleer vervolgens of er is een proces crash rond de tijd die het bestand is gemaakt in de logboeken van de server regio.</span><span class="sxs-lookup"><span data-stu-id="a3053-174">In the region server logs, try to identify the timeline of the file creation, and then see if there was a process crash around the time the file was created.</span></span> <span data-ttu-id="a3053-175">(Contact op met ondersteuning van HBase om u te helpen dit uit te voeren). Dit helpt ons bieden krachtiger mechanismen, zodat u kunt u door deze fout voorkomen en zorg ervoor dat de correcte proces afsluitingen over te slaan.</span><span class="sxs-lookup"><span data-stu-id="a3053-175">(Contact HBase support to assist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="a3053-176">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="a3053-176">Resolution steps</span></span>

<span data-ttu-id="a3053-177">Controleer de aanroepstack en probeer het bepalen van de map waarin het probleem mogelijk worden veroorzaakt (bijvoorbeeld het moet mogelijk de map WALs of TMP).</span><span class="sxs-lookup"><span data-stu-id="a3053-177">Check the call stack and try to determine which folder might be causing the problem (for instance, it might be the WALs folder or the .tmp folder).</span></span> <span data-ttu-id="a3053-178">In de Cloud Explorer of via de HDFS-opdrachten, probeer het probleembestand te zoeken.</span><span class="sxs-lookup"><span data-stu-id="a3053-178">Then, in Cloud Explorer or by using HDFS commands, try to locate the problem file.</span></span> <span data-ttu-id="a3053-179">Meestal is dit een \*-renamePending.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="a3053-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="a3053-180">(De \*-renamePending.json bestand is een journaalbestand dat wordt gebruikt voor het implementeren van de atomic naamswijziging in het stuurprogramma WASB.</span><span class="sxs-lookup"><span data-stu-id="a3053-180">(The \*-renamePending.json file is a journal file that's used to implement the atomic rename operation in the WASB driver.</span></span> <span data-ttu-id="a3053-181">Als gevolg van fouten in deze implementatie van kunnen deze bestanden blijven via na proces crashes, enzovoort.) Force verwijderen van dit bestand in de Cloud Explorer of via de HDFS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="a3053-181">Due to bugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="a3053-182">Soms wordt er mogelijk ook een tijdelijk bestand dat lijkt op met de naam *$$$. $$$* op deze locatie.</span><span class="sxs-lookup"><span data-stu-id="a3053-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="a3053-183">U moet gebruiken de HDFS `ls` opdracht om te zien van dit bestand; u kunt het bestand in de Cloud Explorer kan niet controleren.</span><span class="sxs-lookup"><span data-stu-id="a3053-183">You have to use HDFS `ls` command to see this file; you cannot see the file in Cloud Explorer.</span></span> <span data-ttu-id="a3053-184">Als u wilt verwijderen van dit bestand, gebruikt u de opdracht HDFS `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="a3053-184">To delete this file, use the HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="a3053-185">Na het uitvoeren van deze opdrachten moet HMaster onmiddellijk starten.</span><span class="sxs-lookup"><span data-stu-id="a3053-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="a3053-186">Fout</span><span class="sxs-lookup"><span data-stu-id="a3053-186">Error</span></span>

<span data-ttu-id="a3053-187">Er is geen serveradres wordt vermeld in *hbase: meta* voor xxx regio.</span><span class="sxs-lookup"><span data-stu-id="a3053-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="a3053-188">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3053-188">Detailed description</span></span>

<span data-ttu-id="a3053-189">U ziet een bericht op uw Linux-cluster waarmee wordt aangegeven dat de *hbase: meta* tabel is niet online.</span><span class="sxs-lookup"><span data-stu-id="a3053-189">You might see a message on your Linux cluster that indicates that the *hbase: meta* table is not online.</span></span> <span data-ttu-id="a3053-190">Met `hbck` kunnen melden die ' hbase: meta tabel replicaId 0 is niet gevonden in elke regio. "</span><span class="sxs-lookup"><span data-stu-id="a3053-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="a3053-191">Het probleem mogelijk HMaster kan niet initialiseren nadat u HBase opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="a3053-191">The problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="a3053-192">In de logboeken HMaster ziet u het bericht: "Er is geen serveradres vermeld in hbase: meta voor regio hbase: back- \<regionaam\>'.</span><span class="sxs-lookup"><span data-stu-id="a3053-192">In the HMaster logs, you might see the message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="a3053-193">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="a3053-193">Resolution steps</span></span>

1. <span data-ttu-id="a3053-194">Voer de volgende opdrachten (werkelijke waarden voor de wijziging van toepassing) in de HBase-shell:</span><span class="sxs-lookup"><span data-stu-id="a3053-194">In the HBase shell, enter the following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="a3053-195">Verwijder de *hbase: naamruimte* vermelding.</span><span class="sxs-lookup"><span data-stu-id="a3053-195">Delete the *hbase: namespace* entry.</span></span> <span data-ttu-id="a3053-196">Dit item is mogelijk dezelfde fout die wordt gemeld wanneer de *hbase: naamruimte* tabel wordt gescand.</span><span class="sxs-lookup"><span data-stu-id="a3053-196">This entry might be the same error that's being reported when the *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="a3053-197">Start de actieve HMaster-service actief is, in de UI Ambari HBase weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a3053-197">To bring up HBase in a running state, in the Ambari UI, restart the Active HMaster service.</span></span>  

4. <span data-ttu-id="a3053-198">In de HBase-shell, zodat alle offline tabellen, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3053-198">In the HBase shell, to bring up all offline tables, run the following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="a3053-199">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a3053-199">Additional reading</span></span>

[<span data-ttu-id="a3053-200">Kan niet worden verwerkt de HBase-tabel</span><span class="sxs-lookup"><span data-stu-id="a3053-200">Unable to process the HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="a3053-201">Fout</span><span class="sxs-lookup"><span data-stu-id="a3053-201">Error</span></span>

<span data-ttu-id="a3053-202">HMaster een time-out optreedt bij een fatale uitzondering die vergelijkbaar is met ' java.io.IOException: time-out 300000ms wachten naamruimte tabel moet worden toegewezen. "</span><span class="sxs-lookup"><span data-stu-id="a3053-202">HMaster times out with a fatal exception similar to "java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="a3053-203">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3053-203">Detailed description</span></span>

<span data-ttu-id="a3053-204">U kunt dit probleem kan optreden als er veel tabellen en regio's die niet is leeggemaakt wanneer u uw HMaster services opnieuw start.</span><span class="sxs-lookup"><span data-stu-id="a3053-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="a3053-205">Opnieuw opstarten kan mislukken en ziet u het vorige foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a3053-205">Restart might fail, and you'll see the preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="a3053-206">Mogelijke oorzaak</span><span class="sxs-lookup"><span data-stu-id="a3053-206">Probable cause</span></span>

<span data-ttu-id="a3053-207">Dit is een bekend probleem met de service HMaster.</span><span class="sxs-lookup"><span data-stu-id="a3053-207">This is a known issue with the HMaster service.</span></span> <span data-ttu-id="a3053-208">Algemene cluster starten van de taken kunnen lang duren.</span><span class="sxs-lookup"><span data-stu-id="a3053-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="a3053-209">HMaster afgesloten omdat de tabel naamruimte nog niet is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a3053-209">HMaster shuts down because the namespace table isn’t yet assigned.</span></span> <span data-ttu-id="a3053-210">Dit gebeurt alleen in scenario's waarin grote hoeveelheid gegevens unflushed bestaat en een time-out van vijf minuten is niet voldoende.</span><span class="sxs-lookup"><span data-stu-id="a3053-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="a3053-211">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="a3053-211">Resolution steps</span></span>

1. <span data-ttu-id="a3053-212">Ga in de UI Ambari naar **HBase** > **Configs**.</span><span class="sxs-lookup"><span data-stu-id="a3053-212">In the Ambari UI, go to **HBase** > **Configs**.</span></span> <span data-ttu-id="a3053-213">Voeg de volgende instelling in het bestand aangepaste hbase-site.xml:</span><span class="sxs-lookup"><span data-stu-id="a3053-213">In the custom hbase-site.xml file, add the following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="a3053-214">De vereiste services (HMaster en mogelijk andere HBase-services) opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="a3053-214">Restart the required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="a3053-215">Wat veroorzaakt een fout opnieuw opstarten op een server regio</span><span class="sxs-lookup"><span data-stu-id="a3053-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="a3053-216">Probleem</span><span class="sxs-lookup"><span data-stu-id="a3053-216">Issue</span></span>

<span data-ttu-id="a3053-217">Een fout opnieuw opstarten op een server regio kan worden voorkomen door de volgende best practices.</span><span class="sxs-lookup"><span data-stu-id="a3053-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="a3053-218">U wordt aangeraden zwaar worden belast activiteit te onderbreken, wanneer u van plan bent om te HBase regio servers opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="a3053-218">We recommend that you pause heavy workload activity when you are planning to restart HBase region servers.</span></span> <span data-ttu-id="a3053-219">Als een toepassing wordt voortgezet verbinding maken met servers in regio als shutdown bezig is, wordt regio server opnieuw opstarten trager worden door enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="a3053-219">If an application continues to connect with region servers when shutdown is in progress, the region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="a3053-220">Het is ook een goed idee eerst leegmaken van alle tabellen.</span><span class="sxs-lookup"><span data-stu-id="a3053-220">Also, it's a good idea to first flush all the tables.</span></span> <span data-ttu-id="a3053-221">Zie voor informatie over het leegmaken van tabellen [HDInsight HBase: suggesties voor verbeteringen aan het opstarten van de HBase-cluster door het leegmaken van tabellen](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="a3053-221">For a reference on how to flush tables, see [HDInsight HBase: How to improve the HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="a3053-222">Als u de bewerking voor opnieuw opstarten op HBase regio servers van de Ambari UI hebt gestart, ziet u onmiddellijk dat de servers regio werd afgesloten, maar ze niet meteen opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a3053-222">If you initiate the restart operation on HBase region servers from the Ambari UI, you immediately see that the region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="a3053-223">Dit is wat er gebeurt achter de schermen:</span><span class="sxs-lookup"><span data-stu-id="a3053-223">Here's what's happening behind the scenes:</span></span> 

1. <span data-ttu-id="a3053-224">De Ambari-agent verzendt een aanvraag tot stoppen met de regio-server.</span><span class="sxs-lookup"><span data-stu-id="a3053-224">The Ambari agent sends a stop request to the region server.</span></span>
2. <span data-ttu-id="a3053-225">De Ambari-agent wacht gedurende 30 seconden voor de regio server afsluiten.</span><span class="sxs-lookup"><span data-stu-id="a3053-225">The Ambari agent waits for 30 seconds for the region server to shut down gracefully.</span></span> 
3. <span data-ttu-id="a3053-226">Als uw toepassing blijft om te verbinden met de regio-server, sluit de server niet omlaag onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="a3053-226">If your application continues to connect with the region server, the server won't shut down immediately.</span></span> <span data-ttu-id="a3053-227">De 30 seconden time-out is verstreken voordat de afsluiting.</span><span class="sxs-lookup"><span data-stu-id="a3053-227">The 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="a3053-228">Na 30 seconden, de Ambari-agent verzendt een force-kill (`kill -9`) opdracht met de regio-server.</span><span class="sxs-lookup"><span data-stu-id="a3053-228">After 30 seconds, the Ambari agent sends a force-kill (`kill -9`) command to the region server.</span></span> <span data-ttu-id="a3053-229">U kunt dit zien in het logboek ambari-agent (in de /var/log /-map van het respectieve werkrolknooppunt):</span><span class="sxs-lookup"><span data-stu-id="a3053-229">You can see this in the ambari-agent log (in the /var/log/ directory of the respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="a3053-230">Vanwege het abrupte afsluiten, kan de poort die is gekoppeld aan het proces niet worden vrijgegeven, hoewel de regio serverproces is gestopt.</span><span class="sxs-lookup"><span data-stu-id="a3053-230">Because of the abrupt shutdown, the port associated with the process might not be released, even though the region server process is stopped.</span></span> <span data-ttu-id="a3053-231">Deze situatie kan leiden tot een AddressBindException bij het starten van de regio-server, zoals wordt weergegeven in de volgende Logboeken.</span><span class="sxs-lookup"><span data-stu-id="a3053-231">This situation can lead to an AddressBindException when the region server is starting, as shown in the following logs.</span></span> <span data-ttu-id="a3053-232">U kunt dit controleren in de regio-server.log in de map /var/log/hbase op de worker-knooppunten waar de regio-server niet kan worden gestart.</span><span class="sxs-lookup"><span data-stu-id="a3053-232">You can verify this in the region-server.log in the /var/log/hbase directory on the worker nodes where the region server fails to start.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding to /10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="a3053-233">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="a3053-233">Resolution steps</span></span>

1. <span data-ttu-id="a3053-234">Wilt u de belasting op de HBase regio-servers te verminderen voordat u een opnieuw opstarten initiëren.</span><span class="sxs-lookup"><span data-stu-id="a3053-234">Try to reduce the load on the HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="a3053-235">U kunt ook (als stap 1 niet help), probeer het opnieuw wilt opstarten regio servers op de worker-knooppunten met behulp van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a3053-235">Alternatively (if step 1 doesn't help), try to manually restart region servers on the worker nodes by using the following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

