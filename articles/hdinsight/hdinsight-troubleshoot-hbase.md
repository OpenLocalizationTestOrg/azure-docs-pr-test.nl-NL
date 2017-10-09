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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>HBase oplossen met behulp van Azure HDInsight

Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen bij het werken met Apache HBase nettoladingen in Apache Ambari.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Hoe voer hbck opdracht rapporten met meerdere niet-toegewezen gebieden

Een algemene foutmelding dat u mogelijk zien bij het uitvoeren van Hallo `hbase hbck` opdracht is "meerdere regio's wordt niet-toegewezen of gaten in Hallo keten van regio's."

Hallo HBase Master UI ziet u Hallo aantal regio's die zijn op alle servers van de regio in onbalans gebracht. U kunt vervolgens uitvoert `hbase hbck` opdracht toosee gaten in Hallo regio keten.

Gaten mogelijk eerst worden veroorzaakt door Hallo offline regio's in dat geval fix Hallo toewijzingen. 

toobring Hallo normale status van niet-toegewezen gebieden back tooa, voltooien Hallo stappen te volgen:

1. Aanmelden toohello HDInsight HBase-cluster via SSH.
2. tooconnect met Hallo ZooKeeper shell, Voer Hallo `hbase zkcli` opdracht.
3. Voer Hallo `rmr /hbase/regions-in-transition` opdracht of Hallo `rmr /hbase-unsecure/regions-in-transition` opdracht.
4. tooexit van Hallo `hbase zkcli` -shell, gebruikt u Hallo `exit` opdracht.
5. Open Hallo Apache Ambari gebruikersinterface en start Hallo actieve HBase Master-service opnieuw.
6. Voer Hallo `hbase hbck` opdracht (zonder opties) opnieuw. Controleer Hallo-uitvoer van deze opdracht tooensure die alle regio's worden toegewezen.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Hoe los ik problemen time-out bij gebruik van hbck opdrachten voor toewijzingen regio

### <a name="issue"></a>Probleem

Een mogelijke oorzaak voor time-out voor problemen bij het gebruik van Hallo `hbck` opdracht is mogelijk dat meerdere regio's in Hallo 'in de overgangsfase zijn' status gedurende een lange periode. Deze regio's kunt u zien als offline in Hallo HBase Master UI. Omdat een groot aantal gebieden tootransition probeert, time-out mogelijk HBase hoofd- en kan niet toobring die gebieden weer online worden.

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Aanmelden toohello HDInsight HBase-cluster via SSH.
2. tooconnect met Hallo ZooKeeper shell, Voer Hallo `hbase zkcli` opdracht.
3. Voer Hallo `rmr /hbase/regions-in-transition` of Hallo `rmr /hbase-unsecure/regions-in-transition` opdracht.
4. Hallo tooexit `hbase zkcli` -shell, gebruikt u Hallo `exit` opdracht.
5. In Hallo Ambari UI, opnieuw opstarten Hallo actieve HBase-hoofdservice.
6. Voer Hallo `hbase hbck -fixAssignments` opdracht opnieuw.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Hoe ik geforceerde-/ uitschakelen HDFS veilige modus in een cluster

### <a name="issue"></a>Probleem

Hallo lokale Hadoop Distributed File System (HDFS) is vastgelopen in de veilige modus op Hallo HDInsight-cluster.

### <a name="detailed-description"></a>Gedetailleerde beschrijving

Deze fout kan zijn veroorzaakt door een fout opgetreden tijdens het uitvoeren van Hallo HDFS-opdracht te volgen:

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

Hallo-fout die u tegenkomen kunt wanneer u toorun Hallo opdracht probeert ziet er als volgt:

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

### <a name="probable-cause"></a>Mogelijke oorzaak

Hallo HDInsight-cluster is verkleind tooa zeer weinig knooppunten. het aantal knooppunten Hallo lager is dan of toohello HDFS replicatie factor sluit.

### <a name="resolution-steps"></a>Stappen voor het oplossen 

1. Status van HDFS op Hallo HDInsight-cluster door het uitvoeren van de volgende opdrachten Hallo HALLO hallo ophalen:

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
2. U kunt ook Hallo integriteit van HDFS op Hallo HDInsight-cluster met behulp van de volgende opdrachten Hallo Hallo controleren:

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

3. Als u vaststelt dat er geen ontbreekt, is beschadigd of under-gerepliceerde blokken, of dat deze blokken kunnen worden genegeerd, voert u Hallo opdracht tootake Hallo naam knooppunt buiten de veilige modus te volgen:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Hoe los JDBC of SQLLine verbinding problemen met Apache Phoenix

### <a name="resolution-steps"></a>Stappen voor het oplossen

tooconnect met Phoenix, moet u Hallo IP-adres van een actief ZooKeeper-knooppunt opgeven. Zorg ervoor dat Hallo ZooKeeper service toowhich sqlline.py probeert tooconnect actief is.
1. Aanmelden toohello HDInsight-cluster via SSH.
2. Voer Hallo volgende opdracht:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Hallo IP-adres van de actieve ZooKeeper knooppunt Hallo kunt u krijgen via Hallo Ambari UI. Ga te**HBase** > **snelkoppelingen** > **ZK\* (actief)** > **Zookeeper Info**. 

3. Als Hallo sqlline.py tooPhoenix verbindt en geen time-out biedt, Voer Hallo volgende opdracht uit toovalidate Hallo beschikbaarheid en de gezondheid van Phoenix:

   ```apache
           !tables
           !quit
   ```      
4. Als deze opdracht werkt, is er geen probleem. Hallo IP-adres opgegeven door de gebruiker Hallo is mogelijk onjuist. Als het Hallo-opdracht voor langere tijd wordt onderbroken en wordt vervolgens de volgende fout Hallo, blijven echter toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Hallo volgende opdrachten uit Hallo hoofdknooppunt (hn0) toodiagnose Hallo voorwaarde Hallo Phoenix systeem worden uitgevoerd. Catalogustabel:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   Hallo-opdracht moet een fout vergelijkbare toohello volgende retourneren: 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. Hallo Ambari UI, uitvoeren Hallo stappen toorestart hello HMaster service op alle ZooKeeper-knooppunten te volgen:

    1. In Hallo **samenvatting** sectie van HBase, ga te**HBase** > **actieve HBase Master**. 
    2. In Hallo **onderdelen** sectie, Hallo HBase Master-service opnieuw starten.
    3. Herhaal deze stappen voor alle resterende **stand-by HBase Master** services. 

Het kan een Hallo HBase Master service toostabilize toofive minuten in beslag nemen en Hallo herstelproces te voltooien. Herhaal Hallo sqlline.py opdrachten tooconfirm die Hallo systeem na een paar minuten. Catalogustabel actief is en dat deze kan worden opgevraagd. 

Wanneer Hallo systeem. Catalogustabel back toonormal, Hallo connectiviteit probleem tooPhoenix moet worden automatisch opgelost.


## <a name="what-causes-a-master-server-toofail-toostart"></a>Waarom een hoofdserver toofail toostart

### <a name="error"></a>Fout 

Een atomic naamswijzigingen fout optreedt.

### <a name="detailed-description"></a>Gedetailleerde beschrijving

Tijdens het opstartproces hello voltooit HMaster veel initialisatiestappen. Deze omvatten het verplaatsen van gegevens vanaf het begin hello (TMP) gegevens van de map toohello. Hallo vooraf geschreven Logboeken (WALs) map toosee HMaster ook kijkt als er een niet-reagerende regio-servers, enzovoort. 

Tijdens het opstarten HMaster biedt een eenvoudige `list` opdracht op deze mappen. Als HMaster op elk gewenst moment een onverwacht bestand in een van deze mappen ziet, er een uitzondering gegenereerd en niet kan worden gestart.  

### <a name="probable-cause"></a>Mogelijke oorzaak

In de serverlogboeken Hallo regio, probeer tooidentify Hallo tijdlijn Hallo bestand is gemaakt en vervolgens controleren of er is dat een proces crash rond Hallo tijd Hallo-bestand is gemaakt. (Neem contact op met HBase ondersteuning tooassist u dat doet.) Dit helpt ons bieden krachtiger mechanismen, zodat u kunt u door deze fout voorkomen en zorg ervoor dat de correcte proces afsluitingen over te slaan.

### <a name="resolution-steps"></a>Stappen voor het oplossen

Hallo aanroepstack en probeer het toodetermine map waarin Hallo probleem mogelijk worden veroorzaakt (bijvoorbeeld het moet mogelijk Hallo WALs map of Hallo tmp). In de Cloud Explorer of via de HDFS-opdrachten, probeer toolocate Hallo probleembestand. Meestal is dit een \*-renamePending.json-bestand. (Hallo \*-renamePending.json bestand is een journaalbestand dat tooimplement Hallo-atomic naamswijziging Hallo WASB stuurprogramma is gebruikt. Vervaldatum toobugs in deze implementatie van deze bestanden kunnen blijven via na proces crashes, enzovoort.) Force verwijderen van dit bestand in de Cloud Explorer of via de HDFS-opdrachten. 

Soms wordt er mogelijk ook een tijdelijk bestand dat lijkt op met de naam *$$$. $$$* op deze locatie. U hebt toouse HDFS `ls` opdracht toosee dit bestand; u kunt niet Hallo-bestand in de Cloud Explorer bekijken. toodelete dit bestand, de opdracht use Hallo-HDFS `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

Na het uitvoeren van deze opdrachten moet HMaster onmiddellijk starten. 

### <a name="error"></a>Fout

Er is geen serveradres wordt vermeld in *hbase: meta* voor xxx regio.

### <a name="detailed-description"></a>Gedetailleerde beschrijving

U ziet een bericht op uw Linux-cluster die dat Hallo aangeeft *hbase: meta* tabel is niet online. Met `hbck` kunnen melden die ' hbase: meta tabel replicaId 0 is niet gevonden in elke regio. " Hallo probleem wordt mogelijk HMaster kan niet initialiseren nadat u HBase opnieuw opgestart. In Hallo HMaster Logboeken, ziet u het Hallo-bericht: ' geen serveradres vermeld in hbase: meta voor regio hbase: back- \<regionaam\>'.  

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Voer in Hallo HBase-shell, Hallo opdrachten (werkelijke waarden voor de wijziging van toepassing) te volgen:  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Hallo verwijderen *hbase: naamruimte* vermelding. Dit item is mogelijk dezelfde fout die wordt gerapporteerd als Hallo Hallo *hbase: naamruimte* tabel wordt gescand.

3. toobring van HBase actief is, in Hallo Ambari UI, Hallo Active HMaster service opnieuw starten.  

4. In HBase-shell, toobring van alle tabellen offline Hallo uitvoeren Hallo volgende opdracht:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Aanvullende bronnen

[Kan geen tooprocess hello HBase-tabel](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Fout

Time-out opgetreden voor de HMaster met een vergelijkbare too"java.io.IOException fatale uitzondering opgetreden: time-out 300000ms naamruimte tabel toobe toegewezen wachten."

### <a name="detailed-description"></a>Gedetailleerde beschrijving

U kunt dit probleem kan optreden als er veel tabellen en regio's die niet is leeggemaakt wanneer u uw HMaster services opnieuw start. Opnieuw opstarten kan mislukken en ziet u Hallo vóór het foutbericht.  

### <a name="probable-cause"></a>Mogelijke oorzaak

Dit is een bekend probleem met de Hallo HMaster service. Algemene cluster starten van de taken kunnen lang duren. HMaster afgesloten omdat Hallo naamruimte tabel nog niet is toegewezen. Dit gebeurt alleen in scenario's waarin grote hoeveelheid gegevens unflushed bestaat en een time-out van vijf minuten is niet voldoende.
  
### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Ga te in Hallo Ambari UI,**HBase** > **Configs**. Voeg toe Hallo instelling na Hallo aangepaste hbase-site.xml bestand: 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Hallo vereist services (HMaster en eventueel andere HBase-services) opnieuw starten.  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>Wat veroorzaakt een fout opnieuw opstarten op een server regio

### <a name="issue"></a>Probleem

Een fout opnieuw opstarten op een server regio kan worden voorkomen door de volgende best practices. U wordt aangeraden zwaar worden belast activiteit te onderbreken, wanneer u van plan bent toorestart HBase regio servers. Als een toepassing tooconnect met regio servers blijft als afsluiten uitgevoerd wordt, wordt Hallo regio server opnieuw opstarten trager worden door enkele minuten. Het is ook een goed idee toofirst leegmaken dat alle tabellen Hallo. Voor informatie over het tooflush tabellen, Zie [HDInsight HBase: hoe tooimprove hello HBase-cluster opnieuw opstarten, door het leegmaken van tabellen](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Als u Hallo-bewerking voor opnieuw opstarten op HBase regio servers van Hallo Ambari UI hebt gestart, ziet u onmiddellijk dat Hallo regio servers werd afgesloten, maar ze niet meteen opnieuw. 

Dit is wat er gebeurt achter de schermen Hallo: 

1. Hallo Ambari agent verzendt een stop aanvraag toohello regio-server.
2. Hallo Ambari agent wacht gedurende 30 seconden voor Hallo regio server tooshut omlaag probleemloos. 
3. Als uw toepassing tooconnect met Hallo regio server blijft, sluit server Hallo niet af onmiddellijk. Hallo 30 seconden time-out is verstreken voordat de afsluiting. 
4. Na 30 seconden Hallo Ambari agent verzendt een force-kill (`kill -9`) opdracht toohello regio-server. U kunt dit zien in Hallo ambari-agent-logboek (in Hallo /var/log/map van de respectieve werkrolknooppunt Hallo):

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
Vanwege Hallo nu afgesloten, kan Hallo-poort die is gekoppeld aan het Hallo-proces niet worden vrijgegeven, hoewel Hallo regio serverproces is gestopt. Deze situatie kan leiden tooan AddressBindException wanneer Hallo regio server wordt gestart, zoals wordt weergegeven in Hallo logboeken te volgen. U kunt dit controleren in Hallo regio-server.log in Hallo /var/log/hbase map op Hallo worker-knooppunten waar Hallo regio server toostart mislukt. 

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

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Probeer tooreduce Hallo load op Hallo HBase regio servers voordat u een opnieuw opstarten initiëren. 
2. U kunt ook opdrachten (als stap 1 niet help), probeer toomanually herstart regio servers op Hallo worker-knooppunten met behulp van Hallo volgende:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

