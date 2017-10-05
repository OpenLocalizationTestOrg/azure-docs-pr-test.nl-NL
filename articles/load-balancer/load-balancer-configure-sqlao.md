---
title: Load balancer voor de SQL AlwaysOn configureren op | Microsoft Docs
description: Configureer te werken met SQL altijd op Load balancer en hoe u powershell als u wilt maken van de load balancer voor de SQL-implementatie
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 68aad6253f185d53fdd7f11c8660c7287ef12655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="11fc2-103">Load balancer voor SQL altijd configureren op</span><span class="sxs-lookup"><span data-stu-id="11fc2-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="11fc2-104">SQL Server AlwaysOn-beschikbaarheidsgroepen kan nu worden uitgevoerd met ILB.</span><span class="sxs-lookup"><span data-stu-id="11fc2-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="11fc2-105">Beschikbaarheidsgroep is SQL-Server vlaggenschip oplossing voor hoge beschikbaarheid en herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="11fc2-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="11fc2-106">De beschikbaarheidsgroep-Listener kan client toepassingen naadloos verbinding kunnen maken met de primaire replica, ongeacht het aantal van de replica's in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="11fc2-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="11fc2-107">De naam van de listener (DNS) is toegewezen aan een load balanced IP-adres en de Azure load balancer stuurt het binnenkomende verkeer naar alleen de primaire server in de replicaset.</span><span class="sxs-lookup"><span data-stu-id="11fc2-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="11fc2-108">U kunt de ILB ondersteuning voor SQL Server AlwaysOn (listener)-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="11fc2-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="11fc2-109">U nu hebben controle over de toegankelijkheid van de listener en de netwerktaakverdeling IP-adres kunt kiezen uit een specifiek subnet in het virtuele netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="11fc2-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="11fc2-110">Met behulp van ILB op de listener, de SQL server-eindpunt (bijvoorbeeld Server = tcp:ListenerName, 1433; Database = DatabaseName) is alleen toegankelijk is voor:</span><span class="sxs-lookup"><span data-stu-id="11fc2-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="11fc2-111">Services en virtuele machines in hetzelfde virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="11fc2-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="11fc2-112">Services en virtuele machines van de verbonden on-premises netwerk</span><span class="sxs-lookup"><span data-stu-id="11fc2-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="11fc2-113">Services en virtuele machines van de VNets met elkaar verbonden</span><span class="sxs-lookup"><span data-stu-id="11fc2-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="11fc2-115">Afbeelding 1: de SQL AlwaysOn is geconfigureerd met Internet gerichte load balancer</span><span class="sxs-lookup"><span data-stu-id="11fc2-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="11fc2-116">Interne Load Balancer toevoegen aan de service</span><span class="sxs-lookup"><span data-stu-id="11fc2-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="11fc2-117">Er wordt een virtueel netwerk met een subnet met de naam Subnet-1 geconfigureerd in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11fc2-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="11fc2-118">Eindpunten van taakverdeling voor de ILB op elke virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="11fc2-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="11fc2-119">In het bovenstaande voorbeeld hebt u 2 VM genoemd 'sqlsvc1' en 'sqlsvc2' wordt uitgevoerd in de cloud service 'Sqlsvc'.</span><span class="sxs-lookup"><span data-stu-id="11fc2-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="11fc2-120">Na het maken van de ILB met `DirectServerReturn` switch u taakverdeling eindpunten toevoegen aan de ILB waarmee SQL voor listeners configureren voor de beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="11fc2-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="11fc2-121">Zie voor meer informatie over SQL AlwaysOn, [een interne load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="11fc2-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="11fc2-122">Zie ook</span><span class="sxs-lookup"><span data-stu-id="11fc2-122">See Also</span></span>
[<span data-ttu-id="11fc2-123">De load balancer van een Internetgericht configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="11fc2-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="11fc2-124">Een interne load balancer configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="11fc2-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="11fc2-125">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="11fc2-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="11fc2-126">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="11fc2-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
