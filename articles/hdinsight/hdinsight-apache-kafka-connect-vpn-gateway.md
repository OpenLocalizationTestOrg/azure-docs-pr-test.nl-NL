---
title: aaaConnect tooKafka met virtuele netwerken - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toodirectly tooKafka op HDInsight verbinden via een virtueel netwerk van Azure. Meer informatie over hoe tooconnect tooKafka van ontwikkeling-clients met behulp van een VPN-gateway of van clients in uw on-premises netwerk via een VPN-gateway-apparaat.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Verbinding maken met een Azure-netwerk maken tooKafka op HDInsight (preview)

Meer informatie over hoe toodirectly tooKafka op HDInsight met behulp van Azure Virtual Networks verbinding. Dit document bevat informatie over verbinding maken met behulp van de volgende configuraties Hallo tooKafka:

* Basis van resources in een on-premises netwerk. Deze verbinding is gemaakt met behulp van een VPN-apparaat (software of hardware) op uw lokale netwerk.
* Met behulp van een VPN-software-client van een ontwikkelomgeving.

## <a name="architecture-and-planning"></a>Architectuur en planning

HDInsight kan geen directe verbinding tooKafka via Hallo openbare internet. Kafka-clients (producenten en consumenten) moeten in plaats daarvan een van de volgende verbindingsmethoden Hallo gebruiken:

* Hallo-client wordt uitgevoerd in Hallo hetzelfde virtuele netwerk als Kafka op HDInsight. Deze configuratie wordt gebruikt in Hallo [beginnen met Apache Kafka (preview) op HDInsight](hdinsight-apache-kafka-get-started.md) document. Hello rechtstreeks client wordt uitgevoerd op Hallo HDInsight clusterknooppunten of Hallo op een andere virtuele machine in hetzelfde netwerk.

* Verbinding maken met een particulier netwerk, zoals uw on-premises netwerk, toohello virtueel netwerk. Deze configuratie kan clients in uw lokale netwerk toodirectly werk met Kafka. tooenable deze configuratie Hallo volgende taken uitvoeren:

    1. Een virtueel netwerk maken.
    2. Maak een VPN-gateway die gebruikmaakt van een site-naar-site-configuratie. Hallo-configuratie gebruikt in dit document verbindt tooa VPN-gateway-apparaat in uw on-premises netwerk.
    3. Maak een DNS-server in het virtuele netwerk Hallo.
    4. Configureren van forwarding tussen Hallo DNS-server in elk netwerk.
    5. Installeer Kafka op HDInsight in Hallo virtueel netwerk.

    Zie voor meer informatie, Hallo [tooKafka verbinding van een on-premises netwerk](#on-premises) sectie. 

* Verbinding maken met een afzonderlijke machines toohello virtueel netwerk via een VPN-gateway en de VPN-client. tooenable deze configuratie Hallo volgende taken uitvoeren:

    1. Een virtueel netwerk maken.
    2. Maak een VPN-gateway die gebruikmaakt van een punt-naar-site-configuratie. Deze configuratie biedt een VPN-client die kan worden geïnstalleerd op Windows-clients.
    3. Installeer Kafka op HDInsight in Hallo virtueel netwerk.
    4. Kafka voor IP-reclame configureren. Deze configuratie kunt Hallo client tooconnect met IP-adressen in plaats van domeinnamen.
    5. Download en gebruik Hallo VPN-client op Hallo-ontwikkelsysteem.

    Zie voor meer informatie, Hallo [tooKafka verbinden met een VPN-client](#vpnclient) sectie.

    > [!WARNING]
    > Deze configuratie wordt alleen aanbevolen voor ontwikkelingsdoeleinden vanwege Hallo volgende beperkingen:
    >
    > * Elke client moet verbinding maken met behulp van een VPN-software-client. Azure biedt alleen een Windows-client.
    > * Hallo-client geeft niet de naam resolutie aanvragen toohello virtueel netwerk, zodat u de IP-adressering toocommunicate met Kafka moet gebruiken. IP-communicatie vereist aanvullende configuratiestappen op Hallo Kafka-cluster.

Zie voor meer informatie over het gebruik van HDInsight in een virtueel netwerk [HDInsight uitbreiden met behulp van Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>TooKafka vanaf een on-premises netwerk verbinding maken

een cluster Kafka die met uw on-premises netwerk communiceert toocreate Hallo stappen in Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](./connect-on-premises-network.md) document.

> [!IMPORTANT]
> Wanneer u Hallo HDInsight-cluster maakt, selecteert u Hallo __Kafka__ type cluster.

Deze stappen maken Hallo na configuratie:

* Azure Virtual Network
* Site-naar-site VPN-gateway
* Azure Storage-account (gebruikt door HDInsight)
* Kafka in HDInsight

tooverify dat een client Kafka toohello cluster on-premises, gebruik Hallo stappen in Hallo verbinding kan maken [voorbeeld:-client voor Python](#python-client) sectie.

## <a id="vpnclient"></a>TooKafka verbinden met een VPN-client

Gebruik Hallo stappen in deze sectie toocreate Hallo volgende configuratie:

* Azure Virtual Network
* Punt-naar-site VPN-gateway
* Azure Storage-Account (gebruikt door HDInsight)
* Kafka in HDInsight

1. Volg de stappen Hallo in Hallo [werken met zelfondertekende certificaten voor punt-naar-site-verbindingen](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document. Dit document maakt Hallo-certificaten die nodig zijn voor het Hallo-gateway.

2. Open een PowerShell-prompt en gebruik Hallo code toolog in tooyour Azure-abonnement te volgen:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Gebruik Hallo volgende code toocreate variabelen die configuratie-informatie bevatten:

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. Gebruik Hallo volgende code toocreate hello Azure-resourcegroep en virtuele netwerken:

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > Het kan enkele minuten duren voordat dit proces toocomplete.

5. Gebruik Hallo code toocreate hello Azure Storage-Account en de blob-container te volgen:

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. Gebruik Hallo code toocreate hello HDInsight-cluster te volgen:

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > Dit proces duurt ongeveer 20 minuten toocomplete.

8. Hallo cmdlet tooretrieve Hallo-URL voor Hallo Windows VPN-client voor het virtuele netwerk Hallo volgende gebruiken:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    toodownload hello Windows VPN-client gebruik Hallo geretourneerd URI in uw webbrowser.

### <a name="configure-kafka-for-ip-advertising"></a>Kafka configureren voor IP-advertenties

Standaard retourneert Zookeeper domeinnaam Hallo Hallo Kafka beleggingsmakelaars tooclients. Deze configuratie werkt niet met Hallo VPN-software-client, zoals naamomzetting voor entiteiten in Hallo virtueel netwerk niet kiezen. Voor deze configuratie gebruikt Hallo volgende stappen tooconfigure Kafka tooadvertise IP-adressen in plaats van domeinnamen:

1. Ga in een webbrowser toohttps://CLUSTERNAME.azurehdinsight.net. Vervang __CLUSTERNAME__ met de naam van de Hallo Hallo Kafka op HDInsight-cluster.

    Wanneer u wordt gevraagd, Hallo HTTPS-gebruikersnaam en wachtwoord voor Hallo cluster gebruiken. Hallo Ambari-Webgebruikersinterface voor Hallo cluster wordt weergegeven.

2. Selecteer tooview informatie over Kafka, __Kafka__ in de lijst Hallo op Hallo links.

    ![Lijst met Kafka service gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. tooview Kafka-configuratie, selecteer __Configs__ uit Hallo bovenste midden.

    ![Koppelingen naar de configuraties voor Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. Hallo toofind __kafka env__ configuratie, voer `kafka-env` in Hallo __Filter__ op Hallo rechtsboven.

    ![Kafka-configuratie voor kafka env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. tooconfigure Kafka tooadvertise IP-adressen, toevoegen na de tekst toohello onderaan Hallo Hallo __kafka-env-sjabloon__ veld:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. tooconfigure hello interface die Kafka luistert op, geef `listeners` in Hallo __Filter__ op Hallo rechtsboven.

7. tooconfigure Kafka toolisten op alle netwerkinterfaces, Hallo waarde wijzigen in Hallo __listeners__ veld te`PLAINTEXT://0.0.0.0:9092`.

8. Hallo configuratiewijzigingen toosave gebruiken Hallo __opslaan__ knop. Voer een SMS-bericht met een beschrijving van Hallo wijzigingen. Selecteer __OK__ zodra Hallo wijzigingen zijn opgeslagen.

    ![Configuratie knop Opslaan](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. tooprevent fouten bij het opnieuw opstarten Kafka, gebruik Hallo __serviceacties__ en selecteer __inschakelen op onderhoudsmodus__. Selecteer OK toocomplete deze bewerking.

    ![Service-acties, met inschakelen onderhoud gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, gebruik Hallo __opnieuw__ en selecteer __start opnieuw alle van invloed op een__. Bevestig Hallo opnieuw opstarten en gebruik vervolgens Hallo __OK__ knop nadat Hallo-bewerking is voltooid.

    ![Start opnieuw op de knop met alle van invloed op een opnieuw opstarten gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. Onderhoudsmodus toodisable, gebruik Hallo __serviceacties__ en selecteer __inschakelen uit onderhoudsmodus__. Selecteer **OK** toocomplete deze bewerking.

### <a name="connect-toohello-vpn-gateway"></a>Verbinding maken met toohello VPN-gateway

tooconnect toohello VPN-gateway van een __Windows-client__, gebruik Hallo __verbinding tooAzure__ sectie Hallo [een punt-naar-Site-verbinding configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.

## <a id="python-client"></a>Voorbeeld:-Client voor Python

toovalidate connectiviteit tooKafka, Hallo toocreate stappen te volgen en voer een Python producenten en consumenten:

1. Gebruik Hallo na methoden tooretrieve Hallo volledig gekwalificeerde domeinnaam (FQDN) en IP-adressen van de knooppunten Hallo in Hallo Kafka-cluster:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    Dit script wordt ervan uitgegaan dat `$resourceGroupName` Hallo naam is van hello Azure-resourcegroep met Hallo virtueel netwerk.

    Sla Hallo informatie voor gebruik in de volgende stappen Hallo geretourneerd.

2. Gebruik Hallo na tooinstall hello [kafka python](http://kafka-python.readthedocs.io/) client:

        pip install kafka-python

3. toosend gegevens tooKafka gebruik Hallo Python-code te volgen:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Vervang Hallo `'kafka_broker'` vermeldingen met hello-mailadressen geretourneerd uit stap 1 in deze sectie:

    * Als u een __Software VPN-client__, vervang Hallo `kafka_broker` vermeldingen met Hallo IP-adres van uw worker-knooppunten.

    * Als u hebt __naamomzetting via een aangepaste DNS-server ingeschakeld__, vervang Hallo `kafka_broker` vermeldingen met Hallo FQDN-naam van Hallo worker-knooppunten.

    > [!NOTE]
    > Deze code verzendt Hallo tekenreeks `test message` toohello onderwerp `testtopic`. Hallo-standaardconfiguratie van Kafka op HDInsight is toocreate Hallo onderwerp als deze niet bestaat.

4. Hallo-berichten tooretrieve van Kafka, gebruik Hallo Python-code te volgen:

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    Vervang Hallo `'kafka_broker'` vermeldingen met hello-mailadressen geretourneerd uit stap 1 in deze sectie:

    * Als u een __Software VPN-client__, vervang Hallo `kafka_broker` vermeldingen met Hallo IP-adres van uw worker-knooppunten.

    * Als u hebt __naamomzetting via een aangepaste DNS-server ingeschakeld__, vervang Hallo `kafka_broker` vermeldingen met Hallo FQDN-naam van Hallo worker-knooppunten.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van HDInsight met een virtueel netwerk Hallo [uitbreiden Azure HDInsight met behulp van een Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.

Zie voor meer informatie over het maken van een Azure-netwerk met punt-naar-Site VPN-gateway Hallo documenten te volgen:

* [Een punt-naar-Site-verbinding met hello Azure-portal configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Configureren van een punt-naar-Site-verbinding met Azure PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Zie voor meer informatie over het werken met Kafka op HDInsight Hallo documenten te volgen:

* [Aan de slag met Kafka in HDInsight](hdinsight-apache-kafka-get-started.md)
* [Mirroring met Kafka in HDInsight gebruiken](hdinsight-apache-kafka-mirroring.md)
