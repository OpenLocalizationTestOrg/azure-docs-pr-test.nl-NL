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
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Inleiding tot SQL Server altijd op beschikbaarheidsgroepen op virtuele machines in Azure #

Dit artikel bevat een SQL Server-beschikbaarheidsgroepen op Azure Virtual Machines. 

AlwaysOn-beschikbaarheidsgroepen op Azure Virtual Machines zijn vergelijkbaar tooAlways beschikbaarheidsgroepen on-premises. Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

Hallo diagram illustreert Hallo delen van een volledige SQL Server-beschikbaarheidsgroep in Azure Virtual Machines.

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Hallo belangrijk verschil voor een beschikbaarheidsgroep in Azure Virtual Machines is dat virtuele machines in Azure, Hallo vereisen een [netwerktaakverdeler](../../../load-balancer/load-balancer-overview.md). Hallo load balancer bevat Hallo IP-adressen voor Hallo beschikbaarheidsgroep-listener. Als er meer dan één beschikbaarheidsgroep moet elke groep een listener. Één load balancer biedt ondersteuning voor meerdere listeners.

Wanneer u klaar toobuild een beschikbaarheid aroup voor SQL Server op Azure Virtual Machines bent, Raadpleeg toothese zelfstudies.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Een beschikbaarheidsgroep automatisch maken van een sjabloon

[AlwaysOn-beschikbaarheidsgroep configureren voor de Resource Manager in Azure VM automatisch-](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Een beschikbaarheidsgroep handmatig maken in Azure portal

U kunt ook Hallo virtuele machines zelf maken zonder het Hallo-sjabloon. Eerst voldoen aan vereisten Hallo vervolgens Hallo-beschikbaarheidsgroep maken. Zie de volgende onderwerpen Hallo: 

- [Vereisten voor SQL Server AlwaysOn-beschikbaarheidsgroepen configureren op Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [Maken van AlwaysOn-beschikbaarheidsgroep tooimprove beschikbaarheid en herstel na noodgevallen](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Volgende stappen

[Configureren van een SQL Server altijd op beschikbaarheidsgroep op Azure virtuele Machines in verschillende regio's](virtual-machines-windows-portal-sql-availability-group-dr.md).
