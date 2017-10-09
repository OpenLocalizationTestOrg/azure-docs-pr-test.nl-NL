---
title: aaaExtend HDInsight met het virtuele netwerk - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Azure Virtual Network tooconnect HDInsight tooother cloud resources of resources in uw datacenter
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
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="26da3-103">Azure HDInsight met behulp van een Azure-netwerk uitbreiden</span><span class="sxs-lookup"><span data-stu-id="26da3-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="26da3-104">Meer informatie over hoe HDInsight toouse met een [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26da3-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="26da3-105">Een virtueel netwerk van Azure kunt Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="26da3-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="26da3-106">Verbinding tooHDInsight rechtstreeks vanuit een on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="26da3-107">Verbinding maken met HDInsight toodata worden opgeslagen in een virtueel Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="26da3-108">Rechtstreeks toegang tot Hadoop-services die niet openbaar meer dan beschikbaar Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="26da3-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="26da3-109">Kafka-API's of Hallo HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="26da3-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="26da3-110">Hallo-informatie in dit document is een goed begrip van TCP/IP-netwerken vereist.</span><span class="sxs-lookup"><span data-stu-id="26da3-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="26da3-111">Als u niet bekend met TCP/IP-netwerken bent, moet u samenwerken met iemand die dit voordat u wijzigingen tooproduction netwerken.</span><span class="sxs-lookup"><span data-stu-id="26da3-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="26da3-112">Planning</span><span class="sxs-lookup"><span data-stu-id="26da3-112">Planning</span></span>

<span data-ttu-id="26da3-113">Hallo volgen Hallo vragen die u bij het plannen van tooinstall HDInsight in een virtueel netwerk moet beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="26da3-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="26da3-114">Moet u tooinstall HDInsight in een bestaand virtueel netwerk?</span><span class="sxs-lookup"><span data-stu-id="26da3-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="26da3-115">Of maakt u een nieuw netwerk?</span><span class="sxs-lookup"><span data-stu-id="26da3-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="26da3-116">Als u een bestaand virtueel netwerk gebruikt, moet u mogelijk toomodify Hallo netwerkconfiguratie voordat u HDInsight kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="26da3-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="26da3-117">Zie voor meer informatie, Hallo [HDInsight tooan bestaand virtueel netwerk toevoegen](#existingvnet) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="26da3-118">Wilt u tooconnect Hallo virtueel netwerk met HDInsight tooanother virtueel netwerk of uw on-premises netwerk?</span><span class="sxs-lookup"><span data-stu-id="26da3-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="26da3-119">tooeasily werk met bronnen in netwerken, u kunt toocreate een aangepaste DNS-server nodig en doorsturen van DNS-configureren.</span><span class="sxs-lookup"><span data-stu-id="26da3-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="26da3-120">Zie voor meer informatie, Hallo [meerdere netwerken met elkaar verbinden](#multinet) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="26da3-121">Wilt u toch toorestrict/omleiden tooHDInsight binnenkomend of uitgaand verkeer?</span><span class="sxs-lookup"><span data-stu-id="26da3-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="26da3-122">HDInsight moet hebben onbeperkte communicatie met specifieke IP-adressen in hello Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="26da3-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="26da3-123">Er zijn ook verschillende poorten die moeten worden toegestaan via firewalls voor clientcommunicatie.</span><span class="sxs-lookup"><span data-stu-id="26da3-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="26da3-124">Zie voor meer informatie, Hallo [netwerkverkeer beheren](#networktraffic) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="26da3-125"><a id="existingvnet"></a>HDInsight tooan bestaand virtueel netwerk toevoegen</span><span class="sxs-lookup"><span data-stu-id="26da3-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="26da3-126">Gebruik Hallo stappen in deze sectie toodiscover hoe tooadd een nieuwe HDInsight tooan bestaande Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="26da3-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="26da3-127">U kunt een bestaand HDInsight-cluster in een virtueel netwerk niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="26da3-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="26da3-128">Gebruikt u een klassiek of Resource Manager-implementatiemodel voor Hallo virtuele netwerk?</span><span class="sxs-lookup"><span data-stu-id="26da3-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="26da3-129">HDInsight 3,4 en groter vereist een virtueel netwerk van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="26da3-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="26da3-130">Eerdere versies van HDInsight vereist een klassiek virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="26da3-131">Als uw bestaande netwerk een klassiek virtueel netwerk is, moet u een virtueel netwerk van Resource Manager maken en sluit vervolgens Hallo twee.</span><span class="sxs-lookup"><span data-stu-id="26da3-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="26da3-132">[Klassieke vnet's toonew VNets verbinden](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26da3-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="26da3-133">Zodra het is toegevoegd, wordt HDInsight geïnstalleerd in Hallo Resource Manager-netwerk kan communiceren met resources in de klassieke netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="26da3-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="26da3-134">Geforceerde tunneling gebruiken</span><span class="sxs-lookup"><span data-stu-id="26da3-134">Do you use forced tunneling?</span></span> <span data-ttu-id="26da3-135">Geforceerde tunneling is subnetinstelling dat ervoor zorgt dat de uitgaande Internet verkeer tooa apparaat voor controle en logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="26da3-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="26da3-136">HDInsight biedt geen ondersteuning voor geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="26da3-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="26da3-137">Verwijder geforceerde tunneling voordat u HDInsight installeert in een subnet, of een nieuw subnet maken voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26da3-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="26da3-138">Gebruik je netwerkbeveiligingsgroepen, de gebruiker gedefinieerde routes of virtuele netwerkapparaten toorestrict verkeer van of naar Hallo virtuele netwerk?</span><span class="sxs-lookup"><span data-stu-id="26da3-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="26da3-139">Als een beheerde service vereist HDInsight onbeperkte toegang tooseveral IP-adressen in hello Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="26da3-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="26da3-140">tooallow communicatie met deze IP-adressen, eventuele bestaande netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes bijwerken.</span><span class="sxs-lookup"><span data-stu-id="26da3-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="26da3-141">HDInsight als host fungeert voor meerdere services, die verschillende poorten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="26da3-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="26da3-142">Verkeer toothese poorten niet blokkeren.</span><span class="sxs-lookup"><span data-stu-id="26da3-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="26da3-143">Zie voor een lijst met poorten tooallow via virtueel apparaat firewalls, Hallo [beveiliging](#security) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="26da3-144">toofind uw bestaande beveiligingsconfiguratie gebruik hello Azure PowerShell of Azure CLI-opdrachten te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="26da3-145">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="26da3-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="26da3-146">Zie voor meer informatie, Hallo [netwerkbeveiligingsgroepen oplossen](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="26da3-147">Netwerkbeveiligingsgroepen worden toegepast in volgorde op basis van Regelprioriteit.</span><span class="sxs-lookup"><span data-stu-id="26da3-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="26da3-148">Hallo eerste regel die overeenkomt met Hallo verkeer patroon wordt toegepast en geen andere voor dat verkeer wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="26da3-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="26da3-149">De regels van de volgorde van meest strikte tooleast strikte.</span><span class="sxs-lookup"><span data-stu-id="26da3-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="26da3-150">Zie voor meer informatie, Hallo [filteren van netwerkverkeer met netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="26da3-151">Door de gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="26da3-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="26da3-152">Zie voor meer informatie, Hallo [routes oplossen](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="26da3-153">Maken van een HDInsight-cluster en hello Azure Virtual Network selecteren tijdens de configuratie.</span><span class="sxs-lookup"><span data-stu-id="26da3-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="26da3-154">Gebruik Hallo stappen in Hallo aanmaakproces voor documenten toounderstand Hallo-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="26da3-155">Maken van HDInsight met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="26da3-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="26da3-156">HDInsight maken met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="26da3-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="26da3-157">Maken van HDInsight met behulp van Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="26da3-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="26da3-158">HDInsight met behulp van een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="26da3-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="26da3-159">Toevoegen van HDInsight is tooa virtueel netwerk een optionele configuratie-stap.</span><span class="sxs-lookup"><span data-stu-id="26da3-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="26da3-160">Ervoor tooselect Hallo virtueel netwerk worden bij het Hallo-cluster configureren.</span><span class="sxs-lookup"><span data-stu-id="26da3-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="26da3-161"><a id="multinet"></a>Meerdere netwerken met elkaar verbinden</span><span class="sxs-lookup"><span data-stu-id="26da3-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="26da3-162">Hallo grootste uitdaging met een configuratie met meerdere is naamomzetting tussen Hallo netwerken.</span><span class="sxs-lookup"><span data-stu-id="26da3-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="26da3-163">Azure biedt naamomzetting voor Azure-services die zijn geïnstalleerd in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="26da3-164">Deze ingebouwde naamomzetting kunt HDInsight tooconnect toohello resources met behulp van een volledig gekwalificeerde domeinnaam (FQDN) te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="26da3-165">Een resource die beschikbaar is op Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="26da3-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="26da3-166">Bijvoorbeeld microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="26da3-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="26da3-167">Een resource die is in Hallo hetzelfde virtuele netwerk van Azure, met behulp van Hallo __interne DNS-naam__ van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="26da3-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="26da3-168">Wanneer u Hallo standaard naamomzetting gebruikt, zijn Hallo volgende voorbeeld interne DNS-namen toegewezen tooHDInsight worker-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="26da3-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="26da3-169">wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="26da3-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="26da3-170">wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="26da3-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="26da3-171">Deze beide knooppunten kunnen communiceren rechtstreeks met elkaar en andere knooppunten in HDInsight, met behulp van de interne DNS-namen.</span><span class="sxs-lookup"><span data-stu-id="26da3-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="26da3-172">Hallo standaard naamomzetting biedt __niet__ HDInsight tooresolve Hallo namen van bronnen in netwerken die gekoppeld toohello virtueel netwerk zijn toestaan.</span><span class="sxs-lookup"><span data-stu-id="26da3-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="26da3-173">Bijvoorbeeld, het algemene toojoin is uw on-premises netwerk toohello virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="26da3-174">Met alleen Hallo standaard naamomzetting HDInsight kan geen toegang krijgen tot bronnen in Hallo on-premises netwerk met de naam.</span><span class="sxs-lookup"><span data-stu-id="26da3-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="26da3-175">Hallo tegengestelde geldt ook resources in uw on-premises netwerk heeft geen toegang tot resources in Hallo virtueel netwerk met de naam.</span><span class="sxs-lookup"><span data-stu-id="26da3-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="26da3-176">U moet Hallo aangepaste DNS-server maken en configureren van Hallo virtueel netwerk toouse deze voordat u Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="26da3-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="26da3-177">naamomzetting tooenable tussen Hallo virtueel netwerk en bronnen in gekoppelde netwerken, moet u Hallo volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="26da3-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="26da3-178">Maak een aangepaste DNS-server in hello Azure Virtual Network waar u van plan tooinstall HDInsight bent.</span><span class="sxs-lookup"><span data-stu-id="26da3-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="26da3-179">Hallo virtueel netwerk toouse Hallo aangepaste DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="26da3-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="26da3-180">Azure DNS-achtervoegsel voor het virtuele netwerk toegewezen Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="26da3-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="26da3-181">Deze waarde is te vergelijkbare`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="26da3-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="26da3-182">Zie voor informatie over het zoeken naar Hallo DNS-achtervoegsel Hallo [voorbeeld: aangepaste DNS](#example-dns) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="26da3-183">Doorsturen tussen Hallo DNS-servers configureren.</span><span class="sxs-lookup"><span data-stu-id="26da3-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="26da3-184">Hallo-configuratie, is afhankelijk van Hallo-type van het externe netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="26da3-185">Als het externe netwerk Hallo een on-premises netwerk is, configureren van DNS als volgt:</span><span class="sxs-lookup"><span data-stu-id="26da3-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="26da3-186">__Aangepaste DNS__ (in Hallo virtueel netwerk):</span><span class="sxs-lookup"><span data-stu-id="26da3-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="26da3-187">Aanvragen voor Hallo DNS-achtervoegsel van Hallo virtueel netwerk toohello Azure recursieve naamomzetting (168.63.129.16) doorsturen.</span><span class="sxs-lookup"><span data-stu-id="26da3-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="26da3-188">Aanvragen voor bronnen in het virtuele netwerk hello Azure worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="26da3-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="26da3-189">Doorsturen van alle andere aanvragen toohello lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="26da3-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="26da3-190">Hallo lokale DNS verwerkt alle andere aanvragen voor naamomzetting, zelfs aanvragen voor internetbronnen zoals Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="26da3-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="26da3-191">__Lokale DNS__: doorsturen van aanvragen voor Hallo virtueel netwerk DNS-achtervoegsel toohello aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="26da3-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="26da3-192">Hallo aangepaste DNS-server stuurt toohello Azure recursieve resolver.</span><span class="sxs-lookup"><span data-stu-id="26da3-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="26da3-193">Deze configuratie routes aanvragen voor FQDN-namen die Hallo DNS-achtervoegsel van Hallo virtueel netwerk toohello aangepaste DNS-server bevatten.</span><span class="sxs-lookup"><span data-stu-id="26da3-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="26da3-194">Alle andere verzoeken (zelfs voor openbare internet-adressen) worden verwerkt door Hallo lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="26da3-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="26da3-195">Als het externe netwerk Hallo een ander virtueel netwerk van Azure is, configureren van DNS als volgt:</span><span class="sxs-lookup"><span data-stu-id="26da3-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="26da3-196">__Aangepaste DNS__ (in elk virtueel netwerk):</span><span class="sxs-lookup"><span data-stu-id="26da3-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="26da3-197">Aanvragen voor Hallo DNS-achtervoegsel van de virtuele netwerken Hallo doorgestuurd toohello aangepaste DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="26da3-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="26da3-198">Hallo DNS in elk virtueel netwerk is verantwoordelijk voor het oplossen van resources binnen het netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="26da3-199">Alle andere aanvragen toohello Azure recursieve resolver doorsturen.</span><span class="sxs-lookup"><span data-stu-id="26da3-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="26da3-200">Hallo recursieve resolver is verantwoordelijk voor het oplossen van lokale en internetbronnen.</span><span class="sxs-lookup"><span data-stu-id="26da3-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="26da3-201">Hallo DNS-server voor elk netwerk verzendt aanvragen toohello andere, op basis van DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="26da3-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="26da3-202">Andere aanvragen worden omgezet met behulp van hello Azure recursieve resolver.</span><span class="sxs-lookup"><span data-stu-id="26da3-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="26da3-203">Zie voor een voorbeeld van elke configuratie Hallo [voorbeeld: aangepaste DNS](#example-dns) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="26da3-204">Zie voor meer informatie, Hallo [naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="26da3-205">TooHadoop services rechtstreeks verbinding te maken</span><span class="sxs-lookup"><span data-stu-id="26da3-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="26da3-206">De meeste documentatie op HDInsight wordt ervan uitgegaan dat u toegang toohello cluster via Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="26da3-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="26da3-207">Bijvoorbeeld, kunt u de cluster toohello op https://CLUSTERNAME.azurehdinsight.net koppelen.</span><span class="sxs-lookup"><span data-stu-id="26da3-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="26da3-208">Dit adres Hallo openbare-gateway niet beschikbaar is als u nsg's hebt gebruikt of udr's toorestrict toegang vanaf internet Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="26da3-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="26da3-209">tooconnect tooAmbari en andere webpagina's via Hallo virtueel netwerk, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="26da3-210">toodiscover hello interne volledig gekwalificeerde domeinnamen (FQDN) van clusterknooppunten Hallo HDInsight, een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="26da3-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

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

    <span data-ttu-id="26da3-211">Hallo FQDN-naam vinden voor Hallo hoofdknooppunten in Hallo lijst met knooppunten die zijn geretourneerd, en Hallo FQDN's tooconnect tooAmbari en andere webservices gebruiken.</span><span class="sxs-lookup"><span data-stu-id="26da3-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="26da3-212">Bijvoorbeeld: `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="26da3-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="26da3-213">Sommige services die worden gehost op Hallo hoofdknooppunten zijn alleen actief is op één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="26da3-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="26da3-214">Als u probeert toegang tot een service op één hoofdknooppunt en een 404-fout retourneert, overschakelen toohello andere hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="26da3-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="26da3-215">toodetermine hello knooppunt en de poort die een service is beschikbaar op, Zie Hallo [poorten die worden gebruikt door de services van Hadoop op HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="26da3-216"><a id="networktraffic"></a>Beheren van netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="26da3-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="26da3-217">Netwerkverkeer in een virtuele Azure-netwerken kan worden beheerd met behulp van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="26da3-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="26da3-218">**Netwerkbeveiligingsgroepen** (NSG) kunt u toofilter binnenkomend en uitgaand verkeer toohello netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="26da3-219">Zie voor meer informatie, Hallo [filteren van netwerkverkeer met netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="26da3-220">HDInsight biedt geen ondersteuning voor uitgaand verkeer te beperken.</span><span class="sxs-lookup"><span data-stu-id="26da3-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="26da3-221">**Gebruiker gedefinieerde routes** (UDR) definiëren hoe verkeer tussen resources in Hallo netwerk loopt.</span><span class="sxs-lookup"><span data-stu-id="26da3-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="26da3-222">Zie voor meer informatie, Hallo [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="26da3-223">**Virtuele apparaten** Hallo-functionaliteit van apparaten, zoals firewalls en routers repliceren.</span><span class="sxs-lookup"><span data-stu-id="26da3-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="26da3-224">Zie voor meer informatie, Hallo [netwerkapparaten](https://azure.microsoft.com/solutions/network-appliances) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="26da3-225">Als een beheerde service moet HDInsight onbeperkte toegang tooAzure status en beheer van services in hello Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="26da3-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="26da3-226">Wanneer u nsg's en udr's, moet u ervoor zorgen dat HDInsight deze services nog steeds met HDInsight communiceren kunnen.</span><span class="sxs-lookup"><span data-stu-id="26da3-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="26da3-227">HDInsight beschrijft de services op verschillende poorten.</span><span class="sxs-lookup"><span data-stu-id="26da3-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="26da3-228">Wanneer u een virtueel apparaat firewall gebruikt, moet u verkeer op Hallo poorten die worden gebruikt voor deze services toestaan.</span><span class="sxs-lookup"><span data-stu-id="26da3-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="26da3-229">Zie Hallo [vereiste poorten] sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="26da3-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="26da3-230"><a id="hdinsight-ip"></a>HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="26da3-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="26da3-231">Als u gebruiken wilt **netwerkbeveiligingsgroepen** of **gebruiker gedefinieerde routes** toocontrol netwerkverkeer, voert u Hallo van de volgende activiteiten voor de installatie van HDInsight:</span><span class="sxs-lookup"><span data-stu-id="26da3-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="26da3-232">Identificeer hello Azure dat u van plan toouse voor HDInsight bent-regio.</span><span class="sxs-lookup"><span data-stu-id="26da3-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="26da3-233">Hallo IP-adressen vereist voor HDInsight identificeren.</span><span class="sxs-lookup"><span data-stu-id="26da3-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="26da3-234">Zie voor meer informatie, Hallo [IP-adressen die zijn vereist voor HDInsight](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="26da3-235">Hallo netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes voor Hallo subnet dat u van plan tooinstall HDInsight bent maakt of wijzigt in.</span><span class="sxs-lookup"><span data-stu-id="26da3-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="26da3-236">__Netwerkbeveiligingsgroepen__: toestaan __inkomende__ verkeer op poort __443__ van Hallo IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="26da3-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="26da3-237">__Gebruiker gedefinieerde routes__: maken van een route tooeach IP-adres en Hallo __volgende hop type__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="26da3-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="26da3-238">Zie voor meer informatie over netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes Hallo documentatie te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="26da3-239">Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="26da3-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="26da3-240">Gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="26da3-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="26da3-241">Geforceerde tunneling</span><span class="sxs-lookup"><span data-stu-id="26da3-241">Forced tunneling</span></span>

<span data-ttu-id="26da3-242">Geforceerde tunneling is een door de gebruiker gedefinieerde routering configuratie waarbij alle verkeer van een subnet geforceerde tooa specifieke netwerk- of locatie, zoals uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="26da3-243">HDInsight biedt __niet__ ondersteuning geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="26da3-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="26da3-244"><a id="hdinsight-ip"></a>Vereiste IP-adressen</span><span class="sxs-lookup"><span data-stu-id="26da3-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26da3-245">Hallo Azure health en beheerservices moet kunnen toocommunicate met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26da3-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="26da3-246">Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes gebruikt, kunt u verkeer van Hallo IP-adressen voor deze services tooreach HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26da3-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="26da3-247">Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes toocontrol verkeer niet gebruikt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="26da3-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="26da3-248">Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes gebruikt, moet u het verkeer van hello Azure status- en management services tooreach HDInsight toestaan.</span><span class="sxs-lookup"><span data-stu-id="26da3-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="26da3-249">Gebruik Hallo volgende stappen toofind Hallo IP-adressen die moeten worden toegestaan:</span><span class="sxs-lookup"><span data-stu-id="26da3-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="26da3-250">U moet altijd verkeer van Hallo volgende IP-adressen toestaan:</span><span class="sxs-lookup"><span data-stu-id="26da3-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="26da3-251">IP-adres</span><span class="sxs-lookup"><span data-stu-id="26da3-251">IP address</span></span> | <span data-ttu-id="26da3-252">Toegestane poort</span><span class="sxs-lookup"><span data-stu-id="26da3-252">Allowed port</span></span> | <span data-ttu-id="26da3-253">Richting</span><span class="sxs-lookup"><span data-stu-id="26da3-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="26da3-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="26da3-254">168.61.49.99</span></span> | <span data-ttu-id="26da3-255">443</span><span class="sxs-lookup"><span data-stu-id="26da3-255">443</span></span> | <span data-ttu-id="26da3-256">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-256">Inbound</span></span> |
    | <span data-ttu-id="26da3-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="26da3-257">23.99.5.239</span></span> | <span data-ttu-id="26da3-258">443</span><span class="sxs-lookup"><span data-stu-id="26da3-258">443</span></span> | <span data-ttu-id="26da3-259">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-259">Inbound</span></span> |
    | <span data-ttu-id="26da3-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="26da3-260">168.61.48.131</span></span> | <span data-ttu-id="26da3-261">443</span><span class="sxs-lookup"><span data-stu-id="26da3-261">443</span></span> | <span data-ttu-id="26da3-262">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-262">Inbound</span></span> |
    | <span data-ttu-id="26da3-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="26da3-263">138.91.141.162</span></span> | <span data-ttu-id="26da3-264">443</span><span class="sxs-lookup"><span data-stu-id="26da3-264">443</span></span> | <span data-ttu-id="26da3-265">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-265">Inbound</span></span> |

2. <span data-ttu-id="26da3-266">Als uw HDInsight-cluster zich in een van de volgende regio's hello, moet u verkeer van Hallo IP-adressen die worden vermeld voor Hallo regio toestaan:</span><span class="sxs-lookup"><span data-stu-id="26da3-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="26da3-267">Als u gebruikmaakt van Azure-regio Hallo niet wordt weergegeven, klikt u vervolgens alleen gebruiken Hallo vier IP-adressen uit stap 1.</span><span class="sxs-lookup"><span data-stu-id="26da3-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="26da3-268">Land</span><span class="sxs-lookup"><span data-stu-id="26da3-268">Country</span></span> | <span data-ttu-id="26da3-269">Regio</span><span class="sxs-lookup"><span data-stu-id="26da3-269">Region</span></span> | <span data-ttu-id="26da3-270">Toegestane IP-adressen</span><span class="sxs-lookup"><span data-stu-id="26da3-270">Allowed IP addresses</span></span> | <span data-ttu-id="26da3-271">Toegestane poort</span><span class="sxs-lookup"><span data-stu-id="26da3-271">Allowed port</span></span> | <span data-ttu-id="26da3-272">Richting</span><span class="sxs-lookup"><span data-stu-id="26da3-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="26da3-273">Azië</span><span class="sxs-lookup"><span data-stu-id="26da3-273">Asia</span></span> | <span data-ttu-id="26da3-274">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="26da3-274">East Asia</span></span> | <span data-ttu-id="26da3-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="26da3-275">23.102.235.122</span></span></br><span data-ttu-id="26da3-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="26da3-276">52.175.38.134</span></span> | <span data-ttu-id="26da3-277">443</span><span class="sxs-lookup"><span data-stu-id="26da3-277">443</span></span> | <span data-ttu-id="26da3-278">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-279">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="26da3-279">Southeast Asia</span></span> | <span data-ttu-id="26da3-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="26da3-280">13.76.245.160</span></span></br><span data-ttu-id="26da3-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="26da3-281">13.76.136.249</span></span> | <span data-ttu-id="26da3-282">443</span><span class="sxs-lookup"><span data-stu-id="26da3-282">443</span></span> | <span data-ttu-id="26da3-283">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-283">Inbound</span></span> |
    | <span data-ttu-id="26da3-284">Australië</span><span class="sxs-lookup"><span data-stu-id="26da3-284">Australia</span></span> | <span data-ttu-id="26da3-285">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="26da3-285">Australia East</span></span> | <span data-ttu-id="26da3-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="26da3-286">104.210.84.115</span></span></br><span data-ttu-id="26da3-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="26da3-287">13.75.152.195</span></span> | <span data-ttu-id="26da3-288">443</span><span class="sxs-lookup"><span data-stu-id="26da3-288">443</span></span> | <span data-ttu-id="26da3-289">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-290">Australië - zuidoost</span><span class="sxs-lookup"><span data-stu-id="26da3-290">Australia Southeast</span></span> | <span data-ttu-id="26da3-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="26da3-291">13.77.2.56</span></span></br><span data-ttu-id="26da3-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="26da3-292">13.77.2.94</span></span> | <span data-ttu-id="26da3-293">443</span><span class="sxs-lookup"><span data-stu-id="26da3-293">443</span></span> | <span data-ttu-id="26da3-294">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-294">Inbound</span></span> |
    | <span data-ttu-id="26da3-295">Brazilië</span><span class="sxs-lookup"><span data-stu-id="26da3-295">Brazil</span></span> | <span data-ttu-id="26da3-296">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="26da3-296">Brazil South</span></span> | <span data-ttu-id="26da3-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="26da3-297">191.235.84.104</span></span></br><span data-ttu-id="26da3-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="26da3-298">191.235.87.113</span></span> | <span data-ttu-id="26da3-299">443</span><span class="sxs-lookup"><span data-stu-id="26da3-299">443</span></span> | <span data-ttu-id="26da3-300">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-300">Inbound</span></span> |
    | <span data-ttu-id="26da3-301">Canada</span><span class="sxs-lookup"><span data-stu-id="26da3-301">Canada</span></span> | <span data-ttu-id="26da3-302">Canada - oost</span><span class="sxs-lookup"><span data-stu-id="26da3-302">Canada East</span></span> | <span data-ttu-id="26da3-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="26da3-303">52.229.127.96</span></span></br><span data-ttu-id="26da3-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="26da3-304">52.229.123.172</span></span> | <span data-ttu-id="26da3-305">443</span><span class="sxs-lookup"><span data-stu-id="26da3-305">443</span></span> | <span data-ttu-id="26da3-306">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-307">Canada - midden</span><span class="sxs-lookup"><span data-stu-id="26da3-307">Canada Central</span></span> | <span data-ttu-id="26da3-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="26da3-308">52.228.37.66</span></span></br><span data-ttu-id="26da3-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="26da3-309">52.228.45.222</span></span> | <span data-ttu-id="26da3-310">443</span><span class="sxs-lookup"><span data-stu-id="26da3-310">443</span></span> | <span data-ttu-id="26da3-311">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-311">Inbound</span></span> |
    | <span data-ttu-id="26da3-312">China</span><span class="sxs-lookup"><span data-stu-id="26da3-312">China</span></span> | <span data-ttu-id="26da3-313">China - noord</span><span class="sxs-lookup"><span data-stu-id="26da3-313">China North</span></span> | <span data-ttu-id="26da3-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="26da3-314">42.159.96.170</span></span></br><span data-ttu-id="26da3-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="26da3-315">139.217.2.219</span></span> | <span data-ttu-id="26da3-316">443</span><span class="sxs-lookup"><span data-stu-id="26da3-316">443</span></span> | <span data-ttu-id="26da3-317">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-318">China - oost</span><span class="sxs-lookup"><span data-stu-id="26da3-318">China East</span></span> | <span data-ttu-id="26da3-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="26da3-319">42.159.198.178</span></span></br><span data-ttu-id="26da3-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="26da3-320">42.159.234.157</span></span> | <span data-ttu-id="26da3-321">443</span><span class="sxs-lookup"><span data-stu-id="26da3-321">443</span></span> | <span data-ttu-id="26da3-322">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-322">Inbound</span></span> |
    | <span data-ttu-id="26da3-323">Europa</span><span class="sxs-lookup"><span data-stu-id="26da3-323">Europe</span></span> | <span data-ttu-id="26da3-324">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="26da3-324">North Europe</span></span> | <span data-ttu-id="26da3-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="26da3-325">52.164.210.96</span></span></br><span data-ttu-id="26da3-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="26da3-326">13.74.153.132</span></span> | <span data-ttu-id="26da3-327">443</span><span class="sxs-lookup"><span data-stu-id="26da3-327">443</span></span> | <span data-ttu-id="26da3-328">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-329">West-Europa</span><span class="sxs-lookup"><span data-stu-id="26da3-329">West Europe</span></span>| <span data-ttu-id="26da3-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="26da3-330">52.166.243.90</span></span></br><span data-ttu-id="26da3-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="26da3-331">52.174.36.244</span></span> | <span data-ttu-id="26da3-332">443</span><span class="sxs-lookup"><span data-stu-id="26da3-332">443</span></span> | <span data-ttu-id="26da3-333">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-333">Inbound</span></span> |
    | <span data-ttu-id="26da3-334">Duitsland</span><span class="sxs-lookup"><span data-stu-id="26da3-334">Germany</span></span> | <span data-ttu-id="26da3-335">Duitsland - centraal</span><span class="sxs-lookup"><span data-stu-id="26da3-335">Germany Central</span></span> | <span data-ttu-id="26da3-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="26da3-336">51.4.146.68</span></span></br><span data-ttu-id="26da3-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="26da3-337">51.4.146.80</span></span> | <span data-ttu-id="26da3-338">443</span><span class="sxs-lookup"><span data-stu-id="26da3-338">443</span></span> | <span data-ttu-id="26da3-339">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-340">Duitsland - noordoost</span><span class="sxs-lookup"><span data-stu-id="26da3-340">Germany Northeast</span></span> | <span data-ttu-id="26da3-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="26da3-341">51.5.150.132</span></span></br><span data-ttu-id="26da3-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="26da3-342">51.5.144.101</span></span> | <span data-ttu-id="26da3-343">443</span><span class="sxs-lookup"><span data-stu-id="26da3-343">443</span></span> | <span data-ttu-id="26da3-344">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-344">Inbound</span></span> |
    | <span data-ttu-id="26da3-345">India</span><span class="sxs-lookup"><span data-stu-id="26da3-345">India</span></span> | <span data-ttu-id="26da3-346">Centraal-India</span><span class="sxs-lookup"><span data-stu-id="26da3-346">Central India</span></span> | <span data-ttu-id="26da3-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="26da3-347">52.172.153.209</span></span></br><span data-ttu-id="26da3-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="26da3-348">52.172.152.49</span></span> | <span data-ttu-id="26da3-349">443</span><span class="sxs-lookup"><span data-stu-id="26da3-349">443</span></span> | <span data-ttu-id="26da3-350">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-350">Inbound</span></span> |
    | <span data-ttu-id="26da3-351">Japan</span><span class="sxs-lookup"><span data-stu-id="26da3-351">Japan</span></span> | <span data-ttu-id="26da3-352">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="26da3-352">Japan East</span></span> | <span data-ttu-id="26da3-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="26da3-353">13.78.125.90</span></span></br><span data-ttu-id="26da3-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="26da3-354">13.78.89.60</span></span> | <span data-ttu-id="26da3-355">443</span><span class="sxs-lookup"><span data-stu-id="26da3-355">443</span></span> | <span data-ttu-id="26da3-356">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-357">Japan - west</span><span class="sxs-lookup"><span data-stu-id="26da3-357">Japan West</span></span> | <span data-ttu-id="26da3-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="26da3-358">40.74.125.69</span></span></br><span data-ttu-id="26da3-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="26da3-359">138.91.29.150</span></span> | <span data-ttu-id="26da3-360">443</span><span class="sxs-lookup"><span data-stu-id="26da3-360">443</span></span> | <span data-ttu-id="26da3-361">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-361">Inbound</span></span> |
    | <span data-ttu-id="26da3-362">Korea</span><span class="sxs-lookup"><span data-stu-id="26da3-362">Korea</span></span> | <span data-ttu-id="26da3-363">Korea - centraal</span><span class="sxs-lookup"><span data-stu-id="26da3-363">Korea Central</span></span> | <span data-ttu-id="26da3-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="26da3-364">52.231.39.142</span></span></br><span data-ttu-id="26da3-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="26da3-365">52.231.36.209</span></span> | <span data-ttu-id="26da3-366">433</span><span class="sxs-lookup"><span data-stu-id="26da3-366">433</span></span> | <span data-ttu-id="26da3-367">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-368">Korea - zuid</span><span class="sxs-lookup"><span data-stu-id="26da3-368">Korea South</span></span> | <span data-ttu-id="26da3-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="26da3-369">52.231.203.16</span></span></br><span data-ttu-id="26da3-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="26da3-370">52.231.205.214</span></span> | <span data-ttu-id="26da3-371">443</span><span class="sxs-lookup"><span data-stu-id="26da3-371">443</span></span> | <span data-ttu-id="26da3-372">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-372">Inbound</span></span>
    | <span data-ttu-id="26da3-373">Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="26da3-373">United Kingdom</span></span> | <span data-ttu-id="26da3-374">Verenigd Koninkrijk West</span><span class="sxs-lookup"><span data-stu-id="26da3-374">UK West</span></span> | <span data-ttu-id="26da3-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="26da3-375">51.141.13.110</span></span></br><span data-ttu-id="26da3-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="26da3-376">51.141.7.20</span></span> | <span data-ttu-id="26da3-377">443</span><span class="sxs-lookup"><span data-stu-id="26da3-377">443</span></span> | <span data-ttu-id="26da3-378">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-379">Verenigd Koninkrijk Zuid</span><span class="sxs-lookup"><span data-stu-id="26da3-379">UK South</span></span> | <span data-ttu-id="26da3-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="26da3-380">51.140.47.39</span></span></br><span data-ttu-id="26da3-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="26da3-381">51.140.52.16</span></span> | <span data-ttu-id="26da3-382">443</span><span class="sxs-lookup"><span data-stu-id="26da3-382">443</span></span> | <span data-ttu-id="26da3-383">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-383">Inbound</span></span> |
    | <span data-ttu-id="26da3-384">Verenigde Staten</span><span class="sxs-lookup"><span data-stu-id="26da3-384">United States</span></span> | <span data-ttu-id="26da3-385">VS - midden</span><span class="sxs-lookup"><span data-stu-id="26da3-385">Central US</span></span> | <span data-ttu-id="26da3-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="26da3-386">13.67.223.215</span></span></br><span data-ttu-id="26da3-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="26da3-387">40.86.83.253</span></span> | <span data-ttu-id="26da3-388">443</span><span class="sxs-lookup"><span data-stu-id="26da3-388">443</span></span> | <span data-ttu-id="26da3-389">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-390">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="26da3-390">North Central US</span></span> | <span data-ttu-id="26da3-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="26da3-391">157.56.8.38</span></span></br><span data-ttu-id="26da3-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="26da3-392">157.55.213.99</span></span> | <span data-ttu-id="26da3-393">443</span><span class="sxs-lookup"><span data-stu-id="26da3-393">443</span></span> | <span data-ttu-id="26da3-394">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-395">West-centraal VS</span><span class="sxs-lookup"><span data-stu-id="26da3-395">West Central US</span></span> | <span data-ttu-id="26da3-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="26da3-396">52.161.23.15</span></span></br><span data-ttu-id="26da3-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="26da3-397">52.161.10.167</span></span> | <span data-ttu-id="26da3-398">443</span><span class="sxs-lookup"><span data-stu-id="26da3-398">443</span></span> | <span data-ttu-id="26da3-399">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="26da3-400">VS - west 2</span><span class="sxs-lookup"><span data-stu-id="26da3-400">West US 2</span></span> | <span data-ttu-id="26da3-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="26da3-401">52.175.211.210</span></span></br><span data-ttu-id="26da3-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="26da3-402">52.175.222.222</span></span> | <span data-ttu-id="26da3-403">443</span><span class="sxs-lookup"><span data-stu-id="26da3-403">443</span></span> | <span data-ttu-id="26da3-404">Inkomend</span><span class="sxs-lookup"><span data-stu-id="26da3-404">Inbound</span></span> |

    <span data-ttu-id="26da3-405">Zie voor informatie over het Hallo-IP toouse voor Azure Government adressen, Hallo [Azure Government Intelligence en analyse](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="26da3-406">Als u een aangepaste DNS-server met het virtuele netwerk gebruikt, moet u ook toegang vanaf toestaan __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="26da3-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="26da3-407">Dit adres is van de Azure recursieve naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="26da3-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="26da3-408">Zie voor meer informatie, Hallo [naamomzetting voor VM's en rol exemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="26da3-409">Zie voor meer informatie, Hallo [netwerkverkeer beheren](#networktraffic) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="26da3-410"><a id="hdinsight-ports"></a>Vereiste poorten</span><span class="sxs-lookup"><span data-stu-id="26da3-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="26da3-411">Als u van plan bent met een netwerk **virtueel apparaat firewall** toosecure Hallo virtueel netwerk, moet u uitgaand verkeer toestaan op Hallo poorten te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="26da3-412">53</span><span class="sxs-lookup"><span data-stu-id="26da3-412">53</span></span>
* <span data-ttu-id="26da3-413">443</span><span class="sxs-lookup"><span data-stu-id="26da3-413">443</span></span>
* <span data-ttu-id="26da3-414">1433</span><span class="sxs-lookup"><span data-stu-id="26da3-414">1433</span></span>
* <span data-ttu-id="26da3-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="26da3-415">11000-11999</span></span>
* <span data-ttu-id="26da3-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="26da3-416">14000-14999</span></span>

<span data-ttu-id="26da3-417">Zie voor een lijst met poorten voor specifieke services, Hallo [poorten die worden gebruikt door de services van Hadoop op HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="26da3-418">Zie voor meer informatie over firewallregels voor virtuele apparaten Hallo [virtueel apparaat scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span><span class="sxs-lookup"><span data-stu-id="26da3-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="26da3-419"><a id="hdinsight-nsg"></a>Voorbeeld: netwerkbeveiligingsgroepen met HDInsight</span><span class="sxs-lookup"><span data-stu-id="26da3-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="26da3-420">Hallo-voorbeelden in deze sectie laten zien hoe de netwerkbeveiligingsgroep toocreate regels die HDInsight toocommunicate Hello Azure management-services toestaan.</span><span class="sxs-lookup"><span data-stu-id="26da3-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="26da3-421">Voordat u Hallo voorbeelden, aanpassen Hallo IP-adressen toomatch Hallo waarden voor hello Azure-regio u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="26da3-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="26da3-422">U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="26da3-423">Azure Resource Management-sjabloon</span><span class="sxs-lookup"><span data-stu-id="26da3-423">Azure Resource Management template</span></span>

<span data-ttu-id="26da3-424">Hallo maakt volgende Resource Management-sjabloon een virtueel netwerk dat binnenkomend verkeer wordt beperkt, maar wordt verkeer van Hallo IP-adressen vereist voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26da3-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="26da3-425">Deze sjabloon maakt ook een HDInsight-cluster in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="26da3-426">Een beveiligde virtuele Azure-netwerk en een HDInsight Hadoop-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="26da3-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="26da3-427">Hallo IP-adressen in dit voorbeeld toomatch hello Azure-regio u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="26da3-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="26da3-428">U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="26da3-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="26da3-429">Azure PowerShell</span></span>

<span data-ttu-id="26da3-430">Hallo volgende PowerShell-script toocreate een virtueel netwerk dat binnenkomend verkeer beperkt en kunt verkeer van Hallo IP-adressen voor de regio Noord-Europa hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="26da3-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26da3-431">Hallo IP-adressen in dit voorbeeld toomatch hello Azure-regio u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="26da3-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="26da3-432">U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
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
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="26da3-433">In dit voorbeeld laat zien hoe tooadd regels tooallow binnenkomend verkeer op Hallo vereist IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="26da3-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="26da3-434">Het bevat geen een toorestrict regel binnenkomende toegang uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="26da3-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="26da3-435">Hallo volgende voorbeeld laat zien hoe tooenable SSH vanaf Hallo Internet toegang tot:</span><span class="sxs-lookup"><span data-stu-id="26da3-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="26da3-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="26da3-436">Azure CLI</span></span>

<span data-ttu-id="26da3-437">Hallo te volgen stappen toocreate een virtueel netwerk dat binnenkomend verkeer wordt beperkt, maar verkeer van Hallo IP-adressen vereist voor HDInsight kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="26da3-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="26da3-438">Gebruik Hallo na de opdracht toocreate een nieuwe netwerkbeveiligingsgroep met de naam `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="26da3-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="26da3-439">Vervang **RESOURCEGROUPNAME** met de resourcegroep Hallo met hello Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="26da3-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="26da3-440">Vervang **locatie** met Hallo locatie (regio) in die groep Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="26da3-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="26da3-441">Zodra het Hallo-groep is gemaakt, krijgt u informatie over de nieuwe groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="26da3-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="26da3-442">Hallo na tooadd regels toohello nieuwe netwerkbeveiligingsgroep waarmee binnenkomende communicatie op poort 443 van hello Azure HDInsight-status en management-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="26da3-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="26da3-443">Vervang **RESOURCEGROUPNAME** met Hallo-naam van resourcegroep Hallo met hello Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="26da3-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="26da3-444">Hallo IP-adressen in dit voorbeeld toomatch hello Azure-regio u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="26da3-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="26da3-445">U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="26da3-446">tooretrieve unieke id voor deze netwerkbeveiligingsgroep hello, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="26da3-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="26da3-447">Met deze opdracht retourneert een waarde van een vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="26da3-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="26da3-448">Gebruik dubbele aanhalingstekens rond id in Hallo opdracht als u geen Hallo verwacht resultaten krijgt.</span><span class="sxs-lookup"><span data-stu-id="26da3-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="26da3-449">Gebruik hello opdracht tooapply Hallo beveiliging groep tooa netwerksubnet te volgen.</span><span class="sxs-lookup"><span data-stu-id="26da3-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="26da3-450">Vervang Hallo __GUID__ en __RESOURCEGROUPNAME__ waarden Hello die zijn geretourneerd door de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="26da3-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="26da3-451">Vervang __VNETNAME__ en __SUBNETNAME__ met virtuele-netwerknaam Hallo en subnetnaam die u toocreate wilt.</span><span class="sxs-lookup"><span data-stu-id="26da3-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="26da3-452">Zodra deze opdracht is voltooid, kunt u HDInsight kunt installeren in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26da3-453">Deze stappen alleen openen access toohello HDInsight status en de management-service op Hallo Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="26da3-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="26da3-454">Alle andere toegang toohello HDInsight-cluster van externe Hallo virtueel netwerk is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="26da3-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="26da3-455">tooenable toegang van buiten Hallo virtueel netwerk, moet u extra regels van de Netwerkbeveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="26da3-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="26da3-456">Hallo volgende voorbeeld laat zien hoe tooenable SSH vanaf Hallo Internet toegang tot:</span><span class="sxs-lookup"><span data-stu-id="26da3-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="26da3-457"><a id="example-dns"></a>Voorbeeld: DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="26da3-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="26da3-458">Naamomzetting tussen een virtueel netwerk en een netwerk verbonden on-premises</span><span class="sxs-lookup"><span data-stu-id="26da3-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="26da3-459">In dit voorbeeld maakt Hallo veronderstellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="26da3-460">U hebt een Azure-netwerk dat is verbonden tooan on-premises netwerk via een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="26da3-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="26da3-461">aangepaste DNS-server in het virtuele netwerk Hallo Hallo wordt Linux of Unix als Hallo besturingssysteem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26da3-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="26da3-462">[BIND](https://www.isc.org/downloads/bind/) op Hallo aangepaste DNS-server is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="26da3-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="26da3-463">Op Hallo aangepaste DNS-server in het virtuele netwerk Hallo:</span><span class="sxs-lookup"><span data-stu-id="26da3-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="26da3-464">Azure PowerShell of Azure CLI toofind Hallo DNS-achtervoegsel van het virtuele netwerk hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="26da3-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="26da3-465">Gebruik op Hallo aangepaste DNS-server voor het virtuele netwerk hello, na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.local` bestand:</span><span class="sxs-lookup"><span data-stu-id="26da3-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="26da3-466">Vervang Hallo `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` waarde met de Hallo DNS-achtervoegsel van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="26da3-467">Deze configuratie alle DNS-aanvragen voor Hallo DNS-achtervoegsel van Hallo virtueel netwerk toohello Azure recursieve resolver gestuurd.</span><span class="sxs-lookup"><span data-stu-id="26da3-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="26da3-468">Gebruik op Hallo aangepaste DNS-server voor het virtuele netwerk hello, na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.options` bestand:</span><span class="sxs-lookup"><span data-stu-id="26da3-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="26da3-469">Vervang Hallo `10.0.0.0/16` waarde met de Hallo IP-adresbereik van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="26da3-470">Deze vermelding kan name resolution aanvragen adressen binnen dit bereik.</span><span class="sxs-lookup"><span data-stu-id="26da3-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="26da3-471">Hallo IP-adresbereik van Hallo lokale netwerk toohello `acl goodclients { ... }` sectie.</span><span class="sxs-lookup"><span data-stu-id="26da3-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="26da3-472">vermelding kan aanvragen voor naamomzetting van resources in Hallo on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="26da3-473">Vervang de waarde Hallo `192.168.0.1` met Hallo IP-adres van uw lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="26da3-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="26da3-474">Deze vermelding routeert alle andere DNS-aanvragen toohello lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="26da3-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="26da3-475">configuratie van toouse hello, binding opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="26da3-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="26da3-476">Bijvoorbeeld `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="26da3-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="26da3-477">Een voorwaardelijke doorstuurserver toohello lokale DNS-server toevoegen.</span><span class="sxs-lookup"><span data-stu-id="26da3-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="26da3-478">Hallo voorwaardelijke doorstuurserver toosend aanvragen voor Hallo DNS-achtervoegsel van stap 1 toohello aangepaste DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="26da3-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="26da3-479">Raadpleeg Hallo documentatie bij uw DNS-software voor specifieke informatie over het tooadd een voorwaardelijke doorstuurserver.</span><span class="sxs-lookup"><span data-stu-id="26da3-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="26da3-480">Na het voltooien van deze stappen kunt u tooresources in een netwerk met behulp van de volledig gekwalificeerde domeinnamen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="26da3-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="26da3-481">U kunt nu HDInsight installeren in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="26da3-482">Naamomzetting tussen de twee verbonden virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="26da3-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="26da3-483">In dit voorbeeld maakt Hallo veronderstellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="26da3-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="26da3-484">U hebt twee virtuele netwerken van Azure die zijn verbonden via een VPN-gateway of -peering.</span><span class="sxs-lookup"><span data-stu-id="26da3-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="26da3-485">Hallo aangepaste DNS-server in beide netwerken wordt Linux of Unix als Hallo besturingssysteem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26da3-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="26da3-486">[BIND](https://www.isc.org/downloads/bind/) op Hallo aangepaste DNS-servers is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="26da3-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="26da3-487">Gebruik Azure PowerShell of Azure CLI toofind Hallo DNS-achtervoegsel van beide virtuele netwerken:</span><span class="sxs-lookup"><span data-stu-id="26da3-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="26da3-488">Gebruik Hallo na de tekst hello inhoud Hallo `/etc/bind/named.config.local` -bestand op Hallo aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="26da3-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="26da3-489">Deze wijziging hebt aangebracht op Hallo aangepaste DNS-server in beide virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="26da3-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="26da3-490">Vervang Hallo `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` waarde met de DNS-achtervoegsel Hallo Hallo __andere__ virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="26da3-491">Deze vermelding aanvragen voor Hallo DNS-achtervoegsel van Hallo extern netwerk toohello gestuurd aangepaste DNS-server in dat netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="26da3-492">Gebruik op Hallo aangepaste DNS-servers in beide virtuele netwerken, na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.options` bestand:</span><span class="sxs-lookup"><span data-stu-id="26da3-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
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

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="26da3-493">Vervang Hallo `10.0.0.0/16` en `10.1.0.0/16` waarden met Hallo IP-adresbereiken van uw virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="26da3-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="26da3-494">Deze vermelding kan resources in elke netwerk toomake aanvragen van Hallo DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="26da3-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="26da3-495">Alle aanvragen die niet voor DNS-achtervoegsels Hallo Hallo virtuele netwerken (bijvoorbeeld microsoft.com) wordt uitgevoerd door hello Azure recursieve resolver.</span><span class="sxs-lookup"><span data-stu-id="26da3-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="26da3-496">configuratie van toouse hello, binding opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="26da3-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="26da3-497">Bijvoorbeeld: `sudo service bind9 restart` op beide DNS-servers.</span><span class="sxs-lookup"><span data-stu-id="26da3-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="26da3-498">Na het voltooien van deze stappen kunt u tooresources in Hallo virtueel netwerk met behulp van de volledig gekwalificeerde domeinnamen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="26da3-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="26da3-499">U kunt nu HDInsight installeren in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="26da3-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26da3-500">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26da3-500">Next steps</span></span>

* <span data-ttu-id="26da3-501">Zie voor een voorbeeld van de end-to-end van de configuratie van HDInsight tooconnect tooan on-premises netwerk, [verbinding maken met HDInsight tooan on-premises netwerk](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="26da3-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="26da3-502">Zie voor meer informatie over virtuele netwerken van Azure Hallo [Azure Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26da3-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="26da3-503">Zie voor meer informatie over netwerkbeveiligingsgroepen [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="26da3-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="26da3-504">Zie voor meer informatie over de gebruiker gedefinieerde routes, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26da3-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>