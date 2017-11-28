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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="af9fe-104">Verbinding maken met een Azure-netwerk maken tooKafka op HDInsight (preview)</span><span class="sxs-lookup"><span data-stu-id="af9fe-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="af9fe-105">Meer informatie over hoe toodirectly tooKafka op HDInsight met behulp van Azure Virtual Networks verbinding.</span><span class="sxs-lookup"><span data-stu-id="af9fe-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="af9fe-106">Dit document bevat informatie over verbinding maken met behulp van de volgende configuraties Hallo tooKafka:</span><span class="sxs-lookup"><span data-stu-id="af9fe-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="af9fe-107">Basis van resources in een on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-107">From resources in an on-premises network.</span></span> <span data-ttu-id="af9fe-108">Deze verbinding is gemaakt met behulp van een VPN-apparaat (software of hardware) op uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="af9fe-109">Met behulp van een VPN-software-client van een ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="af9fe-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="af9fe-110">Architectuur en planning</span><span class="sxs-lookup"><span data-stu-id="af9fe-110">Architecture and planning</span></span>

<span data-ttu-id="af9fe-111">HDInsight kan geen directe verbinding tooKafka via Hallo openbare internet.</span><span class="sxs-lookup"><span data-stu-id="af9fe-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="af9fe-112">Kafka-clients (producenten en consumenten) moeten in plaats daarvan een van de volgende verbindingsmethoden Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="af9fe-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="af9fe-113">Hallo-client wordt uitgevoerd in Hallo hetzelfde virtuele netwerk als Kafka op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af9fe-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="af9fe-114">Deze configuratie wordt gebruikt in Hallo [beginnen met Apache Kafka (preview) op HDInsight](hdinsight-apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="af9fe-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="af9fe-115">Hello rechtstreeks client wordt uitgevoerd op Hallo HDInsight clusterknooppunten of Hallo op een andere virtuele machine in hetzelfde netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="af9fe-116">Verbinding maken met een particulier netwerk, zoals uw on-premises netwerk, toohello virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="af9fe-117">Deze configuratie kan clients in uw lokale netwerk toodirectly werk met Kafka.</span><span class="sxs-lookup"><span data-stu-id="af9fe-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="af9fe-118">tooenable deze configuratie Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="af9fe-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="af9fe-119">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="af9fe-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="af9fe-120">Maak een VPN-gateway die gebruikmaakt van een site-naar-site-configuratie.</span><span class="sxs-lookup"><span data-stu-id="af9fe-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="af9fe-121">Hallo-configuratie gebruikt in dit document verbindt tooa VPN-gateway-apparaat in uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="af9fe-122">Maak een DNS-server in het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="af9fe-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="af9fe-123">Configureren van forwarding tussen Hallo DNS-server in elk netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="af9fe-124">Installeer Kafka op HDInsight in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="af9fe-125">Zie voor meer informatie, Hallo [tooKafka verbinding van een on-premises netwerk](#on-premises) sectie.</span><span class="sxs-lookup"><span data-stu-id="af9fe-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="af9fe-126">Verbinding maken met een afzonderlijke machines toohello virtueel netwerk via een VPN-gateway en de VPN-client.</span><span class="sxs-lookup"><span data-stu-id="af9fe-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="af9fe-127">tooenable deze configuratie Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="af9fe-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="af9fe-128">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="af9fe-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="af9fe-129">Maak een VPN-gateway die gebruikmaakt van een punt-naar-site-configuratie.</span><span class="sxs-lookup"><span data-stu-id="af9fe-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="af9fe-130">Deze configuratie biedt een VPN-client die kan worden geïnstalleerd op Windows-clients.</span><span class="sxs-lookup"><span data-stu-id="af9fe-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="af9fe-131">Installeer Kafka op HDInsight in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="af9fe-132">Kafka voor IP-reclame configureren.</span><span class="sxs-lookup"><span data-stu-id="af9fe-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="af9fe-133">Deze configuratie kunt Hallo client tooconnect met IP-adressen in plaats van domeinnamen.</span><span class="sxs-lookup"><span data-stu-id="af9fe-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="af9fe-134">Download en gebruik Hallo VPN-client op Hallo-ontwikkelsysteem.</span><span class="sxs-lookup"><span data-stu-id="af9fe-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="af9fe-135">Zie voor meer informatie, Hallo [tooKafka verbinden met een VPN-client](#vpnclient) sectie.</span><span class="sxs-lookup"><span data-stu-id="af9fe-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="af9fe-136">Deze configuratie wordt alleen aanbevolen voor ontwikkelingsdoeleinden vanwege Hallo volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="af9fe-137">Elke client moet verbinding maken met behulp van een VPN-software-client.</span><span class="sxs-lookup"><span data-stu-id="af9fe-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="af9fe-138">Azure biedt alleen een Windows-client.</span><span class="sxs-lookup"><span data-stu-id="af9fe-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="af9fe-139">Hallo-client geeft niet de naam resolutie aanvragen toohello virtueel netwerk, zodat u de IP-adressering toocommunicate met Kafka moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="af9fe-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="af9fe-140">IP-communicatie vereist aanvullende configuratiestappen op Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="af9fe-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="af9fe-141">Zie voor meer informatie over het gebruik van HDInsight in een virtueel netwerk [HDInsight uitbreiden met behulp van Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="af9fe-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="af9fe-142"><a id="on-premises"></a>TooKafka vanaf een on-premises netwerk verbinding maken</span><span class="sxs-lookup"><span data-stu-id="af9fe-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="af9fe-143">een cluster Kafka die met uw on-premises netwerk communiceert toocreate Hallo stappen in Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](./connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="af9fe-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af9fe-144">Wanneer u Hallo HDInsight-cluster maakt, selecteert u Hallo __Kafka__ type cluster.</span><span class="sxs-lookup"><span data-stu-id="af9fe-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="af9fe-145">Deze stappen maken Hallo na configuratie:</span><span class="sxs-lookup"><span data-stu-id="af9fe-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="af9fe-146">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="af9fe-146">Azure Virtual Network</span></span>
* <span data-ttu-id="af9fe-147">Site-naar-site VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="af9fe-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="af9fe-148">Azure Storage-account (gebruikt door HDInsight)</span><span class="sxs-lookup"><span data-stu-id="af9fe-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="af9fe-149">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="af9fe-149">Kafka on HDInsight</span></span>

<span data-ttu-id="af9fe-150">tooverify dat een client Kafka toohello cluster on-premises, gebruik Hallo stappen in Hallo verbinding kan maken [voorbeeld:-client voor Python](#python-client) sectie.</span><span class="sxs-lookup"><span data-stu-id="af9fe-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="af9fe-151"><a id="vpnclient"></a>TooKafka verbinden met een VPN-client</span><span class="sxs-lookup"><span data-stu-id="af9fe-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="af9fe-152">Gebruik Hallo stappen in deze sectie toocreate Hallo volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="af9fe-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="af9fe-153">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="af9fe-153">Azure Virtual Network</span></span>
* <span data-ttu-id="af9fe-154">Punt-naar-site VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="af9fe-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="af9fe-155">Azure Storage-Account (gebruikt door HDInsight)</span><span class="sxs-lookup"><span data-stu-id="af9fe-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="af9fe-156">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="af9fe-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="af9fe-157">Volg de stappen Hallo in Hallo [werken met zelfondertekende certificaten voor punt-naar-site-verbindingen](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span><span class="sxs-lookup"><span data-stu-id="af9fe-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="af9fe-158">Dit document maakt Hallo-certificaten die nodig zijn voor het Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="af9fe-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="af9fe-159">Open een PowerShell-prompt en gebruik Hallo code toolog in tooyour Azure-abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="af9fe-160">Gebruik Hallo volgende code toocreate variabelen die configuratie-informatie bevatten:</span><span class="sxs-lookup"><span data-stu-id="af9fe-160">Use hello following code toocreate variables that contain configuration information:</span></span>

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

4. <span data-ttu-id="af9fe-161">Gebruik Hallo volgende code toocreate hello Azure-resourcegroep en virtuele netwerken:</span><span class="sxs-lookup"><span data-stu-id="af9fe-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

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
    > <span data-ttu-id="af9fe-162">Het kan enkele minuten duren voordat dit proces toocomplete.</span><span class="sxs-lookup"><span data-stu-id="af9fe-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="af9fe-163">Gebruik Hallo code toocreate hello Azure Storage-Account en de blob-container te volgen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

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

6. <span data-ttu-id="af9fe-164">Gebruik Hallo code toocreate hello HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

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
  > <span data-ttu-id="af9fe-165">Dit proces duurt ongeveer 20 minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="af9fe-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="af9fe-166">Hallo cmdlet tooretrieve Hallo-URL voor Hallo Windows VPN-client voor het virtuele netwerk Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="af9fe-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="af9fe-167">toodownload hello Windows VPN-client gebruik Hallo geretourneerd URI in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="af9fe-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="af9fe-168">Kafka configureren voor IP-advertenties</span><span class="sxs-lookup"><span data-stu-id="af9fe-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="af9fe-169">Standaard retourneert Zookeeper domeinnaam Hallo Hallo Kafka beleggingsmakelaars tooclients.</span><span class="sxs-lookup"><span data-stu-id="af9fe-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="af9fe-170">Deze configuratie werkt niet met Hallo VPN-software-client, zoals naamomzetting voor entiteiten in Hallo virtueel netwerk niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="af9fe-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="af9fe-171">Voor deze configuratie gebruikt Hallo volgende stappen tooconfigure Kafka tooadvertise IP-adressen in plaats van domeinnamen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="af9fe-172">Ga in een webbrowser toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="af9fe-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="af9fe-173">Vervang __CLUSTERNAME__ met de naam van de Hallo Hallo Kafka op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="af9fe-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="af9fe-174">Wanneer u wordt gevraagd, Hallo HTTPS-gebruikersnaam en wachtwoord voor Hallo cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="af9fe-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="af9fe-175">Hallo Ambari-Webgebruikersinterface voor Hallo cluster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af9fe-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="af9fe-176">Selecteer tooview informatie over Kafka, __Kafka__ in de lijst Hallo op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="af9fe-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Lijst met Kafka service gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="af9fe-178">tooview Kafka-configuratie, selecteer __Configs__ uit Hallo bovenste midden.</span><span class="sxs-lookup"><span data-stu-id="af9fe-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Koppelingen naar de configuraties voor Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="af9fe-180">Hallo toofind __kafka env__ configuratie, voer `kafka-env` in Hallo __Filter__ op Hallo rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="af9fe-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Kafka-configuratie voor kafka env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="af9fe-182">tooconfigure Kafka tooadvertise IP-adressen, toevoegen na de tekst toohello onderaan Hallo Hallo __kafka-env-sjabloon__ veld:</span><span class="sxs-lookup"><span data-stu-id="af9fe-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="af9fe-183">tooconfigure hello interface die Kafka luistert op, geef `listeners` in Hallo __Filter__ op Hallo rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="af9fe-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="af9fe-184">tooconfigure Kafka toolisten op alle netwerkinterfaces, Hallo waarde wijzigen in Hallo __listeners__ veld te`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="af9fe-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="af9fe-185">Hallo configuratiewijzigingen toosave gebruiken Hallo __opslaan__ knop.</span><span class="sxs-lookup"><span data-stu-id="af9fe-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="af9fe-186">Voer een SMS-bericht met een beschrijving van Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="af9fe-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="af9fe-187">Selecteer __OK__ zodra Hallo wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="af9fe-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Configuratie knop Opslaan](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="af9fe-189">tooprevent fouten bij het opnieuw opstarten Kafka, gebruik Hallo __serviceacties__ en selecteer __inschakelen op onderhoudsmodus__.</span><span class="sxs-lookup"><span data-stu-id="af9fe-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="af9fe-190">Selecteer OK toocomplete deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="af9fe-190">Select OK toocomplete this operation.</span></span>

    ![Service-acties, met inschakelen onderhoud gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="af9fe-192">toorestart Kafka, gebruik Hallo __opnieuw__ en selecteer __start opnieuw alle van invloed op een__.</span><span class="sxs-lookup"><span data-stu-id="af9fe-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="af9fe-193">Bevestig Hallo opnieuw opstarten en gebruik vervolgens Hallo __OK__ knop nadat Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="af9fe-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Start opnieuw op de knop met alle van invloed op een opnieuw opstarten gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="af9fe-195">Onderhoudsmodus toodisable, gebruik Hallo __serviceacties__ en selecteer __inschakelen uit onderhoudsmodus__.</span><span class="sxs-lookup"><span data-stu-id="af9fe-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="af9fe-196">Selecteer **OK** toocomplete deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="af9fe-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="af9fe-197">Verbinding maken met toohello VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="af9fe-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="af9fe-198">tooconnect toohello VPN-gateway van een __Windows-client__, gebruik Hallo __verbinding tooAzure__ sectie Hallo [een punt-naar-Site-verbinding configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span><span class="sxs-lookup"><span data-stu-id="af9fe-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="af9fe-199"><a id="python-client"></a>Voorbeeld:-Client voor Python</span><span class="sxs-lookup"><span data-stu-id="af9fe-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="af9fe-200">toovalidate connectiviteit tooKafka, Hallo toocreate stappen te volgen en voer een Python producenten en consumenten:</span><span class="sxs-lookup"><span data-stu-id="af9fe-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="af9fe-201">Gebruik Hallo na methoden tooretrieve Hallo volledig gekwalificeerde domeinnaam (FQDN) en IP-adressen van de knooppunten Hallo in Hallo Kafka-cluster:</span><span class="sxs-lookup"><span data-stu-id="af9fe-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="af9fe-202">Dit script wordt ervan uitgegaan dat `$resourceGroupName` Hallo naam is van hello Azure-resourcegroep met Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="af9fe-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="af9fe-203">Sla Hallo informatie voor gebruik in de volgende stappen Hallo geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="af9fe-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="af9fe-204">Gebruik Hallo na tooinstall hello [kafka python](http://kafka-python.readthedocs.io/) client:</span><span class="sxs-lookup"><span data-stu-id="af9fe-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="af9fe-205">toosend gegevens tooKafka gebruik Hallo Python-code te volgen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="af9fe-206">Vervang Hallo `'kafka_broker'` vermeldingen met hello-mailadressen geretourneerd uit stap 1 in deze sectie:</span><span class="sxs-lookup"><span data-stu-id="af9fe-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="af9fe-207">Als u een __Software VPN-client__, vervang Hallo `kafka_broker` vermeldingen met Hallo IP-adres van uw worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="af9fe-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="af9fe-208">Als u hebt __naamomzetting via een aangepaste DNS-server ingeschakeld__, vervang Hallo `kafka_broker` vermeldingen met Hallo FQDN-naam van Hallo worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="af9fe-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af9fe-209">Deze code verzendt Hallo tekenreeks `test message` toohello onderwerp `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="af9fe-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="af9fe-210">Hallo-standaardconfiguratie van Kafka op HDInsight is toocreate Hallo onderwerp als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="af9fe-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="af9fe-211">Hallo-berichten tooretrieve van Kafka, gebruik Hallo Python-code te volgen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

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

    <span data-ttu-id="af9fe-212">Vervang Hallo `'kafka_broker'` vermeldingen met hello-mailadressen geretourneerd uit stap 1 in deze sectie:</span><span class="sxs-lookup"><span data-stu-id="af9fe-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="af9fe-213">Als u een __Software VPN-client__, vervang Hallo `kafka_broker` vermeldingen met Hallo IP-adres van uw worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="af9fe-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="af9fe-214">Als u hebt __naamomzetting via een aangepaste DNS-server ingeschakeld__, vervang Hallo `kafka_broker` vermeldingen met Hallo FQDN-naam van Hallo worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="af9fe-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af9fe-215">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af9fe-215">Next steps</span></span>

<span data-ttu-id="af9fe-216">Zie voor meer informatie over het gebruik van HDInsight met een virtueel netwerk Hallo [uitbreiden Azure HDInsight met behulp van een Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="af9fe-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="af9fe-217">Zie voor meer informatie over het maken van een Azure-netwerk met punt-naar-Site VPN-gateway Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="af9fe-218">Een punt-naar-Site-verbinding met hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="af9fe-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="af9fe-219">Configureren van een punt-naar-Site-verbinding met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="af9fe-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="af9fe-220">Zie voor meer informatie over het werken met Kafka op HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="af9fe-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="af9fe-221">Aan de slag met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="af9fe-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="af9fe-222">Mirroring met Kafka in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="af9fe-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
