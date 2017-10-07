---
title: aaaConfigure HBase-cluster-replicatie in virtuele netwerken - Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure HBase-replicatie voor de load balancer, hoge beschikbaarheid, nul uitvaltijd migratie/bijwerken van een HDInsight versie tooanother en herstel na noodgevallen.
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>HBase-cluster-replicatie in virtuele netwerken configureren

Meer informatie over hoe tooconfigure HBase-replicatie binnen één virtueel netwerk (VNet) of tussen twee virtuele netwerken.

Replicatie in een cluster maakt gebruik van een bron-push-methode. Een HBase-cluster kan een bron of bestemming, of beide functies tegelijk kunnen worden verwerkt. Replicatie is asynchroon en Hallo doel van de replicatie is uiteindelijke consistentie. Wanneer een familie bewerken tooa kolom Hallo bron met de replicatie is ingeschakeld ontvangt, is dat de bewerkingsactie doorgegeven tooall doelclusters. Wanneer gegevens worden gerepliceerd van één cluster tooanother, zijn broncluster hello en alle clusters al verbruikt Hallo gegevens bijgehouden tooprevent replicatie lussen.

In deze zelfstudie configureert u de replicatie van een bron-doel. Zie voor andere clustertopologieën [Naslaggids voor Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).

HBase-replicatie gebruik gevallen voor één virtueel netwerk:

* Taakverdeling--bijvoorbeeld scans of MapReduce-taken uitgevoerd op de doelcluster Hallo en ophalen van gegevens in de broncluster Hallo
* Hoge beschikbaarheid
* Gegevens migreren van een HBase-cluster tooanother
* Een Azure HDInsight-cluster upgraden van één versie tooanother

HBase-replicatie gebruik gevallen voor twee virtuele netwerken:

* Herstel na noodgevallen
* Taakverdeling en toepassing hello partitioneren
* Hoge beschikbaarheid

Replicatie van clusters met behulp van [script actie](hdinsight-hadoop-customize-cluster-linux.md) scripts zich bevindt op [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Vereisten
Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Hallo-omgevingen configureren

Er zijn drie mogelijke configuraties:

- Twee HBase-clusters in een virtuele Azure-netwerk
- Twee HBase-clusters in twee verschillende virtuele netwerken in dezelfde regio Hallo
- Twee HBase-clusters in twee verschillende virtuele netwerken in twee verschillende regio's (geo-replicatie)

toomake deze eenvoudiger tooconfigure Hallo-omgevingen, hebben wij enkele [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-overview.md). Als u liever tooconfigure Hallo omgevingen via andere methoden, Zie:

- [Hadoop op basis van Linux-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [HBase-clusters maken in Azure Virtual Network](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Een virtueel netwerk configureren

Klik op volgende installatiekopie toocreate twee HBase-clusters in Hallo Hallo hetzelfde virtuele netwerk. Hallo-sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Twee virtuele netwerken configureren in Hallo dezelfde regio

Klik op volgende installatiekopie toocreate twee virtuele netwerken met VNet-peering en twee HBase-clusters in Hallo Hallo dezelfde regio. Hallo-sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



In dit scenario moeten [VNet-peering](../virtual-network/virtual-network-peering-overview.md). Hallo-sjabloon kunt VNet-peering.   

HBase-replicatie maakt gebruik van IP-adressen van Hallo ZooKeeper virtuele machines. U kunt statische IP-adressen voor Hallo bestemming HBase ZooKeeper-knooppunten moet configureren.

**tooconfigure statische IP-adressen**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. In het linkermenu hello, klikt u op **resourcegroepen**.
3. Klik op de resourcegroep die Hallo bestemming HBase-cluster bevat. Dit is Hallo resourcegroep die u hebt opgegeven tijdens het gebruik van Hallo Resource Manager-sjabloon toocreate Hallo omgeving. U kunt Hallo filter toonarrow omlaag in de lijst hello gebruiken. Hier ziet u een lijst met bronnen die twee virtuele netwerken Hallo bevat.
4. Klik op Hallo virtueel netwerk met Hallo bestemming HBase-cluster. Bijvoorbeeld, klik op **xxxx vnet2**. Ziet u drie apparaten met namen die met beginnen **nic-zookeepermode -**. Deze apparaten zijn Hallo drie ZooKeeper virtuele machines.
5. Klik op een Hallo ZooKeeper virtuele machines.
6. Klik op **IP-configuraties**.
7. Klik op **ipConfig1** uit Hallo-lijst.
8. Klik op **statische**, en noteer Hallo werkelijke IP-adres. U moet Hallo IP-adres tijdens het uitvoeren van Hallo script actie tooenable replicatie.

  ![HDInsight HBase replicatie ZooKeeper vaste IP-adres](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Herhaal stap 6 tooset Hallo statisch IP-adres voor Hallo andere twee ZooKeeper-knooppunten.

Hallo cross-VNet-scenario, moet u Hallo **- IP-** switch bij het aanroepen van Hallo **hdi_enable_replication.sh** script in te grijpen.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Twee virtuele netwerken configureren in twee verschillende regio 's

Klik op Hallo installatiekopie toocreate twee virtuele netwerken in twee verschillende regio's te volgen. Hallo-sjabloon wordt opgeslagen in een openbare Azure Blob-container.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Een VPN-gateway tussen Hallo twee virtuele netwerken maken. Zie voor instructies [een VNet maken met een site-naar-site-verbinding](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

HBase-replicatie maakt gebruik van IP-adressen van Hallo ZooKeeper virtuele machines. U kunt statische IP-adressen voor Hallo bestemming HBase ZooKeeper-knooppunten moet configureren. tooconfigure vaste IP-adres, raadpleegt u "configureren twee virtuele netwerken in hello dezelfde regio" Hallo-sectie in dit artikel.

Hallo cross-VNet-scenario, moet u Hallo **- IP-** switch bij het aanroepen van Hallo **hdi_enable_replication.sh** script in te grijpen.

## <a name="load-test-data"></a>Testgegevens laden

Wanneer u een cluster repliceert, moet u Hallo tabellen tooreplicate opgeven. In deze sectie wordt u sommige gegevens in de broncluster Hallo geladen. In de volgende sectie hello schakelt u replicatie tussen twee clusters met Hallo.

Volg de instructies in Hallo [HBase-zelfstudie: aan de slag met Apache HBase met Hadoop op basis van Linux in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate een **contactpersonen** tabel en sommige gegevens in Hallo tabel invoegen.

## <a name="enable-replication"></a>Replicatie inschakelen

Hallo stappen te volgen laten zien hoe toocall Hallo script actiescript vanaf hello Azure-portal. Zie voor het uitvoeren van een scriptactie met behulp van Azure PowerShell en hello Azure-opdrachtregelinterface (CLI), [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

**tooenable HBase-replicatie van hello Azure-portal**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Open Hallo bron HBase-cluster.
3. Klik op Hallo cluster menu **scriptacties**.
4. Klik op **nieuwe indienen** vanaf de bovenkant Hallo van Hallo-blade.
5. Selecteer of typ de volgende informatie Hallo:

  - **Naam**: Voer **replicatie inschakelen**.
  - **Script-URL Bash**: Voer **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **HEAD**: geselecteerd. Hallo Schakel andere knooppunttypen.
  - **Parameters**: Hallo volgende steekproef replicatie van de parameters inschakelen voor alle bestaande Hallo-tabellen en alle Hallo gegevens kopiëren van toohello doelcluster voor Hallo bron cluster:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Klik op **Create**. Hallo-script kan enige tijd duren, vooral wanneer Hallo - copydata argument wordt gebruikt.

Vereiste argumenten:

|Naam|Beschrijving|
|----|-----------|
|-s,--src-cluster | Hallo DNS-naam opgeven van Hallo bron HBase-cluster. Bijvoorbeeld: -s hbsrccluster,--src-cluster hbsrccluster = |
|-d,--zomertijd-cluster | Hallo DNS-naam opgeven van Hallo bestemming (replica) HBase-cluster. Bijvoorbeeld: -s dsthbcluster,--src-cluster dsthbcluster = |
|-sp,--src-ambari-wachtwoord | Hallo beheerderswachtwoord opgeven voor Ambari op Hallo bron HBase-cluster. |
|-dp,--zomertijd-ambari-wachtwoord | Hallo beheerderswachtwoord opgeven voor Ambari op Hallo bestemming HBase-cluster.|

Optionele argumenten:

|Naam|Beschrijving|
|----|-----------|
|-su,--src-ambari-gebruiker | Hallo beheerdersgebruikersnaam voor Ambari op Hallo bron HBase-cluster opgeven. de standaardwaarde Hallo is **admin**. |
|-du,--zomertijd-ambari-gebruiker | Hallo beheerdersgebruikersnaam voor Ambari op Hallo bestemming HBase-cluster opgeven. de standaardwaarde Hallo is **admin**. |
|-t,--lijst van de tabel | Geef Hallo tabellen toobe gerepliceerd. Bijvoorbeeld:--tabel lijst = 'Tabel1; tabel2; Tabel3'. Als u geen tabellen opgeeft, worden alle bestaande HBase-tabellen gerepliceerd.|
|-m,--machine | Geef Hallo hoofdknooppunt waar Hallo scriptactie worden uitgevoerd. Hallo-waarde is hn1 of hn0. Omdat hn0 meestal veelgebruikte is, wordt u aangeraden hn1. U kunt deze optie gebruiken bij waarvan u Hallo $0 script als een scriptactie hello HDInsight portal of Azure PowerShell uitvoert.|
|-ip | Dit argument is vereist als u bij het inschakelen van replicatie tussen twee virtuele netwerken. Dit argument fungeert als een switch toouse Hallo statische IP-adressen van ZooKeeper-knooppunten van replica-clusters in plaats van FQDN-namen. Hallo statisch IP-adressen moet toobe vooraf geconfigureerd voordat u replicatie inschakelt. |
|-cp - copydata | Schakel Hallo migratie van bestaande gegevens op Hallo tabellen waarvoor replicatie is ingeschakeld. |
|-rpm, -repliceren-phoenix-metagegevens | Replicatie inschakelen voor Phoenix systeemtabellen. <br><br>*Gebruik deze optie voorzichtig.* U wordt aangeraden Phoenix tabellen op de replica-clusters opnieuw te maken voordat u dit script gebruiken. |
|-h,--help | Gebruiksgegevens weergegeven. |

Hallo print_usage() sectie Hallo [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) wordt een gedetailleerde beschrijving van parameters.

Nadat Hallo scriptactie met succes is kunt geïmplementeerd, u gebruiken SSH tooconnect toohello bestemming HBase-cluster, en controleer of Hallo gegevens zijn gerepliceerd.

### <a name="replication-scenarios"></a>Replicatie-scenario 's

Hello volgende lijst ziet u enkele gevallen algemeen gebruik en de bijbehorende parameterinstellingen:

- **Replicatie inschakelen voor alle tabellen tussen clusters met twee Hallo**. Dit scenario vereist geen Hallo kopie/migratie van bestaande gegevens op Hallo tabellen en gebruikt geen Phoenix tabellen. Hallo volgende parameters gebruikt:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Replicatie inschakelen voor specifieke tabellen**. Volgende parameters tooenable replicatie op table1 en table2 Tabel3 hello gebruiken:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Replicatie inschakelen voor specifieke tabellen en kopieer de bestaande gegevens Hallo**. Volgende parameters tooenable replicatie op table1 en table2 Tabel3 hello gebruiken:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Replicatie inschakelen voor alle tabellen met phoenix metagegevens van de bron toodestination repliceren**. Phoenix metagegevens replicatie is niet perfect en wees voorzichtig met moet worden ingeschakeld.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Kopiëren en gegevens migreren

Er zijn twee afzonderlijke script actie scripts voor het kopiëren van/migreren van gegevens na de replicatie is ingeschakeld:

- [Script voor kleine tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (enkele gigabytes in grootte en de algehele kopie is verwachte toofinish in minder dan één uur)

- [Script voor grote tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (meer dan één uur toocopy tootake verwacht)

Kunt u dezelfde procedure in Hallo [replicatie inschakelen](#enable-replication) toocall hello scriptactie Hello volgende parameters:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Hallo print_usage() sectie Hallo [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) bevat een gedetailleerde beschrijving van parameters.

### <a name="scenarios"></a>Scenario's

- **Kopiëren van specifieke tabellen (test1, test2 en test3) voor alle rijen bewerkt tot nu toe (huidige tijdstempel)**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  of

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Kopiëren van specifieke tabellen met een opgegeven tijdperiode**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Schakel replicatie uit

toodisable replicatie, gebruikt u een ander script actiescript zich bevindt op [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). Kunt u dezelfde procedure in Hallo [replicatie inschakelen](#enable-replication) toocall hello scriptactie Hello volgende parameters:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Hallo print_usage() sectie Hallo [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) wordt een gedetailleerde beschrijving van parameters.

### <a name="scenarios"></a>Scenario's

- **Schakel replicatie op alle tabellen**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  of

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Schakel replicatie op de opgegeven tabellen (Tabel1, tabel2 en Tabel3)**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe tooconfigure HBase-replicatie tussen twee datacentra. toolearn meer informatie over HDInsight en HBase, Zie:

* [Aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started]
* [Overzicht van HDInsight HBase][hdinsight-hbase-overview]
* [HBase-clusters maken in Azure Virtual Network][hdinsight-hbase-provision-vnet]
* [Realtime Twitter-gevoel met HBase analyseren][hdinsight-hbase-twitter-sentiment]
* [Analyseren van sensorgegevens met Storm en HBase in HDInsight (Hadoop)][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
