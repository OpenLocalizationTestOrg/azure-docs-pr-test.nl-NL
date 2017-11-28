---
title: Server-beschikbaarheidsgroepen - virtuele Machines van de Azure - noodherstel aaaSQL | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooconfigure de beschikbaarheid van een SQL Server op Azure virtuele machines met een replica in een andere regio groepeert.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="c404b-103">Een AlwaysOn-beschikbaarheidsgroep configureren op virtuele Azure-machines in verschillende regio 's</span><span class="sxs-lookup"><span data-stu-id="c404b-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="c404b-104">Dit artikel wordt uitgelegd hoe tooconfigure een SQL Server Always On availability replica op de virtuele Azure-machines op een externe locatie Azure groepeert.</span><span class="sxs-lookup"><span data-stu-id="c404b-104">This article explains how tooconfigure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="c404b-105">Gebruik deze configuratie toosupport-noodherstel.</span><span class="sxs-lookup"><span data-stu-id="c404b-105">Use this configuration toosupport disaster recovery.</span></span>

<span data-ttu-id="c404b-106">In dit artikel is van toepassing tooAzure virtuele Machines in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c404b-106">This article applies tooAzure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="c404b-107">Hallo volgende afbeelding toont een algemene implementatie van een beschikbaarheidsgroep op Azure virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="c404b-107">hello following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="c404b-109">In deze implementatie worden alle virtuele machines in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="c404b-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="c404b-110">replica's Hallo van beschikbaarheidsgroepen kunnen synchrone doorvoer met automatische failover op de SQL-1 en SQL-2 hebben.</span><span class="sxs-lookup"><span data-stu-id="c404b-110">hello availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="c404b-111">toobuild deze architectuur Zie [beschikbaarheidsgroep sjabloon of zelfstudie](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c404b-111">toobuild this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="c404b-112">Deze architectuur is kwetsbaar toodowntime als ontoegankelijk hello Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="c404b-112">This architecture is vulnerable toodowntime if hello Azure region becomes inaccessible.</span></span> <span data-ttu-id="c404b-113">tooovercome deze kwetsbaarheid, het toevoegen van een replica in een andere Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="c404b-113">tooovercome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="c404b-114">Hallo volgende diagram toont de nieuwe architectuur Hallo zou als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="c404b-114">hello following diagram shows how hello new architecture would look:</span></span>

   ![Beschikbaarheid van groep DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="c404b-116">Hallo voorgaande diagram ziet u een nieuwe virtuele machine SQL 3 genoemd.</span><span class="sxs-lookup"><span data-stu-id="c404b-116">hello preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="c404b-117">SQL-3 is in een andere Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="c404b-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="c404b-118">SQL-3 wordt toohello Windows Server Failover Cluster toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c404b-118">SQL-3 is added toohello Windows Server Failover Cluster.</span></span> <span data-ttu-id="c404b-119">SQL-3 kan een beschikbaarheidsreplica van de groep host.</span><span class="sxs-lookup"><span data-stu-id="c404b-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="c404b-120">Ten slotte ziet dat die hello Azure-regio voor de SQL-3 heeft een nieuwe Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="c404b-120">Finally, notice that hello Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="c404b-121">Een Azure beschikbaarheidsset is vereist wanneer meer dan één virtuele machine bevindt zich in dezelfde regio Hallo.</span><span class="sxs-lookup"><span data-stu-id="c404b-121">An Azure availability set is required when more than one virtual machine is in hello same region.</span></span> <span data-ttu-id="c404b-122">Hallo beschikbaarheidsset is niet vereist als er slechts één virtuele machine zich in de regio hello.</span><span class="sxs-lookup"><span data-stu-id="c404b-122">If only one virtual machine is in hello region, then hello availability set is not required.</span></span> <span data-ttu-id="c404b-123">U kunt alleen een virtuele machine in een beschikbaarheidsset tijdens de aanmaak plaatsen.</span><span class="sxs-lookup"><span data-stu-id="c404b-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="c404b-124">Als Hallo virtuele machine staat al in een beschikbaarheidsset bevindt, kunt u een virtuele machine voor een extra replica later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c404b-124">If hello virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="c404b-125">In deze architectuur wordt Hallo replica in de externe regio Hallo normaal gesproken geconfigureerd met asynchrone doorvoermodus voor beschikbaarheid en handmatige failover-modus.</span><span class="sxs-lookup"><span data-stu-id="c404b-125">In this architecture, hello replica in hello remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="c404b-126">Als replica's van beschikbaarheidsgroepen op Azure virtuele machines in verschillende Azure-regio's, moet elke regio:</span><span class="sxs-lookup"><span data-stu-id="c404b-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="c404b-127">Een virtuele netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="c404b-127">A virtual network gateway</span></span>
* <span data-ttu-id="c404b-128">Een verbinding met virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="c404b-128">A virtual network gateway connection</span></span>

<span data-ttu-id="c404b-129">Hallo volgende diagram toont hoe Hallo netwerken communiceren tussen datacenters.</span><span class="sxs-lookup"><span data-stu-id="c404b-129">hello following diagram shows how hello networks communicate between data centers.</span></span>

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="c404b-131">Deze architectuur leidt ertoe dat kosten voor uitgaande gegevens voor gegevens gerepliceerd tussen Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="c404b-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="c404b-132">Zie [bandbreedte prijzen](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="c404b-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="c404b-133">Externe replica maken</span><span class="sxs-lookup"><span data-stu-id="c404b-133">Create remote replica</span></span>

<span data-ttu-id="c404b-134">een replica in een externe Datacenter toocreate Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c404b-134">toocreate a replica in a remote data center, do hello following steps:</span></span>

1. <span data-ttu-id="c404b-135">[Een virtueel netwerk maken in de nieuwe regio Hallo](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c404b-135">[Create a virtual network in hello new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="c404b-136">[Een VNet-naar-VNet-verbinding configureren met hello Azure-portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c404b-136">[Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="c404b-137">In sommige gevallen mogelijk hebt u toouse PowerShell toocreate hello VNet-naar-VNet-verbinding.</span><span class="sxs-lookup"><span data-stu-id="c404b-137">In some cases, you may have toouse PowerShell toocreate hello VNet-to-VNet connection.</span></span> <span data-ttu-id="c404b-138">Als u verschillende Azure-accounts kan niet u Hallo verbinding configureren in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="c404b-138">For example, if you use different Azure accounts you cannot configure hello connection in hello portal.</span></span> <span data-ttu-id="c404b-139">In dit geval ziet, [Azure-portal configureren een VNet-naar-VNet-verbinding gebruikt Hallo](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c404b-139">In this case see, [Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="c404b-140">[Maken van een domeincontroller in de nieuwe regio Hallo](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="c404b-140">[Create a domain controller in hello new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="c404b-141">Deze domeincontroller biedt verificatie als de domeincontroller Hallo in Hallo primaire site niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="c404b-141">This domain controller provides authentication if hello domain controller in hello primary site is not available.</span></span>

1. <span data-ttu-id="c404b-142">[Maken van een virtuele machine van SQL Server in de nieuwe regio Hallo](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="c404b-142">[Create a SQL Server virtual machine in hello new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="c404b-143">[Maak een Azure load balancer in Hallo-netwerk op Hallo nieuw gebied](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="c404b-143">[Create an Azure load balancer in hello network on hello new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="c404b-144">Deze load balancer moet:</span><span class="sxs-lookup"><span data-stu-id="c404b-144">This load balancer must:</span></span>

   - <span data-ttu-id="c404b-145">Zich in hetzelfde netwerk en subnet Hallo zoals Hallo van nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c404b-145">Be in hello same network and subnet as hello new virtual machine.</span></span>
   - <span data-ttu-id="c404b-146">Een statisch IP-adres voor Hallo beschikbaarheidsgroep-listener hebben.</span><span class="sxs-lookup"><span data-stu-id="c404b-146">Have a static IP address for hello availability group listener.</span></span>
   - <span data-ttu-id="c404b-147">Een back-endpool die bestaan uit alleen Hallo virtuele machines in dezelfde regio Hallo zoals Hallo load balancer bevatten.</span><span class="sxs-lookup"><span data-stu-id="c404b-147">Include a backend pool consisting of only hello virtual machines in hello same region as hello load balancer.</span></span>
   - <span data-ttu-id="c404b-148">Gebruik een TCP-poort test specifieke toohello IP-adres.</span><span class="sxs-lookup"><span data-stu-id="c404b-148">Use a TCP port probe specific toohello IP address.</span></span>
   - <span data-ttu-id="c404b-149">Een load balancing-regel specifieke toohello SQL Server in Hallo hebben dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="c404b-149">Have a load balancing rule specific toohello SQL Server in hello same region.</span></span>  

1. <span data-ttu-id="c404b-150">[Toevoegen van Failover Clustering functie toohello nieuwe SQL-Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="c404b-150">[Add Failover Clustering feature toohello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="c404b-151">[Lid worden van domein van Hallo nieuwe SQL Server toohello](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="c404b-151">[Join hello new SQL Server toohello domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="c404b-152">[Stel Hallo nieuwe SQL Server-service-account toouse een domeinaccount](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="c404b-152">[Set hello new SQL Server service account toouse a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="c404b-153">[Hallo nieuwe SQL Server toohello Windows Server Failover Cluster toevoegen](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="c404b-153">[Add hello new SQL Server toohello Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="c404b-154">Maak een bron van de IP-adres op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c404b-154">Create an IP address resource on hello cluster.</span></span>

   <span data-ttu-id="c404b-155">U kunt Hallo IP-adres resource maken in Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="c404b-155">You can create hello IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="c404b-156">Met de rechtermuisknop op de rol van Hallo beschikbaarheid groep, klikt u op **Resource toevoegen**, **meer bronnen**, en klik op **IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="c404b-156">Right-click hello availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![IP-adres maken](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="c404b-158">Dit IP-adres als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="c404b-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="c404b-159">Hallo-netwerk van Hallo remote Datacenter gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c404b-159">Use hello network from hello remote data center.</span></span>
   - <span data-ttu-id="c404b-160">Hallo IP-adres van de nieuwe Azure load balancer Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c404b-160">Assign hello IP address from hello new Azure load balancer.</span></span> 

1. <span data-ttu-id="c404b-161">Hallo op nieuwe SQL-Server in SQL Server Configuration Manager [inschakelen altijd op beschikbaarheidsgroepen](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="c404b-161">On hello new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="c404b-162">[Open firewallpoorten op de nieuwe SQL-Server Hallo](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="c404b-162">[Open firewall ports on hello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="c404b-163">Hallo poortnummers moet u tooopen is afhankelijk van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="c404b-163">hello port numbers you need tooopen depend on your environment.</span></span> <span data-ttu-id="c404b-164">Open poorten voor Hallo mirroring-eindpunt en Azure load balancer health test.</span><span class="sxs-lookup"><span data-stu-id="c404b-164">Open ports for hello mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="c404b-165">[Toevoegen van een beschikbaarheidsgroep van de replica-toohello op Hallo nieuwe SQL-Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="c404b-165">[Add a replica toohello availability group on hello new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="c404b-166">Voor een replica in een externe Azure-regio, moet u deze voor asynchrone replicatie met handmatige failover instellen.</span><span class="sxs-lookup"><span data-stu-id="c404b-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="c404b-167">Hallo IP-adres resource toevoegen als een afhankelijkheid voor Hallo listener client access point (netwerknaam) cluster.</span><span class="sxs-lookup"><span data-stu-id="c404b-167">Add hello IP address resource as a dependency for hello listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="c404b-168">Hallo volgende schermafbeelding ziet u een correct geconfigureerde clusterbron voor IP-adres:</span><span class="sxs-lookup"><span data-stu-id="c404b-168">hello following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="c404b-170">Hallo clusterbrongroep bevat beide IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="c404b-170">hello cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="c404b-171">Beide IP-adressen zijn afhankelijkheden voor het Hallo-listener client access point.</span><span class="sxs-lookup"><span data-stu-id="c404b-171">Both IP addresses are dependencies for hello listener client access point.</span></span> <span data-ttu-id="c404b-172">Gebruik Hallo **of** operator in Hallo afhankelijkheid clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="c404b-172">Use hello **OR** operator in hello cluster dependency configuration.</span></span>

1. <span data-ttu-id="c404b-173">[Hallo Clusterparameters instellen in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="c404b-173">[Set hello cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="c404b-174">Hallo PowerShell-script uitvoeren met de clusternetwerknaam hello, IP-adres en testpoort die u hebt geconfigureerd op Hallo load balancer in de nieuwe regio Hallo.</span><span class="sxs-lookup"><span data-stu-id="c404b-174">Run hello PowerShell script with hello cluster network name, IP address, and probe port that you configured on hello load balancer in hello new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="c404b-175">Set-verbinding voor meerdere subnetten</span><span class="sxs-lookup"><span data-stu-id="c404b-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="c404b-176">Hallo replica in de externe Datacenter Hallo is onderdeel van de beschikbaarheidsgroep hello, maar het is in een ander subnet.</span><span class="sxs-lookup"><span data-stu-id="c404b-176">hello replica in hello remote data center is part of hello availability group but it is in a different subnet.</span></span> <span data-ttu-id="c404b-177">Als deze replica de primaire replica hello wordt, optreden verbindingstime toepassing.</span><span class="sxs-lookup"><span data-stu-id="c404b-177">If this replica becomes hello primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="c404b-178">Dit gedrag is hetzelfde als een lokale beschikbaarheidsgroep in een implementatie met meerdere subnetten Hallo.</span><span class="sxs-lookup"><span data-stu-id="c404b-178">This behavior is hello same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="c404b-179">tooallow verbindingen van clienttoepassingen, Hallo clientverbinding bijwerken of cachegebruik op Hallo cluster netwerknaambron naamomzetting configureren.</span><span class="sxs-lookup"><span data-stu-id="c404b-179">tooallow connections from client applications, either update hello client connection or configure name resolution caching on hello cluster network name resource.</span></span>

<span data-ttu-id="c404b-180">Bij voorkeur bijwerken Hallo client verbinding tekenreeksen tooset `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="c404b-180">Preferably, update hello client connection strings tooset `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="c404b-181">Zie [verbinding te maken met MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="c404b-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="c404b-182">Als u verbindingsreeksen Hallo niet wijzigen, kunt u de naam resolutie caching kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="c404b-182">If you cannot modify hello connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="c404b-183">Zie [time-outs voor verbindingen in meerdere subnetten beschikbaarheidsgroep](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="c404b-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-tooremote-region"></a><span data-ttu-id="c404b-184">Failover tooremote regio</span><span class="sxs-lookup"><span data-stu-id="c404b-184">Fail over tooremote region</span></span>

<span data-ttu-id="c404b-185">tootest listener connectiviteit toohello externe regio, u kunt een failover Hallo replica toohello externe regio.</span><span class="sxs-lookup"><span data-stu-id="c404b-185">tootest listener connectivity toohello remote region, you can fail over hello replica toohello remote region.</span></span> <span data-ttu-id="c404b-186">Hallo replica asynchroon is, is failover kwetsbaar toopotential gegevens verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="c404b-186">While hello replica is asynchronous, failover is vulnerable toopotential data loss.</span></span> <span data-ttu-id="c404b-187">toofail via zonder gegevensverlies, Hallo beschikbaarheid modus toosynchronous wijzigen en Hallo failover-modus tooautomatic ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c404b-187">toofail over without data loss, change hello availability mode toosynchronous and set hello failover mode tooautomatic.</span></span> <span data-ttu-id="c404b-188">Gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c404b-188">Use hello following steps:</span></span>

1. <span data-ttu-id="c404b-189">In **Objectverkenner**, verbinding toohello exemplaar van SQL Server die als host fungeert voor de primaire replica Hallo.</span><span class="sxs-lookup"><span data-stu-id="c404b-189">In **Object Explorer**, connect toohello instance of SQL Server that hosts hello primary replica.</span></span>
1. <span data-ttu-id="c404b-190">Onder **AlwaysOn Availability Groups**, **beschikbaarheidsgroepen**, met de rechtermuisknop op de beschikbaarheidsgroep en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c404b-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="c404b-191">Op Hallo **algemene** pagina onder **Beschikbaarheidsreplica**, set Hallo secundaire replica in Hallo DR site toouse **synchroon doorvoeren** beschikbaarheidsmodus en **Automatische** failover-modus.</span><span class="sxs-lookup"><span data-stu-id="c404b-191">On hello **General** page, under **Availability Replicas**, set hello secondary replica in hello DR site toouse **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="c404b-192">Als u een secundaire replica in dezelfde site als de primaire replica voor hoge beschikbaarheid, stelt u deze replica te**asynchrone doorvoeren** en **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="c404b-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica too**Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="c404b-193">Klik op OK.</span><span class="sxs-lookup"><span data-stu-id="c404b-193">Click OK.</span></span>
1. <span data-ttu-id="c404b-194">In **Objectverkenner**, met de rechtermuisknop op het Hallo-beschikbaarheidsgroep en klikt u op **Dashboard weergeven**.</span><span class="sxs-lookup"><span data-stu-id="c404b-194">In **Object Explorer**, right-click hello availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="c404b-195">Controleer op Hallo dashboard dat Hallo replica op Hallo DR-site is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="c404b-195">On hello dashboard, verify that hello replica on hello DR site is synchronized.</span></span>
1. <span data-ttu-id="c404b-196">In **Objectverkenner**, met de rechtermuisknop op het Hallo-beschikbaarheidsgroep en klikt u op **Failover...** . SQL Server Management Studios Hiermee opent u een wizard toofail via SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c404b-196">In **Object Explorer**, right-click hello availability group, and click **Failover...**. SQL Server Management Studios opens a wizard toofail over SQL Server.</span></span>  
1. <span data-ttu-id="c404b-197">Klik op **volgende**, en selecteer Hallo SQL Server-exemplaar op Hallo DR-site.</span><span class="sxs-lookup"><span data-stu-id="c404b-197">Click **Next**, and select hello SQL Server instance in hello DR site.</span></span> <span data-ttu-id="c404b-198">Klik op **volgende** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c404b-198">Click **Next** again.</span></span>
1. <span data-ttu-id="c404b-199">Verbinding maken met SQL Server-exemplaar toohello op Hallo DR-site en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c404b-199">Connect toohello SQL Server instance in hello DR site and click **Next**.</span></span>
1. <span data-ttu-id="c404b-200">Op Hallo **samenvatting** pagina, Hallo instellingen controleren en klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c404b-200">On hello **Summary** page, verify hello settings and click **Finish**.</span></span>

<span data-ttu-id="c404b-201">Nadat de verbinding test, Hallo primaire replica back tooyour primaire gegevens center en instellingen voor het Hallo beschikbaarheid modus back tootheir normale operationele te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="c404b-201">After testing connectivity, move hello primary replica back tooyour primary data center and set hello availability mode back tootheir normal operating settings.</span></span> <span data-ttu-id="c404b-202">Hallo ziet volgende tabel u Hallo normale operationele instellingen voor Hallo-architectuur in dit document beschreven:</span><span class="sxs-lookup"><span data-stu-id="c404b-202">hello following table shows hello normal operational settings for hello architecture described in this document:</span></span>

| <span data-ttu-id="c404b-203">Locatie</span><span class="sxs-lookup"><span data-stu-id="c404b-203">Location</span></span> | <span data-ttu-id="c404b-204">Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="c404b-204">Server Instance</span></span> | <span data-ttu-id="c404b-205">Rol</span><span class="sxs-lookup"><span data-stu-id="c404b-205">Role</span></span> | <span data-ttu-id="c404b-206">De Beschikbaarheidsmodus</span><span class="sxs-lookup"><span data-stu-id="c404b-206">Availability Mode</span></span> | <span data-ttu-id="c404b-207">Failover-modus</span><span class="sxs-lookup"><span data-stu-id="c404b-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="c404b-208">Primaire Datacenter</span><span class="sxs-lookup"><span data-stu-id="c404b-208">Primary data center</span></span> | <span data-ttu-id="c404b-209">SQL-1</span><span class="sxs-lookup"><span data-stu-id="c404b-209">SQL-1</span></span> | <span data-ttu-id="c404b-210">Primair</span><span class="sxs-lookup"><span data-stu-id="c404b-210">Primary</span></span> | <span data-ttu-id="c404b-211">Synchrone</span><span class="sxs-lookup"><span data-stu-id="c404b-211">Synchronous</span></span> | <span data-ttu-id="c404b-212">Automatisch</span><span class="sxs-lookup"><span data-stu-id="c404b-212">Automatic</span></span>
| <span data-ttu-id="c404b-213">Primaire Datacenter</span><span class="sxs-lookup"><span data-stu-id="c404b-213">Primary data center</span></span> | <span data-ttu-id="c404b-214">SQL-2</span><span class="sxs-lookup"><span data-stu-id="c404b-214">SQL-2</span></span> | <span data-ttu-id="c404b-215">Secundair</span><span class="sxs-lookup"><span data-stu-id="c404b-215">Secondary</span></span> | <span data-ttu-id="c404b-216">Synchrone</span><span class="sxs-lookup"><span data-stu-id="c404b-216">Synchronous</span></span> | <span data-ttu-id="c404b-217">Automatisch</span><span class="sxs-lookup"><span data-stu-id="c404b-217">Automatic</span></span>
| <span data-ttu-id="c404b-218">Secundaire of door de externe Datacenter</span><span class="sxs-lookup"><span data-stu-id="c404b-218">Secondary or remote data center</span></span> | <span data-ttu-id="c404b-219">SQL-3</span><span class="sxs-lookup"><span data-stu-id="c404b-219">SQL-3</span></span> | <span data-ttu-id="c404b-220">Secundair</span><span class="sxs-lookup"><span data-stu-id="c404b-220">Secondary</span></span> | <span data-ttu-id="c404b-221">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="c404b-221">Asynchronous</span></span> | <span data-ttu-id="c404b-222">Handmatig</span><span class="sxs-lookup"><span data-stu-id="c404b-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="c404b-223">Meer informatie over de geplande en geforceerde handmatige failover</span><span class="sxs-lookup"><span data-stu-id="c404b-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="c404b-224">Zie de volgende onderwerpen Hallo voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="c404b-224">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="c404b-225">Voer een geplande handmatige Failover van een beschikbaarheidsgroep (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="c404b-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="c404b-226">Voer een geforceerde handmatige Failover van een beschikbaarheidsgroep (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="c404b-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="c404b-227">Aanvullende koppelingen</span><span class="sxs-lookup"><span data-stu-id="c404b-227">Additional Links</span></span>

* [<span data-ttu-id="c404b-228">Altijd op beschikbaarheidsgroepen</span><span class="sxs-lookup"><span data-stu-id="c404b-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="c404b-229">Virtuele Machines in Azure</span><span class="sxs-lookup"><span data-stu-id="c404b-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="c404b-230">Azure Load Balancers</span><span class="sxs-lookup"><span data-stu-id="c404b-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="c404b-231">Azure Beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="c404b-231">Azure Availability Sets</span></span>](../manage-availability.md)
