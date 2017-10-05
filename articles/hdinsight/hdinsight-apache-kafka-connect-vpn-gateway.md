---
title: Verbinding maken met virtuele netwerken - Azure HDInsight met Kafka | Microsoft Docs
description: Informatie over het rechtstreeks verbinding maken met Kafka in HDInsight via een virtueel netwerk van Azure. Informatie over het verbinden met Kafka van ontwikkeling clients met behulp van een VPN-gateway of van clients in uw on-premises netwerk via een VPN-gateway-apparaat.
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="eba2b-104">Verbinding maken met Kafka op HDInsight (preview) via een virtueel Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="eba2b-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="eba2b-105">Informatie over het rechtstreeks verbinding maken met Kafka op HDInsight met behulp van Azure Virtual Networks.</span><span class="sxs-lookup"><span data-stu-id="eba2b-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="eba2b-106">Dit document bevat informatie over verbinding maken met Kafka met behulp van de volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="eba2b-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="eba2b-107">Basis van resources in een on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-107">From resources in an on-premises network.</span></span> <span data-ttu-id="eba2b-108">Deze verbinding is gemaakt met behulp van een VPN-apparaat (software of hardware) op uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="eba2b-109">Met behulp van een VPN-software-client van een ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="eba2b-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="eba2b-110">Architectuur en planning</span><span class="sxs-lookup"><span data-stu-id="eba2b-110">Architecture and planning</span></span>

<span data-ttu-id="eba2b-111">HDInsight kan geen directe verbinding met Kafka via het openbare internet.</span><span class="sxs-lookup"><span data-stu-id="eba2b-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="eba2b-112">Kafka-clients (producenten en consumenten) moeten in plaats daarvan een van de volgende verbindingsmethoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="eba2b-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="eba2b-113">Voer de client in hetzelfde virtuele netwerk als Kafka op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eba2b-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="eba2b-114">Deze configuratie wordt gebruikt in de [beginnen met Apache Kafka (preview) op HDInsight](hdinsight-apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="eba2b-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="eba2b-115">De client voert rechtstreeks op de clusterknooppunten HDInsight of op een andere virtuele machine in hetzelfde netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="eba2b-116">Verbinding maken met een particulier netwerk, zoals uw on-premises netwerk aan het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="eba2b-117">Deze configuratie kan clients in uw on-premises netwerk rechtstreeks werken met Kafka.</span><span class="sxs-lookup"><span data-stu-id="eba2b-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="eba2b-118">Om deze configuratie inschakelt, moet u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="eba2b-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="eba2b-119">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="eba2b-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="eba2b-120">Maak een VPN-gateway die gebruikmaakt van een site-naar-site-configuratie.</span><span class="sxs-lookup"><span data-stu-id="eba2b-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="eba2b-121">De configuratie die in dit document gebruikt verbindt met een VPN-gateway-apparaat in uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="eba2b-122">Maak een DNS-server in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="eba2b-123">Doorsturen van tussen de DNS-server in elk netwerk configureren.</span><span class="sxs-lookup"><span data-stu-id="eba2b-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="eba2b-124">Installeer Kafka op HDInsight in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="eba2b-125">Zie voor meer informatie de [verbinding maken met Kafka uit een on-premises netwerk](#on-premises) sectie.</span><span class="sxs-lookup"><span data-stu-id="eba2b-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="eba2b-126">Verbinding met het maken van afzonderlijke computers aan het virtuele netwerk via een VPN-gateway en de VPN-client.</span><span class="sxs-lookup"><span data-stu-id="eba2b-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="eba2b-127">Om deze configuratie inschakelt, moet u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="eba2b-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="eba2b-128">Een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="eba2b-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="eba2b-129">Maak een VPN-gateway die gebruikmaakt van een punt-naar-site-configuratie.</span><span class="sxs-lookup"><span data-stu-id="eba2b-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="eba2b-130">Deze configuratie biedt een VPN-client die kan worden geïnstalleerd op Windows-clients.</span><span class="sxs-lookup"><span data-stu-id="eba2b-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="eba2b-131">Installeer Kafka op HDInsight in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="eba2b-132">Kafka voor IP-reclame configureren.</span><span class="sxs-lookup"><span data-stu-id="eba2b-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="eba2b-133">Deze configuratie kan de client verbinding maken via IP-adressen in plaats van domeinnamen.</span><span class="sxs-lookup"><span data-stu-id="eba2b-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="eba2b-134">Download en gebruik van de VPN-client op het ontwikkelsysteem.</span><span class="sxs-lookup"><span data-stu-id="eba2b-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="eba2b-135">Zie voor meer informatie de [Kafka met een VPN-client verbinding maken met](#vpnclient) sectie.</span><span class="sxs-lookup"><span data-stu-id="eba2b-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="eba2b-136">Deze configuratie wordt alleen aanbevolen voor ontwikkelingsdoeleinden vanwege de volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="eba2b-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="eba2b-137">Elke client moet verbinding maken met behulp van een VPN-software-client.</span><span class="sxs-lookup"><span data-stu-id="eba2b-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="eba2b-138">Azure biedt alleen een Windows-client.</span><span class="sxs-lookup"><span data-stu-id="eba2b-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="eba2b-139">De client geeft niet aanvragen voor naamomzetting aan het virtuele netwerk, zodat u IP-adressen om te communiceren met Kafka moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eba2b-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="eba2b-140">IP-communicatie is aanvullende configuratie van het cluster Kafka vereist.</span><span class="sxs-lookup"><span data-stu-id="eba2b-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="eba2b-141">Zie voor meer informatie over het gebruik van HDInsight in een virtueel netwerk [HDInsight uitbreiden met behulp van Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="eba2b-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="eba2b-142"><a id="on-premises"></a>Verbinding maken met Kafka vanuit een on-premises netwerk</span><span class="sxs-lookup"><span data-stu-id="eba2b-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="eba2b-143">Maakt een Kafka-cluster die communiceert met uw on-premises netwerk, volg de stappen in de [HDInsight verbinding maken met uw lokale netwerk](./connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="eba2b-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eba2b-144">Bij het maken van het HDInsight-cluster, selecteer de __Kafka__ type cluster.</span><span class="sxs-lookup"><span data-stu-id="eba2b-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="eba2b-145">Deze stappen maken de volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="eba2b-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="eba2b-146">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="eba2b-146">Azure Virtual Network</span></span>
* <span data-ttu-id="eba2b-147">Site-naar-site VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="eba2b-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="eba2b-148">Azure Storage-account (gebruikt door HDInsight)</span><span class="sxs-lookup"><span data-stu-id="eba2b-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="eba2b-149">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eba2b-149">Kafka on HDInsight</span></span>

<span data-ttu-id="eba2b-150">Om te controleren of een Kafka client kan verbinding maken met het cluster van on-premises, gebruikt u de stappen in de [voorbeeld:-client voor Python](#python-client) sectie.</span><span class="sxs-lookup"><span data-stu-id="eba2b-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="eba2b-151"><a id="vpnclient"></a>Verbinding maken met Kafka met een VPN-client</span><span class="sxs-lookup"><span data-stu-id="eba2b-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="eba2b-152">Gebruik de stappen in deze sectie voor het maken van de volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="eba2b-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="eba2b-153">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="eba2b-153">Azure Virtual Network</span></span>
* <span data-ttu-id="eba2b-154">Punt-naar-site VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="eba2b-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="eba2b-155">Azure Storage-Account (gebruikt door HDInsight)</span><span class="sxs-lookup"><span data-stu-id="eba2b-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="eba2b-156">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eba2b-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="eba2b-157">Volg de stappen in de [werken met zelfondertekende certificaten voor punt-naar-site-verbindingen](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span><span class="sxs-lookup"><span data-stu-id="eba2b-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="eba2b-158">Dit document wordt gemaakt van de certificaten die nodig zijn voor de gateway.</span><span class="sxs-lookup"><span data-stu-id="eba2b-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="eba2b-159">Open een PowerShell-prompt en de volgende code gebruiken voor aanmelding bij uw Azure-abonnement:</span><span class="sxs-lookup"><span data-stu-id="eba2b-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="eba2b-160">De volgende code gebruiken voor het maken van variabelen die configuratie-informatie bevatten:</span><span class="sxs-lookup"><span data-stu-id="eba2b-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="eba2b-161">De volgende code gebruiken voor het maken van de Azure-resourcegroep en het virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="eba2b-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="eba2b-162">Het kan enkele minuten duren voordat dit proces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="eba2b-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="eba2b-163">Gebruik de volgende code en de Azure Storage-Account en de blob-container te maken:</span><span class="sxs-lookup"><span data-stu-id="eba2b-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="eba2b-164">De volgende code gebruiken voor het maken van het HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="eba2b-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="eba2b-165">Dit proces duurt ongeveer twintig minuten om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="eba2b-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="eba2b-166">Gebruik de volgende cmdlet voor het ophalen van de URL voor de Windows VPN-client voor het virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="eba2b-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="eba2b-167">Gebruik de geretourneerde URI in uw webbrowser voor het downloaden van de Windows VPN-client.</span><span class="sxs-lookup"><span data-stu-id="eba2b-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="eba2b-168">Kafka configureren voor IP-advertenties</span><span class="sxs-lookup"><span data-stu-id="eba2b-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="eba2b-169">Standaard retourneert Zookeeper de domeinnaam van de beleggingsmakelaars Kafka aan clients.</span><span class="sxs-lookup"><span data-stu-id="eba2b-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="eba2b-170">Deze configuratie werkt niet met de VPN-software-client, zoals naamomzetting voor entiteiten in het virtuele netwerk niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="eba2b-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="eba2b-171">Gebruik de volgende stappen voor het configureren van Kafka voor het adverteren van IP-adressen in plaats van domeinnamen voor deze configuratie:</span><span class="sxs-lookup"><span data-stu-id="eba2b-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="eba2b-172">Met een webbrowser, gaat u naar https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="eba2b-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="eba2b-173">Vervang __CLUSTERNAME__ met de naam van de Kafka op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="eba2b-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="eba2b-174">Wanneer u wordt gevraagd, gebruikt u de HTTPS-gebruikersnaam en het wachtwoord voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="eba2b-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="eba2b-175">De Ambari-Webgebruikersinterface voor het cluster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="eba2b-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="eba2b-176">Als u informatie op Kafka, selecteer __Kafka__ uit de lijst aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="eba2b-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Lijst met Kafka service gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="eba2b-178">Selecteer om te geven Kafka configuratie, __Configs__ uit het midden van de bovenste.</span><span class="sxs-lookup"><span data-stu-id="eba2b-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Koppelingen naar de configuraties voor Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="eba2b-180">Vinden de __kafka env__ configuratie, voer `kafka-env` in de __Filter__ op de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="eba2b-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Kafka-configuratie voor kafka env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="eba2b-182">Toevoegen voor het configureren van Kafka voor het adverteren van IP-adressen, de volgende tekst naar de onderkant van de __kafka-env-sjabloon__ veld:</span><span class="sxs-lookup"><span data-stu-id="eba2b-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="eba2b-183">Voer voor het configureren van de interface die Kafka luistert op `listeners` in de __Filter__ op de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="eba2b-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="eba2b-184">Als u wilt configureren Kafka om te luisteren op alle netwerkinterfaces, wijzig de waarde in de __listeners__ veld `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="eba2b-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="eba2b-185">Voor het opslaan van wijzigingen in de configuratie, gebruiken de __opslaan__ knop.</span><span class="sxs-lookup"><span data-stu-id="eba2b-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="eba2b-186">Voer een SMS-bericht met een beschrijving van de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="eba2b-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="eba2b-187">Selecteer __OK__ nadat de wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="eba2b-187">Select __OK__ once the changes have been saved.</span></span>

    ![Configuratie knop Opslaan](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="eba2b-189">Gebruiken om fouten te voorkomen bij het opnieuw opstarten Kafka, de __serviceacties__ en selecteer __inschakelen op onderhoudsmodus__.</span><span class="sxs-lookup"><span data-stu-id="eba2b-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="eba2b-190">Klik op OK om deze bewerking te voltooien.</span><span class="sxs-lookup"><span data-stu-id="eba2b-190">Select OK to complete this operation.</span></span>

    ![Service-acties, met inschakelen onderhoud gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="eba2b-192">Als opnieuw Kafka, wilt u de __opnieuw__ en selecteer __start opnieuw alle van invloed op een__.</span><span class="sxs-lookup"><span data-stu-id="eba2b-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="eba2b-193">Bevestig het opnieuw opstarten en gebruik vervolgens de __OK__ knop nadat de bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="eba2b-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Start opnieuw op de knop met alle van invloed op een opnieuw opstarten gemarkeerd](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="eba2b-195">U schakelt onderhoudsmodus uit de __serviceacties__ en selecteer __inschakelen uit de onderhoudsmodus__.</span><span class="sxs-lookup"><span data-stu-id="eba2b-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="eba2b-196">Selecteer **OK** om deze bewerking te voltooien.</span><span class="sxs-lookup"><span data-stu-id="eba2b-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="eba2b-197">Verbinding maken met de VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="eba2b-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="eba2b-198">Verbinding maken met de VPN-gateway van een __Windows-client__, gebruiken de __verbinding maken met Azure__ sectie van de [een punt-naar-Site-verbinding configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span><span class="sxs-lookup"><span data-stu-id="eba2b-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="eba2b-199"><a id="python-client"></a>Voorbeeld:-Client voor Python</span><span class="sxs-lookup"><span data-stu-id="eba2b-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="eba2b-200">Gebruik de volgende stappen voor het maken en uitvoeren van een Python producenten en consumenten voor het valideren van de verbinding met Kafka:</span><span class="sxs-lookup"><span data-stu-id="eba2b-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="eba2b-201">Gebruik een van de volgende methoden voor het ophalen van de volledig gekwalificeerde domeinnaam (FQDN) en IP-adressen van de knooppunten in het cluster Kafka:</span><span class="sxs-lookup"><span data-stu-id="eba2b-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="eba2b-202">Dit script wordt ervan uitgegaan dat `$resourceGroupName` is de naam van de Azure-resourcegroep met het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="eba2b-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="eba2b-203">De geretourneerde gegevens voor gebruik opslaan in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="eba2b-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="eba2b-204">Gebruik de volgende voor het installeren van de [kafka python](http://kafka-python.readthedocs.io/) client:</span><span class="sxs-lookup"><span data-stu-id="eba2b-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="eba2b-205">Om gegevens te verzenden naar Kafka, moet u de volgende Python-code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="eba2b-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="eba2b-206">Vervang de `'kafka_broker'` vermeldingen met de adressen die is geretourneerd uit stap 1 in deze sectie:</span><span class="sxs-lookup"><span data-stu-id="eba2b-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="eba2b-207">Als u een __Software VPN-client__, vervang de `kafka_broker` vermeldingen met het IP-adres van uw worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="eba2b-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="eba2b-208">Als u hebt __naamomzetting via een aangepaste DNS-server ingeschakeld__, vervang de `kafka_broker` vermeldingen met de FQDN-naam van de worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="eba2b-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eba2b-209">Deze code verzendt de tekenreeks `test message` naar het onderwerp `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="eba2b-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="eba2b-210">De standaardconfiguratie van Kafka op HDInsight is het maken van het onderwerp, als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="eba2b-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="eba2b-211">Voor het ophalen van de berichten van Kafka, moet u de volgende Python-code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="eba2b-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="eba2b-212">Vervang de `'kafka_broker'` vermeldingen met de adressen die is geretourneerd uit stap 1 in deze sectie:</span><span class="sxs-lookup"><span data-stu-id="eba2b-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="eba2b-213">Als u een __Software VPN-client__, vervang de `kafka_broker` vermeldingen met het IP-adres van uw worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="eba2b-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="eba2b-214">Als u hebt __naamomzetting via een aangepaste DNS-server ingeschakeld__, vervang de `kafka_broker` vermeldingen met de FQDN-naam van de worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="eba2b-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eba2b-215">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eba2b-215">Next steps</span></span>

<span data-ttu-id="eba2b-216">Zie voor meer informatie over het gebruik van HDInsight met een virtueel netwerk, de [uitbreiden Azure HDInsight met behulp van een Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="eba2b-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="eba2b-217">Zie de volgende documenten voor meer informatie over het maken van een Azure-netwerk met punt-naar-Site VPN-gateway:</span><span class="sxs-lookup"><span data-stu-id="eba2b-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="eba2b-218">Een punt-naar-Site-verbinding met de Azure portal configureren</span><span class="sxs-lookup"><span data-stu-id="eba2b-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="eba2b-219">Configureren van een punt-naar-Site-verbinding met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="eba2b-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="eba2b-220">Zie de volgende documenten voor meer informatie over het werken Kafka in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eba2b-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="eba2b-221">Aan de slag met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eba2b-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="eba2b-222">Mirroring met Kafka in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="eba2b-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
