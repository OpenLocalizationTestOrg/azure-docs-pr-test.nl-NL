---
title: aaaHigh beschikbaarheid voor Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe HDInsight-clusters betrouwbaarheid en beschikbaarheid verbeteren met behulp van een extra hoofdknooppunt. Meer informatie over hoe dit heeft gevolgen voor Hadoop-services zoals Ambari en Hive, evenals hoe tooindividually tooeach hoofdknooppunt via SSH verbinding.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: hoge beschikbaarheid voor hadoop
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>Beschikbaarheid en betrouwbaarheid van Hadoop-clusters in HDInsight

HDInsight-clusters bieden twee hoofdknooppunten tooincrease Hallo beschikbaarheid en betrouwbaarheid van Hadoop-services en taken worden uitgevoerd.

Hadoop bereikt door het repliceren van services en gegevens op meerdere knooppunten in een cluster toe te hoge beschikbaarheid en betrouwbaarheid. Standaard distributies van Hadoop hebben echter meestal alleen voor slechts één hoofdknooppunt. Een storing optreedt van één hoofdknooppunt Hallo kan leiden tot Hallo cluster toostop werken. HDInsight biedt twee headnodes tooimprove Hadoop beschikbaarheid en betrouwbaarheid.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="availability-and-reliability-of-nodes"></a>Beschikbaarheid en betrouwbaarheid van knooppunten

Knooppunten in een HDInsight-cluster worden geïmplementeerd met behulp van Azure Virtual Machines. Hallo volgende secties worden besproken Hallo afzonderlijke knooppunten die worden gebruikt met HDInsight. 

> [!NOTE]
> Niet alle knooppunttypen worden gebruikt voor het type van een cluster. Een Hadoop-clustertype heeft bijvoorbeeld geen eventuele Nimbus-knooppunten. Zie voor meer informatie over knooppunten die wordt gebruikt door HDInsight-clustertypen Hallo Cluster typen sectie Hallo [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.

### <a name="head-nodes"></a>HEAD-knooppunten

tooensure hoge beschikbaarheid van Hadoop-services, HDInsight biedt twee hoofdknooppunten. Beide hoofdknooppunten zijn tegelijkertijd actief en wordt uitgevoerd binnen Hallo HDInsight-cluster. Sommige services, zoals HDFS of YARN, zijn alleen op elk moment 'active' op één hoofdknooppunt. Andere services zoals HiveServer2 of Hive-MetaStore actief zijn op beide hoofdknooppunten op Hallo hetzelfde moment.

HEAD-knooppunten (en andere knooppunten in HDInsight) hebben een numerieke waarde als onderdeel van het Hallo-hostnaam van Hallo-knooppunt. Bijvoorbeeld: `hn0-CLUSTERNAME` of `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> Koppel geen Hallo numerieke waarde aan of een knooppunt primair of secundair wordt. Hallo numerieke waarde is alleen aanwezig tooprovide een unieke naam voor elk knooppunt.

### <a name="nimbus-nodes"></a>Nimbus-knooppunten

Nimbus-knooppunten zijn beschikbaar met Storm-clusters. Hallo Nimbus-knooppunten bieden vergelijkbare functionaliteit toohello Hadoop JobTracker met distributie en verwerking bewaking over worker-knooppunten. HDInsight biedt twee Nimbus-knooppunten voor Storm-clusters

### <a name="zookeeper-nodes"></a>Zookeeper-knooppunten

[ZooKeeper](http://zookeeper.apache.org/) knooppunten worden gebruikt voor de keuze opvulteken master services op hoofdknooppunten. Ze zijn ook gebruikte tooinsure dat services, gegevensknooppunten (worker) en gateways weten welke hoofd-service actief is op het hoofdknooppunt. HDInsight biedt standaard drie ZooKeeper-knooppunten.

### <a name="worker-nodes"></a>Worker-knooppunten

Worker-knooppunten niet Hallo werkelijke data-analyse uitvoeren als een taak verzonden toohello cluster wordt. Als een werkrolknooppunt is mislukt, wordt in het Hallo-taak die bezig was ingediende tooanother werkrolknooppunt is. HDInsight maakt standaard vier worker-knooppunten. U kunt dit nummer toosuit uw behoeften wijzigen tijdens en na het maken van het cluster.

### <a name="edge-node"></a>Edge-knooppunt

Een edge-knooppunt deelneemt niet actief aan gegevensanalyse binnen Hallo-cluster. Deze wordt gebruikt door ontwikkelaars of gegevenswetenschappers bij het werken met Hadoop. Hallo edge-knooppunt leven in hetzelfde virtuele Azure-netwerk als Hallo andere knooppunten in cluster Hallo Hallo en rechtstreeks toegang tot alle andere knooppunten. Hallo edge-knooppunt kan worden gebruikt zonder resources verlaten kritieke Hadoop-services of analyse taken.

Op HDInsight R Server is momenteel het enige clustertype hello, waarmee een edge-knooppunt standaard. Voor op HDInsight R Server, Hallo edge-knooppunt wordt gebruikt test R code lokaal op Hallo knooppunt voordat het wordt ingediend toohello cluster voor gedistribueerde verwerking.

Zie voor informatie over het gebruik van een edge-knooppunt met clustertypen dan R Server Hallo [edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md) document.

## <a name="accessing-hello-nodes"></a>Toegang tot Hallo knooppunten

RAS-cluster toohello via Hallo internet is beschikbaar via een openbare-gateway. Hallo edge-knooppunt toegang is beperkt tooconnecting toohello hoofdknooppunten en (indien aanwezig). Toegang tooservices uitgevoerd op Hallo hoofdknooppunten niet wordt toegepast wanneer er meerdere hoofdknooppunten. Hallo openbare gateway routes aanvragen toohello head-knooppunt dat als host fungeert voor Hallo aangevraagde service. Als de Ambari is momenteel gehost op een secundair hoofdknooppunt hello, routeert Hallo gateway binnenkomende aanvragen voor Ambari toothat knooppunt.

Toegang via openbare Hallo-gateway is beperkt tooport 443 (HTTPS), 22 en 23.

* Poort __443__ gebruikte tooaccess is Ambari en andere web-gebruikersinterface of REST-API's die worden gehost op Hallo hoofdknooppunten.

* Poort __22__ gebruikte tooaccess Hallo primaire hoofdknooppunt of edge-knooppunt met SSH.

* Poort __23__ gebruikte tooaccess Hallo secundair hoofdknooppunt met SSH is. Bijvoorbeeld: `ssh username@mycluster-ssh.azurehdinsight.net` toohello primaire hoofdknooppunt van het Hallo-cluster met de naam verbindt **mijncluster**.

Zie voor meer informatie over het gebruik van SSH Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>Interne volledig gekwalificeerde domeinnamen (FQDN)

Knooppunten in een HDInsight-cluster hebben een interne IP-adres en de FQDN-naam die alleen toegankelijk zijn vanuit Hallo-cluster. Bij het openen van services op Hallo-cluster met behulp van de interne FQDN of IP-adres hello, moet u Ambari tooverify Hallo IP of FQDN toouse gebruiken bij het openen van Hallo-service.

Bijvoorbeeld Hallo Oozie-service kan alleen worden uitgevoerd op één hoofdknooppunt en met behulp van Hallo `oozie` opdracht van een SSH-sessie Hallo URL toohello service is vereist. Deze URL kan uit de Ambari worden opgehaald met behulp van de volgende opdracht Hallo:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

Met deze opdracht retourneert een waarde van een vergelijkbare toohello na de opdracht Hallo interne URL toouse Hello bevat `oozie` opdracht:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Zie voor meer informatie over het werken met Hallo Ambari REST-API [bewaken en beheren van HDInsight met behulp van Hallo Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Toegang tot andere knooppunttypen

U kunt verbinding maken toonodes die niet rechtstreeks toegankelijk via internet met behulp van de volgende methoden Hallo Hallo zijn:

* **SSH**: eenmaal zijn verbonden tooa hoofdknooppunt via SSH, kunt u vervolgens SSH uit Hallo hoofdknooppunt tooconnect tooother knooppunten in cluster hello gebruiken. Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

* **SSH-Tunnel**: als u een webservice die worden gehost op tooaccess moet een van Hallo knooppunten die niet beschikbaar gesteld toohello internet, moet u een SSH-tunnel. Zie voor meer informatie, Hallo [een SSH-tunnel gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

* **Azure Virtual Network**: als uw cluster maakt deel uit van een virtueel netwerk in Azure een resource in HDInsight Hallo hetzelfde virtuele netwerk rechtstreeks toegang tot alle knooppunten in cluster Hallo. Zie voor meer informatie, Hallo [uitbreiden HDInsight met behulp van Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.

## <a name="how-toocheck-on-a-service-status"></a>Hoe toocheck op de status van een service

toocheck hello status van services die worden uitgevoerd op hoofdknooppunten Hallo Hallo Ambari-Webgebruikersinterface gebruiken of Hallo Ambari REST-API.

### <a name="ambari-web-ui"></a>Ambari-webgebruikersinterface

Hallo Ambari-Webgebruikersinterface is op https://CLUSTERNAME.azurehdinsight.net zichtbaar. Vervang **CLUSTERNAME** met Hallo-naam van het cluster. Als u wordt gevraagd, voert u Hallo HTTP gebruikersreferenties voor uw cluster. Hallo HTTP standaardgebruikersnaam is **admin** en Hallo wachtwoord is opgegeven bij het maken van de cluster Hallo Hallo-wachtwoord.

Wanneer u op Hallo Ambari pagina aankomt, vindt u op Hallo links van de pagina Hallo Hallo geïnstalleerd services.

![Geïnstalleerde services](./media/hdinsight-high-availability-linux/services.png)

Er zijn een reeks pictogrammen die kunnen worden weergegeven de volgende tooa tooindicate servicestatus. Alle waarschuwingen gerelateerde tooa-service kan worden bekeken met Hallo **waarschuwingen** koppeling bovenaan Hallo Hallo pagina. U kunt elke service tooview meer informatie over het selecteren.

Tijdens het Hallo-servicepagina bevat informatie over het Hallo-status en configuratie van elke service, biedt het geen informatie waarop hoofdknooppunt Hallo-service wordt uitgevoerd op. tooview deze informatie, gebruik Hallo **Hosts** koppeling bovenaan Hallo Hallo pagina. Deze pagina bevat hosts binnen het Hallo-cluster, inclusief Hallo hoofdknooppunten.

![lijst met hosts](./media/hdinsight-high-availability-linux/hosts.png)

Selecteren Hallo-koppeling voor een van de hoofdknooppunten Hallo weergegeven Hallo services en onderdelen die op dat knooppunt worden uitgevoerd.

![Onderdeelstatus](./media/hdinsight-high-availability-linux/nodeservices.png)

Zie voor meer informatie over het gebruik van Ambari [bewaken en beheren van HDInsight met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>Ambari REST-API

Hallo Ambari REST-API beschikbaar is via Hallo internet. Hallo HDInsight openbare gateway verwerkt routering aanvragen toohello hoofdknooppunt waarop Hallo REST-API wordt gehost.

U kunt Hallo opdracht toocheck Hallo status van een service via Hallo Ambari REST-API te volgen:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Vervang **wachtwoord** met het wachtwoord voor gebruikersaccount (admin) Hallo HTTP.
* Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.
* Vervang **SERVICENAME** met de naam van service Hallo Hallo gewenste toocheck Hallo status.

Bijvoorbeeld, toocheck Hallo status Hallo **HDFS** service op een cluster met de naam **mijncluster**, met een wachtwoord van **wachtwoord**, zou u Hallo volgende opdracht gebruiken:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

Hallo-antwoord is vergelijkbaar toohello JSON te volgen:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Hallo URL geeft aan dat Hallo service momenteel wordt uitgevoerd op een hoofdknooppunt met de naam **hn0 CLUSTERNAME**.

Hallo status geeft aan dat de Hallo service momenteel wordt uitgevoerd, of **gestart**.

Als u niet welke services zijn geïnstalleerd op het Hallo-cluster weet, kunt u Hallo opdracht tooretrieve een lijst te volgen:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Zie voor meer informatie over het werken met Hallo Ambari REST-API [bewaken en beheren van HDInsight met behulp van Hallo Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Serviceonderdelen

Services kunnen de onderdelen die u wenst dat toocheck Hallo status van afzonderlijk bevatten. HDFS bevat bijvoorbeeld Hallo NameNode onderdeel. informatie over een onderdeel tooview Hallo opdracht zou zijn:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Als u niet welke onderdelen worden geleverd door een service weet, kunt u Hallo opdracht tooretrieve een lijst te volgen:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Hoe tooaccess logboekbestanden op Hallo hoofdknooppunten

### <a name="ssh"></a>SSH

Tijdens het hoofdknooppunt verbonden tooa via SSH logboekbestanden kunnen worden gevonden in het **/var/log**. Bijvoorbeeld: **/var/log/hadoop-yarn/yarn** bevatten de logboeken voor YARN.

Elke hoofdknooppunt kan unieke logboekvermeldingen, hebben, dus moet u controleren Hallo van beide aanmeldt.

### <a name="sftp"></a>SFTP

U kunt ook verbinding maken met hoofdknooppunt toohello met Hallo SSH File Transfer Protocol of Secure File Transfer Protocol (SFTP) en logboekbestanden Hallo rechtstreeks downloaden.

Vergelijkbare toousing een SSH-client, wanneer u verbinding maakt toohello cluster moet u opgeven Hallo SSH gebruiker account naam en het Hallo SSH-adres van Hallo-cluster. Bijvoorbeeld `sftp username@mycluster-ssh.azurehdinsight.net`. Hallo wachtwoord opgeven voor Hallo account wanneer u wordt gevraagd, of geef een openbare sleutel met behulp van Hallo `-i` parameter.

Eenmaal zijn verbonden, krijgt u een `sftp>` prompt. Vanaf deze prompt kunt u mappen, uploaden en downloaden van bestanden. Bijvoorbeeld Hallo opdrachten na toohello mappen wijzigen **/var/log/hadoop/hdfs** directory en vervolgens alle bestanden in de directory hello te downloaden.

    cd /var/log/hadoop/hdfs
    get *

Voer voor een lijst met beschikbare opdrachten `help` op Hallo `sftp>` prompt.

> [!NOTE]
> Er zijn ook grafische interfaces waarmee u toovisualize Hallo bestandssysteem wanneer verbinding met SFTP. Bijvoorbeeld: [MobaXTerm](http://mobaxterm.mobatek.net/) kunt u met behulp van een interface vergelijkbare tooWindows Explorer Hallo-bestandssysteem voor toobrowse.

### <a name="ambari"></a>Ambari

> [!NOTE]
> tooaccess logboekbestanden met Ambari, moet u een SSH-tunnel. Hallo webinterfaces voor afzonderlijke services Hallo niet openbaar op Hallo Internet worden weergegeven. Zie voor informatie over het gebruik van een SSH-tunnel Hallo [SSH-Tunneling gebruiken](hdinsight-linux-ambari-ssh-tunnel.md) document.

Selecteer in de Hallo Ambari-Webgebruikersinterface, Hallo-service die u wenst dat tooview logboeken voor (bijvoorbeeld YARN). Gebruik vervolgens **snelkoppelingen** tooselect welke hoofdknooppunt tooview Hallo logboeken voor.

![Met behulp van snelle koppelingen tooview Logboeken](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Hoe tooconfigure knooppuntgrootte Hallo

Hallo-grootte van een knooppunt kan alleen worden ingeschakeld tijdens het maken van het cluster. U vindt een lijst met Hallo andere VM-grootten beschikbaar voor HDInsight op Hallo [HDInsight pagina met prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

Wanneer u een cluster maakt, kunt u de grootte Hallo Hallo-knooppunten opgeven. Hallo volgende informatie bevat richtlijnen voor het gebruik van toospecify Hallo grootte Hallo [Azure-portal][preview-portal], [Azure PowerShell][azure-powershell], en Hallo [Azure CLI][azure-cli]:

* **Azure-portal**: wanneer u een cluster maakt, kunt u Hallo grootte van Hallo knooppunten gebruikt door Hallo cluster instellen:

    ![Afbeelding van het maken van clusterwizard met knooppunt grootte selectie](./media/hdinsight-high-availability-linux/headnodesize.png)

* **Azure CLI**: bij gebruik van Hallo `azure hdinsight cluster create` uitvoert, en u kunt de grootte Hallo Hallo hoofd, worker en ZooKeeper-knooppunten instellen met behulp van Hallo `--headNodeSize`, `--workerNodeSize`, en `--zookeeperNodeSize` parameters.

* **Azure PowerShell**: bij gebruik van Hallo `New-AzureRmHDInsightCluster` cmdlet, u kunt de grootte Hallo Hallo hoofd, worker en ZooKeeper-knooppunten instellen met behulp van Hallo `-HeadNodeVMSize`, `-WorkerNodeSize`, en `-ZookeeperNodeSize` parameters.

## <a name="next-steps"></a>Volgende stappen

Gebruik Hallo koppelingen toolearn meer over elementen die worden vermeld in dit document te volgen.

* [Ambari REST-verwijzing](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Installeer en configureer hello Azure CLI](../cli-install-nodejs.md)
* [Azure PowerShell installeren en configureren ](/powershell/azure/overview)
* [HDInsight met Ambari beheren](hdinsight-hadoop-manage-ambari.md)
* [Linux gebaseerde HDInsight-clusters inrichten](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
