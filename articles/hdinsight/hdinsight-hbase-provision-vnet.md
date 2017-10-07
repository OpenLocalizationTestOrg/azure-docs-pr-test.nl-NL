---
title: aaaCreate HBase-clusters in een virtueel netwerk - Azure | Microsoft Docs
description: Aan de slag met HBase in Azure HDInsight. Meer informatie over hoe toocreate HDInsight HBase-clusters op Azure Virtual Network.
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>HBase-clusters maken in HDInsight in Azure Virtual Network
Meer informatie over hoe toocreate Azure HDInsight HBase-clusters in een [Azure Virtual Network][1].

Aan de integratie van virtueel netwerk, HBase-clusters geïmplementeerde toohello virtuele netwerk als uw toepassingen zodat kunnen worden toepassingen rechtstreeks met HBase kunnen communiceren. Hallo voordelen zijn:

* Directe verbinding Hallo web application toohello knooppunten van de HBase-cluster hello, waarmee communicatie via externe procedureaanroepen HBase Java call (RPC) API's.
* Verbeterde prestaties omdat u niet hoeft uw verkeer Ga via meerdere gateways en load balancers.
* Hallo mogelijkheid tooprocess gevoelige informatie op een veiliger manier zonder een openbaar eindpunt bloot te stellen.

### <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Een werkstation met Azure PowerShell**. Zie [installeren en gebruiken Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>HBase-cluster in virtueel netwerk maken
In deze sectie maakt u een Linux-gebaseerde HBase-cluster maken met Hallo afhankelijke Azure Storage-account aan een virtuele Azure-netwerk met een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md). Voor andere methoden voor het maken van cluster en inzicht Hallo-instellingen, Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md). Zie voor meer informatie over het gebruik van een sjabloon toocreate Hadoop-clusters in HDInsight, [maken Hadoop-clusters in HDInsight met behulp van Azure Resource Manager-sjablonen](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Sommige eigenschappen zijn hardgecodeerd in Hallo-sjabloon. Bijvoorbeeld:
>
> * **Locatie**: VS-Oost 2
> * **Clusterversie**: 3.5
> * **Aantal worker-knooppunten cluster**: 2
> * **Storage-account standaard**: een unieke tekenreeks
> * **Virtuele-netwerknaam**: &lt;Clusternaam >-vnet
> * **Adresruimte voor virtueel netwerk**: 10.0.0.0/16
> * **De subnetnaam van het**: subnet1
> * **Adresbereik van**: 10.0.0.0/24
>
> &lt;Clusternaam > is vervangen door de clusternaam Hallo u opgeven wanneer Hallo-sjabloon gebruikt.
>
>

1. Klik op Hallo installatiekopie tooopen Hallo sjabloon in hello Azure-portal te volgen. Hallo-sjabloon bevindt zich in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Van Hallo **aangepaste implementatie** blade Voer Hallo volgende eigenschappen:

   * **Abonnement**: Selecteer een Azure-abonnement gebruikt toocreate hello HDInsight-cluster, Hallo afhankelijke opslagaccount en Hallo virtuele Azure-netwerk.
   * **Resourcegroep**: Selecteer **nieuw**, en geef een nieuwe Resourcegroepnaam.
   * **Locatie**: Selecteer een locatie voor resourcegroep Hallo.
   * **Clusternaam**: Voer een naam voor Hallo Hadoop-cluster toobe gemaakt.
   * **Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is **admin**.
   * **SSH-gebruikersnaam en wachtwoord**: de standaardgebruikersnaam Hallo **sshuser**.  U kunt de naam wijzigen.
   * **Ik ga akkoord toohello voorwaarden Hallo hierboven**: (selecteren)
3. Klik op **Kopen**. Het duurt ongeveer 20 minuten toocreate een cluster. Zodra het Hallo-cluster is gemaakt, klikt u op Hallo cluster-blade in de portal tooopen Hallo deze.

Nadat u Hallo-zelfstudie hebt voltooid, kunt u toodelete Hallo-cluster. Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt. Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt. Aangezien Hallo kosten voor Hallo cluster vaak zoveel hoger zijn dan Hallo kosten voor opslag, is het financieel aantrekkelijk toodelete clusters wanneer ze zich niet in gebruik. Zie voor instructies van het verwijderen van een cluster Hallo [beheren Hadoop-clusters in HDInsight met behulp van Azure-portal Hallo](hdinsight-administer-use-management-portal.md#delete-clusters).

toobegin werken met uw nieuwe HBase-cluster, kunt u Hallo procedures gevonden in [aan de slag met HBase met Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Verbinding maken met toohello HBase-cluster met HBase Java RPC-API 's
1. Maken van een infrastructuur als een dienst (IaaS) virtuele machine in hetzelfde virtuele Azure-netwerk Hallo en Hallo hetzelfde subnet. Zie voor instructies over het maken van een nieuwe virtuele machine voor IaaS [maken van een virtuele Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Wanneer Hallo stappen in dit document uitvoert, moet u de volgende waarden voor de netwerkconfiguratie Hallo Hallo gebruiken:

   * **Virtueel netwerk**: &lt;Clusternaam >-vnet
   * **Subnet**: subnet1

   > [!IMPORTANT]
   > Vervang &lt;Clusternaam > met Hallo-naam die u hebt gebruikt bij het maken van Hallo HDInsight-cluster in de vorige stappen.
   >
   >

   Met deze waarden, Hallo virtuele machine wordt geplaatst in Hallo hetzelfde virtuele netwerk en subnet als Hallo HDInsight-cluster. Deze configuratie kan ze toodirectly met elkaar communiceren. Er is een toocreate manier een HDInsight-cluster met een leeg edge-knooppunt. Hallo edge-knooppunt kan worden gebruikt toomanage Hallo-cluster.  Zie voor meer informatie [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).

2. Wanneer u een Java-toepassing tooconnect tooHBase op afstand gebruikt, moet u Hallo volledig gekwalificeerde domeinnaam (FQDN). toodetermine, moet u Hallo verbindingsspecifieke DNS-achtervoegsel van de HBase-cluster Hallo ophalen. toodo, kunt u een van de volgende methoden hello gebruiken:

   * Een Web browser toomake een oproep Ambari gebruiken:

     Blader toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / als host fungeert voor? minimal_response = true. Hiermee schakelt u een JSON-bestand met Hallo DNS-achtervoegsels.
   * Gebruik Hallo Ambari-website:

     1. Te bladeren https://&lt;ClusterName >. azurehdinsight.net.
     2. Klik op **Hosts** in het bovenste menu Hallo.
   * Gebruik Curl toomake REST-aanroepen:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     Hallo JSON JavaScript Object Notation ()-gegevens geretourneerd, Hallo 'hostnaam' vermelding te vinden. Het bevat Hallo FQDN voor Hallo knooppunten in cluster Hallo. Bijvoorbeeld:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     Hallo-gedeelte van Hallo domein naam die begint met de naam van de cluster Hallo is Hallo DNS-achtervoegsel. Bijvoorbeeld: mycluster.b1.cloudapp.net.
   * Azure PowerShell gebruiken

     Gebruik hello Azure PowerShell-script tooregister Hallo na **Get-ClusterDetail** functie, die gebruikt tooreturn Hallo DNS-achtervoegsel worden kan:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Na het actieve hello Azure PowerShell-script gebruik Hallo volgende tooreturn Hallo DNS-achtervoegsel opdracht met behulp van Hallo **Get-ClusterDetail** functie. Geef uw naam van HDInsight HBase-cluster, naam van de serverbeheerder en beheerderswachtwoord wanneer u deze opdracht.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Deze opdracht retourneert Hallo DNS-achtervoegsel. Bijvoorbeeld: **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify die virtuele machine Hallo kan communiceren met de Hallo HBase-cluster, gebruikt u Hallo opdracht `ping headnode0.<dns suffix>` van Hallo virtuele machine. Bijvoorbeeld: ping headnode0.mycluster.b1.cloudapp.net.

toouse deze informatie in een Java-toepassing en u kunt stappen Hallo in [Maven gebruiken toobuild Java-toepassingen die gebruikmaken van HBase met HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate een toepassing. toohave hello toepassing tooa externe HBase-server verbinding kan maken, wijzigen Hallo **hbase-site.xml** bestand in dit voorbeeld toouse Hallo FQDN voor Zookeeper. Bijvoorbeeld:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Voor meer informatie over naamomzetting in virtuele netwerken in Azure, met inbegrip van hoe toouse uw eigen DNS-server, Zie [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toocreate een HBase-cluster. toolearn meer, Zie:

* [Aan de slag met HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Lege edge-knooppunten in HDInsight gebruiken](hdinsight-apps-use-edge-node.md)
* [HBase-replicatie in HDInsight configureren](hdinsight-hbase-replication.md)
* [Hadoop-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Aan de slag met HBase met Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md)
* [Twitter-gevoel met HBase in HDInsight analyseren](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Overzicht van Virtual Network][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Details voor de nieuwe HBase-cluster Hallo inrichten"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Scriptactie toocustomize een HBase-cluster gebruiken"

[azure-preview-portal]: https://portal.azure.com
