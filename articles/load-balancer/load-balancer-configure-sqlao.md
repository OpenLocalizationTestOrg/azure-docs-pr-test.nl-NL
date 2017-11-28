---
title: aaaConfigure Load balancer voor de SQL AlwaysOn | Microsoft Docs
description: Load balancer toowork configureren met SQL altijd op en hoe tooleverage powershell toocreate load balancer voor Hallo SQL-implementatie
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
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="b2427-103">Load balancer voor SQL altijd configureren op</span><span class="sxs-lookup"><span data-stu-id="b2427-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="b2427-104">SQL Server AlwaysOn-beschikbaarheidsgroepen kan nu worden uitgevoerd met ILB.</span><span class="sxs-lookup"><span data-stu-id="b2427-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="b2427-105">Beschikbaarheidsgroep is SQL-Server vlaggenschip oplossing voor hoge beschikbaarheid en herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="b2427-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="b2427-106">Hallo beschikbaarheidsgroep-Listener clienttoepassingen in staat stelt tooseamlessly verbinding maken met de primaire replica toohello, ongeacht het aantal Hallo replica's in de configuratie van Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2427-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="b2427-107">Hallo-listener (DNS)-naam is toegewezen tooa netwerktaakverdeling IP-adres en Azure load balancer Hallo binnenkomende verkeer tooonly Hallo primaire server stuurt in Hallo replicaset.</span><span class="sxs-lookup"><span data-stu-id="b2427-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="b2427-108">U kunt de ILB ondersteuning voor SQL Server AlwaysOn (listener)-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="b2427-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="b2427-109">U nu hebben controle over Hallo toegankelijkheid van Hallo-listener en Hallo netwerktaakverdeling IP-adres kunt kiezen uit een specifiek subnet in het virtuele netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="b2427-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="b2427-110">Hallo via ILB Hallo-listener voor SQL server-eindpunt (bijvoorbeeld Server = tcp:ListenerName, 1433; Database = DatabaseName) is alleen toegankelijk is voor:</span><span class="sxs-lookup"><span data-stu-id="b2427-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="b2427-111">Services en virtuele machines in hetzelfde virtuele netwerk Hallo</span><span class="sxs-lookup"><span data-stu-id="b2427-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="b2427-112">Services en virtuele machines van de verbonden on-premises netwerk</span><span class="sxs-lookup"><span data-stu-id="b2427-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="b2427-113">Services en virtuele machines van de VNets met elkaar verbonden</span><span class="sxs-lookup"><span data-stu-id="b2427-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="b2427-115">Afbeelding 1: de SQL AlwaysOn is geconfigureerd met Internet gerichte load balancer</span><span class="sxs-lookup"><span data-stu-id="b2427-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="b2427-116">Interne Load Balancer toohello service toevoegen</span><span class="sxs-lookup"><span data-stu-id="b2427-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="b2427-117">In Hallo voorbeeld te volgen, wordt er een virtueel netwerk met een subnet met de naam Subnet-1 geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="b2427-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="b2427-118">Eindpunten van taakverdeling voor de ILB op elke virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="b2427-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="b2427-119">Hallo bovenstaande voorbeeld hebt u 2 VM genoemd 'sqlsvc1' en 'sqlsvc2' wordt uitgevoerd in de cloud Hallo service 'Sqlsvc'.</span><span class="sxs-lookup"><span data-stu-id="b2427-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="b2427-120">Na het maken van Hallo ILB met `DirectServerReturn` overschakelen, u toevoegen taakverdeling eindpunten toohello ILB tooallow SQL tooconfigure Hallo listeners voor beschikbaarheidsgroepen Hallo laden.</span><span class="sxs-lookup"><span data-stu-id="b2427-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="b2427-121">Zie voor meer informatie over SQL AlwaysOn, [een interne load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="b2427-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b2427-122">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b2427-122">See Also</span></span>
[<span data-ttu-id="b2427-123">De load balancer van een Internetgericht configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="b2427-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="b2427-124">Een interne load balancer configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="b2427-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="b2427-125">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="b2427-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b2427-126">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="b2427-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
