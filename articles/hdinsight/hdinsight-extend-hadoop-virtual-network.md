---
title: HDInsight met het virtuele netwerk - Azure uitbreiden | Microsoft Docs
description: Informatie over het gebruik van Azure Virtual Network verbinding maken met HDInsight andere cloudresources of resources in uw datacenter
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="776e8-103">Azure HDInsight met behulp van een Azure-netwerk uitbreiden</span><span class="sxs-lookup"><span data-stu-id="776e8-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="776e8-104">Informatie over het gebruik van HDInsight met een [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="776e8-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="776e8-105">Een virtueel netwerk van Azure, kunt de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="776e8-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="776e8-106">Verbinding maken met HDInsight rechtstreeks vanuit een on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="776e8-107">Verbinding maken met HDInsight gegevens opslaat in een virtueel Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="776e8-108">Rechtstreeks toegang hebben tot Hadoop-services die niet beschikbaar openbaar via internet zijn.</span><span class="sxs-lookup"><span data-stu-id="776e8-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="776e8-109">Kafka-API's of de HBase-Java-API.</span><span class="sxs-lookup"><span data-stu-id="776e8-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="776e8-110">De informatie in dit document is een goed begrip van TCP/IP-netwerken vereist.</span><span class="sxs-lookup"><span data-stu-id="776e8-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="776e8-111">Als u niet bekend met TCP/IP-netwerken bent, moet u samenwerken met iemand die dit voordat u wijzigingen op productienetwerken.</span><span class="sxs-lookup"><span data-stu-id="776e8-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="776e8-112">Planning</span><span class="sxs-lookup"><span data-stu-id="776e8-112">Planning</span></span>

<span data-ttu-id="776e8-113">Hier volgen de vragen die u bij het plannen voor het installeren van HDInsight in een virtueel netwerk moet beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="776e8-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="776e8-114">Moet u voor het installeren van HDInsight in een bestaand virtueel netwerk?</span><span class="sxs-lookup"><span data-stu-id="776e8-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="776e8-115">Of maakt u een nieuw netwerk?</span><span class="sxs-lookup"><span data-stu-id="776e8-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="776e8-116">Als u een bestaand virtueel netwerk gebruikt, moet u wellicht de netwerkconfiguratie wijzigen voordat u HDInsight kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="776e8-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="776e8-117">Zie voor meer informatie de [HDInsight toevoegen aan een bestaand virtueel netwerk](#existingvnet) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="776e8-118">Wilt u toch verbinding maken met het virtuele netwerk met HDInsight op een ander virtueel netwerk of uw on-premises netwerk?</span><span class="sxs-lookup"><span data-stu-id="776e8-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="776e8-119">Eenvoudig werkt alleen met resources in netwerken, moet u een aangepaste DNS-server maken en configureren van DNS-doorsturen.</span><span class="sxs-lookup"><span data-stu-id="776e8-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="776e8-120">Zie voor meer informatie de [meerdere netwerken met elkaar verbinden](#multinet) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="776e8-121">Wilt u beperken/omleiden binnenkomend of uitgaand verkeer naar HDInsight?</span><span class="sxs-lookup"><span data-stu-id="776e8-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="776e8-122">HDInsight moet hebben onbeperkte communicatie met specifieke IP-adressen in de Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="776e8-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="776e8-123">Er zijn ook verschillende poorten die moeten worden toegestaan via firewalls voor clientcommunicatie.</span><span class="sxs-lookup"><span data-stu-id="776e8-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="776e8-124">Zie voor meer informatie de [netwerkverkeer beheren](#networktraffic) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="776e8-125"><a id="existingvnet"></a>HDInsight toevoegen aan een bestaand virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="776e8-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="776e8-126">Gebruik de stappen in deze sectie om te ontdekken hoe u een nieuwe HDInsight toevoegt aan een bestaand virtueel netwerk van Azure.</span><span class="sxs-lookup"><span data-stu-id="776e8-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="776e8-127">U kunt een bestaand HDInsight-cluster in een virtueel netwerk niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="776e8-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="776e8-128">Gebruikt u een klassiek of Resource Manager-implementatiemodel voor het virtuele netwerk?</span><span class="sxs-lookup"><span data-stu-id="776e8-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="776e8-129">HDInsight 3,4 en groter vereist een virtueel netwerk van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="776e8-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="776e8-130">Eerdere versies van HDInsight vereist een klassiek virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="776e8-131">Als uw bestaande netwerk een klassiek virtueel netwerk is, moet u een virtueel netwerk van Resource Manager maken en sluit vervolgens de twee.</span><span class="sxs-lookup"><span data-stu-id="776e8-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="776e8-132">[Klassieke vnet's verbinden met nieuwe VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="776e8-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="776e8-133">Zodra toegevoegd, wordt HDInsight geïnstalleerd in het Resource Manager-netwerk kan communiceren met resources in het klassieke netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="776e8-134">Geforceerde tunneling gebruiken</span><span class="sxs-lookup"><span data-stu-id="776e8-134">Do you use forced tunneling?</span></span> <span data-ttu-id="776e8-135">Geforceerde tunneling is subnetinstelling dat ervoor zorgt uitgaand internetverkeer met een apparaat voor controle dat en logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="776e8-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="776e8-136">HDInsight biedt geen ondersteuning voor geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="776e8-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="776e8-137">Verwijder geforceerde tunneling voordat u HDInsight installeert in een subnet, of een nieuw subnet maken voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="776e8-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="776e8-138">Gebruik je netwerkbeveiligingsgroepen, de gebruiker gedefinieerde routes of virtuele netwerkapparaten naar het verkeer te beperken van of naar het virtuele netwerk?</span><span class="sxs-lookup"><span data-stu-id="776e8-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="776e8-139">Als een beheerde service vereist HDInsight onbeperkte toegang tot verschillende IP-adressen in de Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="776e8-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="776e8-140">Werk alle bestaande netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes zodat de communicatie met deze IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="776e8-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="776e8-141">HDInsight als host fungeert voor meerdere services, die verschillende poorten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="776e8-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="776e8-142">Geen verkeer blokkeert dat via deze poorten.</span><span class="sxs-lookup"><span data-stu-id="776e8-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="776e8-143">Zie voor een lijst met poorten om toe te staan via firewalls virtueel apparaat, de [beveiliging](#security) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="776e8-144">Als u uw bestaande beveiligingsconfiguratie zoekt, gebruikt u de volgende Azure PowerShell of Azure CLI-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="776e8-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="776e8-145">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="776e8-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="776e8-146">Zie voor meer informatie de [netwerkbeveiligingsgroepen oplossen](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="776e8-147">Netwerkbeveiligingsgroepen worden toegepast in volgorde op basis van Regelprioriteit.</span><span class="sxs-lookup"><span data-stu-id="776e8-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="776e8-148">De eerste regel die overeenkomt met het patroon verkeer wordt toegepast en geen andere voor dat verkeer wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="776e8-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="776e8-149">Volgorde van de regels van meest strikte op minimaal.</span><span class="sxs-lookup"><span data-stu-id="776e8-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="776e8-150">Zie voor meer informatie de [filteren van netwerkverkeer met netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="776e8-151">Door de gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="776e8-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="776e8-152">Zie voor meer informatie de [routes oplossen](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="776e8-153">Maken van een HDInsight-cluster en het virtuele netwerk van Azure selecteren tijdens de configuratie.</span><span class="sxs-lookup"><span data-stu-id="776e8-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="776e8-154">Gebruik de stappen in de volgende documenten voor inzicht in het proces voor het cluster maken:</span><span class="sxs-lookup"><span data-stu-id="776e8-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * [<span data-ttu-id="776e8-155">HDInsight maken met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="776e8-155">Create HDInsight using the Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="776e8-156">HDInsight maken met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="776e8-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="776e8-157">Maken van HDInsight met behulp van Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="776e8-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="776e8-158">HDInsight met behulp van een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="776e8-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="776e8-159">HDInsight toe te voegen aan een virtueel netwerk is een optionele configuratie-stap.</span><span class="sxs-lookup"><span data-stu-id="776e8-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="776e8-160">Zorg ervoor dat het virtuele netwerk selecteren bij het configureren van het cluster.</span><span class="sxs-lookup"><span data-stu-id="776e8-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="776e8-161"><a id="multinet"></a>Meerdere netwerken met elkaar verbinden</span><span class="sxs-lookup"><span data-stu-id="776e8-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="776e8-162">De grootste uitdaging met een configuratie met meerdere is naamomzetting tussen de netwerken.</span><span class="sxs-lookup"><span data-stu-id="776e8-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="776e8-163">Azure biedt naamomzetting voor Azure-services die zijn geïnstalleerd in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="776e8-164">Deze ingebouwde naamomzetting kunt HDInsight verbinding maken met de volgende bronnen met behulp van een volledig gekwalificeerde domeinnaam (FQDN):</span><span class="sxs-lookup"><span data-stu-id="776e8-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="776e8-165">Een resource die beschikbaar is op het internet.</span><span class="sxs-lookup"><span data-stu-id="776e8-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="776e8-166">Bijvoorbeeld microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="776e8-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="776e8-167">Alle bronnen die zich in hetzelfde Azure-netwerk, met behulp van de __interne DNS-naam__ van de resource.</span><span class="sxs-lookup"><span data-stu-id="776e8-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="776e8-168">Bijvoorbeeld, wanneer u de standaard-naamomzetting, volgen voorbeeld interne DNS-namen is toegewezen aan HDInsight worker-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="776e8-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="776e8-169">wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="776e8-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="776e8-170">wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="776e8-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="776e8-171">Deze beide knooppunten kunnen communiceren rechtstreeks met elkaar en andere knooppunten in HDInsight, met behulp van de interne DNS-namen.</span><span class="sxs-lookup"><span data-stu-id="776e8-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="776e8-172">De standaard-naamomzetting biedt __niet__ HDInsight omzetten van de namen van bronnen in netwerken die zijn gekoppeld aan het virtuele netwerk toestaan.</span><span class="sxs-lookup"><span data-stu-id="776e8-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="776e8-173">Het is bijvoorbeeld algemene uw on-premises netwerk koppelen aan het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="776e8-174">Met alleen de standaard naamomzetting HDInsight kan geen toegang krijgen tot bronnen in de on-premises netwerk met de naam.</span><span class="sxs-lookup"><span data-stu-id="776e8-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="776e8-175">Het omgekeerde geldt ook resources in uw on-premises netwerk geen toegang tot bronnen in het virtuele netwerk met de naam.</span><span class="sxs-lookup"><span data-stu-id="776e8-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="776e8-176">U moet de aangepaste DNS-server maken en configureren van het virtuele netwerk om het te gebruiken voordat u het HDInsight-cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="776e8-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="776e8-177">Om naamomzetting tussen het virtuele netwerk en bronnen in de gekoppelde netwerken, moet u de volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="776e8-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="776e8-178">Maak een aangepaste DNS-server in de Azure Virtual Network waaruit u plant voor het installeren van HDInsight.</span><span class="sxs-lookup"><span data-stu-id="776e8-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="776e8-179">Het virtuele netwerk voor het gebruik van de aangepaste DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="776e8-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="776e8-180">Zoeken naar dat de Azure DNS-achtervoegsel voor het virtuele netwerk toegewezen.</span><span class="sxs-lookup"><span data-stu-id="776e8-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="776e8-181">Deze waarde is vergelijkbaar met `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="776e8-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="776e8-182">Zie voor meer informatie over het zoeken naar de DNS-achtervoegsel de [voorbeeld: aangepaste DNS](#example-dns) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="776e8-183">Doorsturen van tussen de DNS-servers configureren.</span><span class="sxs-lookup"><span data-stu-id="776e8-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="776e8-184">De configuratie is afhankelijk van het type van het externe netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="776e8-185">Als het externe netwerk een on-premises netwerk is, configureren van DNS als volgt:</span><span class="sxs-lookup"><span data-stu-id="776e8-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="776e8-186">__Aangepaste DNS__ (in het virtuele netwerk):</span><span class="sxs-lookup"><span data-stu-id="776e8-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="776e8-187">Aanvragen voor de DNS-achtervoegsel van het virtuele netwerk naar de Azure recursieve resolver (168.63.129.16) doorsturen.</span><span class="sxs-lookup"><span data-stu-id="776e8-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="776e8-188">Azure verwerkt aanvragen voor bronnen in het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="776e8-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="776e8-189">Doorsturen van alle andere verzoeken naar de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="776e8-190">De lokale DNS-server verwerkt alle andere aanvragen voor naamomzetting, zelfs aanvragen voor internetbronnen zoals Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="776e8-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="776e8-191">__Lokale DNS__: doorsturen van aanvragen voor het virtuele netwerk DNS-achtervoegsel voor de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="776e8-192">De aangepaste DNS-server stuurt vervolgens door naar de Azure recursieve-resolver.</span><span class="sxs-lookup"><span data-stu-id="776e8-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="776e8-193">Deze configuratie routes aanvragen voor FQDN-namen die het DNS-achtervoegsel van het virtuele netwerk voor de aangepaste DNS-server bevatten.</span><span class="sxs-lookup"><span data-stu-id="776e8-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="776e8-194">Alle andere verzoeken (zelfs voor openbare internet-adressen) worden verwerkt door de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="776e8-195">Als het externe netwerk een ander virtueel netwerk van Azure is, configureren van DNS als volgt:</span><span class="sxs-lookup"><span data-stu-id="776e8-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="776e8-196">__Aangepaste DNS__ (in elk virtueel netwerk):</span><span class="sxs-lookup"><span data-stu-id="776e8-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="776e8-197">Aanvragen voor het DNS-achtervoegsel van de virtuele netwerken worden doorgestuurd naar de aangepaste DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="776e8-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="776e8-198">De DNS-server in elk virtueel netwerk is verantwoordelijk voor het oplossen van resources binnen het netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="776e8-199">Alle andere verzoeken naar de Azure recursieve resolver doorsturen.</span><span class="sxs-lookup"><span data-stu-id="776e8-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="776e8-200">De recursieve resolver is verantwoordelijk voor het oplossen van lokale en internetbronnen.</span><span class="sxs-lookup"><span data-stu-id="776e8-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="776e8-201">De DNS-server voor elk netwerk aanvragen naar de andere verzendt, op basis van DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="776e8-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="776e8-202">Andere aanvragen worden omgezet met behulp van de Azure recursieve-resolver.</span><span class="sxs-lookup"><span data-stu-id="776e8-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="776e8-203">Zie voor een voorbeeld van elke configuratie, de [voorbeeld: aangepaste DNS](#example-dns) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="776e8-204">Zie voor meer informatie de [naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="776e8-205">Rechtstreeks verbinding maken met Hadoop-services</span><span class="sxs-lookup"><span data-stu-id="776e8-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="776e8-206">De meeste documentatie op HDInsight wordt ervan uitgegaan dat u toegang tot het cluster via internet hebt.</span><span class="sxs-lookup"><span data-stu-id="776e8-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="776e8-207">Bijvoorbeeld, u verbinding kunt maken met het cluster op https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="776e8-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="776e8-208">Dit adres wordt gebruikt voor de openbare-gateway niet beschikbaar is als u nsg's of udr's hebt gebruikt om toegang te beperken van het internet.</span><span class="sxs-lookup"><span data-stu-id="776e8-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="776e8-209">Voor verbinding met Ambari en andere webpagina's via het virtuele netwerk, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="776e8-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="776e8-210">Voor het detecteren van de interne volledig gekwalificeerde domeinnamen (FQDN) van de clusterknooppunten HDInsight, moet u een van de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="776e8-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

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

    <span data-ttu-id="776e8-211">De FQDN-naam vinden voor de hoofdknooppunten in de lijst met knooppunten die zijn geretourneerd, en de FQDN's gebruiken voor verbinding met Ambari en andere web-services.</span><span class="sxs-lookup"><span data-stu-id="776e8-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="776e8-212">Bijvoorbeeld: `http://<headnode-fqdn>:8080` voor toegang tot de Ambari.</span><span class="sxs-lookup"><span data-stu-id="776e8-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="776e8-213">Sommige services die worden gehost op de hoofdknooppunten zijn alleen actief is op één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="776e8-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="776e8-214">Als u probeert toegang tot een service op één hoofdknooppunt en een 404-fout retourneert, overschakelen naar het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="776e8-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="776e8-215">Zie het vaststellen van het knooppunt en de poort die een service beschikbaar is op de [poorten die worden gebruikt door de services van Hadoop op HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="776e8-216"><a id="networktraffic"></a>Beheren van netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="776e8-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="776e8-217">Netwerkverkeer in een virtuele Azure-netwerken kan worden beheerd met behulp van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="776e8-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="776e8-218">**Netwerkbeveiligingsgroepen** (NSG) kunt u binnenkomend en uitgaand verkeer op het netwerk te filteren.</span><span class="sxs-lookup"><span data-stu-id="776e8-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="776e8-219">Zie voor meer informatie de [filteren van netwerkverkeer met netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="776e8-220">HDInsight biedt geen ondersteuning voor uitgaand verkeer te beperken.</span><span class="sxs-lookup"><span data-stu-id="776e8-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="776e8-221">**Gebruiker gedefinieerde routes** (UDR) definiëren hoe verkeersstromen tussen resources in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="776e8-222">Zie voor meer informatie de [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="776e8-223">**Virtuele apparaten** repliceren van de functionaliteit van apparaten, zoals firewalls en routers.</span><span class="sxs-lookup"><span data-stu-id="776e8-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="776e8-224">Zie voor meer informatie de [netwerkapparaten](https://azure.microsoft.com/solutions/network-appliances) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="776e8-225">Als een beheerde service vereist HDInsight onbeperkte toegang tot Azure-status en beheer van services in de Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="776e8-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="776e8-226">Wanneer u nsg's en udr's, moet u ervoor zorgen dat HDInsight deze services nog steeds met HDInsight communiceren kunnen.</span><span class="sxs-lookup"><span data-stu-id="776e8-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="776e8-227">HDInsight beschrijft de services op verschillende poorten.</span><span class="sxs-lookup"><span data-stu-id="776e8-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="776e8-228">Wanneer u een virtueel apparaat firewall gebruikt, moet u verkeer op de poorten die voor deze services toestaan.</span><span class="sxs-lookup"><span data-stu-id="776e8-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="776e8-229">Zie de sectie [vereiste poorten] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="776e8-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="776e8-230"><a id="hdinsight-ip"></a>HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="776e8-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="776e8-231">Als u gebruiken wilt **netwerkbeveiligingsgroepen** of **gebruiker gedefinieerde routes** netwerkverkeer wordt beheerd, voert u de volgende acties voor de installatie van HDInsight:</span><span class="sxs-lookup"><span data-stu-id="776e8-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="776e8-232">Identificeer de Azure-regio die u wilt gebruiken voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="776e8-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="776e8-233">Identificeer de IP-adressen die door HDInsight vereist.</span><span class="sxs-lookup"><span data-stu-id="776e8-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="776e8-234">Zie voor meer informatie de [IP-adressen die zijn vereist voor HDInsight](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="776e8-235">Maak of wijzig de netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes voor het subnet dat u van plan bent voor het installeren van HDInsight in.</span><span class="sxs-lookup"><span data-stu-id="776e8-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="776e8-236">__Netwerkbeveiligingsgroepen__: toestaan __inkomende__ verkeer op poort __443__ van de IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="776e8-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="776e8-237">__Gebruiker gedefinieerde routes__: Maak een route voor elk IP-adres en stel de __volgende hop type__ naar __Internet__.</span><span class="sxs-lookup"><span data-stu-id="776e8-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="776e8-238">Zie de volgende documentatie voor meer informatie over netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes:</span><span class="sxs-lookup"><span data-stu-id="776e8-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="776e8-239">Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="776e8-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="776e8-240">Gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="776e8-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="776e8-241">Geforceerde tunneling</span><span class="sxs-lookup"><span data-stu-id="776e8-241">Forced tunneling</span></span>

<span data-ttu-id="776e8-242">Geforceerde tunneling is een gebruiker gedefinieerde routering configuratie waarbij alle verkeer van een subnet wordt geforceerd voor een specifieke netwerk- of locatie, zoals uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="776e8-243">HDInsight biedt __niet__ ondersteuning geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="776e8-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="776e8-244"><a id="hdinsight-ip"></a>Vereiste IP-adressen</span><span class="sxs-lookup"><span data-stu-id="776e8-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="776e8-245">De Azure management van de status en -services moet communiceren met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="776e8-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="776e8-246">Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes gebruikt, kunt u verkeer van de IP-adressen voor deze services te bereiken van HDInsight.</span><span class="sxs-lookup"><span data-stu-id="776e8-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="776e8-247">Als u niet netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes waarmee verkeer gebruikt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="776e8-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="776e8-248">Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes gebruikt, moet u het verkeer van de Azure status en de management-services te bereiken HDInsight toestaan.</span><span class="sxs-lookup"><span data-stu-id="776e8-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="776e8-249">Gebruik de volgende stappen uit om te zoeken de IP-adressen dat moeten worden toegestaan:</span><span class="sxs-lookup"><span data-stu-id="776e8-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="776e8-250">U moet altijd verkeer van de volgende IP-adressen toestaan:</span><span class="sxs-lookup"><span data-stu-id="776e8-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="776e8-251">IP-adres</span><span class="sxs-lookup"><span data-stu-id="776e8-251">IP address</span></span> | <span data-ttu-id="776e8-252">Toegestane poort</span><span class="sxs-lookup"><span data-stu-id="776e8-252">Allowed port</span></span> | <span data-ttu-id="776e8-253">Richting</span><span class="sxs-lookup"><span data-stu-id="776e8-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="776e8-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="776e8-254">168.61.49.99</span></span> | <span data-ttu-id="776e8-255">443</span><span class="sxs-lookup"><span data-stu-id="776e8-255">443</span></span> | <span data-ttu-id="776e8-256">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-256">Inbound</span></span> |
    | <span data-ttu-id="776e8-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="776e8-257">23.99.5.239</span></span> | <span data-ttu-id="776e8-258">443</span><span class="sxs-lookup"><span data-stu-id="776e8-258">443</span></span> | <span data-ttu-id="776e8-259">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-259">Inbound</span></span> |
    | <span data-ttu-id="776e8-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="776e8-260">168.61.48.131</span></span> | <span data-ttu-id="776e8-261">443</span><span class="sxs-lookup"><span data-stu-id="776e8-261">443</span></span> | <span data-ttu-id="776e8-262">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-262">Inbound</span></span> |
    | <span data-ttu-id="776e8-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="776e8-263">138.91.141.162</span></span> | <span data-ttu-id="776e8-264">443</span><span class="sxs-lookup"><span data-stu-id="776e8-264">443</span></span> | <span data-ttu-id="776e8-265">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-265">Inbound</span></span> |

2. <span data-ttu-id="776e8-266">Als uw HDInsight-cluster zich in een van de volgende regio's, moet u het verkeer van de IP-adressen die worden vermeld voor de regio toestaan:</span><span class="sxs-lookup"><span data-stu-id="776e8-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="776e8-267">Als de Azure-regio u niet wordt weergegeven, klikt u vervolgens gebruik alleen de vier IP-adressen uit stap 1.</span><span class="sxs-lookup"><span data-stu-id="776e8-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="776e8-268">Land</span><span class="sxs-lookup"><span data-stu-id="776e8-268">Country</span></span> | <span data-ttu-id="776e8-269">Regio</span><span class="sxs-lookup"><span data-stu-id="776e8-269">Region</span></span> | <span data-ttu-id="776e8-270">Toegestane IP-adressen</span><span class="sxs-lookup"><span data-stu-id="776e8-270">Allowed IP addresses</span></span> | <span data-ttu-id="776e8-271">Toegestane poort</span><span class="sxs-lookup"><span data-stu-id="776e8-271">Allowed port</span></span> | <span data-ttu-id="776e8-272">Richting</span><span class="sxs-lookup"><span data-stu-id="776e8-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="776e8-273">Azië</span><span class="sxs-lookup"><span data-stu-id="776e8-273">Asia</span></span> | <span data-ttu-id="776e8-274">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="776e8-274">East Asia</span></span> | <span data-ttu-id="776e8-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="776e8-275">23.102.235.122</span></span></br><span data-ttu-id="776e8-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="776e8-276">52.175.38.134</span></span> | <span data-ttu-id="776e8-277">443</span><span class="sxs-lookup"><span data-stu-id="776e8-277">443</span></span> | <span data-ttu-id="776e8-278">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-279">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="776e8-279">Southeast Asia</span></span> | <span data-ttu-id="776e8-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="776e8-280">13.76.245.160</span></span></br><span data-ttu-id="776e8-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="776e8-281">13.76.136.249</span></span> | <span data-ttu-id="776e8-282">443</span><span class="sxs-lookup"><span data-stu-id="776e8-282">443</span></span> | <span data-ttu-id="776e8-283">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-283">Inbound</span></span> |
    | <span data-ttu-id="776e8-284">Australië</span><span class="sxs-lookup"><span data-stu-id="776e8-284">Australia</span></span> | <span data-ttu-id="776e8-285">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="776e8-285">Australia East</span></span> | <span data-ttu-id="776e8-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="776e8-286">104.210.84.115</span></span></br><span data-ttu-id="776e8-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="776e8-287">13.75.152.195</span></span> | <span data-ttu-id="776e8-288">443</span><span class="sxs-lookup"><span data-stu-id="776e8-288">443</span></span> | <span data-ttu-id="776e8-289">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-290">Australië - zuidoost</span><span class="sxs-lookup"><span data-stu-id="776e8-290">Australia Southeast</span></span> | <span data-ttu-id="776e8-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="776e8-291">13.77.2.56</span></span></br><span data-ttu-id="776e8-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="776e8-292">13.77.2.94</span></span> | <span data-ttu-id="776e8-293">443</span><span class="sxs-lookup"><span data-stu-id="776e8-293">443</span></span> | <span data-ttu-id="776e8-294">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-294">Inbound</span></span> |
    | <span data-ttu-id="776e8-295">Brazilië</span><span class="sxs-lookup"><span data-stu-id="776e8-295">Brazil</span></span> | <span data-ttu-id="776e8-296">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="776e8-296">Brazil South</span></span> | <span data-ttu-id="776e8-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="776e8-297">191.235.84.104</span></span></br><span data-ttu-id="776e8-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="776e8-298">191.235.87.113</span></span> | <span data-ttu-id="776e8-299">443</span><span class="sxs-lookup"><span data-stu-id="776e8-299">443</span></span> | <span data-ttu-id="776e8-300">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-300">Inbound</span></span> |
    | <span data-ttu-id="776e8-301">Canada</span><span class="sxs-lookup"><span data-stu-id="776e8-301">Canada</span></span> | <span data-ttu-id="776e8-302">Canada - oost</span><span class="sxs-lookup"><span data-stu-id="776e8-302">Canada East</span></span> | <span data-ttu-id="776e8-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="776e8-303">52.229.127.96</span></span></br><span data-ttu-id="776e8-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="776e8-304">52.229.123.172</span></span> | <span data-ttu-id="776e8-305">443</span><span class="sxs-lookup"><span data-stu-id="776e8-305">443</span></span> | <span data-ttu-id="776e8-306">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-307">Canada - midden</span><span class="sxs-lookup"><span data-stu-id="776e8-307">Canada Central</span></span> | <span data-ttu-id="776e8-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="776e8-308">52.228.37.66</span></span></br><span data-ttu-id="776e8-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="776e8-309">52.228.45.222</span></span> | <span data-ttu-id="776e8-310">443</span><span class="sxs-lookup"><span data-stu-id="776e8-310">443</span></span> | <span data-ttu-id="776e8-311">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-311">Inbound</span></span> |
    | <span data-ttu-id="776e8-312">China</span><span class="sxs-lookup"><span data-stu-id="776e8-312">China</span></span> | <span data-ttu-id="776e8-313">China - noord</span><span class="sxs-lookup"><span data-stu-id="776e8-313">China North</span></span> | <span data-ttu-id="776e8-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="776e8-314">42.159.96.170</span></span></br><span data-ttu-id="776e8-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="776e8-315">139.217.2.219</span></span> | <span data-ttu-id="776e8-316">443</span><span class="sxs-lookup"><span data-stu-id="776e8-316">443</span></span> | <span data-ttu-id="776e8-317">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-318">China - oost</span><span class="sxs-lookup"><span data-stu-id="776e8-318">China East</span></span> | <span data-ttu-id="776e8-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="776e8-319">42.159.198.178</span></span></br><span data-ttu-id="776e8-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="776e8-320">42.159.234.157</span></span> | <span data-ttu-id="776e8-321">443</span><span class="sxs-lookup"><span data-stu-id="776e8-321">443</span></span> | <span data-ttu-id="776e8-322">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-322">Inbound</span></span> |
    | <span data-ttu-id="776e8-323">Europa</span><span class="sxs-lookup"><span data-stu-id="776e8-323">Europe</span></span> | <span data-ttu-id="776e8-324">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="776e8-324">North Europe</span></span> | <span data-ttu-id="776e8-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="776e8-325">52.164.210.96</span></span></br><span data-ttu-id="776e8-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="776e8-326">13.74.153.132</span></span> | <span data-ttu-id="776e8-327">443</span><span class="sxs-lookup"><span data-stu-id="776e8-327">443</span></span> | <span data-ttu-id="776e8-328">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-329">West-Europa</span><span class="sxs-lookup"><span data-stu-id="776e8-329">West Europe</span></span>| <span data-ttu-id="776e8-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="776e8-330">52.166.243.90</span></span></br><span data-ttu-id="776e8-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="776e8-331">52.174.36.244</span></span> | <span data-ttu-id="776e8-332">443</span><span class="sxs-lookup"><span data-stu-id="776e8-332">443</span></span> | <span data-ttu-id="776e8-333">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-333">Inbound</span></span> |
    | <span data-ttu-id="776e8-334">Duitsland</span><span class="sxs-lookup"><span data-stu-id="776e8-334">Germany</span></span> | <span data-ttu-id="776e8-335">Duitsland - centraal</span><span class="sxs-lookup"><span data-stu-id="776e8-335">Germany Central</span></span> | <span data-ttu-id="776e8-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="776e8-336">51.4.146.68</span></span></br><span data-ttu-id="776e8-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="776e8-337">51.4.146.80</span></span> | <span data-ttu-id="776e8-338">443</span><span class="sxs-lookup"><span data-stu-id="776e8-338">443</span></span> | <span data-ttu-id="776e8-339">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-340">Duitsland - noordoost</span><span class="sxs-lookup"><span data-stu-id="776e8-340">Germany Northeast</span></span> | <span data-ttu-id="776e8-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="776e8-341">51.5.150.132</span></span></br><span data-ttu-id="776e8-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="776e8-342">51.5.144.101</span></span> | <span data-ttu-id="776e8-343">443</span><span class="sxs-lookup"><span data-stu-id="776e8-343">443</span></span> | <span data-ttu-id="776e8-344">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-344">Inbound</span></span> |
    | <span data-ttu-id="776e8-345">India</span><span class="sxs-lookup"><span data-stu-id="776e8-345">India</span></span> | <span data-ttu-id="776e8-346">Centraal-India</span><span class="sxs-lookup"><span data-stu-id="776e8-346">Central India</span></span> | <span data-ttu-id="776e8-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="776e8-347">52.172.153.209</span></span></br><span data-ttu-id="776e8-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="776e8-348">52.172.152.49</span></span> | <span data-ttu-id="776e8-349">443</span><span class="sxs-lookup"><span data-stu-id="776e8-349">443</span></span> | <span data-ttu-id="776e8-350">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-350">Inbound</span></span> |
    | <span data-ttu-id="776e8-351">Japan</span><span class="sxs-lookup"><span data-stu-id="776e8-351">Japan</span></span> | <span data-ttu-id="776e8-352">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="776e8-352">Japan East</span></span> | <span data-ttu-id="776e8-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="776e8-353">13.78.125.90</span></span></br><span data-ttu-id="776e8-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="776e8-354">13.78.89.60</span></span> | <span data-ttu-id="776e8-355">443</span><span class="sxs-lookup"><span data-stu-id="776e8-355">443</span></span> | <span data-ttu-id="776e8-356">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-357">Japan - west</span><span class="sxs-lookup"><span data-stu-id="776e8-357">Japan West</span></span> | <span data-ttu-id="776e8-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="776e8-358">40.74.125.69</span></span></br><span data-ttu-id="776e8-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="776e8-359">138.91.29.150</span></span> | <span data-ttu-id="776e8-360">443</span><span class="sxs-lookup"><span data-stu-id="776e8-360">443</span></span> | <span data-ttu-id="776e8-361">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-361">Inbound</span></span> |
    | <span data-ttu-id="776e8-362">Korea</span><span class="sxs-lookup"><span data-stu-id="776e8-362">Korea</span></span> | <span data-ttu-id="776e8-363">Korea - centraal</span><span class="sxs-lookup"><span data-stu-id="776e8-363">Korea Central</span></span> | <span data-ttu-id="776e8-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="776e8-364">52.231.39.142</span></span></br><span data-ttu-id="776e8-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="776e8-365">52.231.36.209</span></span> | <span data-ttu-id="776e8-366">433</span><span class="sxs-lookup"><span data-stu-id="776e8-366">433</span></span> | <span data-ttu-id="776e8-367">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-368">Korea - zuid</span><span class="sxs-lookup"><span data-stu-id="776e8-368">Korea South</span></span> | <span data-ttu-id="776e8-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="776e8-369">52.231.203.16</span></span></br><span data-ttu-id="776e8-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="776e8-370">52.231.205.214</span></span> | <span data-ttu-id="776e8-371">443</span><span class="sxs-lookup"><span data-stu-id="776e8-371">443</span></span> | <span data-ttu-id="776e8-372">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-372">Inbound</span></span>
    | <span data-ttu-id="776e8-373">Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="776e8-373">United Kingdom</span></span> | <span data-ttu-id="776e8-374">Verenigd Koninkrijk West</span><span class="sxs-lookup"><span data-stu-id="776e8-374">UK West</span></span> | <span data-ttu-id="776e8-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="776e8-375">51.141.13.110</span></span></br><span data-ttu-id="776e8-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="776e8-376">51.141.7.20</span></span> | <span data-ttu-id="776e8-377">443</span><span class="sxs-lookup"><span data-stu-id="776e8-377">443</span></span> | <span data-ttu-id="776e8-378">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-379">Verenigd Koninkrijk Zuid</span><span class="sxs-lookup"><span data-stu-id="776e8-379">UK South</span></span> | <span data-ttu-id="776e8-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="776e8-380">51.140.47.39</span></span></br><span data-ttu-id="776e8-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="776e8-381">51.140.52.16</span></span> | <span data-ttu-id="776e8-382">443</span><span class="sxs-lookup"><span data-stu-id="776e8-382">443</span></span> | <span data-ttu-id="776e8-383">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-383">Inbound</span></span> |
    | <span data-ttu-id="776e8-384">Verenigde Staten</span><span class="sxs-lookup"><span data-stu-id="776e8-384">United States</span></span> | <span data-ttu-id="776e8-385">VS - midden</span><span class="sxs-lookup"><span data-stu-id="776e8-385">Central US</span></span> | <span data-ttu-id="776e8-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="776e8-386">13.67.223.215</span></span></br><span data-ttu-id="776e8-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="776e8-387">40.86.83.253</span></span> | <span data-ttu-id="776e8-388">443</span><span class="sxs-lookup"><span data-stu-id="776e8-388">443</span></span> | <span data-ttu-id="776e8-389">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-390">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="776e8-390">North Central US</span></span> | <span data-ttu-id="776e8-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="776e8-391">157.56.8.38</span></span></br><span data-ttu-id="776e8-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="776e8-392">157.55.213.99</span></span> | <span data-ttu-id="776e8-393">443</span><span class="sxs-lookup"><span data-stu-id="776e8-393">443</span></span> | <span data-ttu-id="776e8-394">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-395">West-centraal VS</span><span class="sxs-lookup"><span data-stu-id="776e8-395">West Central US</span></span> | <span data-ttu-id="776e8-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="776e8-396">52.161.23.15</span></span></br><span data-ttu-id="776e8-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="776e8-397">52.161.10.167</span></span> | <span data-ttu-id="776e8-398">443</span><span class="sxs-lookup"><span data-stu-id="776e8-398">443</span></span> | <span data-ttu-id="776e8-399">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="776e8-400">VS - west 2</span><span class="sxs-lookup"><span data-stu-id="776e8-400">West US 2</span></span> | <span data-ttu-id="776e8-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="776e8-401">52.175.211.210</span></span></br><span data-ttu-id="776e8-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="776e8-402">52.175.222.222</span></span> | <span data-ttu-id="776e8-403">443</span><span class="sxs-lookup"><span data-stu-id="776e8-403">443</span></span> | <span data-ttu-id="776e8-404">Inkomend</span><span class="sxs-lookup"><span data-stu-id="776e8-404">Inbound</span></span> |

    <span data-ttu-id="776e8-405">Zie voor informatie over de IP-adressen voor Azure Government, de [Azure Government Intelligence en analyse](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="776e8-406">Als u een aangepaste DNS-server met het virtuele netwerk gebruikt, moet u ook toegang vanaf toestaan __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="776e8-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="776e8-407">Dit adres is van de Azure recursieve naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="776e8-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="776e8-408">Zie voor meer informatie de [naamomzetting voor VM's en rol exemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="776e8-409">Zie voor meer informatie de [netwerkverkeer beheren](#networktraffic) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="776e8-410"><a id="hdinsight-ports"></a>Vereiste poorten</span><span class="sxs-lookup"><span data-stu-id="776e8-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="776e8-411">Als u van plan bent met een netwerk **virtueel apparaat firewall** wilt beveiligen van het virtuele netwerk, moet u uitgaand verkeer op de volgende poorten toestaan:</span><span class="sxs-lookup"><span data-stu-id="776e8-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="776e8-412">53</span><span class="sxs-lookup"><span data-stu-id="776e8-412">53</span></span>
* <span data-ttu-id="776e8-413">443</span><span class="sxs-lookup"><span data-stu-id="776e8-413">443</span></span>
* <span data-ttu-id="776e8-414">1433</span><span class="sxs-lookup"><span data-stu-id="776e8-414">1433</span></span>
* <span data-ttu-id="776e8-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="776e8-415">11000-11999</span></span>
* <span data-ttu-id="776e8-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="776e8-416">14000-14999</span></span>

<span data-ttu-id="776e8-417">Zie voor een lijst met poorten voor specifieke services, de [poorten die worden gebruikt door de services van Hadoop op HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="776e8-418">Zie voor meer informatie over firewallregels voor virtuele apparaten de [virtueel apparaat scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span><span class="sxs-lookup"><span data-stu-id="776e8-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="776e8-419"><a id="hdinsight-nsg"></a>Voorbeeld: netwerkbeveiligingsgroepen met HDInsight</span><span class="sxs-lookup"><span data-stu-id="776e8-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="776e8-420">De voorbeelden in deze sectie laten zien hoe netwerkbeveiliging groep regels maken die HDInsight om te communiceren met de Azure management-services toestaan.</span><span class="sxs-lookup"><span data-stu-id="776e8-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="776e8-421">Voordat u de voorbeelden gebruiken, pas de IP-adressen zodat deze overeenkomen met de waarden voor de Azure-regio die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="776e8-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="776e8-422">U vindt deze informatie in de [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="776e8-423">Azure Resource Management-sjabloon</span><span class="sxs-lookup"><span data-stu-id="776e8-423">Azure Resource Management template</span></span>

<span data-ttu-id="776e8-424">De volgende Resource Management-sjabloon maakt u een virtueel netwerk dat binnenkomend verkeer wordt beperkt, maar wordt verkeer van de IP-adressen die door HDInsight vereist.</span><span class="sxs-lookup"><span data-stu-id="776e8-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="776e8-425">Deze sjabloon maakt ook een HDInsight-cluster in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* [<span data-ttu-id="776e8-426">Een beveiligde virtuele Azure-netwerk en een HDInsight Hadoop-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="776e8-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="776e8-427">Wijzig de IP-adressen die in dit voorbeeld overeenkomt met de Azure-regio die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="776e8-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="776e8-428">U vindt deze informatie in de [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="776e8-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="776e8-429">Azure PowerShell</span></span>

<span data-ttu-id="776e8-430">Gebruik de volgende PowerShell-script te maken van een virtueel netwerk waarmee binnenkomend verkeer beperkt en het verkeer van de IP-adressen voor de regio Noord-Europa.</span><span class="sxs-lookup"><span data-stu-id="776e8-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="776e8-431">Wijzig de IP-adressen die in dit voorbeeld overeenkomt met de Azure-regio die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="776e8-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="776e8-432">U vindt deze informatie in de [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="776e8-433">In dit voorbeeld laat zien hoe u regels voor binnenkomend verkeer op de vereiste IP-adressen toestaan toevoegt.</span><span class="sxs-lookup"><span data-stu-id="776e8-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="776e8-434">Het bevat geen een regel voor het beperken van binnenkomende toegang uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="776e8-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="776e8-435">Het volgende voorbeeld toont hoe u SSH toegang via Internet:</span><span class="sxs-lookup"><span data-stu-id="776e8-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="776e8-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="776e8-436">Azure CLI</span></span>

<span data-ttu-id="776e8-437">Gebruik de volgende stappen voor het maken van een virtueel netwerk dat binnenkomend verkeer wordt beperkt, maar wordt verkeer van de IP-adressen die door HDInsight vereist.</span><span class="sxs-lookup"><span data-stu-id="776e8-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="776e8-438">Gebruik de volgende opdracht voor het maken van een nieuwe netwerkbeveiligingsgroep met de naam `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="776e8-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="776e8-439">Vervang **RESOURCEGROUPNAME** met de resourcegroep met de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="776e8-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="776e8-440">Vervang **locatie** met de locatie (regio) die in de groep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="776e8-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="776e8-441">Zodra de groep is gemaakt, krijgt u informatie over de nieuwe groep.</span><span class="sxs-lookup"><span data-stu-id="776e8-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="776e8-442">Gebruik de volgende regels toevoegen aan de nieuwe netwerkbeveiligingsgroep waarmee binnenkomende communicatie op poort 443 van de status en management-service van Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="776e8-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="776e8-443">Vervang **RESOURCEGROUPNAME** met de naam van de resourcegroep met de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="776e8-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="776e8-444">Wijzig de IP-adressen die in dit voorbeeld overeenkomt met de Azure-regio die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="776e8-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="776e8-445">U vindt deze informatie in de [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="776e8-446">Gebruik de volgende opdracht voor het ophalen van de unieke id voor deze netwerkbeveiligingsgroep:</span><span class="sxs-lookup"><span data-stu-id="776e8-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="776e8-447">Met deze opdracht retourneert een waarde die vergelijkbaar is met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="776e8-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="776e8-448">Gebruik dubbele aanhalingstekens rond id in de opdracht als u niet de verwachte resultaten krijgt.</span><span class="sxs-lookup"><span data-stu-id="776e8-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="776e8-449">Gebruik de volgende opdracht toe te passen van de netwerkbeveiligingsgroep aan een subnet.</span><span class="sxs-lookup"><span data-stu-id="776e8-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="776e8-450">Vervang de __GUID__ en __RESOURCEGROUPNAME__ waarden met de resultaten worden geretourneerd van de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="776e8-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="776e8-451">Vervang __VNETNAME__ en __SUBNETNAME__ met de virtuele-netwerknaam en het subnet-naam die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="776e8-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="776e8-452">Zodra deze opdracht is voltooid, kunt u HDInsight kunt installeren in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="776e8-453">Deze stappen alleen toegang tot de HDInsight-status en management service op de Azure-cloud geopend.</span><span class="sxs-lookup"><span data-stu-id="776e8-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="776e8-454">Geen andere toegang hebben tot het HDInsight-cluster buiten het virtuele netwerk is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="776e8-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="776e8-455">Voor toegang van buiten het virtuele netwerk, moet u extra regels van de Netwerkbeveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="776e8-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="776e8-456">Het volgende voorbeeld toont hoe u SSH toegang via Internet:</span><span class="sxs-lookup"><span data-stu-id="776e8-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="776e8-457"><a id="example-dns"></a>Voorbeeld: DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="776e8-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="776e8-458">Naamomzetting tussen een virtueel netwerk en een netwerk verbonden on-premises</span><span class="sxs-lookup"><span data-stu-id="776e8-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="776e8-459">In dit voorbeeld wordt de volgende veronderstellingen:</span><span class="sxs-lookup"><span data-stu-id="776e8-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="776e8-460">U hebt een virtueel netwerk van Azure die is verbonden met een on-premises netwerk via een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="776e8-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="776e8-461">De aangepaste DNS-server in het virtuele netwerk wordt Linux of Unix worden uitgevoerd als het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="776e8-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="776e8-462">[BIND](https://www.isc.org/downloads/bind/) is geïnstalleerd op de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="776e8-463">De aangepaste DNS-server in het virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="776e8-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="776e8-464">Azure PowerShell of Azure CLI gebruiken het DNS-achtervoegsel van het virtuele netwerk te vinden:</span><span class="sxs-lookup"><span data-stu-id="776e8-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="776e8-465">De aangepaste DNS-server voor het virtuele netwerk, gebruikt u de volgende tekst als de inhoud van de `/etc/bind/named.conf.local` bestand:</span><span class="sxs-lookup"><span data-stu-id="776e8-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="776e8-466">Vervang de `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` waarde met de DNS-achtervoegsel van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="776e8-467">Deze configuratie routeert alle DNS-aanvragen voor het DNS-achtervoegsel van het virtuele netwerk naar de Azure recursieve-resolver.</span><span class="sxs-lookup"><span data-stu-id="776e8-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="776e8-468">De aangepaste DNS-server voor het virtuele netwerk, gebruikt u de volgende tekst als de inhoud van de `/etc/bind/named.conf.options` bestand:</span><span class="sxs-lookup"><span data-stu-id="776e8-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="776e8-469">Vervang de `10.0.0.0/16` waarde met het IP-adresbereik van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="776e8-470">Deze vermelding kan name resolution aanvragen adressen binnen dit bereik.</span><span class="sxs-lookup"><span data-stu-id="776e8-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="776e8-471">Toevoegen van het IP-adresbereik van de on-premises netwerk naar de `acl goodclients { ... }` sectie.</span><span class="sxs-lookup"><span data-stu-id="776e8-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="776e8-472">vermelding kan aanvragen voor naamomzetting van resources in de on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="776e8-473">Vervang de waarde `192.168.0.1` met het IP-adres van uw lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="776e8-474">Deze vermelding routeert DNS-aanvragen naar de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="776e8-475">Opnieuw opstarten binding voor het gebruik van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="776e8-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="776e8-476">Bijvoorbeeld `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="776e8-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="776e8-477">Een voorwaardelijke doorstuurserver toevoegen aan de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="776e8-478">Configureer de voorwaardelijke doorstuurserver voor het verzenden van aanvragen voor het DNS-achtervoegsel uit stap 1 voor de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="776e8-479">Raadpleeg de documentatie bij uw DNS-software voor specifieke informatie over het toevoegen van een voorwaardelijke doorstuurserver.</span><span class="sxs-lookup"><span data-stu-id="776e8-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="776e8-480">Na het voltooien van deze stappen kunt u verbinding maken met resources in een netwerk met behulp van de volledig gekwalificeerde domeinnamen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="776e8-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="776e8-481">U kunt nu HDInsight installeren in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="776e8-482">Naamomzetting tussen de twee verbonden virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="776e8-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="776e8-483">In dit voorbeeld wordt de volgende veronderstellingen:</span><span class="sxs-lookup"><span data-stu-id="776e8-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="776e8-484">U hebt twee virtuele netwerken van Azure die zijn verbonden via een VPN-gateway of -peering.</span><span class="sxs-lookup"><span data-stu-id="776e8-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="776e8-485">De aangepaste DNS-server in beide netwerken wordt Linux of Unix worden uitgevoerd als het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="776e8-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="776e8-486">[BIND](https://www.isc.org/downloads/bind/) is geïnstalleerd op de aangepaste DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="776e8-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="776e8-487">Azure PowerShell of Azure CLI gebruiken de DNS-achtervoegsel van beide virtuele netwerken vinden:</span><span class="sxs-lookup"><span data-stu-id="776e8-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="776e8-488">Gebruik de volgende tekst als de inhoud van de `/etc/bind/named.config.local` -bestand op de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="776e8-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="776e8-489">Deze wijziging hebt aangebracht op de aangepaste DNS-server in beide virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="776e8-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="776e8-490">Vervang de `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` waarde met de DNS-achtervoegsel van de __andere__ virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="776e8-491">Deze vermelding routeert aanvragen voor het DNS-achtervoegsel van het externe netwerk naar de aangepaste DNS-server in dat netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="776e8-492">Op de aangepaste DNS-servers in beide virtuele netwerken, gebruikt u de volgende tekst als de inhoud van de `/etc/bind/named.conf.options` bestand:</span><span class="sxs-lookup"><span data-stu-id="776e8-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="776e8-493">Vervang de `10.0.0.0/16` en `10.1.0.0/16` waarden met het IP-adresbereiken van uw virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="776e8-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="776e8-494">Deze vermelding kan resources in elk netwerk aanvragen van de DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="776e8-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="776e8-495">Alle aanvragen die niet voor de DNS-achtervoegsels van de virtuele netwerken (bijvoorbeeld microsoft.com) wordt uitgevoerd door de Azure recursieve-resolver.</span><span class="sxs-lookup"><span data-stu-id="776e8-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="776e8-496">Opnieuw opstarten binding voor het gebruik van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="776e8-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="776e8-497">Bijvoorbeeld: `sudo service bind9 restart` op beide DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="776e8-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="776e8-498">Na het voltooien van deze stappen kunt u verbinding maken met resources in het virtuele netwerk met behulp van de volledig gekwalificeerde domeinnamen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="776e8-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="776e8-499">U kunt nu HDInsight installeren in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="776e8-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="776e8-500">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="776e8-500">Next steps</span></span>

* <span data-ttu-id="776e8-501">Zie voor een voorbeeld van de end-to-end van de configuratie van HDInsight verbinding maken met een on-premises netwerk, [verbinding maken met HDInsight op een on-premises netwerk](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="776e8-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="776e8-502">Zie voor meer informatie over virtuele netwerken in Azure, de [Azure Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="776e8-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="776e8-503">Zie voor meer informatie over netwerkbeveiligingsgroepen [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="776e8-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="776e8-504">Zie voor meer informatie over de gebruiker gedefinieerde routes, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="776e8-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>