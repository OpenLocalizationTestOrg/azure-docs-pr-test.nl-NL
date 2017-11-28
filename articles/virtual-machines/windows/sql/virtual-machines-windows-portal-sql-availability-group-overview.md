---
title: Beschikbaarheid van SQL Server - virtuele Azure-Machines - overzicht groepen | Microsoft Docs
description: Dit artikel bevat een SQL Server-beschikbaarheidsgroepen op virtuele machines in Azure.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="3016b-103">Inleiding tot SQL Server altijd op beschikbaarheidsgroepen op virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="3016b-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="3016b-104">Dit artikel bevat een SQL Server-beschikbaarheidsgroepen op Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="3016b-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="3016b-105">AlwaysOn-beschikbaarheidsgroepen op Azure Virtual Machines zijn vergelijkbaar met on-premises altijd op beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="3016b-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="3016b-106">Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="3016b-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="3016b-107">Het diagram illustreert de onderdelen van een volledige SQL Server-beschikbaarheidsgroep in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="3016b-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="3016b-109">Het belangrijkste verschil voor een beschikbaarheidsgroep in Azure Virtual Machines is dat de virtuele machines van Azure, vereist een [netwerktaakverdeler](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3016b-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="3016b-110">De load balancer bevat de IP-adressen voor de beschikbaarheidsgroeplistener.</span><span class="sxs-lookup"><span data-stu-id="3016b-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="3016b-111">Als er meer dan één beschikbaarheidsgroep moet elke groep een listener.</span><span class="sxs-lookup"><span data-stu-id="3016b-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="3016b-112">Één load balancer biedt ondersteuning voor meerdere listeners.</span><span class="sxs-lookup"><span data-stu-id="3016b-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="3016b-113">Wanneer u gereed bent voor het bouwen van een aroup van de beschikbaarheid van SQL Server op Azure Virtual Machines, verwijzen naar deze zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="3016b-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="3016b-114">Een beschikbaarheidsgroep automatisch maken van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="3016b-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="3016b-115">AlwaysOn-beschikbaarheidsgroep configureren voor de Resource Manager in Azure VM automatisch-</span><span class="sxs-lookup"><span data-stu-id="3016b-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="3016b-116">Een beschikbaarheidsgroep handmatig maken in Azure portal</span><span class="sxs-lookup"><span data-stu-id="3016b-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="3016b-117">U kunt ook de virtuele machines zelf maken zonder de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3016b-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="3016b-118">Eerst, voldoen aan de vereisten en de beschikbaarheidsgroep te maken.</span><span class="sxs-lookup"><span data-stu-id="3016b-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="3016b-119">Zie de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="3016b-119">See the following topics:</span></span> 

- [<span data-ttu-id="3016b-120">Vereisten voor SQL Server AlwaysOn-beschikbaarheidsgroepen configureren op Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="3016b-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="3016b-121">Maak altijd op beschikbaarheidsgroep voor het verbeteren van de beschikbaarheid en herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="3016b-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="3016b-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3016b-122">Next steps</span></span>

<span data-ttu-id="3016b-123">[Configureren van een SQL Server altijd op beschikbaarheidsgroep op Azure virtuele Machines in verschillende regio's](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="3016b-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
