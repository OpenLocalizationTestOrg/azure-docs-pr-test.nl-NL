---
title: aaaSQL Server-beschikbaarheidsgroepen - Azure Virtual Machines - overzicht | Microsoft Docs
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
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="edbd1-103">Inleiding tot SQL Server altijd op beschikbaarheidsgroepen op virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="edbd1-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="edbd1-104">Dit artikel bevat een SQL Server-beschikbaarheidsgroepen op Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="edbd1-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="edbd1-105">AlwaysOn-beschikbaarheidsgroepen op Azure Virtual Machines zijn vergelijkbaar tooAlways beschikbaarheidsgroepen on-premises.</span><span class="sxs-lookup"><span data-stu-id="edbd1-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="edbd1-106">Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="edbd1-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="edbd1-107">Hallo diagram illustreert Hallo delen van een volledige SQL Server-beschikbaarheidsgroep in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="edbd1-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="edbd1-109">Hallo belangrijk verschil voor een beschikbaarheidsgroep in Azure Virtual Machines is dat virtuele machines in Azure, Hallo vereisen een [netwerktaakverdeler](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="edbd1-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="edbd1-110">Hallo load balancer bevat Hallo IP-adressen voor Hallo beschikbaarheidsgroep-listener.</span><span class="sxs-lookup"><span data-stu-id="edbd1-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="edbd1-111">Als er meer dan één beschikbaarheidsgroep moet elke groep een listener.</span><span class="sxs-lookup"><span data-stu-id="edbd1-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="edbd1-112">Één load balancer biedt ondersteuning voor meerdere listeners.</span><span class="sxs-lookup"><span data-stu-id="edbd1-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="edbd1-113">Wanneer u klaar toobuild een beschikbaarheid aroup voor SQL Server op Azure Virtual Machines bent, Raadpleeg toothese zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="edbd1-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="edbd1-114">Een beschikbaarheidsgroep automatisch maken van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="edbd1-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="edbd1-115">AlwaysOn-beschikbaarheidsgroep configureren voor de Resource Manager in Azure VM automatisch-</span><span class="sxs-lookup"><span data-stu-id="edbd1-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="edbd1-116">Een beschikbaarheidsgroep handmatig maken in Azure portal</span><span class="sxs-lookup"><span data-stu-id="edbd1-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="edbd1-117">U kunt ook Hallo virtuele machines zelf maken zonder het Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="edbd1-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="edbd1-118">Eerst voldoen aan vereisten Hallo vervolgens Hallo-beschikbaarheidsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="edbd1-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="edbd1-119">Zie de volgende onderwerpen Hallo:</span><span class="sxs-lookup"><span data-stu-id="edbd1-119">See hello following topics:</span></span> 

- [<span data-ttu-id="edbd1-120">Vereisten voor SQL Server AlwaysOn-beschikbaarheidsgroepen configureren op Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="edbd1-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="edbd1-121">Maken van AlwaysOn-beschikbaarheidsgroep tooimprove beschikbaarheid en herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="edbd1-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="edbd1-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edbd1-122">Next steps</span></span>

<span data-ttu-id="edbd1-123">[Configureren van een SQL Server altijd op beschikbaarheidsgroep op Azure virtuele Machines in verschillende regio's](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="edbd1-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
