---
title: de configuratie van een SAP multi-SID in Azure aaaCreate | Microsoft Docs
description: Handleiding toohigh beschikbaarheid SAP NetWeaver multi-SID-configuratie op Windows virtuele machines
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="8b317-103">Maak een SAP NetWeaver multi-SID-configuratie</span><span class="sxs-lookup"><span data-stu-id="8b317-103">Create an SAP NetWeaver multi-SID configuration</span></span>

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

<span data-ttu-id="8b317-104">In September 2016 Microsoft uitgebracht een functie waar u meerdere virtuele IP-adressen beheren kunt met behulp van een Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b317-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="8b317-105">Er bestaat al deze functionaliteit in hello Azure externe load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b317-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="8b317-106">Als u een SAP-implementatie hebt, kunt u een interne load balancer toocreate een Windows-clusterconfiguratie voor SAP ASC's / SCS, zoals beschreven in Hallo [handleiding voor hoge beschikbaarheid SAP NetWeaver op VM's van Windows] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="8b317-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="8b317-107">Dit artikel is gericht op hoe toomove van een enkele ASC's / SCS installatie tooan SAP multi-SID configuratie door het installeren van extra SAP ASC's / SCS exemplaren geclusterd in een bestaand Windows Server Failover Clustering (WSFC)-cluster.</span><span class="sxs-lookup"><span data-stu-id="8b317-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="8b317-108">Wanneer dit proces is voltooid, beschikt u hebt geconfigureerd een SAP multi-SID-cluster.</span><span class="sxs-lookup"><span data-stu-id="8b317-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8b317-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8b317-109">Prerequisites</span></span>
<span data-ttu-id="8b317-110">U al een WSFC-cluster dat wordt gebruikt voor één SAP ASC's / SCS exemplaar hebt geconfigureerd zoals beschreven in Hallo [handleiding voor hoge beschikbaarheid SAP NetWeaver op VM's van Windows] [ sap-ha-guide] en zoals weergegeven in dit diagram.</span><span class="sxs-lookup"><span data-stu-id="8b317-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Hoge beschikbaarheid SAP ASC's / SCS exemplaar][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="8b317-112">Doel-architectuur</span><span class="sxs-lookup"><span data-stu-id="8b317-112">Target architecture</span></span>

<span data-ttu-id="8b317-113">Hallo doel is tooinstall meerdere SAP ABAP ASC's of SAP Java SCS geclusterde exemplaren in Hallo dezelfde WSFC-cluster, zoals hier wordt geïllustreerd:</span><span class="sxs-lookup"><span data-stu-id="8b317-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Meerdere SAP ASC's / SCS geclusterde exemplaren in Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="8b317-115">Er is een limiet toohello aantal persoonlijke front-end-IP-adressen voor elke Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b317-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="8b317-116">maximum aantal exemplaren in een WSFC-cluster SAP ASC's / SCS Hallo is gelijk toohello kunt u het maximum aantal persoonlijke front-end-IP-adressen voor elke Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b317-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="8b317-117">Zie voor meer informatie over de limieten van de load balancer 'persoonlijke front-end-IP per load balancer in [netwerken limieten: Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="8b317-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="8b317-118">Hallo voltooid Liggend met twee SAP-systemen voor hoge beschikbaarheid eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="8b317-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![SAP hoge beschikbaarheid multi-SID-configuratie met twee SAP-systeem beveiligings-id 's][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="8b317-120">Hallo setup moet voldoen aan de volgende voorwaarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="8b317-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="8b317-121">Hallo SAP ASC's / SCS exemplaren moeten delen Hallo dezelfde WSFC-cluster.</span><span class="sxs-lookup"><span data-stu-id="8b317-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="8b317-122">Elke DBMS SID moet een eigen toegewezen WSFC-cluster hebben.</span><span class="sxs-lookup"><span data-stu-id="8b317-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="8b317-123">SAP-toepassingsservers die deel uitmaken van tooone SAP-systeem SID moeten hebben hun eigen toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8b317-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="8b317-124">Hallo-infrastructuur voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8b317-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="8b317-125">tooprepare uw infrastructuur, kunt u een extra exemplaar van de SAP ASC's / SCS installeren Hello volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="8b317-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="8b317-126">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="8b317-126">Parameter name</span></span> | <span data-ttu-id="8b317-127">Waarde</span><span class="sxs-lookup"><span data-stu-id="8b317-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b317-128">SAP ASC 'S/SCS SID</span><span class="sxs-lookup"><span data-stu-id="8b317-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="8b317-129">PR1-lb-ASC 's</span><span class="sxs-lookup"><span data-stu-id="8b317-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="8b317-130">SAP DBMS interne load balancer</span><span class="sxs-lookup"><span data-stu-id="8b317-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="8b317-131">PR5</span><span class="sxs-lookup"><span data-stu-id="8b317-131">PR5</span></span> |
| <span data-ttu-id="8b317-132">Naam van de virtuele host SAP</span><span class="sxs-lookup"><span data-stu-id="8b317-132">SAP virtual host name</span></span> | <span data-ttu-id="8b317-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="8b317-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="8b317-134">SAP ASC's / SCS virtuele host (extra Azure load balancer IP-adres)</span><span class="sxs-lookup"><span data-stu-id="8b317-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="8b317-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="8b317-135">10.0.0.50</span></span> |
| <span data-ttu-id="8b317-136">SAP ASC's / SCS exemplaarnummer</span><span class="sxs-lookup"><span data-stu-id="8b317-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="8b317-137">50</span><span class="sxs-lookup"><span data-stu-id="8b317-137">50</span></span> |
| <span data-ttu-id="8b317-138">De testpoort ILB voor extra SAP ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="8b317-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="8b317-139">62350</span><span class="sxs-lookup"><span data-stu-id="8b317-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="8b317-140">Elk IP-adres vereist voor SAP ASC's / SCS cluster exemplaren, een unieke testpoort.</span><span class="sxs-lookup"><span data-stu-id="8b317-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="8b317-141">Als u één IP-adres op een Azure interne load balancer testpoort 62300 gebruikt, kan geen andere IP-adres op dat load balancer testpoort 62300 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8b317-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="8b317-142">Voor onze toepassing, omdat de testpoort 62300 is al gereserveerd, gebruiken we de testpoort 62350.</span><span class="sxs-lookup"><span data-stu-id="8b317-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="8b317-143">U kunt extra exemplaren van het SAP ASC's / SCS installeren in Hallo bestaande WSFC-cluster met twee knooppunten:</span><span class="sxs-lookup"><span data-stu-id="8b317-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="8b317-144">De rol virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8b317-144">Virtual machine role</span></span> | <span data-ttu-id="8b317-145">Hostnaam van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8b317-145">Virtual machine host name</span></span> | <span data-ttu-id="8b317-146">Statisch IP-adres</span><span class="sxs-lookup"><span data-stu-id="8b317-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b317-147">1e clusterknooppunt voor ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="8b317-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="8b317-148">PR1-ASC's-0</span><span class="sxs-lookup"><span data-stu-id="8b317-148">pr1-ascs-0</span></span> |<span data-ttu-id="8b317-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="8b317-149">10.0.0.10</span></span> |
| <span data-ttu-id="8b317-150">2e clusterknooppunt voor ASC's / SCS-exemplaar</span><span class="sxs-lookup"><span data-stu-id="8b317-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="8b317-151">PR1-ASC's-1</span><span class="sxs-lookup"><span data-stu-id="8b317-151">pr1-ascs-1</span></span> |<span data-ttu-id="8b317-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="8b317-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="8b317-153">Maken van een virtuele host-naam voor geclusterde Hallo SAP ASC's / SCS exemplaar op Hallo DNS-server</span><span class="sxs-lookup"><span data-stu-id="8b317-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="8b317-154">U kunt een DNS-vermelding voor de naam van de virtuele host Hallo van Hallo ASC's / SCS-exemplaar maken met behulp van Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="8b317-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="8b317-155">Nieuwe SAP ASC's / SCS virtuele host-naam</span><span class="sxs-lookup"><span data-stu-id="8b317-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="8b317-156">Bijbehorende IP-adres</span><span class="sxs-lookup"><span data-stu-id="8b317-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="8b317-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="8b317-157">pr5-sap-cl</span></span> |<span data-ttu-id="8b317-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="8b317-158">10.0.0.50</span></span> |

<span data-ttu-id="8b317-159">Hallo nieuwe hostnaam en IP-adres worden weergegeven in Hallo DNS-beheer, zoals wordt weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="8b317-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Lijst met DNS-beheer markeren Hallo gedefinieerd DNS-vermelding voor Hallo nieuwe SAP ASC's / SCS virtuele clusternaam en TCP/IP-adres][sap-ha-guide-figure-6004]

<span data-ttu-id="8b317-161">Hallo-procedure voor het maken van een DNS-vermelding wordt ook beschreven in de belangrijkste Hallo [handleiding voor hoge beschikbaarheid SAP NetWeaver op VM's van Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="8b317-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="8b317-162">Hallo moet nieuwe IP-adres dat u toewijst toohello virtuele host-naam van Hallo extra ASC's / SCS exemplaar worden Hallo hetzelfde als Hallo nieuwe IP-adres dat aan u toohello SAP Azure load balancer toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8b317-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="8b317-163">In ons scenario is Hallo IP-adres 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="8b317-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="8b317-164">Een IP-adres tooan bestaande Azure interne load balancer toevoegen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b317-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="8b317-165">toocreate meer dan één exemplaar van de SAP ASC's / SCS in Hallo dezelfde WSFC-cluster, gebruikt u PowerShell tooadd een IP-adres tooan bestaande Azure interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b317-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="8b317-166">Elk IP-adres vereist een eigen regels load balancing, testpoort, front-end-IP-adresgroep en back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="8b317-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="8b317-167">Hallo voegt volgende script een nieuwe IP-adres tooan bestaande load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b317-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="8b317-168">Hallo PowerShell variabelen voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8b317-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="8b317-169">Hallo-script worden alle benodigde taakverdeling regels maken voor alle SAP ASC's / SCS-poorten.</span><span class="sxs-lookup"><span data-stu-id="8b317-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="8b317-170">Na het uitvoeren van script hello, Hallo Hallo resultaten worden weergegeven in Azure-portal, zoals wordt weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="8b317-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Nieuwe front-end-IP-groep in hello Azure-portal][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="8b317-172">Toevoegen van schijven toocluster machines en Hallo SIOS clusterschijf share configureren</span><span class="sxs-lookup"><span data-stu-id="8b317-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="8b317-173">U moet het delen van een nieuwe clusterschijf voor elk extra exemplaar van de SAP ASC's / SCS toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8b317-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="8b317-174">Hallo WSFC share clusterschijf momenteel in gebruik is voor Windows Server 2012 R2 Hallo SIOS DataKeeper softwareoplossing.</span><span class="sxs-lookup"><span data-stu-id="8b317-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="8b317-175">Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b317-175">Do hello following:</span></span>
1. <span data-ttu-id="8b317-176">Toevoegen van een extra schijf of schijven met dezelfde grootte Hallo (die u moet toostripe) tooeach Hallo clusterknooppunten en maak deze.</span><span class="sxs-lookup"><span data-stu-id="8b317-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="8b317-177">Storage-replicatie configureren met SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="8b317-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="8b317-178">Deze procedure wordt ervan uitgegaan dat u SIOS DataKeeper op Hallo WSFC-clustermachines al hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8b317-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="8b317-179">Als u deze hebt geïnstalleerd, moet u replicatie tussen Hallo machines nu configureren.</span><span class="sxs-lookup"><span data-stu-id="8b317-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="8b317-180">Hallo-proces wordt uitgebreid beschreven in de belangrijkste Hallo [handleiding voor hoge beschikbaarheid SAP NetWeaver op VM's van Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="8b317-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![DataKeeper synchroon spiegelen voor Hallo nieuwe SAP ASC's / SCS share schijf][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="8b317-182">Virtuele machines voor SAP-toepassingsservers en DBMS-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="8b317-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="8b317-183">toocomplete hello infrastructuur voorbereiden Hallo tweede SAP-systeem, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b317-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="8b317-184">Implementeer toegewezen virtuele machines voor SAP-toepassingsservers en opslaan in hun eigen toegewezen beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="8b317-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="8b317-185">Toegewezen virtuele machines voor DBMS-cluster implementeren en ze in hun eigen toegewezen beschikbaarheidsgroep plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8b317-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="8b317-186">Hallo tweede SAP SID2 NetWeaver systeem installeert</span><span class="sxs-lookup"><span data-stu-id="8b317-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="8b317-187">Hallo complete proces van het installeren van een tweede SID2 SAP-systeem wordt beschreven in de belangrijkste Hallo [handleiding voor hoge beschikbaarheid SAP NetWeaver op VM's van Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="8b317-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="8b317-188">Hallo op hoog niveau procedure is als volgt:</span><span class="sxs-lookup"><span data-stu-id="8b317-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="8b317-189">[Eerste Hallo SAP-clusterknooppunt installeren][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="8b317-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="8b317-190">In deze stap maakt u SAP installeert met een hoge beschikbaarheid ASC's / SCS-exemplaar op Hallo **bestaande WSFC-clusterknooppunt 1**.</span><span class="sxs-lookup"><span data-stu-id="8b317-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="8b317-191">[Hallo SAP-profiel van Hallo ASC's / SCS-exemplaar wijzigen][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="8b317-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="8b317-192">[Configureer een testpoort][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="8b317-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="8b317-193">In deze stap maakt configureert u een SAP-clusterbron SAP-SID2-IP-testpoort met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b317-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="8b317-194">Deze configuratie niet uitvoeren op een van Hallo SAP ASC's / SCS clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="8b317-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="8b317-195">[Hallo database-exemplaar installeren] [sap-ha-handleiding-9.2].</span><span class="sxs-lookup"><span data-stu-id="8b317-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="8b317-196">In deze stap maakt installeert u DBMS op een speciale WSFC-cluster.</span><span class="sxs-lookup"><span data-stu-id="8b317-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="8b317-197">[Tweede clusterknooppunt Hallo installeren] [sap-ha-handleiding-9.3].</span><span class="sxs-lookup"><span data-stu-id="8b317-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="8b317-198">In deze stap maakt installeert u SAP met een hoge beschikbaarheid ASC's / SCS-exemplaar op Hallo bestaande WSFC-cluster van het knooppunt 2.</span><span class="sxs-lookup"><span data-stu-id="8b317-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="8b317-199">Open Windows Firewall-poorten voor Hallo SAP ASC's / SCS instance en ProbePort.</span><span class="sxs-lookup"><span data-stu-id="8b317-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="8b317-200">U kunt alle Windows Firewall-poorten die worden gebruikt door SAP ASC's / SCS wilt openen op beide clusterknooppunten die worden gebruikt voor SAP ASC's / SCS-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="8b317-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="8b317-201">Deze poorten worden vermeld in Hallo [handleiding voor hoge beschikbaarheid SAP NetWeaver op VM's van Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="8b317-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="8b317-202">Ook openen hello Azure interne load balancer-testpoort, 62350 in ons scenario.</span><span class="sxs-lookup"><span data-stu-id="8b317-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="8b317-203">[Hallo het starttype Hallo SAP Ebruikers Windows service-exemplaar wijzigen][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="8b317-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="8b317-204">[Hallo SAP primaire toepassingsserver installeren] [ sap-ha-guide-9.5] toegewezen op Hallo van nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b317-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="8b317-205">[Hallo SAP aanvullende toepassingsserver installeren] [ sap-ha-guide-9.6] toegewezen op Hallo van nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b317-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="8b317-206">[Testen van failover-Hallo SAP ASC's / SCS-exemplaar en SIOS replicatie][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="8b317-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b317-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b317-207">Next steps</span></span>

- <span data-ttu-id="8b317-208">[Limieten voor netwerken: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="8b317-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="8b317-209">[Meerdere VIP's voor Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="8b317-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="8b317-210">[Handleiding voor hoge beschikbaarheid SAP NetWeaver op VM's van Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="8b317-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
