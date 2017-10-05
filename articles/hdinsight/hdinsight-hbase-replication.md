---
title: HBase-cluster-replicatie in virtuele netwerken - Azure configureren | Microsoft Docs
description: Informatie over het configureren van HBase-replicatie voor taakverdeling, hoge beschikbaarheid, nul uitvaltijd migratie/bijwerken van een HDInsight versie naar een andere en herstel na noodgevallen.
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
ms.openlocfilehash: 895709391486acb4a9d7a54ef046956539913f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>HBase-cluster-replicatie in virtuele netwerken configureren

Informatie over het configureren van HBase-replicatie binnen één virtueel netwerk (VNet) of tussen twee virtuele netwerken.

Replicatie in een cluster maakt gebruik van een bron-push-methode. Een HBase-cluster kan een bron of bestemming, of beide functies tegelijk kunnen worden verwerkt. Replicatie is asynchroon en het doel van de replicatie is uiteindelijke consistentie. Als de bron een bewerking naar de kolomfamilie voor een met de replicatie is ingeschakeld ontvangt, wordt die bewerken doorgegeven aan alle doelclusters. Wanneer gegevens worden gerepliceerd van de ene cluster naar een andere, worden de broncluster en alle clusters die de gegevens al hebt gebruikt om te voorkomen dat replicatie lussen worden bijgehouden.

In deze zelfstudie configureert u de replicatie van een bron-doel. Zie voor andere clustertopologieën [Naslaggids voor Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).

HBase-replicatie gebruik gevallen voor één virtueel netwerk:

* Taakverdeling--bijvoorbeeld scans of MapReduce-taken uitgevoerd op het doelcluster en ophalen van gegevens in de broncluster
* Hoge beschikbaarheid
* Migreren van gegevens van een HBase-cluster naar een andere
* Een Azure HDInsight-cluster upgraden met één versie naar een andere

HBase-replicatie gebruik gevallen voor twee virtuele netwerken:

* Herstel na noodgevallen
* Taakverdeling en partitioneren van de toepassing
* Hoge beschikbaarheid

Replicatie van clusters met behulp van [script actie](hdinsight-hadoop-customize-cluster-linux.md) scripts zich bevindt op [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Vereisten
Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-the-environments"></a>De omgevingen configureren

Er zijn drie mogelijke configuraties:

- Twee HBase-clusters in een virtuele Azure-netwerk
- Twee HBase-clusters in twee verschillende virtuele netwerken in dezelfde regio
- Twee HBase-clusters in twee verschillende virtuele netwerken in twee verschillende regio's (geo-replicatie)

Voor het configureren van de omgevingen te vereenvoudigen hebben wij enkele [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-overview.md). Als u liever de omgevingen met behulp van andere methoden configureren, Zie:

- [Hadoop op basis van Linux-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [HBase-clusters maken in Azure Virtual Network](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Een virtueel netwerk configureren

Klik op de volgende afbeelding om twee HBase-clusters maken in hetzelfde virtuele netwerk. De sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a>Twee virtuele netwerken configureren in dezelfde regio

Klik op de volgende afbeelding om twee virtuele netwerken met VNet-peering en twee HBase-clusters maken in dezelfde regio. De sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



In dit scenario moeten [VNet-peering](../virtual-network/virtual-network-peering-overview.md). De sjabloon kunt VNet-peering.   

HBase-replicatie maakt gebruik van IP-adressen van de ZooKeeper virtuele machines. U kunt statische IP-adressen voor de bestemming HBase ZooKeeper-knooppunten moet configureren.

**Statische IP-adressen configureren**

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Klik in het menu links op **resourcegroepen**.
3. Klik op de resourcegroep die het doel HBase-cluster bevat. Dit is de resourcegroep die u hebt opgegeven wanneer u de Resource Manager-sjabloon gebruikt om de omgeving te maken. Beperken van de lijst kunt u het filter. Hier ziet u een lijst met bronnen die de twee virtuele netwerken bevat.
4. Klik op het virtuele netwerk waarin het doel HBase-cluster. Bijvoorbeeld, klik op **xxxx vnet2**. Ziet u drie apparaten met namen die met beginnen **nic-zookeepermode -**. Deze apparaten zijn de drie ZooKeeper virtuele machines.
5. Klik op een van de ZooKeeper virtuele machines.
6. Klik op **IP-configuraties**.
7. Klik op **ipConfig1** uit de lijst.
8. Klik op **statische**, en noteer de IP-adres. U moet het IP-adres tijdens het uitvoeren van de scriptactie replicatie in te schakelen.

  ![HDInsight HBase replicatie ZooKeeper vaste IP-adres](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Herhaal stap 6 instellen van het statische IP-adres voor de andere twee ZooKeeper-knooppunten.

Voor het scenario voor cross-VNet, moet u de **- IP-** switch bij het aanroepen van de **hdi_enable_replication.sh** script in te grijpen.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Twee virtuele netwerken configureren in twee verschillende regio 's

Klik op de volgende afbeelding om twee virtuele netwerken maken in twee verschillende regio's. De sjabloon wordt opgeslagen in een openbare Azure Blob-container.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

Een VPN-gateway tussen de twee virtuele netwerken maken. Zie voor instructies [een VNet maken met een site-naar-site-verbinding](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

HBase-replicatie maakt gebruik van IP-adressen van de ZooKeeper virtuele machines. U kunt statische IP-adressen voor de bestemming HBase ZooKeeper-knooppunten moet configureren. Zie de sectie 'Twee virtuele netwerken configureren in dezelfde regio' in dit artikel voor het configureren van vaste IP-adres.

Voor het scenario voor cross-VNet, moet u de **- IP-** switch bij het aanroepen van de **hdi_enable_replication.sh** script in te grijpen.

## <a name="load-test-data"></a>Testgegevens laden

Wanneer u een cluster repliceert, moet u de tabellen te repliceren. In deze sectie wordt u sommige gegevens in de broncluster geladen. In de volgende sectie schakelt u replicatie tussen de twee clusters.

Volg de instructies in [HBase-zelfstudie: aan de slag met Apache HBase met Hadoop op basis van Linux in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) maken een **contactpersonen** tabel en sommige gegevens in de tabel invoegen.

## <a name="enable-replication"></a>Replicatie inschakelen

De volgende stappen laten zien hoe het script actiescript aanroepen vanuit de Azure-portal. Zie voor het uitvoeren van een scriptactie met behulp van Azure PowerShell en de Azure-opdrachtregelinterface (CLI), [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

**HBase-replicatie van de Azure-portal in te schakelen**

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Open de bron HBase-cluster.
3. Klik op het menu cluster **scriptacties**.
4. Klik op **nieuwe indienen** vanaf de bovenkant van de blade.
5. Selecteer of Voer de volgende informatie:

  - **Naam**: Voer **replicatie inschakelen**.
  - **Script-URL Bash**: Voer **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **HEAD**: geselecteerd. De knooppunttypen wissen.
  - **Parameters**: het volgende voorbeeld parameters replicatie inschakelen voor de bestaande tabellen en kopieer alle gegevens van de bron-cluster naar het doelcluster:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Klik op **Create**. Het script kan enige tijd duren, vooral wanneer het argument - copydata wordt gebruikt.

Vereiste argumenten:

|Naam|Beschrijving|
|----|-----------|
|-s,--src-cluster | Geef de DNS-naam van de bron HBase-cluster. Bijvoorbeeld: -s hbsrccluster,--src-cluster hbsrccluster = |
|-d,--zomertijd-cluster | Geef de DNS-naam van het doel (replica) HBase-cluster. Bijvoorbeeld: -s dsthbcluster,--src-cluster dsthbcluster = |
|-sp,--src-ambari-wachtwoord | Geef het beheerderswachtwoord voor Ambari op de bron HBase-cluster. |
|-dp,--zomertijd-ambari-wachtwoord | Geef het beheerderswachtwoord voor Ambari op de doelcluster HBase.|

Optionele argumenten:

|Naam|Beschrijving|
|----|-----------|
|-su,--src-ambari-gebruiker | Geef de gebruikersnaam van de beheerder voor Ambari op de bron HBase-cluster. De standaardwaarde is **admin**. |
|-du,--zomertijd-ambari-gebruiker | Geef de gebruikersnaam van de beheerder voor Ambari op de doelcluster HBase. De standaardwaarde is **admin**. |
|-t,--lijst van de tabel | Geef de tabellen worden gerepliceerd. Bijvoorbeeld:--tabel lijst = 'Tabel1; tabel2; Tabel3'. Als u geen tabellen opgeeft, worden alle bestaande HBase-tabellen gerepliceerd.|
|-m,--machine | Geef het hoofdknooppunt waar de scriptactie wordt uitgevoerd. De waarde is hn1 of hn0. Omdat hn0 meestal veelgebruikte is, wordt u aangeraden hn1. U kunt deze optie gebruiken als u het script $0 als de scriptactie van een van de HDInsight-portal of Azure PowerShell.|
|-ip | Dit argument is vereist als u bij het inschakelen van replicatie tussen twee virtuele netwerken. Dit argument fungeert als een overschakelen naar de statische IP-adressen van ZooKeeper-knooppunten uit replica clusters gebruiken in plaats van FQDN-namen. De statische IP-adressen moeten vooraf geconfigureerde voordat u replicatie inschakelt. |
|-cp - copydata | Schakel de migratie van bestaande gegevens op de tabellen waarvoor replicatie is ingeschakeld. |
|-rpm, -repliceren-phoenix-metagegevens | Replicatie inschakelen voor Phoenix systeemtabellen. <br><br>*Gebruik deze optie voorzichtig.* U wordt aangeraden Phoenix tabellen op de replica-clusters opnieuw te maken voordat u dit script gebruiken. |
|-h,--help | Gebruiksgegevens weergegeven. |

De sectie print_usage() van de [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) wordt een gedetailleerde beschrijving van parameters.

Nadat de scriptactie is geïmplementeerd, kunt u SSH verbinding maken met het doelcluster HBase en controleer of dat de gegevens zijn gerepliceerd.

### <a name="replication-scenarios"></a>Replicatie-scenario 's

De volgende lijst ziet u enkele gevallen algemeen gebruik en de bijbehorende parameterinstellingen:

- **Replicatie inschakelen voor alle tabellen tussen twee clusters**. Dit scenario is niet vereist voor de kopie/migratie van bestaande gegevens op de tabellen en gebruikt geen Phoenix tabellen. Gebruik de volgende parameters:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Replicatie inschakelen voor specifieke tabellen**. De volgende parameters gebruiken om replicatie van table1 en table2 Tabel3 in te schakelen:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Replicatie inschakelen voor specifieke tabellen en kopieer de bestaande gegevens**. De volgende parameters gebruiken om replicatie van table1 en table2 Tabel3 in te schakelen:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Replicatie inschakelen voor alle tabellen met het repliceren van phoenix metagegevens van bron naar doel**. Phoenix metagegevens replicatie is niet perfect en wees voorzichtig met moet worden ingeschakeld.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Kopiëren en gegevens migreren

Er zijn twee afzonderlijke script actie scripts voor het kopiëren van/migreren van gegevens na de replicatie is ingeschakeld:

- [Script voor kleine tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (enkele gigabytes in grootte en de algehele kopie is voltooid in minder dan een uur verwacht)

- [Script voor grote tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (verwachte langer duurt dan een uur kopiëren)

Kunt u dezelfde procedure in [replicatie inschakelen](#enable-replication) aanroepen van de scriptactie met de volgende parameters:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

De sectie print_usage() van de [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) bevat een gedetailleerde beschrijving van parameters.

### <a name="scenarios"></a>Scenario's

- **Kopiëren van specifieke tabellen (test1, test2 en test3) voor alle rijen bewerkt tot nu toe (huidige tijdstempel)**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  of

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Kopiëren van specifieke tabellen met een opgegeven tijdperiode**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Schakel replicatie uit

Als replicatie wilt uitschakelen, gebruikt u een ander script actiescript zich bevindt op [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). Kunt u dezelfde procedure in [replicatie inschakelen](#enable-replication) aanroepen van de scriptactie met de volgende parameters:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

De sectie print_usage() van de [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) wordt een gedetailleerde beschrijving van parameters.

### <a name="scenarios"></a>Scenario's

- **Schakel replicatie op alle tabellen**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  of

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Schakel replicatie op de opgegeven tabellen (Tabel1, tabel2 en Tabel3)**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe het configureren van HBase-replicatie tussen twee datacentra. Zie voor meer informatie over HDInsight en HBase:

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
