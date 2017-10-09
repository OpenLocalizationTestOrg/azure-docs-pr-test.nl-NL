---
title: aaaTroubleshoot HBase met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het werken met HBase en Azure HDInsight toocommon.
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
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="beac4-103">HBase oplossen met behulp van Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="beac4-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="beac4-104">Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen bij het werken met Apache HBase nettoladingen in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="beac4-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="beac4-105">Hoe voer hbck opdracht rapporten met meerdere niet-toegewezen gebieden</span><span class="sxs-lookup"><span data-stu-id="beac4-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="beac4-106">Een algemene foutmelding dat u mogelijk zien bij het uitvoeren van Hallo `hbase hbck` opdracht is "meerdere regio's wordt niet-toegewezen of gaten in Hallo keten van regio's."</span><span class="sxs-lookup"><span data-stu-id="beac4-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="beac4-107">Hallo HBase Master UI ziet u Hallo aantal regio's die zijn op alle servers van de regio in onbalans gebracht.</span><span class="sxs-lookup"><span data-stu-id="beac4-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="beac4-108">U kunt vervolgens uitvoert `hbase hbck` opdracht toosee gaten in Hallo regio keten.</span><span class="sxs-lookup"><span data-stu-id="beac4-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="beac4-109">Gaten mogelijk eerst worden veroorzaakt door Hallo offline regio's in dat geval fix Hallo toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="beac4-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="beac4-110">toobring Hallo normale status van niet-toegewezen gebieden back tooa, voltooien Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="beac4-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="beac4-111">Aanmelden toohello HDInsight HBase-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="beac4-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="beac4-112">tooconnect met Hallo ZooKeeper shell, Voer Hallo `hbase zkcli` opdracht.</span><span class="sxs-lookup"><span data-stu-id="beac4-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="beac4-113">Voer Hallo `rmr /hbase/regions-in-transition` opdracht of Hallo `rmr /hbase-unsecure/regions-in-transition` opdracht.</span><span class="sxs-lookup"><span data-stu-id="beac4-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="beac4-114">tooexit van Hallo `hbase zkcli` -shell, gebruikt u Hallo `exit` opdracht.</span><span class="sxs-lookup"><span data-stu-id="beac4-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="beac4-115">Open Hallo Apache Ambari gebruikersinterface en start Hallo actieve HBase Master-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="beac4-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="beac4-116">Voer Hallo `hbase hbck` opdracht (zonder opties) opnieuw.</span><span class="sxs-lookup"><span data-stu-id="beac4-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="beac4-117">Controleer Hallo-uitvoer van deze opdracht tooensure die alle regio's worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="beac4-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="beac4-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Hoe los ik problemen time-out bij gebruik van hbck opdrachten voor toewijzingen regio</span><span class="sxs-lookup"><span data-stu-id="beac4-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="beac4-119">Probleem</span><span class="sxs-lookup"><span data-stu-id="beac4-119">Issue</span></span>

<span data-ttu-id="beac4-120">Een mogelijke oorzaak voor time-out voor problemen bij het gebruik van Hallo `hbck` opdracht is mogelijk dat meerdere regio's in Hallo 'in de overgangsfase zijn' status gedurende een lange periode.</span><span class="sxs-lookup"><span data-stu-id="beac4-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="beac4-121">Deze regio's kunt u zien als offline in Hallo HBase Master UI.</span><span class="sxs-lookup"><span data-stu-id="beac4-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="beac4-122">Omdat een groot aantal gebieden tootransition probeert, time-out mogelijk HBase hoofd- en kan niet toobring die gebieden weer online worden.</span><span class="sxs-lookup"><span data-stu-id="beac4-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="beac4-123">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="beac4-123">Resolution steps</span></span>

1. <span data-ttu-id="beac4-124">Aanmelden toohello HDInsight HBase-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="beac4-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="beac4-125">tooconnect met Hallo ZooKeeper shell, Voer Hallo `hbase zkcli` opdracht.</span><span class="sxs-lookup"><span data-stu-id="beac4-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="beac4-126">Voer Hallo `rmr /hbase/regions-in-transition` of Hallo `rmr /hbase-unsecure/regions-in-transition` opdracht.</span><span class="sxs-lookup"><span data-stu-id="beac4-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="beac4-127">Hallo tooexit `hbase zkcli` -shell, gebruikt u Hallo `exit` opdracht.</span><span class="sxs-lookup"><span data-stu-id="beac4-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="beac4-128">In Hallo Ambari UI, opnieuw opstarten Hallo actieve HBase-hoofdservice.</span><span class="sxs-lookup"><span data-stu-id="beac4-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="beac4-129">Voer Hallo `hbase hbck -fixAssignments` opdracht opnieuw.</span><span class="sxs-lookup"><span data-stu-id="beac4-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="beac4-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Hoe ik geforceerde-/ uitschakelen HDFS veilige modus in een cluster</span><span class="sxs-lookup"><span data-stu-id="beac4-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="beac4-131">Probleem</span><span class="sxs-lookup"><span data-stu-id="beac4-131">Issue</span></span>

<span data-ttu-id="beac4-132">Hallo lokale Hadoop Distributed File System (HDFS) is vastgelopen in de veilige modus op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="beac4-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="beac4-133">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="beac4-133">Detailed description</span></span>

<span data-ttu-id="beac4-134">Deze fout kan zijn veroorzaakt door een fout opgetreden tijdens het uitvoeren van Hallo HDFS-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="beac4-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="beac4-135">Hallo-fout die u tegenkomen kunt wanneer u toorun Hallo opdracht probeert ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="beac4-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
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

### <a name="probable-cause"></a><span data-ttu-id="beac4-136">Mogelijke oorzaak</span><span class="sxs-lookup"><span data-stu-id="beac4-136">Probable cause</span></span>

<span data-ttu-id="beac4-137">Hallo HDInsight-cluster is verkleind tooa zeer weinig knooppunten.</span><span class="sxs-lookup"><span data-stu-id="beac4-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="beac4-138">het aantal knooppunten Hallo lager is dan of toohello HDFS replicatie factor sluit.</span><span class="sxs-lookup"><span data-stu-id="beac4-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="beac4-139">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="beac4-139">Resolution steps</span></span> 

1. <span data-ttu-id="beac4-140">Status van HDFS op Hallo HDInsight-cluster door het uitvoeren van de volgende opdrachten Hallo HALLO hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="beac4-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

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
2. <span data-ttu-id="beac4-141">U kunt ook Hallo integriteit van HDFS op Hallo HDInsight-cluster met behulp van de volgende opdrachten Hallo Hallo controleren:</span><span class="sxs-lookup"><span data-stu-id="beac4-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
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

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="beac4-142">Als u vaststelt dat er geen ontbreekt, is beschadigd of under-gerepliceerde blokken, of dat deze blokken kunnen worden genegeerd, voert u Hallo opdracht tootake Hallo naam knooppunt buiten de veilige modus te volgen:</span><span class="sxs-lookup"><span data-stu-id="beac4-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="beac4-143">Hoe los JDBC of SQLLine verbinding problemen met Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="beac4-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="beac4-144">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="beac4-144">Resolution steps</span></span>

<span data-ttu-id="beac4-145">tooconnect met Phoenix, moet u Hallo IP-adres van een actief ZooKeeper-knooppunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="beac4-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="beac4-146">Zorg ervoor dat Hallo ZooKeeper service toowhich sqlline.py probeert tooconnect actief is.</span><span class="sxs-lookup"><span data-stu-id="beac4-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="beac4-147">Aanmelden toohello HDInsight-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="beac4-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="beac4-148">Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="beac4-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="beac4-149">Hallo IP-adres van de actieve ZooKeeper knooppunt Hallo kunt u krijgen via Hallo Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="beac4-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="beac4-150">Ga te**HBase** > **snelkoppelingen** > **ZK\* (actief)** > **Zookeeper Info**.</span><span class="sxs-lookup"><span data-stu-id="beac4-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="beac4-151">Als Hallo sqlline.py tooPhoenix verbindt en geen time-out biedt, Voer Hallo volgende opdracht uit toovalidate Hallo beschikbaarheid en de gezondheid van Phoenix:</span><span class="sxs-lookup"><span data-stu-id="beac4-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="beac4-152">Als deze opdracht werkt, is er geen probleem.</span><span class="sxs-lookup"><span data-stu-id="beac4-152">If this command works, there is no issue.</span></span> <span data-ttu-id="beac4-153">Hallo IP-adres opgegeven door de gebruiker Hallo is mogelijk onjuist.</span><span class="sxs-lookup"><span data-stu-id="beac4-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="beac4-154">Als het Hallo-opdracht voor langere tijd wordt onderbroken en wordt vervolgens de volgende fout Hallo, blijven echter toostep 5.</span><span class="sxs-lookup"><span data-stu-id="beac4-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="beac4-155">Hallo volgende opdrachten uit Hallo hoofdknooppunt (hn0) toodiagnose Hallo voorwaarde Hallo Phoenix systeem worden uitgevoerd. Catalogustabel:</span><span class="sxs-lookup"><span data-stu-id="beac4-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="beac4-156">Hallo-opdracht moet een fout vergelijkbare toohello volgende retourneren:</span><span class="sxs-lookup"><span data-stu-id="beac4-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="beac4-157">Hallo Ambari UI, uitvoeren Hallo stappen toorestart hello HMaster service op alle ZooKeeper-knooppunten te volgen:</span><span class="sxs-lookup"><span data-stu-id="beac4-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="beac4-158">In Hallo **samenvatting** sectie van HBase, ga te**HBase** > **actieve HBase Master**.</span><span class="sxs-lookup"><span data-stu-id="beac4-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="beac4-159">In Hallo **onderdelen** sectie, Hallo HBase Master-service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="beac4-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="beac4-160">Herhaal deze stappen voor alle resterende **stand-by HBase Master** services.</span><span class="sxs-lookup"><span data-stu-id="beac4-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="beac4-161">Het kan een Hallo HBase Master service toostabilize toofive minuten in beslag nemen en Hallo herstelproces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="beac4-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="beac4-162">Herhaal Hallo sqlline.py opdrachten tooconfirm die Hallo systeem na een paar minuten. Catalogustabel actief is en dat deze kan worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="beac4-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="beac4-163">Wanneer Hallo systeem. Catalogustabel back toonormal, Hallo connectiviteit probleem tooPhoenix moet worden automatisch opgelost.</span><span class="sxs-lookup"><span data-stu-id="beac4-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="beac4-164">Waarom een hoofdserver toofail toostart</span><span class="sxs-lookup"><span data-stu-id="beac4-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="beac4-165">Fout</span><span class="sxs-lookup"><span data-stu-id="beac4-165">Error</span></span> 

<span data-ttu-id="beac4-166">Een atomic naamswijzigingen fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="beac4-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="beac4-167">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="beac4-167">Detailed description</span></span>

<span data-ttu-id="beac4-168">Tijdens het opstartproces hello voltooit HMaster veel initialisatiestappen.</span><span class="sxs-lookup"><span data-stu-id="beac4-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="beac4-169">Deze omvatten het verplaatsen van gegevens vanaf het begin hello (TMP) gegevens van de map toohello.</span><span class="sxs-lookup"><span data-stu-id="beac4-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="beac4-170">Hallo vooraf geschreven Logboeken (WALs) map toosee HMaster ook kijkt als er een niet-reagerende regio-servers, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="beac4-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="beac4-171">Tijdens het opstarten HMaster biedt een eenvoudige `list` opdracht op deze mappen.</span><span class="sxs-lookup"><span data-stu-id="beac4-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="beac4-172">Als HMaster op elk gewenst moment een onverwacht bestand in een van deze mappen ziet, er een uitzondering gegenereerd en niet kan worden gestart.</span><span class="sxs-lookup"><span data-stu-id="beac4-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="beac4-173">Mogelijke oorzaak</span><span class="sxs-lookup"><span data-stu-id="beac4-173">Probable cause</span></span>

<span data-ttu-id="beac4-174">In de serverlogboeken Hallo regio, probeer tooidentify Hallo tijdlijn Hallo bestand is gemaakt en vervolgens controleren of er is dat een proces crash rond Hallo tijd Hallo-bestand is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="beac4-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="beac4-175">(Neem contact op met HBase ondersteuning tooassist u dat doet.) Dit helpt ons bieden krachtiger mechanismen, zodat u kunt u door deze fout voorkomen en zorg ervoor dat de correcte proces afsluitingen over te slaan.</span><span class="sxs-lookup"><span data-stu-id="beac4-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="beac4-176">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="beac4-176">Resolution steps</span></span>

<span data-ttu-id="beac4-177">Hallo aanroepstack en probeer het toodetermine map waarin Hallo probleem mogelijk worden veroorzaakt (bijvoorbeeld het moet mogelijk Hallo WALs map of Hallo tmp).</span><span class="sxs-lookup"><span data-stu-id="beac4-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="beac4-178">In de Cloud Explorer of via de HDFS-opdrachten, probeer toolocate Hallo probleembestand.</span><span class="sxs-lookup"><span data-stu-id="beac4-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="beac4-179">Meestal is dit een \*-renamePending.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="beac4-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="beac4-180">(Hallo \*-renamePending.json bestand is een journaalbestand dat tooimplement Hallo-atomic naamswijziging Hallo WASB stuurprogramma is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="beac4-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="beac4-181">Vervaldatum toobugs in deze implementatie van deze bestanden kunnen blijven via na proces crashes, enzovoort.) Force verwijderen van dit bestand in de Cloud Explorer of via de HDFS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="beac4-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="beac4-182">Soms wordt er mogelijk ook een tijdelijk bestand dat lijkt op met de naam *$$$. $$$* op deze locatie.</span><span class="sxs-lookup"><span data-stu-id="beac4-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="beac4-183">U hebt toouse HDFS `ls` opdracht toosee dit bestand; u kunt niet Hallo-bestand in de Cloud Explorer bekijken.</span><span class="sxs-lookup"><span data-stu-id="beac4-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="beac4-184">toodelete dit bestand, de opdracht use Hallo-HDFS `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="beac4-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="beac4-185">Na het uitvoeren van deze opdrachten moet HMaster onmiddellijk starten.</span><span class="sxs-lookup"><span data-stu-id="beac4-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="beac4-186">Fout</span><span class="sxs-lookup"><span data-stu-id="beac4-186">Error</span></span>

<span data-ttu-id="beac4-187">Er is geen serveradres wordt vermeld in *hbase: meta* voor xxx regio.</span><span class="sxs-lookup"><span data-stu-id="beac4-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="beac4-188">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="beac4-188">Detailed description</span></span>

<span data-ttu-id="beac4-189">U ziet een bericht op uw Linux-cluster die dat Hallo aangeeft *hbase: meta* tabel is niet online.</span><span class="sxs-lookup"><span data-stu-id="beac4-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="beac4-190">Met `hbck` kunnen melden die ' hbase: meta tabel replicaId 0 is niet gevonden in elke regio. "</span><span class="sxs-lookup"><span data-stu-id="beac4-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="beac4-191">Hallo probleem wordt mogelijk HMaster kan niet initialiseren nadat u HBase opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="beac4-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="beac4-192">In Hallo HMaster Logboeken, ziet u het Hallo-bericht: ' geen serveradres vermeld in hbase: meta voor regio hbase: back- \<regionaam\>'.</span><span class="sxs-lookup"><span data-stu-id="beac4-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="beac4-193">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="beac4-193">Resolution steps</span></span>

1. <span data-ttu-id="beac4-194">Voer in Hallo HBase-shell, Hallo opdrachten (werkelijke waarden voor de wijziging van toepassing) te volgen:</span><span class="sxs-lookup"><span data-stu-id="beac4-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="beac4-195">Hallo verwijderen *hbase: naamruimte* vermelding.</span><span class="sxs-lookup"><span data-stu-id="beac4-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="beac4-196">Dit item is mogelijk dezelfde fout die wordt gerapporteerd als Hallo Hallo *hbase: naamruimte* tabel wordt gescand.</span><span class="sxs-lookup"><span data-stu-id="beac4-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="beac4-197">toobring van HBase actief is, in Hallo Ambari UI, Hallo Active HMaster service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="beac4-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="beac4-198">In HBase-shell, toobring van alle tabellen offline Hallo uitvoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="beac4-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="beac4-199">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="beac4-199">Additional reading</span></span>

[<span data-ttu-id="beac4-200">Kan geen tooprocess hello HBase-tabel</span><span class="sxs-lookup"><span data-stu-id="beac4-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="beac4-201">Fout</span><span class="sxs-lookup"><span data-stu-id="beac4-201">Error</span></span>

<span data-ttu-id="beac4-202">Time-out opgetreden voor de HMaster met een vergelijkbare too"java.io.IOException fatale uitzondering opgetreden: time-out 300000ms naamruimte tabel toobe toegewezen wachten."</span><span class="sxs-lookup"><span data-stu-id="beac4-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="beac4-203">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="beac4-203">Detailed description</span></span>

<span data-ttu-id="beac4-204">U kunt dit probleem kan optreden als er veel tabellen en regio's die niet is leeggemaakt wanneer u uw HMaster services opnieuw start.</span><span class="sxs-lookup"><span data-stu-id="beac4-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="beac4-205">Opnieuw opstarten kan mislukken en ziet u Hallo vóór het foutbericht.</span><span class="sxs-lookup"><span data-stu-id="beac4-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="beac4-206">Mogelijke oorzaak</span><span class="sxs-lookup"><span data-stu-id="beac4-206">Probable cause</span></span>

<span data-ttu-id="beac4-207">Dit is een bekend probleem met de Hallo HMaster service.</span><span class="sxs-lookup"><span data-stu-id="beac4-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="beac4-208">Algemene cluster starten van de taken kunnen lang duren.</span><span class="sxs-lookup"><span data-stu-id="beac4-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="beac4-209">HMaster afgesloten omdat Hallo naamruimte tabel nog niet is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="beac4-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="beac4-210">Dit gebeurt alleen in scenario's waarin grote hoeveelheid gegevens unflushed bestaat en een time-out van vijf minuten is niet voldoende.</span><span class="sxs-lookup"><span data-stu-id="beac4-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="beac4-211">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="beac4-211">Resolution steps</span></span>

1. <span data-ttu-id="beac4-212">Ga te in Hallo Ambari UI,**HBase** > **Configs**.</span><span class="sxs-lookup"><span data-stu-id="beac4-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="beac4-213">Voeg toe Hallo instelling na Hallo aangepaste hbase-site.xml bestand:</span><span class="sxs-lookup"><span data-stu-id="beac4-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="beac4-214">Hallo vereist services (HMaster en eventueel andere HBase-services) opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="beac4-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="beac4-215">Wat veroorzaakt een fout opnieuw opstarten op een server regio</span><span class="sxs-lookup"><span data-stu-id="beac4-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="beac4-216">Probleem</span><span class="sxs-lookup"><span data-stu-id="beac4-216">Issue</span></span>

<span data-ttu-id="beac4-217">Een fout opnieuw opstarten op een server regio kan worden voorkomen door de volgende best practices.</span><span class="sxs-lookup"><span data-stu-id="beac4-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="beac4-218">U wordt aangeraden zwaar worden belast activiteit te onderbreken, wanneer u van plan bent toorestart HBase regio servers.</span><span class="sxs-lookup"><span data-stu-id="beac4-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="beac4-219">Als een toepassing tooconnect met regio servers blijft als afsluiten uitgevoerd wordt, wordt Hallo regio server opnieuw opstarten trager worden door enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="beac4-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="beac4-220">Het is ook een goed idee toofirst leegmaken dat alle tabellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="beac4-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="beac4-221">Voor informatie over het tooflush tabellen, Zie [HDInsight HBase: hoe tooimprove hello HBase-cluster opnieuw opstarten, door het leegmaken van tabellen](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="beac4-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="beac4-222">Als u Hallo-bewerking voor opnieuw opstarten op HBase regio servers van Hallo Ambari UI hebt gestart, ziet u onmiddellijk dat Hallo regio servers werd afgesloten, maar ze niet meteen opnieuw.</span><span class="sxs-lookup"><span data-stu-id="beac4-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="beac4-223">Dit is wat er gebeurt achter de schermen Hallo:</span><span class="sxs-lookup"><span data-stu-id="beac4-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="beac4-224">Hallo Ambari agent verzendt een stop aanvraag toohello regio-server.</span><span class="sxs-lookup"><span data-stu-id="beac4-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="beac4-225">Hallo Ambari agent wacht gedurende 30 seconden voor Hallo regio server tooshut omlaag probleemloos.</span><span class="sxs-lookup"><span data-stu-id="beac4-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="beac4-226">Als uw toepassing tooconnect met Hallo regio server blijft, sluit server Hallo niet af onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="beac4-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="beac4-227">Hallo 30 seconden time-out is verstreken voordat de afsluiting.</span><span class="sxs-lookup"><span data-stu-id="beac4-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="beac4-228">Na 30 seconden Hallo Ambari agent verzendt een force-kill (`kill -9`) opdracht toohello regio-server.</span><span class="sxs-lookup"><span data-stu-id="beac4-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="beac4-229">U kunt dit zien in Hallo ambari-agent-logboek (in Hallo /var/log/map van de respectieve werkrolknooppunt Hallo):</span><span class="sxs-lookup"><span data-stu-id="beac4-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

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
<span data-ttu-id="beac4-230">Vanwege Hallo nu afgesloten, kan Hallo-poort die is gekoppeld aan het Hallo-proces niet worden vrijgegeven, hoewel Hallo regio serverproces is gestopt.</span><span class="sxs-lookup"><span data-stu-id="beac4-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="beac4-231">Deze situatie kan leiden tooan AddressBindException wanneer Hallo regio server wordt gestart, zoals wordt weergegeven in Hallo logboeken te volgen.</span><span class="sxs-lookup"><span data-stu-id="beac4-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="beac4-232">U kunt dit controleren in Hallo regio-server.log in Hallo /var/log/hbase map op Hallo worker-knooppunten waar Hallo regio server toostart mislukt.</span><span class="sxs-lookup"><span data-stu-id="beac4-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

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
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
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

### <a name="resolution-steps"></a><span data-ttu-id="beac4-233">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="beac4-233">Resolution steps</span></span>

1. <span data-ttu-id="beac4-234">Probeer tooreduce Hallo load op Hallo HBase regio servers voordat u een opnieuw opstarten initiëren.</span><span class="sxs-lookup"><span data-stu-id="beac4-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="beac4-235">U kunt ook opdrachten (als stap 1 niet help), probeer toomanually herstart regio servers op Hallo worker-knooppunten met behulp van Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="beac4-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

